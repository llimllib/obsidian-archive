Recently at work I wanted to deploy an [[Observable Framework]] app that required users to be logged in to our google account.

To do so, I decided to write the simplest possible oauth2 proxy using [express](https://expressjs.com/), [passport](https://github.com/jaredhanson/passport) and [[sqlite]]. Here's how I did it.

## Create a google project

I prefer to interact with cloud services via CLI, but I haven't previously set up google's CLI for this employer, so I did it via the cloud console. 

(Frustratingly, that means this will all probably be out of date in 6 months, but if I don't write it down I won't remember a thing)

- go to your google cloud console and [create a new project](https://console.cloud.google.com/projectcreate?previousPage=%2Fapis%2Fcredentials%3Fauthuser%3D0%26project%3Dllimllib-takahe&organizationId=0&authuser=0)
- navigate to the [API & Credentials](https://console.cloud.google.com/apis/credentials?authuser=0&project=llimllib-takahe&organizationId=0) section
- click on the `OAuth consent screen` tab on the left
	- choose `internal` or `external` users - the former is only available in a google workspace
	- give your app a name, list its domain name (I think you can skip this if you just want to test), add that domain to the "Authorized domains" list, and give your email as a developer contact
	- at the scopes screen, which can be bewildering if you have lots of services enabled, you only need three: `.../auth/userinfo.email`, `.../auth/userinfo.profile`, and `openid`
		- you should see these three scopes in "your non-sensitive scopes". click `Save and continue`
	- If you're creating an app with external users, add yourself and any colleagues you want to test with as test users.
		- If you're creating an internal app, you won't have to deal with this step
	- You've now "configured your consent screen", and you are allowed to create an oauth2 credential (yay?)
- Click on the `Credentials` tab on the left
	- Click the `+ create credentials` button to reveal a dropdown, and select `Create OAuth client ID`
	- Choose `Web Application`
	- Add `http://localhost:7890` as an "Authorized domain"
	- Add `http://localhost:7890/auth/google/callback` as an "Authorized redirect URI"
		- Note that I set both of these up without https! This makes testing easier
		- You may also add your real domain if you know where you'll be hosting your app; otherwise you can come back and make another credential later with the appropriate domains
	- A modal should pop up, telling you that an OAuth client has been created. Copy the client id and secret, we'll need them in a second

Wow, that's a lot of steps when you write it all down! But now we have a client ID and secret, which is all we really wanted, and we're ready to write our proxy.

## Create an app

Let's make an [[Observable framework]] app, and add an express proxy in front of it using the client ID and secret we just created.

- Assuming you have `npm` installed, run: `npm init @observablehq`, choose a title, and accept the rest of the default options
- change into the directory you just created
- Run `npm run build` to build the site into a static `dist` folder, which we will serve from our proxy
- Install the dependencies for our proxy: `npm install --save better-sqlite3 better-sqlite3-session-store express express-session passport passport-google-oauth2`
- Make a directory to hold your proxy server: `mkdir proxy`
- set 5 environment variables in your environment; I use [[direnv]] or [[mise]] for this:
	- SESSION_SECRET="some random string"
	- BASE_URL="http://localhost:7890"
	- GOOGLE_CLIENT_ID="your-gogle-client-id.apps.googleusercontent.com"
	- GOOGLE_CLIENT_SECRET="your-google-client-secret"
	- PORT="7890"
- Edit `server.js` in the `proxy` directory
	- Copy the below in as `server.js`. I've tried to leave heavy comments with links to all relevant documentation:

```javascript
import { existsSync } from "node:fs";
import { join } from "node:path";
import { URL } from "node:url";

import Database from "better-sqlite3";
import express from "express";
import session from "express-session";
import sqlite3_session_store from "better-sqlite3-session-store";
import { Strategy as GoogleStrategy } from "passport-google-oauth2";
import passport from "passport";

// Create a sqlite session store
const SqliteStore = sqlite3_session_store(session);

// We'll want to serve static files out of the dist dir in the directory one
// level up from this file
const STATIC_ROOT = join(import.meta.dirname, "..", "dist");

// Create a database, and enable WAL mode for improved performance
//
// To enable verbose debug info: add { verbose: console.log } options object
// https://github.com/WiseLibs/better-sqlite3/blob/v9.4.3/docs/api.md#new-databasepath-options
const DB = new Database("users.db");
DB.pragma("journal_mode = WAL");

// Create a users table
DB.exec(
  `CREATE TABLE IF NOT EXISTS users(email TEXT PRIMARY KEY, profile JSONB)`,
);

// Prepare a query to find a user
const findUser = DB.prepare(`SELECT email, profile FROM users WHERE email=?`);

// Prepare a query to find a user
const insertUser = DB.prepare(`INSERT INTO users(email, profile) VALUES(?, ?)`);

// Create the root express app object
const app = express();

// Add the express-session manager to our app, with the SqliteStore configured
// to use our sqlite db for storing users
//
// session config: https://github.com/expressjs/session/blob/v1.18.0/README.md#sessionoptions
// SqliteStore config: https://github.com/attestate/better-sqlite3-session-store/blob/v0.1.0/README.md#usage
app.use(
  session({
    store: new SqliteStore({
      client: DB,
      expired: {
        clear: true, // clear expired sessions regularly
        intervalMs: 15 * 60 * 1000, // every 15 minutes
      },
    }),
    // this must be set in the environment to a random value
    // https://github.com/expressjs/session/blob/v1.18.0/README.md#secret
    secret: process.env.SESSION_SECRET,
    resave: false,
    saveUninitialized: true,
  }),
);

// Configure passport to use google oauth
//
// https://www.passportjs.org/concepts/authentication/google/
//
passport.use(
  new GoogleStrategy(
    {
      // the oauth client ID and secret we created need to be in the process'
      // environment
      clientID: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
      passReqToCallback: true,
      callbackURL: `${process.env.BASE_URL}/auth/google/callback`,
      userProfileURL: "https://www.googleapis.com/oauth2/v3/userinfo",
    },

    // This is the "verify function", a callback whose job is to match the
    // request to a user. It has three types of return:
    // - success: done(null, <user object>)
    // - failure (invalid user): done(null, false)
    // - error (server problem): done(err)
    //
    // In our case, we're happy to allow anybody to register and use the app,
    // so we just create a user if one doesn't exist. If you need to restrict
    // access to particular users, here's where you can do so by calling
    // `done(null, false)` for invalid users
    //
    // Read the full documentation here:
    // https://www.passportjs.org/concepts/authentication/strategies/#verify-function
    async (request, accessToken, refreshToken, profile, done) => {
      if (!profile.verified) {
        return done(null, false, {
          message: "Google OAuth user must be verified",
        });
      }

      if (!findUser.get(profile.email)) {
        insertUser.run(profile.email, JSON.stringify(profile));
      }

      return done(null, findUser.get(profile.email));
    },
  ),
);

// serialize the user to the session; in this case we just store their email
// address as the key to look them up in the database.
// https://www.passportjs.org/concepts/authentication/sessions/
passport.serializeUser((user, done) => {
  done(null, user.email);
});

// deserialize the user from the session to a user object. Error if we have a
// user session but cant find the user. Particularly this can happen if
// we're using sqlite and not storing the database anywhere that it will
// persist
passport.deserializeUser(async (email, done) => {
  const user = findUser.run(email);
  if (!user) {
    done(new Error(`couldn't find user ${user}`));
  }
  done(null, user);
});

// use passport middleware for all requests.
app.use(passport.initialize());
app.use(passport.session());

// handle the google auth route
// https://www.passportjs.org/concepts/authentication/google/
app.get(
  "/auth/google",
  passport.authenticate("google", {
    scope: ["email", "profile"],
  }),
);

// handle the google auth logout
// https://www.passportjs.org/concepts/authentication/google/
app.get("/auth/logout", async (req, res) => {
  req.session.destroy();
  res.redirect(302, "/?loggedout");
});

// handle the oauth callback. The user first hits /auth/google, then goes to
// google to log in, then gets redirected to /auth/google/callback
// https://www.passportjs.org/concepts/authentication/google/
app.get(
  "/auth/google/callback",
  passport.authenticate("google", {
    successRedirect: "/auth/redirect",
    failureRedirect: "/auth/google",
  }),
);

// Enforce authentication on all routes attached below here
app.use(async (req, res, next) => {
  if (req.user) {
    return next();
  }

  req.session.loginDestination = req.url;
  return res.redirect(302, "/auth/google");
});

// Since passport.authenticate() takes a static value for successRedirect, we
// need an endpoint to redirect a user to their destination after successfully
// authenticating.
app.get("/auth/redirect", (req, res) => {
  const destination = req.session.loginDestination;
  if (destination) {
    delete req.session.loginDestination;
    return res.redirect(302, destination);
  }
  return res.redirect(302, "/");
});

// observable expects Clean URLs; turn /somepath?query=string into
// /somepath.html?query=string
//
// https://observablehq.com/framework/routing#pages
app.use((req, res, next) => {
  var url = new URL(`http://${req.headers.host}${req.url}`);
  var path = url.pathname;
  if (path === "/" || existsSync(join(STATIC_ROOT, path))) {
    return next();
  }
  url.pathname += ".html";
  res.writeHead(301, { Location: url.toString() });
  res.end();
});

// finally, we can serve the static app!
app.use(express.static(STATIC_ROOT));

// allow configuration of host and port by env vars HOST and PORT
const PORT = process.env.PORT || 3000;
const HOST = process.env.HOST || "0.0.0.0";

// start the server
app.listen(PORT, HOST, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```