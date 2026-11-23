# site-generator-speed

[![site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/azucaa/site-generator-speed/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/azucaa/site-generator-speed/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A fast, dependency-free drop-in replacement for makefun-site 1.0.0, entered in the make.fun bounty
[site-generator-speed-01-run-20261122](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
("Build a static site faster").

`run(input)` in `solve.js` returns, for every case's input, exactly the output tree
makefun-site 1.0.0's build returns — each page's `index.html`, the index and tag pages,
`build-report.txt` and each static file, byte for byte — and does it faster. The reference
escapes Markdown text one character at a time (a regex replace per character), re-slugs the
same tag names again and again, counts words with a global regex, and classifies every line
with a stack of regexes. This version keeps the reference's rules exactly — its front matter,
template dialect, Markdown subset, slug rule and report — but does the work in bulk: plain
runs of inline text are copied with a single slice, escaping only touches the characters
that need it, slugs and long dates are memoised within a case, lines are classified by their
first characters, and blocks are rendered in one pass with no token objects.

`main.ts` is the harness driver the baseline ships: it reads every case from
`/input/cases.json`, answers each with `run`, and writes `/output/answers.json`. It turns
V8's incremental marking off before importing `solve.js`, as the house baseline does.

## Layout

- `solve.js` — the generator itself (ES module, no dependencies).
- `main.ts` — the harness driver.
- `package.json` — `{ "type": "module" }`.

## Licence

MIT — see `LICENSE`.
