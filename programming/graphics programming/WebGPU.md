https://surma.dev/things/webgpu/

> I want to share what I learned while wrapping my head around GPUs and WebGPU. The goal for this blog post is to make WebGPU accessible for web developers. But here’s an early heads up: I won’t use WebGPU to generate graphics. Instead, I will use WebGPU to access the raw computing power a GPU provides. Maybe I will do a follow-up blog post how to use WebGPU to render to your screen, but there is already [quite a bit of content](https://austin-eng.com/webgpu-samples) out there. I will go as deep as necessary to make sense of WebGPU and hopefully enable you to use it _effectively_ — but not necessarily _efficiently_. I can’t make you a GPU performance expert; mostly because I am not one myself.

In the end he uses a compute shader to write a 2d canvas demo - the compute shader is calculating the position and handling collisions for thousands of balls, while there is a regular old canvas 2d renderer. Super neat!

WebGPU is as of right now only available on FF and Chrome behind a flag, and the API is not yet set.