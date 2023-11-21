https://github.com/privatenumber/tsx

> Features

> - Blazing fast (_ed_: 🙄) on-demand TypeScript & ESM compilation
> - Works in both [CommonJS and ESM packages](https://nodejs.org/api/packages.html#type)
> - Supports next-gen TypeScript extensions (`.cts` & `.mts`)
> - Hides experimental feature warnings
> - TypeScript REPL
> - Resolves `tsconfig.json` [`paths`](https://www.typescriptlang.org/tsconfig#paths)

I'ved used [[ts-node]] for small stuff, and it works... fine. `tsx` uses `esbuild` instead of `tsc`, so it should be faster but also it doesn't typecheck.