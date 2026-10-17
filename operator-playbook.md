# Adversarial Process Framework v1.7 — Operator Playbook

Use this when you are actually running the framework live.

## What Changed From v1.6

- Added REFRAME escape hatch as a distinct reset type (with guardrail).
- Tightened truth override: Operator names the dodged question, never the answer.
- Added mid-loop round extension (one time per loop, with substantive reasoning).
- Operator approval now requires reviewing the Challenger's unraised-risk self-audit.
- **Doc hygiene:** Model names replaced with `[BUILDER_MODEL]` and `[CHALLENGER_MODEL]` placeholders. Fill in your current model pairing at the start of each test run.

## Default setup

- **Builder:** `[BUILDER_MODEL]`
- **Challenger:** `[CHALLENGER_MODEL]`
- **Operator:** [your name]
- **Default round limit:** 5

Pick your two models before Topic 1 and note them here for the test run. Models should be from different providers where possible (different training lineage = less shared blind spots). Keep both models at comparable capability tiers — a frontier model vs. a mid-tier model produces a bully, not an adversary.

## Before Topic 1

1. Define the topic in one sentence.
2. Decide round limit now.
3. Tell both models their role.
4. Tell the Builder to produce `v1.0`.
5. Start a private Operator scorecard for the topic.

## Operator private scorecard

Track these four lines each round:

- Strongest valid objection raised this round:
- Strongest material risk still unraised:
- Weakest procedural move this round:
- Did revision improve truth, or only defensibility?

Do not send this unless needed for a reset or final decision.

## Handoff rules

### Send to Challenger
Only send:
- latest Builder structured output
- latest deliverable version
- current Objection Ledger
- version delta from prior round

Header format:
`ROUND [X] — BUILDER OUTPUT — v[topic].[round]`

### Send to Builder
Only send:
- latest Challenger structured review
- canonical Objection Ledger

Header format:
`ROUND [X] — CHALLENGER OUTPUT — v[topic].[round]`

Do not editorialize.
Do not summarize what you think.
Do not mediate.

## What good Challenger behavior looks like

- hits the most expensive plausible mistake early
- uses objections on substance, not polish
- upgrades or drops weak objections fast
- does not drift into co-authoring
- does not hide behind procedure
- completes the unraised-risk self-audit honestly before sign-off

## What bad Challenger behavior looks like

- spends all 3 objections on safe critiques
- keeps missing the core failure mode
- re-raises weak objections without strengthening them
- starts drafting alternatives instead of attacking
- wins on admissibility while missing truth
- returns "no unraised arguments" on the self-audit as a rubber-stamp move

## What good Builder behavior looks like

- accepts valid criticism cleanly
- rejects with equal-or-higher tier evidence
- revises proportionally with explicit tier-matching proportion statements
- improves the actual deliverable, not just the defense
- uses SELF-FAIL only when the approach is genuinely broken, with all three required elements

## What bad Builder behavior looks like

- buries weak spots under volume
- argues wording instead of substance
- marks things resolved before they are
- uses procedure as armor
- makes cosmetic changes in response to CRITICAL objections
- uses SELF-FAIL without the three required elements (escape hatch abuse)

## When to issue a standard RESET

Issue reset immediately if:
- either model starts essaying
- the argument shifts to tone/style/process instead of substance
- the Challenger is clearly missing the biggest risk
- the Builder is clearly dodging the strongest objection

Reset format:
`RESET — [specific instruction]`

Examples:
- `RESET — Back to structured format only.`
- `RESET — Objection #1 is not the real risk. Attack the cost model.`

## When to issue a TRUTH OVERRIDE

Issue truth override when both models are technically compliant but dodging the real issue.

Format:
`RESET — Truth override. You're both dodging [specific question].`

**Targeting rule:** Name the question being dodged. **Do not name the answer.**

Valid: `RESET — Truth override. You're both dodging customer data locality.`

Invalid: `RESET — Truth override. The answer is on-premise because of GDPR.`

If you can only describe the dodge by stating the answer, the loop is no longer adversarial — it's operator-directed. Pause it, don't reset it.

## When to issue a REFRAME

Issue REFRAME when both models are compliant and engaged, but neither Builder's approach nor Challenger's objections are solving the real problem. This is different from truth override — truth override says "attack the dodged question." REFRAME says "neither of your paths gets there; Builder, start over with a new constraint."

Format:
`RESET — REFRAME. Neither current path solves the real problem. Builder, rebuild from scratch with this constraint: [X]. Versioning resets to v[topic].0.`

**Guardrail:** Only use REFRAME when you can name **why** current paths are insufficient.

Valid: `RESET — REFRAME. Both paths assume the deliverable will be used by a single operator. The real use case is a team of five with conflicting priorities. Builder, rebuild with team-conflict as the primary constraint.`

Invalid: `RESET — REFRAME. Neither of these works. Try something else.`

If you can't name the insufficiency, the issue is probably your impatience, not process failure. REFRAME is a heavy move and should be rare — expect to use it less than once per three topics. If you're using it more, you may be using it as an impatience vent instead of a structural correction.

## When to EXTEND the round limit

The default round limit is 5. You may extend once per loop if substantive work remains.

Format:
`EXTEND — [current round] to [new limit]. Reason: [specific substantive work that requires more rounds].`

Valid reasons: "Objection #3 has been materially strengthened across two rounds and is one revision from resolution." / "The Builder's last revision surfaced a new dependency that needs one round to pressure-test."

Invalid reasons: "Let's give it more time." / "I think they can get there." / "We're close."

**Second extension = automatic deadlock.** If two extensions are needed, the framework isn't converging. Skip the second extension, activate Final Position Statement process immediately.

## Approval rule

Do not approve because the loop feels complete.

Approve only if:
- ledger is clean
- no queued material objection vanished
- the strongest remaining argument against the output is truly minor or accepted risk
- your scorecard does not show an obvious unraised landmine
- **the Challenger's unraised-risk self-audit surfaced a real argument (not "none") and it was genuinely below MINOR severity or raised and resolved**

If the Challenger's self-audit returned "no unraised arguments," be skeptical. Zero across a full loop is unusual. If you can think of an argument the Challenger should have raised and didn't, return it to the loop with a targeted question.

Approval format:
`v[topic].[round] APPROVED`

## Deadlock rule

If round limit hits (and extension is already used or declined):
1. Stop the loop.
2. Send both models the core dispute in 2-3 sentences.
3. Collect one-paragraph Final Position Statements.
4. Decide.
5. Builder produces `v[topic].F`.
6. Lock topic.

## SELF-FAIL rule

A Builder SELF-FAIL is only valid if it includes three elements:

- **(a)** The specific broken assumption or approach.
- **(b)** Why this required adversarial pressure to surface.
- **(c)** What would have to be true for a different approach to work.

A SELF-FAIL missing any of the three = reject and continue the loop. Common abuse pattern: "The approach is broken because it can't meet the constraints." That's (a) only. Reject.

Valid SELF-FAIL example:
- (a) "The deliverable assumes a single-operator workflow, but the constraints require team coordination."
- (b) "Challenger's objection #3 on handoff latency is what surfaced this — the single-operator assumption was invisible until we tried to calculate inter-stage handoff costs."
- (c) "A team-coordination approach could work if we can define a handoff protocol that bounds latency to under 2 hours per stage."

If the Builder can write that, the SELF-FAIL is honest discovery. If they can't, they're trying to exit.

## After topic close

Do a 2-minute retrospective.

### Builder
- Did Builder absorb criticism or just defend better?
- Did Builder improve truth?
- Any evasive SELF-FAIL behavior? Did flags include all three elements?
- Did revision proportionality statements match the actual scope of changes?

### Challenger
- Did Challenger raise the strongest real objection early enough?
- What did Challenger miss?
- Did it waste objection slots?
- Was the unraised-risk self-audit honest or performative?

### Process
- Did framework surface the real disagreement?
- Did procedure help or block truth?
- Was REFRAME used? Correctly or lazily?
- Was round extension used? Reasoning substantive?
- Any rule to patch before next run?

## Default recommendation for your tests

Use:
- **`[BUILDER_MODEL]` as Builder first**
- **`[CHALLENGER_MODEL]` as Challenger first**

Then swap roles on a second topic.

That gives you a better read on role-fit, not just raw model quality.
