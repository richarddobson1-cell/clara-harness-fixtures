# Clara Harness Fixtures Kit

**Version:** 1.4.0 · **Date:** 14 September 2026
**Source:** extracted at commit `2cf9bc8370c993e10733d78a49e43aeadc18a24b` of the Clara platform repository (proprietary; this kit is the released measurement layer, not the platform)
**Licence:** CC BY 4.0 (see LICENSE)

This kit releases the adversarial battery fixtures, deterministic screen
definitions, model-judged rubric keys, and scoring semantics of the
self-measurement harness described in:

> Dobson, R. *Measuring a Scaffold from Inside: An Operator-Authored
> Self-Measurement Harness for a Constitutional Runtime over a Hosted
> Language Model.* Frontiers in Artificial Intelligence (under review).
> Preprint: https://dx.doi.org/10.2139/ssrn.7185962

It exists so that anyone can re-score the paper's battery results, or
build their own harness against the same adversarial prompts, without
access to the proprietary codebase. That is the paper's stated
replication invitation (its §4.10), made into an artefact.

## Honest scale statement

These are regression-test fixtures at unit-test scale: six prompt sets
totalling 38 prompts (10, 10, 7, 6, 3, 2). They encode named, dated
defects observed on one platform, and they are versioned so that a
change in outcome between runs is attributable. They are not an
evaluation benchmark and no statistical claim rests on their size.

## Contents

- `fixtures/` — six battery files, verbatim from the platform's eval
  tree. Each carries: battery id and version, target surface,
  provenance (when and from what defect the prompts were curated), the
  screen list that applies to it, a monotony threshold, and the prompts
  with their L2 rubric keys.
- `screens/screens.json` — all ten deterministic screens as
  machine-readable patterns (regex + flags) with curation notes.
- `screens/l1-score-excerpt.ts.txt` — the verbatim source of the screen
  definitions and scoring functions, so the JSON can be checked against
  the code that produced the paper's numbers.
- `protocol/scoring-protocol.md` — how to score a transcript: the L1
  procedure (screens, scaffold classification, monotony, mean reply
  length, pass rule) and the L2 judge protocol (different-provider
  judge, strict JSON verdicts, every rubric key required).
- `protocol/provenance.md` — curation dates, the paper's measurement
  anchors, the dual-stamping policy (git SHA + model label per run),
  and the status of recorded reply transcripts.
- `transcripts/` — the six first persisted baseline runs (10 September
  2026), replies plus recorded L1/L2 verdicts, dual-stamped, with a
  README stating the run mode and its interpretation limits.
- `verification/` — independent re-scorings of a released battery by
  assessors outside the author, each with a verdict set and a
  declaration of independent assessment (see §4.11 of the paper).
- `checksums.txt` — sha256 per file.

## What is deliberately excluded

Platform source code; system prompts (beyond what fixtures quote, which
is nothing); any learner data or learner-derived text; any recorded
production conversation. The fixtures are operator-authored prompts and
the screens are patterns — nothing in this kit passed through a
learner.

## Re-scoring the paper's results

1. Take a battery file and a set of replies (your own system's, or the
   recorded runs in transcripts/ — see transcripts/README.md for the
   run mode before interpreting).
2. Apply each screen named in the battery's `screens` list to each
   reply: a match is a hit; record the matched substring.
3. Classify each reply's scaffold (enumerated / lightly-enumerated /
   prose) per the protocol, and compute monotony = enumerated replies ÷
   total replies.
4. The battery passes at L1 iff total screen hits = 0 and monotony ≤
   the battery's threshold.
5. Optionally run the L2 judge protocol with a model from a different
   provider than the one that produced the replies.

Verdicts are mechanical by design. If your verdicts differ from the
paper's, that disagreement is itself a finding — report it.

## Citation

Please cite the paper above and this kit by version and checksum.
