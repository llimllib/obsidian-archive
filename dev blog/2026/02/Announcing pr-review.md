---
created: 2026-02-12T22:11:18.399Z
updated: 2026-02-12T22:11:18.399Z
---
https://github.com/llimllib/pr-review

My run of a project a day continues with [[pr-review]], an updated version of my [[An AI tool I find useful|review script]] that adds sub-agents and uses the [[pi]] framework rather than the [[llm]] command.

Install it: `brew install llimllib/tap/pr-review` or download a binary at the releases page.

To make the [[Making a single-file executable with node and esbuild|binary]], I used [[bun]], which seems to have worked well.

I kept all the same arguments as my old review script, with the exception that the `-c` short arg now is for `--color` rather than `--context`, so you should be able to convert to it easily if you're using that one.

The big benefit I'm excited for is agents that can ask and answer questions, instead of a review script that only has the diff and no additional context. That does make it slower, but I'm hopeful that an increase in quality of response will offset the speed difference.