---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
If you're using the `osxkeychain` github credentials manager, here's a command to retrieve your github password from the command line:

`security find-internet-password -w -s 'github.com'`

----------

Here's how to add an API secret to your keychain:

`security add-generic-password -s '<service name>' -a '<account name>' -w '<password>'`

And how to retrieve it:

`security find-generic-password -w -s '<service name>'`

You can add `-a <account name>` to that if the service name is not enough to specify the password exactly, but find works if there's only one matching service.