---
created: 2026-02-24T13:12:59.964Z
updated: 2026-02-24T13:12:59.964Z
---
> Now let's come back to our jumping thought experiment: the issue here is that, if you jump to a random byte of a CSV file, you cannot know whether you landed in a quoted cell or not. So, if you read ahead and find a line break, is it delineating a CSV row, or is just allowed here because we stand in a quoted cell? And if you find a double quote? Are you opening a quoted cell or are you closing one?...

> Armed with our sample, we can now jump to some random byte of our CSV file and assess the situation.

> The first thing that we need to do is to multiply the maximum byte size of our sampled rows by some constant (I recommend 32 to abide by the beforementioned fetichism). Using the above example, we would need to multiply 19131 by 32, yielding 612192.

> We will then proceed to read that many bytes following our landing point. But we will do so twice: one time reading from the stream as-is and one time pretending a double quote exists just before our landing point.

> The goal here is to test the only two hypothesis we have: either we landed in an unquoted section or we landed in a quoted one.

- [Guillaume Plique](https://github.com/medialab/xan/blob/a235ec0589d29df91153ad2bfb623feb0ab45650/docs/blog/csv_base_jumping.md)

Clever idea for probabalistically determining whether you're inside a quoted column or not: sample the column length from the first N rows, and compare two samples from around the byte position you want to jump to to that sample. You are very likely to end up with one sample being vastly more similar than the other, and you can back out from there to determining whether you're in a quoted column or not.

This enables chunked processing of csv files, which is otherwise quite difficult.

[xan](https://github.com/medialab/xan) is already in my [[csv tools]] list. Found via [Tony Finch](https://dotat.at/:/AERHE.html)'s excellent link blog