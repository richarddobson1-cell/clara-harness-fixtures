# Transcripts — first persisted baseline runs, 10 September 2026

One file per battery. Each carries the full run row: replies in prompt
order, per-reply L1 verdicts (scaffold class and screen hits), first-run
L2 judge verdicts with notes, the aggregate, and the dual stamp (git SHA
2cf9bc8370c993e10733d78a49e43aeadc18a24b, substrate model label
gpt-5.1). Judge model: claude-sonnet-4-6 — a different provider from
the substrate that produced the replies, per the harness's standing
judged-independence policy.

## What mode these runs are — read before interpreting

These are LIVE RAW-COMPOSITION runs: the surface's system prompt plus
the battery prompts, sent directly to the substrate. They deliberately
exclude the production runtime around the model — no per-account
provenance block is injected, no post-generation strip or quarantine
runs, no tool calls are available. They therefore measure what the
prompt-plus-substrate produces, which is exactly what the batteries are
for; they do NOT measure the production path, and several L2 rubric
keys that presuppose runtime-injected context (for example
answers_from_provenance_block) fail by construction in this mode.
Treat L2 verdicts on such keys as characterising the raw composition,
not the deployed system.

## Re-scoring

The L1 verdicts recorded here are reproducible mechanically from the
replies and the released screen definitions — that is the point. Score
the replies yourself per protocol/scoring-protocol.md and compare
against the recorded verdicts before looking at them.
