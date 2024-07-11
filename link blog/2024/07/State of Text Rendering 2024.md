---
created: 2024-07-11T12:49:58.430Z
updated: 2024-07-11T12:49:58.430Z
---
https://behdad.org/text2024/

Behdad Esfahbod, the primary author of [[HarfBuzz]][^1], presents an extremely thorough document on the state of text rendering in 2024.

> Using HarfBuzz on the web has been on the rise, first transpiled to JavaScript, and more recently cross-compiled to WebAssembly, through [harfbuzzjs](https://github.com/harfbuzz/harfbuzzjs). Apps like [Photopea](https://www.photopea.com/), an online photo editor, use it that way. [Crowbar](https://www.corvelsoftware.co.uk/crowbar/) by [Simon Cozens](https://www.simon-cozens.org/) is an OpenType shaping debugger web-app built using the HarfBuzz buffer-messaging API. [Sploot](https://simoncozens.github.io/sploot/) is another web-app by Simon, a font inspector. [Prezi](https://prezi.com/open-source-thanks/) and [Figma](https://www.figma.com/) also use HarfBuzz in their web-apps.

Neat! I didn't know photopea was shaping text in js, rather than using the browser's default abilities.

> While my proposed use of flatfonts fell flat on its face, better ergonomics for building and consuming fonts have lived on in terms of Google’s [Oxidize](https://github.com/googlefonts/oxidize) effort to port both font compilation and font consumption (font access initially, followed by shaping) platform to the [Rust](https://www.rust-lang.org/) programming language. This has a huge impact on software security because of Rust language’s safety guarantees while dealing with untrusted font data as in web-fonts.

> Moreover, the [fontations](https://github.com/googlefonts/fontations) platform, which is the Rust framework Oxidize is producing, will unify font compilation and consumption, reducing the number of places new font-format features need to be implemented from three (FontTools, FreeType, and HarfBuzz) to one (Fontations), which would reduce development cost and overhead.

In "Beyond Emulation: Fully-programmable fonts", he comments on two fun recent fonts:

> Finally, I proposed that the future of font shaping and drawing/​painting will involve a fully-programmable paradigm. I proposed [WebAssembly](https://webassembly.org/) (Wasm), and went ahead to [prototype](https://github.com/harfbuzz/harfbuzz/blob/main/docs/wasm-shaper.md) the shaping aspect in HarfBuzz’s Wasm shaper using the [wasm-micro-runtime](https://github.com/bytecodealliance/wasm-micro-runtime) Wasm engine. [Simon Cozens](https://www.simon-cozens.org/), as usual, implemented [several](https://github.com/harfbuzz/harfbuzz-wasm-examples) impressive examples, because why not!

> Two tongue-in-cheek mis-uses of the HarfBuzz Wasm shaper appeared recently: the [Bad Apple font](https://github.com/hsfzxjy/Bad-Apple-Font), and [llama.ttf](https://github.com/fuglede/llama.ttf). Check them out! To be clear, in a solid implementation of the Wasm shaper, acts like llama.ttf will not be possible because of CPU time budgets enforced. Bad Apple will become much easier and faster when we introduce the draw API in Wasm.

Finally, he reflects on the biggest threats to the OSS font ecosystem:

> The biggest threat to the ecosystem is that Google reduces resources it currently pours into the ecosystem. Mozilla already cut most of its (much smaller) involvement, by way of abandoning Servo and Firefox OS. The Linux Desktop has been benefiting from Google’s investment into HarfBuzz, FreeType, and other projects.

> While the Rust migration is beneficial to the ecosystem in the long term, in the short term it has the potential to fragment the ecosystem and reduce resources (specially from Google) available to the C / C++ and the Python platforms which we need to update for quite a few years more.

[^1]: : HarfBuzz ([github](https://github.com/harfbuzz/harfbuzz), [homepage](https://harfbuzz.github.io/)) is a text shaping library used basically everywhere. If you interact with open source software that renders text, you almost certainly are using HarfBuzz