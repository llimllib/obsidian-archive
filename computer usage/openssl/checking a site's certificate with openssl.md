I encountered a problem with a site that wasn't presenting the full certificate chain, causing an error `Verify return code: 21 (unable to verify the first certificate)`.

On a site that correctly gives its full certificate chain, here's the relevant bits of what you see:

```
$ openssl s_client -connect billmill.org:443                
Connecting to 161.35.57.166
CONNECTED(00000006)
depth=2 C=US, O=Internet Security Research Group, CN=ISRG Root X1
verify return:1
depth=1 C=US, O=Let's Encrypt, CN=R3
verify return:1
depth=0 CN=billmill.org
verify return:1
---
Certificate chain
 0 s:CN=billmill.org
   i:C=US, O=Let's Encrypt, CN=R3
   a:PKEY: id-ecPublicKey, 256 (bit); sigalg: RSA-SHA256
   v:NotBefore: Feb 21 00:09:41 2024 GMT; NotAfter: May 21 00:09:40 2024 GMT
 1 s:C=US, O=Let's Encrypt, CN=R3
   i:C=US, O=Internet Security Research Group, CN=ISRG Root X1
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Sep  4 00:00:00 2020 GMT; NotAfter: Sep 15 16:00:00 2025 GMT
---
<snip>
Verify return code: 0 (ok)
<snip>
```

On a site where the entire chain is not presented, you'll see `20:unable to get local issue certificate` followed by `21:unable to verify the first certificate`:

```
$ openssl s_client -connect incomplete-chain.badssl.com:443         
Connecting to 104.154.89.105
CONNECTED(00000006)
depth=0 C=US, ST=California, L=Walnut Creek, O=Lucas Garron Torres, CN=*.badssl.com
verify error:num=20:unable to get local issuer certificate
verify return:1
depth=0 C=US, ST=California, L=Walnut Creek, O=Lucas Garron Torres, CN=*.badssl.com
verify error:num=21:unable to verify the first certificate
verify return:1
depth=0 C=US, ST=California, L=Walnut Creek, O=Lucas Garron Torres, CN=*.badssl.com
verify error:num=10:certificate has expired
notAfter=May 17 12:00:00 2022 GMT
verify return:1
depth=0 C=US, ST=California, L=Walnut Creek, O=Lucas Garron Torres, CN=*.badssl.com
notAfter=May 17 12:00:00 2022 GMT
verify return:1
---
Certificate chain
 0 s:C=US, ST=California, L=Walnut Creek, O=Lucas Garron Torres, CN=*.badssl.com
   i:C=US, O=DigiCert Inc, CN=DigiCert SHA2 Secure Server CA
   a:PKEY: rsaEncryption, 2048 (bit); sigalg: RSA-SHA256
   v:NotBefore: Mar 23 00:00:00 2020 GMT; NotAfter: May 17 12:00:00 2022 GMT
```

(Sadly, [badssl.com](https://badssl.com/) appears to be dead and full of expired certificates; at least in this case I can use it to demonstrate the issue)