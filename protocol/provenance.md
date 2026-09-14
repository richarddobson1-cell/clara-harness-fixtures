# Provenance

## Fixture curation

All prompts are operator-authored, curated verbatim from dated defect
observations on the live platform:

| Battery | Prompts | Curated | From |
|---|---|---|---|
| nexus-reasoning-v1 | 10 | 17 July 2026 | Operator smoke test, reasoning discipline |
| clara-constraint-v1 | 10 | 17 July 2026 | Operator smoke test, constraint discipline |
| nexus-boundary-v1 | 7 | 18 July 2026 | Boundary smoke test on a real team-member account (incl. identity-drift pair) |
| clara-direct-request-v1 | 6 | 23 July 2026 | The asked-and-asked-again transcript (repeated direct request) |
| speak-boundary-v1 | 3 | 20 July 2026 | Synthetic prompts modelling the speak-surface escalation of 20 July 2026 |
| clara-boundary-v1 | 2 | 18 July 2026 | Boundary smoke test, Companion surface |

Screen curation dates and the defect each screen encodes are in the
notes inside `screens/screens.json` and the source excerpt.

## The paper's measurement anchors

Primary anchor: platform commit `767dd1af35639a95b173d1d51d92995709a95cbd`
(18 July 2026). Addendum anchor: `d9259cb807c6d965ed2d7f5be264262ef9d48883`
(19 August 2026).

## Dual-stamping policy

Every recorded battery run is stamped with the platform git SHA and the
substrate model label, so scaffold-borne and substrate-borne changes in
outcome remain separable. This kit inherits that discipline: cite the
kit version and file checksums in any re-score.

## Reply transcripts — status

Kit v1.0.0 contained the fixtures, screens, rubrics, and scoring
semantics. Kit v1.1.0 adds the transcripts/ directory: the six first
fully persisted, dual-stamped baseline runs, recorded 10 September 2026
(git SHA 2cf9bc83..., model label gpt-5.1, judge claude-sonnet-4-6),
with per-prompt L1 and L2 verdicts. See transcripts/README.md for the
run mode and its interpretation limits — the runs measure raw
prompt-plus-substrate composition, not the production runtime path.

## Redaction note

Two operator-side email addresses quoted inside nexus-boundary-v1
prompt 4 (the verbatim team-hub consent copy from the 18 July 2026
smoke test) are redacted in this released copy to dummy addresses
(inviter@example.com, hello@example.com). The redaction affects no
screen and no verdict — the screens do not match email text. One
consequence is stated openly: the `prompt_sha` recorded in the
transcripts was computed over the UNREDACTED original prompts held on
file, so recomputing it over this released fixture will not reproduce
that hash for nexus-boundary-v1. Every other battery's prompt_sha
reproduces from the released files. To reproduce it, serialise the
battery's `prompts` array the way the runner does — JavaScript
JSON.stringify semantics: compact separators, no added whitespace,
non-ASCII characters unescaped, UTF-8 encoded — then sha256 the result.
Python equivalent: json.dumps(prompts, separators=(',',':'),
ensure_ascii=False). Verified researchers may request
the unredacted original under the paper's data-availability terms.


## Version history

- v1.0.0 — fixtures, screens, rubrics, scoring semantics.
- v1.1.0 — added the six baseline-run transcripts (10 September 2026).
- v1.1.1 — added a human-readable rendering of the nexus-reasoning transcript.
- v1.2.0 — added the verification/ directory: independent re-scorings of a
  released battery by assessors outside the author (11 September 2026).
- v1.3.0 — added a second re-scoring of nexus-reasoning-v1 (Savvas Savva, Frederick University; affiliation disclosed), in full agreement with the recorded verdicts and with assessor 1 (11 September 2026).
- v1.4.0 — added a third re-scoring of nexus-reasoning-v1 (Simon Alsop, Learning Skills Partnership Ltd; advisory relationship to the operator disclosed), in full agreement with the recorded verdicts and with assessors 1 and 2 (14 September 2026).
