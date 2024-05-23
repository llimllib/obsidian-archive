---
updated: '2023-10-30T11:50:44Z'
created: '2023-10-30T11:50:44Z'
---
https://github.com/dtolnay/anyhow

> This library provides [`anyhow::Error`](https://docs.rs/anyhow/1.0/anyhow/struct.Error.html), a trait object based error type for easy idiomatic error handling in [[Rust]] applications.

> ...Use Anyhow if you don't care what error type your functions return, you just want it to be easy. This is common in application code. Use [thiserror](https://github.com/dtolnay/thiserror) if you are a library that wants to design your own dedicated error type(s) so that on failures the caller gets exactly the information that you choose.

via [Tom MacWright](https://tmcw.github.io/2023/10/29/tidbyt-rs.html)