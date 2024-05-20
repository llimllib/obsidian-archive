---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://c9x.me/compile/

> QBE is compiler backend that aims to provide 70% of the performance of industrial optimizing compilers in 10% of the code. QBE fosters language innovation by offering a compact user-friendly and performant backend. The size limit constrains QBE to focus on the essential and prevents embarking on a never-ending path of diminishing returns.

### Overview

> The C codebase of QBE is intended to remain hobby-scale and pleasant to hack on. Despite the small footprint, QBE provides a number of optimizations with good impact/weight ratio. It also facilitates integration with foreign systems by implementing the C ABI in full. This means that programs compiled by QBE can trivially call into C, and vice versa. The current version of QBE can target _amd64_ (linux and osx), _arm64_, and _riscv64_.

The backend that [[Cproc - small readable c compiler]] aims itself at. Seems like an attempt to do a simpler, smaller LLVM. Has simple IR example on the front page, which is nice.