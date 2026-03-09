---
created: 2026-01-03T19:33:39.998Z
updated: 2026-03-06T13:17:48.320Z
---
https://bitwarden.com

What I use for password management after I finally switched off [[Lastpass]]

---

CLI usage:

```
brew instll bitwarden-cli
# this initializes bw on your computer and only needs to be run once 
# (I think)
bw login "email@address.here"

# now you need to export the session ID (or pass it along to
# any command that needs it). In the previous step, we could
# have passed --raw to login and exported that as well, but
# normally you only have to "unlock"
export BW_SESSION=$(bw unlock --raw)

# print an item template that you can edit
bw get template item

# base64 encode
bw encode

# Create a secure note (type = 2) with two custom fields for
# an API credential
bw get template item |
  jq --arg key "$MOZ_JWT_ISSUER" \ 
     --arg secret "$MOZ_JWT_SECRET" \
 '.name = "Mozilla add-on API Credentials" |
  .notes = "" |
  .type = 2 |
  .secureNote = {"type": 0} |
  .fields = [
    {"name": "api-key", "value": $key, "type": 0},
    {"name": "api-secret", "value": $secret, "type": 1}
  ]' |
  bw encode |
  bw create item

# retrieve the value of the key
bw get item "Mozilla add-on API Credentials" |
  jq -r '.fields[] | select(.name == "api-key") | .value'
```