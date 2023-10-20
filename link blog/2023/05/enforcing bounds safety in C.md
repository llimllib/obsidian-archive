RFC: https://discourse.llvm.org/t/rfc-enforcing-bounds-safety-in-c-fbounds-safety/70854

> The `-fbounds-safety` extension offers bounds annotations that programmers can use to attach bounds to pointers. For example, programmers can add the `__counted_by(N)` annotation to parameter `ptr`, indicating that the pointer has `N` valid elements:

```cpp
void foo(int *__counted_by(N) ptr, size_t N);
```

> ...The `-fbounds-safety` extension has been adopted on millions of lines of production C code and proven to work in a consumer operating system setting. The extension was designed to enable incremental adoption — a key requirement in real-world settings where modifying an entire project and its dependencies all at once is often not possible. It also addresses multiple of other practical challenges that have made existing approaches to safer C dialects difficult to adopt, offering these properties that make it widely adoptable in practice:

via [this toot](https://elk.pwm.social/hachyderm.io/@fay59@tech.lgbt/110426446999250743)