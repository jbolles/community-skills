# Changelog

## 0.9.1 - 2026-09-12

Fixes from the first community run, reported by a user who installed the plugin
from the marketplace and ran a full seven-reader panel on a lead-gen page.

- **Script paths work when installed as a plugin.** `SKILL.md` called its scripts
  by a repo-relative path that only resolved inside a `.claude/skills/` copy.
  All ten calls now go through `${CLAUDE_PLUGIN_ROOT}`. `INSTALL.md` says what
  to change if you copy the skill into a repo instead.
- **A narrow reader agent ships with the plugin.** The cost figures assumed an
  agent type (`sonnet-worker`) that only exists in an Agency Brain, so a plugin
  install fell back to `general-purpose` and paid two and a half times the quoted
  figures (measured: 105k per reader, 733k for seven, on a machine with about two
  hundred tool definitions). `agents/seo-council-reader.md` is now the spawn
  target, and Step 3 states the `general-purpose` range for anyone who cannot use
  it.
- **`scores.cjs summary` no longer claims repeatability it has not seen.** The
  "repeatability is well evidenced" line printed unconditionally, including on a
  fresh store with one record. It now prints only when a page has been scored
  twice; otherwise the summary says neither property is evidenced yet.
- **`mode` has three values for three states.** The record field accepted any
  string and documented only `conformance` and `fallback`, so a run with a filled
  target brief and a run with nothing at all were indistinguishable and averaged
  together. It is now validated to `conformance`, `assigned` or `inferred`, matching
  the three input states in `rubric-core.md`. Existing `fallback` records are read
  as `inferred` and noted.

## 0.9.0 - 2026-08-18

First public release. Version 0.9 rather than 1.0 for one honest reason: the
evaluation index is proven repeatable (it reads the same twice on the same page)
but its sensitivity, whether it moves when a page genuinely improves, is not yet
evidenced. See the README's "Honest limits" section.

- Six-dimension rubric with written band anchors, four vertical overlays
  (ecommerce, lead-gen, local, B2B), and a two-reader design on search intent.
- Independent per-dimension scoring by separate agents, so disagreements are
  discovered rather than authored.
- A mandatory attribution gate that keeps named practitioners represented as
  analytical lenses, never as if they reviewed a page.
- A scores log and the method for building your own calibration anchors over time.
- Re-score mode: when re-scoring a page already in the log, re-run only the
  dimensions whose inputs changed (roughly a third of the cost), with an explicit
  distinction between a page that genuinely changed and a corrected re-run.
- Works from nothing but a URL and a target query; every other input is optional
  with a stated cost.
