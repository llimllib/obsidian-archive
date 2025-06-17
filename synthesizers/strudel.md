---
created: 2025-06-17T12:17:28.408Z
updated: 2025-06-17T12:17:28.408Z
---
https://strudel.cc/
https://strudel.cc/workshop/getting-started/

Strudel is a fun music notation language with an online repl. Via [Lu Wilson](https://www.todepond.com/)

- Unfortunately it seems like you mostly need to use Chrome with it.
- Derives from [TidalCycles](https://tidalcycles.org/), which is a haskell UI on top of [[supercollider]]

Here's how to connect my keyboard and use it as a piano, via [this issue](https://club.tidalcycles.org/t/baked-in-support-for-midi-in-audio-in-and-audio-devices-channels/5098). There is [midi support](https://strudel.cc/learn/input-output/), but right now it's really only for control knobs.

```js
await WebMidi.enable()
const myInput = WebMidi.inputs[0];
const noteControls = Array.from(Array(128)).map(x => null)
myInput.removeListener('noteon');
myInput.removeListener('noteoff');
myInput.addListener('noteon', e => {
  const [n, vel] = e.dataBytes;
  superdough({ note: n, s: 'piano', postgain: vel / 127 }, 0.05, 10).then(function (x) {
    noteControls[n] = x;
  });
});
myInput.addListener('noteoff', e => {
  const [note] = e.dataBytes;
  const { mute } = noteControls[note]
  mute(0.1);
  noteControls[note] = null
})

sound("bd - bd -, hh hh hh hh").gain(.5)
```