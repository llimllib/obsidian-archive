https://www.snaplet.dev/post/postgresql-in-the-browser (more techy)
https://supabase.com/blog/postgres-wasm (more general)

Uses [v86](https://github.com/copy/v86) to put a whole linux VM in the browser, with [Buildroot linux](https://buildroot.uclibc.org/)
! Super cool.

I do somewhat agree with [a commenter on news.yc though](https://news.ycombinator.com/item?id=33074355):

> The dream is a real wasm native postgres; in fact to get all of postgresql's cool shared mem proccess stuff and make it something like shared array buffer! The dream is also that WASI interface and new-school OS interfaces like memfd_create are increasingly aligned.

> Instead of rationalization our interfaces, however, it's just emulation layer on top of emulation layer, tech debt all the way down.

Later, they say:

>> Are there future plans at creating a native WASM version of Postgres?

> Yup! I think that should be the goal, and we (Supabase & Snaplet) would be very happy to work with anyone that wants to build towards that.