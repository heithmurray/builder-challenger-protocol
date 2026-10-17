# Builder-Challenger Protocol
### Version 1.7 — April 24, 2026
### Formerly the Adversarial Process Framework (v1.5 to v1.7)
### Author: Heith Murray (v1.5); refined with AI assistance and external review (v1.6, v1.7)
### License: CC BY 4.0 (see LICENSE)

---

## What This Is

A reusable framework for running two AI models against each other to produce high-quality, battle-tested deliverables. One model builds. The other attacks. They loop until genuine agreement is reached. A human makes all final calls.

This framework is project-agnostic. It can be applied to any research, strategy, or build process where adversarial pressure improves output quality.

---

## What Changed From v1.6

Version 1.7 keeps the v1.6 structure intact. The v1.6 framework was already handling most failure modes well; v1.7 addresses four residual gaps and tightens two existing rules without adding bloat:

1. **REFRAME escape hatch.** A new Operator move for cases where neither the Builder's approach nor the Challenger's objections are solving the right problem. Closes the structural gap where a third path gets filtered out.
2. **Truth override targeting rule.** Tightens the existing truth-override reset to prevent the Operator from sliding into naming the answer rather than naming the dodged question.
3. **Sign-off self-audit.** Adds a pre-approval Challenger self-check for what wasn't raised, turning the existing "judged on what you miss" incentive into a procedural gate.
4. **Mid-loop round extension.** Adds an explicit Operator move to extend the round limit once with reasoning, distinct from the pre-Round-1 limit-setting already in v1.6.
5. **Revision proportionality tier-matching.** Tightens the existing Proportional revision rule by requiring Builder to state objection tier and match revision scope to it.
6. **SELF-FAIL three-element rigor.** Tightens the existing SELF-FAIL rule by requiring specific structured reasoning, not just any reasoning.

**Doc hygiene:** Model names are replaced with `[BUILDER_MODEL]` and `[CHALLENGER_MODEL]` placeholders throughout. The framework is provider-agnostic by design — model selection is a deployment decision, not a framework decision. Fill in the placeholders with whichever two models you're running for a given test.

---

## The Problem This Solves

AI models are people-pleasers. Left to their own devices, they produce smart-sounding work that nobody ever stress-tests. When two models are told to "challenge each other" without structure, the result is one of three failure modes:

**Drift** — Both models go on tangents, producing long essays that wander away from the actual question. Energy goes into sounding thorough instead of being useful.

**Performative disagreement** — Models "push back" on surface-level wording while agreeing on substance. The output looks adversarial but nothing actually gets pressure-tested.

**Fake consensus** — After several rounds, models converge to end the loop. Concessions are vague ("in the interest of moving forward"), and the final output is a compromise that neither model would defend under real scrutiny.

This framework uses structure to force genuine adversarial pressure — not attitude, not prompting, not hoping the models feel combative. The format itself makes drift, theater, and fake consensus structurally difficult.

---

## Roles

### Builder ([BUILDER_MODEL])

The Builder produces all deliverables. Research docs, strategy proposals, architecture specs, final locked files — all come from one voice. The Builder's job is to produce the strongest possible version of whatever the current topic demands, defend it under critique, and incorporate valid criticisms without diluting the work.

The Builder does not get defensive. Valid criticism gets accepted explicitly. Invalid criticism gets rejected with specific reasoning. The Builder never concedes a point just to end a round.

**Builder Self-Fail:** If the Builder determines mid-revision that the core approach is fundamentally broken — an accepted objection cascades into a problem that cannot be patched, or a critical assumption collapses — the Builder may flag SELF-FAIL in the "Remaining open questions" section. A valid SELF-FAIL flag must contain three elements:

- **(a) The specific assumption or approach that's broken** — name it concretely, not generally.
- **(b) Why this required adversarial pressure to surface** — explain why this wasn't obvious at v1.0, to distinguish honest discovery from evasion.
- **(c) What would have to be true for a different approach to work** — define the conditions that would make a restart viable, to prevent SELF-FAIL from being used as a blanket exit.

A SELF-FAIL that omits any of the three elements is rejected by the Operator and the loop continues. SELF-FAIL is an honesty mechanism, not an escape hatch from hard revision work.

The Operator then decides: restart the topic with a new approach (version resets to v[topic].0), or continue the current loop if the Operator disagrees with the Builder's assessment. This prevents a round of theater where both sides know the approach is dead but the format forces continued iteration.

### Challenger ([CHALLENGER_MODEL])

The Challenger does not produce deliverables. The Challenger's sole job is to find what's wrong, what's missing, what's assumed, and what would be most expensive if the Builder is wrong. The Challenger attacks the work — not the wording, not the tone, not the formatting. The substance.

The Challenger does not suggest alternatives unless directly asked. The Challenger identifies problems. The Builder solves them. This separation prevents the Challenger from drifting into co-authoring, which kills the adversarial dynamic.

**Permitted exceptions:** The Challenger may propose tests, validation criteria, falsification conditions, and disconfirming evidence to seek. These are pressure-testing tools, not deliverable content. The Challenger still never produces draft sections, rewritten passages, or replacement deliverables.

**Ledger ownership:** The Challenger owns the canonical Objection Ledger. The Builder references the ledger in responses but does not modify its state. The Challenger updates the ledger each round. If the Builder marks an objection as "resolved" in its response, that status is not final until the Challenger confirms it in the next ledger update. This prevents the Builder from unilaterally closing objections that were only partially fixed.

**Challenge-quality duty:** The Challenger is responsible not only for raising objections, but for raising the right objections. Missing the most consequential flaw is a Challenger failure even if the review looks technically well-structured.

### Operator

The Operator manages handoffs, reviews agreements, and makes all go/no-go decisions. The Operator does not mediate arguments. The Operator does not rewrite outputs. The Operator's job is to keep the process moving and make final calls when the models can't resolve on their own.

The Operator's decision is final and non-appealable. When the Operator makes a call, both models accept it and move forward.

**Operator private scorecard:** The Operator keeps a lightweight private scorecard each round. It is not passed into the loop unless needed for a reset or final decision. The scorecard contains four fields only:
- Strongest valid objection raised this round
- Strongest material risk still unraised
- Weakest procedural move this round
- Did the revision improve truth, or only defensibility?

This reduces cognitive load and makes model-quality comparisons cleaner without bloating the visible process.

---

## The Loop

Every topic goes through the same loop. No exceptions.

### Step 1 — Builder Produces

The Builder delivers a complete output for the current topic. Not a draft. Not an outline. The best version the Builder can produce on the first pass. The Builder labels the output with its version number (see Versioning).

### Step 2 — Challenger Reviews

The Challenger responds using the **Challenger Review Format** (below). No essays. No freeform feedback. The structured format only. Each objection is scope-tagged, severity-rated, and evidence-typed.

### Step 3 — Builder Responds

The Builder responds using the **Builder Response Format** (below). Every objection gets an explicit accept or reject with reasoning. Rejections must be supported by evidence of equal or higher tier than the objection, or by demonstrating a concrete flaw in the objection's reasoning or calculation. The Builder produces a revised output incorporating accepted criticisms, with an updated version number. If the Builder determines the core approach is broken, it flags SELF-FAIL (see Builder Self-Fail under Roles).

### Step 4 — Convergence Check

After each Builder revision, the Challenger reviews the updated output and updates the canonical Objection Ledger. Queued objections from prior rounds must be explicitly dispositioned — each one is either re-raised as open, dropped as mooted by revision, dropped as conceded with reason, or reclassified as later-topic. No silent expiration. The loop continues until the Challenger can complete the **Sign-Off Checklist** (below) — meaning all objections are resolved, disproven, or explicitly accepted by the Operator as a trade-off.

### Step 5 — Operator Approval

Once both models agree, the Operator reviews the final output using the **Operator Approval Checklist** (below). The Operator approves (referencing the version number), rejects with specific feedback, or sends it back into the loop with a targeted question. If sent back, the version number increments in sequence.

Only after Operator approval does the next topic begin. Approved topics are locked (see Topic Locking).

---

## Structured Formats

These formats are mandatory. They exist to prevent drift, force specificity, and make the Operator's review job simple. Freeform responses are not allowed during the adversarial loop.

### Verdict Definitions

**REVISE** — The output has fixable objections. The Builder can resolve them within the current loop without reframing the core claim.

**FAIL** — The core claim collapses or the topic needs a fundamental restart or reframe. Fixing individual objections is not sufficient; the approach itself is flawed.

**PASS** — No blocking objections remain. Only valid when the Challenger is ready to proceed to the Sign-Off Checklist. PASS without a completed Sign-Off Checklist is not valid.

### Challenger Review Format

Every Challenger review must contain exactly these sections, in this order:

**Verdict:** PASS, FAIL, or REVISE (see Verdict Definitions above).

**Core claim being evaluated:** One sentence restating what the Builder is asserting. This forces the Challenger to engage with the actual argument, not a strawman.

**What survives scrutiny:** Name at least one specific element that is solid and should not change. General praise ("the structure is sound") does not count. Specific praise ("the fee calculation correctly uses taker rates at 0.1% for market orders on Binance") does count. On a FAIL verdict, the Challenger states "none material" or identifies specific salvageable fragments worth preserving if the topic restarts — not forced praise, but a salvage assessment that gives the Builder useful signal for the next approach.

**Objections (numbered, max 3 per round):** The top 3 most important problems, numbered. At least one objection each round must target what the Challenger believes is the single most consequential risk to the deliverable — not the easiest to articulate, not the most defensible, but the one that would cost the most if missed. This prevents a weak Challenger from spending all three slots on safe, secondary critiques while the real problem goes unraised. Objection IDs are persistent for the life of the topic — new objections get new IDs, old objections are never renumbered, only reclassified. Each objection must include:

- **Scope tag:** IN-SCOPE (directly relevant to current topic), DEPENDENCY RISK (relevant but belongs partly to a future topic), or LATER-TOPIC (belongs entirely to a future topic). Only IN-SCOPE objections can block approval. DEPENDENCY RISK objections default to IN-SCOPE if they could invalidate the current topic's recommendation, assumptions, economics, feasibility, or safety — unless the Operator explicitly rules otherwise. LATER-TOPIC objections are logged and deferred.
- **Severity:** CRITICAL, SIGNIFICANT, or MINOR (see Severity Definitions below). Every SIGNIFICANT or CRITICAL objection must include one sentence explaining why the next lower severity would be insufficient.
- **Evidence type:** What kind of evidence supports this objection (see Evidence Hierarchy below).
- **The objection itself:** What's wrong, why it matters, and what evidence would resolve it.

No vague complaints. "This feels weak" is not an objection. "The fee calculation assumes Binance maker fees but the strategy uses market orders which pay taker fees, inflating costs by 0.15%" is an objection.

If more than 3 objections exist, the Challenger flags remaining items as "queued for next round" in a single line with their IDs. Queued objections must be explicitly dispositioned in the next round (see Step 4).

If every objection is rated MINOR, the Builder can call that out and request the Challenger either upgrade the severity with evidence or concede.

**Fatal-flaw scan:** In every review, the Challenger must state whether Objection #1 is the most expensive plausible mistake in the output. If not, the Challenger must explain why the most expensive plausible mistake is not yet ripe enough to object on with the available evidence. This makes "I didn't have enough confidence" explicit instead of invisible.

**Scope tag disputes:** If the Builder disagrees with a scope tag, it is not argued through the adversarial loop. The Builder flags the dispute as a one-line question to the Operator. The Operator rules. The loop continues on substance, not scope.

**Objection Ledger:** The Challenger owns this ledger and is the only party that updates it. Running status of all objections across rounds for this topic. Objection IDs are persistent — never renumbered. The Builder may claim an objection is resolved in its response, but that status is not confirmed until the Challenger verifies and updates the ledger.

- Open: [list by ID]
- Resolved: [list by ID]
- Queued: [list by ID]
- Dropped: [list by ID with reason — must specify: mooted by revision / conceded / reclassified as later-topic]
- Accepted Risk: [list by ID with Operator approval note]
- Disproven: [list by ID]

**Hidden assumptions:** What must be true for the Builder's output to hold that isn't explicitly stated or defended.

**Most expensive mistake:** If the Builder is wrong about one thing in this output, which error would cost the most (time, money, or credibility)? This forces prioritization.

**Recommended next move:** What specific action should the Builder take in the next revision.

### Builder Response Format

Every Builder response must contain exactly these sections, in this order:

**Response to verdict:** Accept or contest, with reasoning.

**Accepted objections (numbered, matching Challenger's IDs):** For each accepted objection — what's being changed and why the Challenger is right. Include evidence type for supporting reasoning.

**Rejected objections (numbered, matching Challenger's IDs):** For each rejected objection — specific reasoning for why the criticism doesn't hold. Rejection must be supported by evidence of equal or higher tier than the objection's evidence, or by demonstrating a concrete flaw in the objection's reasoning or calculation. A rejection supported only by lower-tier evidence than the objection can be challenged by the Challenger and must be upgraded or the objection accepted.

**Weak objection challenge:** If any objection was rejected due to inadequate evidence tier, incorrect scope tag, or insufficient specificity, the Builder flags it here. The Challenger must either materially strengthen the objection in the next round or drop it with reason. Re-raising the same weak objection without material strengthening is not permitted — the Challenger must upgrade the evidence, narrow the claim, or concede.

**Assumption responses:** For each hidden assumption the Challenger identified — either defended with evidence or acknowledged and incorporated into the revised output.

**Revisions made:** Specific list of what changed in the output, with version delta from the prior round (what was added, removed, or modified).

For each accepted objection, the Builder must state: **"Objection [ID] was tier [CRITICAL/SIGNIFICANT/MINOR]. My revision changed [specific content]. The proportion is appropriate because [reasoning]."** This tier-matching statement makes revision proportionality verifiable rather than subjective. Accepting a CRITICAL objection with only a wording change is a procedural win, not a substantive one — the proportion statement must justify why the change scope matches the objection severity.

Revisions should be proportional to accepted objections — major expansion of the deliverable beyond what the accepted objections require must be explicitly justified. Unrelated expansion can be flagged by the Challenger or reset by the Operator.

**Remaining open questions:** Anything unresolved that needs further research or Operator input. If the Builder believes the core approach is broken, SELF-FAIL is flagged here with the three required elements: (a) the specific broken assumption, (b) why it required adversarial pressure to surface, (c) what would have to be true for a different approach to work.

**Updated output:** The revised deliverable incorporating all accepted changes, labeled with the new version number.

### Sign-Off Checklist

Before the Challenger can approve a final output, it must explicitly answer all of the following:

1. **Have all my numbered objections been resolved, disproven, or accepted by the Operator as a trade-off?** (Yes/No — if No, list unresolved objection IDs. "Addressed" does not count as resolved.)
2. **Am I conceding any objections? If so, state each concession and the specific reason I'm dropping it.** ("In the interest of moving forward" is not a valid reason. "The Builder demonstrated with fee data that my concern about cost impact was overstated by 80%" is a valid reason.)
3. **Final objection scan: I have actively tested this output for hidden assumptions, missing economics, dependency failures, scope drift, and untested claims.** State the single strongest remaining argument against this output, then explain why it is an acceptable risk or trade-off. If any unresolved issue is above MINOR severity, approval cannot be granted.
4. **Unraised-risk self-audit:** State the strongest argument against this deliverable that I did **not** raise as a numbered objection, and why I chose not to raise it. This argument must meet the same evidence-tier standard as a real objection — if the strongest unraised argument is above MINOR severity, I cannot approve and must raise it as a new objection in the next round. If I cannot name any unraised argument at all, my objections were not comprehensive and approval is premature.
5. **Objection Ledger final state:** List all objections by persistent ID as Resolved, Disproven, Dropped (with reason: mooted / conceded / reclassified), or Accepted Risk. Open count must be zero.
6. **Did I miss any material risk earlier in the loop that only became obvious late?** (Yes/No — if Yes, name it. This does not block approval automatically, but it is logged against Challenger quality.)
7. **Does this output meet the quality bar for the project it serves?** (Yes/No)
8. **Final verdict:** APPROVED or NOT APPROVED.

---

## Severity Definitions

These definitions are binding. Both models use the same rubric. Every objection rated SIGNIFICANT or CRITICAL must include one sentence explaining why the next lower severity would be insufficient. This forces calibration and prevents severity inflation.

**CRITICAL** — If this is wrong, the deliverable fails its purpose or creates major risk. The project cannot proceed safely with this error in place. Examples: wrong market selected, risk guardrail that doesn't actually prevent the failure it's designed to prevent, cost math that's off by an order of magnitude.

**SIGNIFICANT** — Materially weakens the reliability, economics, or credibility of the deliverable, but is not fatal. The project could proceed, but the output is meaningfully worse with this flaw. Examples: fee estimate that's off by 50%, missing failure mode that's plausible but not certain, assumption that's defensible but untested.

**MINOR** — Improves polish, clarity, or edge-case robustness without changing core viability. The deliverable works with this flaw; it just works slightly less well. Examples: formatting inconsistency, missing citation for a well-known fact, edge case that's unlikely to occur in practice.

---

## Evidence Hierarchy

When objections, defenses, or claims cite evidence, both models must identify which type they're using. Strongest to weakest:

**Tier 1 — Direct calculation or reproduced math.** The model ran the numbers and can show the work. This is the strongest form of evidence because it's independently verifiable.

**Tier 2 — Primary source.** Raw spec, original document, official API documentation, exchange fee schedule, regulatory text. The actual source, not someone's summary of it.

**Tier 3 — Empirical results with stated assumptions.** Backtest data, published research with methodology disclosed, measured performance with conditions specified. Strong, but only as strong as the assumptions.

**Tier 4 — Secondary summary.** News article, blog post, analyst report, third-party review. Useful for context but not sufficient as sole support for a CRITICAL objection.

**Tier 5 — Model inference or intuition.** The model believes this to be true based on training data or reasoning, but cannot point to a specific source. Acceptable for raising questions and flagging risks. Not acceptable as sole support for any objection rated SIGNIFICANT or above.

**Enforcement rules:**
- A CRITICAL objection supported only by Tier 5 evidence can be challenged by the Builder and must be upgraded or dropped.
- A MINOR objection can be supported by any tier.
- When rejecting an objection, the Builder must provide evidence of equal or higher tier than the objection's evidence, or demonstrate a concrete flaw in the objection's reasoning or calculation. A rejection supported only by lower-tier evidence can be challenged by the Challenger and must be upgraded or the objection accepted.

---

## Deadlock Protocol

Default round limit is 5. The Operator may set a different limit at the start of any topic based on complexity — but must declare it before Round 1. If no custom limit is set, 5 applies.

**Mid-loop round extension:** The Operator may extend the round limit once (and only once) during a loop with explicit reasoning. Format: `EXTEND — [current round] to [new limit]. Reason: [what substantive work remains that requires more rounds].` A valid extension reason names specific substantive work that needs more rounds — "we're close to resolution on objection #3" is valid; "let's give it more time" is not. A second extension attempt is a deadlock by definition — if two extensions are needed, the framework isn't converging on its own, and the Final Position Statement process activates immediately regardless of remaining rounds.

If the loop hits the round limit without convergence, the deadlock protocol activates:

1. The loop stops. No more exchanges on this topic.
2. The Operator provides a 2-3 sentence summary of the core dispute to both models, alongside the latest round's output. This ensures both models have sufficient context to write informed final positions despite the minimal handoff protocol.
3. Each model submits a **Final Position Statement** — one paragraph maximum. Contains: their claim, their single strongest piece of evidence (with evidence tier identified), and why they believe the other model is wrong.
4. The Operator reads both statements and makes the call.
5. The Operator's decision is final. No appeals. No "one more round."
6. The Builder produces the final output incorporating the Operator's decision, labeled with version v[topic].F.
7. The next topic begins.

Deadlock escalation is not a failure. Some disagreements are genuine judgment calls, and that's exactly what the human is for.

---

## Reset Command

If the process drifts — models start writing essays, arguing about wording instead of substance, producing performative disagreement, or ignoring the structured formats — the Operator issues a reset.

**The reset command is: "RESET — [specific instruction]"**

Examples:
- "RESET — Back to structured formats. Challenger, use the review format."
- "RESET — You're arguing about the wrong thing. The question is [X]."
- "RESET — Both of you are agreeing too easily. Challenger, do the final objection scan before signing off."

**Truth-over-procedure override:** If the Operator judges that both models are technically complying with the framework while avoiding the main substantive risk, the Operator may issue a truth override reset. This overrules procedural comfort. The next round must attack the real issue directly even if the prior round was formally valid.

Format: `RESET — Truth override. You're both dodging [specific dodged question].`

**Targeting rule for truth override:** The Operator may name the question that's being dodged. The Operator may **not** name the answer to that question. Naming the question preserves the Operator's role as process manager. Naming the answer turns the Operator into a third agent, which breaks the framework. Valid: `RESET — Truth override. You're both dodging customer data locality.` Invalid: `RESET — Truth override. The answer is on-premise because of GDPR.` The second form is the Operator breaking role. If the Operator can only surface the question as a full answer, the loop is no longer adversarial — it's operator-directed, and should be paused, not reset.

**REFRAME escape hatch:** If both models are technically compliant but neither Builder's approach nor Challenger's objections are solving the right problem, the Operator may issue a REFRAME reset. This is distinct from a standard reset or a truth override because it directs the Builder to restart from a new constraint rather than adjust within the current approach.

Format: `RESET — REFRAME. Neither current path solves the real problem. Builder, rebuild from scratch with this constraint: [X]. Versioning resets to v[topic].0.`

**Guardrail for REFRAME:** REFRAME may only be issued when the Operator can name **why** the current paths are insufficient — a specific incompatibility between both paths and the real objective. If the Operator cannot name the insufficiency, the issue is probably Operator impatience, not process failure, and REFRAME is not valid. "I don't like either answer" is not sufficient reason. "Both paths assume the deliverable will be used by a single operator, but the real use case is a team of five with conflicting priorities" is sufficient reason. REFRAME is a heavy move and should be rare.

When any reset is issued, both models acknowledge it and immediately comply. No meta-discussion about the reset. No explaining why the drift happened. Just snap back to the format and continue.

---

## Handoff Protocol

When the Operator passes output between models, what gets sent matters as much as the format. Bad handoffs reintroduce drift.

**What the Challenger receives:** The Builder's latest structured output only — the updated deliverable plus the Builder Response Format fields — plus two persistent items: the current Objection Ledger (from the Challenger's own prior round) and the version delta from the prior round. Not the full conversation history. Not prior rounds beyond what's captured in the ledger.

**What the Builder receives:** The Challenger's latest structured review only — the Challenger Review Format fields including the canonical Objection Ledger. Not the Operator's commentary. Not prior Builder versions.

**What the Operator keeps:** Everything. The Operator maintains the full exchange history for context, but the models only see the latest round's output plus the persistent ledger. This prevents context bloat, reduces token waste, and keeps both models focused on the current state of the work rather than relitigating prior rounds.

**Handoff format:** When pasting output between models, the Operator uses a simple header: "ROUND [X] — [BUILDER/CHALLENGER] OUTPUT — v[topic].[round]" followed by the structured content. Nothing else. No editorializing, no "here's what I think," no framing. The structure does the work.

---

## Versioning

Every deliverable is versioned across rounds. The Builder labels each revision explicitly.

**Format:** v[topic].[round] — for example, Topic 1 first draft is v1.0, first revision after Challenger feedback is v1.1, second revision is v1.2. If the topic goes to deadlock and the Operator makes a call, the final version is labeled v[topic].F (for Final).

**Operator-initiated re-entry:** If the Operator sends an approved or in-progress version back into the loop with a targeted question, the version increments in sequence from where it left off. If v1.3 was the last reviewed version and the Operator sends it back, the next Builder output is v1.4.

**Self-Fail restart:** If the Builder flags SELF-FAIL and the Operator approves the restart, versioning resets to v[topic].0 for the new approach. The prior version history is preserved in the Operator's records but does not carry forward into the new loop.

**REFRAME restart:** If the Operator issues REFRAME, versioning also resets to v[topic].0 for the new approach. The prior version history is preserved in the Operator's records as evidence of what was tried and why it didn't fit.

**The Operator's review is always against the latest version number.** When approving, the Operator references the version: "v1.3 APPROVED." This creates an unambiguous record of what was locked.

---

## Topic Locking

Once the Operator approves a topic, it is locked. The deliverable is final. Neither model can reopen, revise, or relitigate a locked topic during the adversarial process.

If a later topic reveals a problem with a previously locked topic — a hidden dependency, a flawed assumption that only becomes visible downstream — that is not a reopening. It is a new topic added to the queue. It goes through the full adversarial loop from scratch with its own versioning. The original locked deliverable remains locked until the new topic produces an approved replacement.

**Priority insertion:** When a new topic is created from a downstream discovery, it is inserted as the next topic in the queue by default. The Operator may override this and place it elsewhere if the dependency is not blocking. The Operator decides insertion point; "next up" is the default.

This prevents the process from becoming an endless revision cycle where nothing is ever truly finished.

---

## Operator Approval Checklist

Before the Operator can approve a topic, the Operator must confirm all of the following:

1. **Reviewed the latest version of the deliverable.** (Version number: ___)
2. **Reviewed the final Objection Ledger.** No open objections remain. All dropped objections have documented reasons (mooted / conceded / reclassified). No objection quietly disappeared between rounds.
3. **Reviewed all concessions in the Sign-Off Checklist.** Concession reasons are substantive, not procedural.
4. **Confirmed no queued objection above MINOR severity was left unresolved.** If any SIGNIFICANT or CRITICAL objection was queued and never re-raised or explicitly dispositioned, the Operator flags it for the Challenger to address before approval.
5. **Reviewed the Challenger's unraised-risk self-audit.** The argument the Challenger named as "strongest unraised" is genuinely below MINOR severity, or was raised and resolved as a new objection. A self-audit that returns "none" is reviewed with skepticism — zero unraised arguments across an entire loop is unusual and may indicate insufficient scrutiny.
6. **Reviewed the private scorecard.** No obvious material risk remains unraised without deliberate acceptance.
7. **Final decision:** APPROVED (with version number) / REJECTED (with specific feedback) / RETURNED TO LOOP (with targeted question).

---

## Retrospective Scoring (Private to Operator)

After each topic closes, the Operator records a short retrospective. This is for model comparison and framework tuning, not for reopening the topic.

**Builder score prompts:**
- Did the Builder absorb valid criticism cleanly?
- Did the Builder improve truth or only improve defense?
- Did the Builder use SELF-FAIL honestly or evasively? (Did SELF-FAIL flags include all three required elements?)
- Did revision proportionality statements match the actual scope of changes?

**Challenger score prompts:**
- Did the Challenger raise the strongest real objection early enough?
- What was the strongest material risk the Challenger missed?
- Did the Challenger spend objection slots on secondary issues while a more expensive risk existed?
- Did the unraised-risk self-audit surface genuinely significant missed arguments, or was it performative?

**Process score prompts:**
- Did the framework surface the real disagreement?
- Did procedure help truth, or become a shield against it?
- Was REFRAME used? Was it used correctly (specific incompatibility named) or lazily (operator impatience)?
- Was the round extension used? Was the reasoning substantive?
- Should any new rule be added before the next topic?

This retrospective does not change the locked result. It improves model selection and future runs.

---

## Rules

**Length control:** Challenger reviews should be under 500 words — the 3-objection-per-round cap makes this achievable. If a round genuinely requires more space, the Challenger flags it and the Operator can grant an exception. Builder responses should be as long as needed for the revised output, but the response-to-objections section should be under 500 words. If either model starts producing walls of text in the argument sections, the Operator issues a reset.

**Proportional revision:** Builder revisions must be proportional to accepted objections. Changes should be targeted to what was accepted. For each accepted objection, the Builder must state the objection's tier, what the revision changed, and why the proportion is appropriate. Major expansion of the deliverable beyond what the accepted objections require must be explicitly justified. Unrelated expansion can be flagged by the Challenger or reset by the Operator. This prevents the Builder from burying weak spots under volume or making cosmetic changes to CRITICAL objections.

**No co-authoring:** The Challenger critiques. The Builder writes. The Challenger may propose tests, validation criteria, and disconfirming evidence to seek — these are pressure-testing tools, not deliverable content. The Challenger never produces alternative drafts, suggested rewrites, or "here's how I would say it" passages. The moment the Challenger starts writing deliverable text, the adversarial dynamic is dead.

**No tone management:** Neither model should comment on the other's tone, attitude, or style. The only thing that matters is whether the substance holds up. "Your response feels dismissive" is never a valid part of an exchange.

**No meta-discussion:** Models do not discuss the process during the process. No "I think we're making good progress" or "This has been a productive exchange." Evaluate the work, not the experience.

**Specificity standard:** Every objection must be specific enough that the Builder knows exactly what to fix. Every concession must include the specific reason. Every rejection must include the specific counter-evidence at the required evidence tier. If it can't be made specific, it doesn't belong in the exchange.

**Weak objection accountability:** If an objection is rejected by the Builder due to inadequate evidence tier, incorrect scope tag, or insufficient specificity, the Challenger must either materially strengthen the objection in the next round (upgrade evidence, narrow the claim, or add specificity) or drop it with documented reason. Re-raising the same weak objection without material strengthening is not permitted. This reduces low-quality critique pressure and ensures the Challenger's objections earn their place.

**Anti-lawyering:** The framework exists to improve the work, not to win arguments. If procedural challenges — evidence-tier disputes, scope-tag disputes, specificity challenges, weak-objection flags, proportional-revision complaints — outnumber substantive engagement with the actual deliverable across two consecutive Builder rounds, the Operator issues a reset. Both models are reminded: the goal is a better deliverable, not a more defensible position. A pattern of procedural maneuvering that delays substantive progress is treated as drift and handled accordingly.

**One topic at a time:** The loop resolves one topic completely before the next topic begins. No "while we're at it" tangents. No pulling forward concerns from future topics. If the Challenger raises something that belongs to a later topic, it is scope-tagged as LATER-TOPIC, logged in the Objection Ledger, and deferred. The current loop continues on its own topic.

**Closure standard:** An objection is closed only when it meets one of these four states: fixed in the deliverable (resolved), proven wrong by the Builder with evidence at the required tier (disproven), explicitly accepted by the Operator as a known trade-off (accepted risk), or determined to belong to a different project entirely — not a later topic in the current queue (out of scope). Out-of-scope closure can only be applied by Operator ruling — neither the Builder nor the Challenger can unilaterally close an objection as out of scope. The Operator must include a note identifying where the issue belongs or why no destination exists. The word "addressed" is not a valid closure state. If the Builder claims to have "addressed" an objection without meeting one of these four standards, the Challenger rejects the closure.

**Objection ID persistence:** Objection IDs are assigned once and persist for the life of the topic. New objections get new IDs. Old objections are never renumbered, only reclassified. If an objection evolves through rounds, it keeps its original ID with a note on what changed. This prevents fake resolution through relabeling.

**Missed-fatal-flaw accountability:** If a later round, deadlock statement, or Operator review reveals a more consequential flaw than anything the Challenger raised earlier, that miss is recorded in the retrospective even if the final deliverable is approved. This does not automatically invalidate the topic, but it does count against Challenger quality.

---

## How to Use This Framework

1. Define your topic list and order before starting.
2. Assign Builder and Challenger roles.
3. Operator sets round limit per topic (default: 5) before Round 1.
4. Builder produces first output for Topic 1, labeled v1.0.
5. Challenger reviews using the structured format with scope tags, severity ratings (with justification for SIGNIFICANT+), evidence types, and the fatal-flaw scan. Challenger establishes the canonical Objection Ledger.
6. Builder responds with evidence at equal or higher tier than objections when rejecting. Revisions are proportional to accepted objections, with tier-matching proportion statements per accepted objection. Builder flags any weak objections for upgrade-or-drop.
7. Challenger updates the canonical Objection Ledger. Queued objections are explicitly dispositioned each round — re-raised, mooted, conceded, or reclassified. No silent expiration. Weak objections flagged by the Builder are either strengthened or dropped.
8. Operator keeps the private scorecard during the loop.
9. If the loop is approaching the round limit with substantive work remaining, the Operator may extend once with specific reasoning.
10. If both models are technically complying but dodging the real issue, the Operator issues truth override reset (naming the question, not the answer).
11. If neither path is solving the right problem, the Operator issues REFRAME with specific incompatibility named.
12. Loop continues until Sign-Off Checklist is completed with all objections resolved, disproven, accepted as trade-offs, or ruled out of scope — and the Challenger has completed the unraised-risk self-audit.
13. Operator reviews using the Operator Approval Checklist and approves with version number.
14. Topic is locked. Move to Topic 2. Repeat.
15. If the Builder flags SELF-FAIL with all three required elements, the Operator decides: restart topic or continue.
16. If deadlock hits on any topic, follow the deadlock protocol.
17. If drift occurs at any point, issue a reset.
18. If scope tag disputes arise, Operator rules directly — not through the adversarial loop.
19. If a locked topic needs revision due to downstream discovery, add a new topic to the queue (default: next up).
20. After topic close, complete the retrospective scoring before starting the next high-stakes topic.

The Operator's responsibilities are: managing handoffs between models, verifying Objection Ledger integrity across rounds (no silent disappearances), reviewing final agreements using the Operator Approval Checklist, making go/no-go decisions, ruling on scope tag disputes and out-of-scope closures, ruling on Builder SELF-FAIL requests, issuing resets (including truth override and REFRAME), extending round limits when appropriate, breaking deadlocks, managing queue priority when new topics are inserted, and keeping the private scorecard. The Operator should not be rewriting outputs, mediating tone disputes, or managing the models' relationship. If the Operator is doing more than reviewing, deciding, and managing flow, the framework isn't working — issue a reset.
