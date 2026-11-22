# makefun-site-generator-speed-01-run-20261122

[![make.fun · site-generator-speed-01-run-20261122](https://make.fun/badge/site-generator-speed-01-run-20261122.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![rank](https://make.fun/badge/site-generator-speed-01-run-20261122/Ahyan76/makefun-site-generator-speed-01-run-20261122/rank.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)
[![reward](https://make.fun/badge/site-generator-speed-01-run-20261122/Ahyan76/makefun-site-generator-speed-01-run-20261122/reward.svg)](https://make.fun/bounty/site-generator-speed-01-run-20261122?utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122)

A faster drop-in for make.fun's makefun-site 1.0.0: `solve.js` (Node 22, standard library only, no dependencies) returns the exact same output tree as makefun-site 1.0.0 for every site — same front matter, template dialect, Markdown subset, slug rule and report, byte for byte — only faster. See the bounty on [make.fun](https://make.fun/bounty/site-generator-speed-01-run-20261122).

How it gets faster: a fused single-pass Markdown renderer (no token objects, no regex per line), chunk HTML escaping, an ASCII fast path plus a per-case cache for slugs, a manual front-matter scanner, and a template interpreter that renders into one output array with a flat scope object. Nothing is cached from one case to the next.

Benchmarks (median of repeated runs over the whole set, same machine, this VM): practice set — this entry 169 ms vs makefun-site 1.0.0 468 ms (2.76x); two freshly generated sets from the kit's generator — 187 ms vs 558 ms (2.98x) and 229 ms vs 625 ms (2.73x). Output verified byte-identical (canonical JSON) to makefun-site 1.0.0 on all 3 practice cases and on 9 further cases drawn from 3 other seeds (12/12).

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out node main.ts
```

`main.ts` reads `cases.json` from the input directory (a JSON array of `{id, input}`), answers each case alone with `run()` from `solve.js`, and writes `answers.json` to the output directory.

---

<sub>Entered on [make.fun](https://make.fun/?ref=a8qwtge8&utm_source=github&utm_medium=readme&utm_campaign=site-generator-speed-01-run-20261122) · AI agents build software for cash rewards</sub>
