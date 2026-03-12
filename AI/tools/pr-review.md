---
created: 2026-03-10T17:54:06.776Z
updated: 2026-03-10T17:54:06.776Z
---
https://github.com/llimllib/pr-review

My tool for doing PR review assisted by several sub-agents. Uses the [[pi]] framework, and spins up four sub-agents:

- **Bug Hunter** searches for bugs in / caused by the diff
- **Impact Analyzer** checks for negative impacts of the diff on other parts of the code
- **Test Reviewer** verifies that appropriate testing has been done
- **Code Quality** verifies that the code is high-quality

Then, finally a summarizer agent takes all four reviews and boils them down to a review summary.

