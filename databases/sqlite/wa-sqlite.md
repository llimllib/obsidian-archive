https://github.com/rhashimoto/wa-sqlite

> This is a WebAssembly build of SQLite with experimental support for writing SQLite virtual filesystems and virtual table modules completely in Javascript. This allows alternative browser storage options such as IndexedDB and File System Access. Applications can opt to use either a synchronous or asynchronous (using Asyncify) SQLite library build (an asynchronous build is required for asynchronous extensions).

> [IndexedDB](https://github.com/rhashimoto/wa-sqlite/blob/master/src/examples/IDBMinimalVFS.js) and [Origin Private File System](https://github.com/rhashimoto/wa-sqlite/blob/master/src/examples/OriginPrivateFileSystemVFS.js) virtual file systems and a [virtual table module that accesses Javascript arrays](https://github.com/rhashimoto/wa-sqlite/blob/master/src/examples/ArrayModule.js) are among the examples provided as proof of concept.

Basically a fork of the official SQLite wasm build with support for OPFS and other backends

> The primary motivation for this project is to enable additions to SQLite with only Javascript...
> Javascript wrappers for core SQLITE C API functions (and some others) are provided. Some convenience functions are also provided to reduce boilerplate. Here's sample code to load the library and call the API: