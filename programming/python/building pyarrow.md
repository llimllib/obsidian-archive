---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
pyarrow couldn't find openssl on my system. To get it to build, I had to do:

`OPENSSL_ROOT_DIR=/opt/homebrew/Cellar/openssl@3/3.0.5 pip install pyarrow`
