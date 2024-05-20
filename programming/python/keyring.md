---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://pypi.org/project/keyring/

> The Python keyring library provides an easy way to access the system keyring service from python. It can be used in any application that needs safe password storage.

> -   macOS [Keychain](https://en.wikipedia.org/wiki/Keychain_%28software%29)  
> -   Freedesktop [Secret Service](http://standards.freedesktop.org/secret-service/) supports many DE including GNOME (requires [secretstorage](https://pypi.python.org/pypi/secretstorage))
> -   KDE4 & KDE5 [KWallet](https://en.wikipedia.org/wiki/KWallet) (requires [dbus](https://pypi.python.org/pypi/dbus-python)) 
> -   [Windows Credential Locker](https://docs.microsoft.com/en-us/windows/uwp/security/credential-locker)

I found this tool super helpful when building command line tooling for a mixed-OS team. Store a secret in the system's secret store, whatever that may be.