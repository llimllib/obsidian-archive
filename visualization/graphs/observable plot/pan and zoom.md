---
created: 2024-09-24T15:56:34.000Z
updated: 2024-09-24T15:56:34.000Z
---
There's a long-standing [issue](https://github.com/observablehq/plot/issues/1590) waiting for panning and zooming in observable plot. Mike Bostock [started](https://github.com/observablehq/plot/pull/2083) work on it in June, but that work appears to have stalled.

He also provides [an example](https://observablehq.observablehq.cloud/framework-example-mortgage-rates/) of brushed zoom, where you control a plotted window via selecting an area on a second window.

The issue provides several example notebooks for hacks around the current lack of functionality, but I'd probably just build the chart in d3 instead of observable for this functionality at the moment.