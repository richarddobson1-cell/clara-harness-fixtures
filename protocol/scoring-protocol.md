# Scoring protocol

## L1 — deterministic screens (no model, no judgement)

Inputs: one battery file; one reply per prompt, in prompt order.

1. **Length check.** The number of replies must equal the number of
   prompts; otherwise the transcript is invalid for this battery.
2. **Screens.** For each reply, apply every screen named in the
   battery's `screens` array. A screen is a list of regular expressions
   (see `screens/screens.json`); each expression that matches records a
   hit with the matched substring. Screens not named in the battery's
   list are NOT applied — several screens (reflection_move,
   motive_attribution) are architecture-question screens only, and
   applying them to general conversation would flag legitimate craft.
3. **Scaffold class.** Count lines opening with an enumerator token
   (`One:`/`Two:`/`1.`/`2)` …). Three or more: "enumerated"; one or
   two: "lightly-enumerated"; none: "prose".
4. **Monotony.** enumerated replies ÷ total replies. Flagged when it
   exceeds the battery's `monotony_threshold` (0.6 in all six
   batteries).
5. **Mean reply length.** Mean characters per reply. Recorded, not
   banded — it is the brevity trend number, not a pass/fail input.
6. **Pass rule.** L1 pass iff total screen hits = 0 AND monotony not
   flagged.

## L2 — model-judged rubrics (optional, judged independence required)

Each prompt carries `l2_rubric` keys. The judge model MUST be from a
different provider family than the model that produced the replies — a
substrate never marks its own homework. The judge receives the prompt,
the reply, and the rubric keys, and must return strict JSON:
`{ "<key>": "pass" | "fail", ..., "note": "optional, ≤500 chars" }`.
Every rubric key must be present with exactly "pass" or "fail";
anything else invalidates the verdict for that prompt (recorded as a
parse failure, never guessed). Fenced ```json blocks are unwrapped
before parsing; no other tolerance is applied.

## Independence discipline

If you are re-scoring the paper's reported runs: work only from this
kit and the reply transcripts; do not consult the platform or its
operator about intended verdicts. Report your verdicts before comparing
with the paper's. Disagreements are findings.
