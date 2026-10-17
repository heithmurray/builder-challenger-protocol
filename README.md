# Adversarial Process Framework

**Version 1.7.** A structured way to make two AI models stress-test each other's work, with one human making every final call.

One model builds. The other attacks. They loop, in a fixed format, until real agreement is reached. The human (the Operator) manages handoffs and decides go or no-go.

## Why

Left alone, AI models are people-pleasers. Told to "challenge each other" without structure, they tend to fail in one of three ways:

- **Drift:** long essays that wander away from the question.
- **Performative disagreement:** pushback on wording while agreeing on substance.
- **Fake consensus:** vague concessions to end the loop.

This framework uses structure, not attitude, to make those failures hard: scope tags, severity ratings, an evidence hierarchy, a canonical objection ledger, and a sign-off checklist.

## What's here

| File | Use it for |
|---|---|
| [framework.md](framework.md) | The framework itself: roles, the loop, formats, rules |
| [operator-playbook.md](operator-playbook.md) | Running it live, step by step |
| [prompt-pack.md](prompt-pack.md) | Copy-paste starter prompts for the Builder and the Challenger |
| [test-sheet.md](test-sheet.md) | One sheet per test run, to score how it went |

## Quick start

1. List your topics in order, and pick which model builds and which attacks.
2. Set the round limit before Round 1. **The default is 5.** Fill in `[your name]` in the playbook and test sheet.
3. The Builder produces a first draft; the Challenger reviews it in the structured format and keeps the objection ledger.
4. Loop until the sign-off checklist is complete, then approve the version and lock the topic.

## Built-in brakes

- **A 5-round default limit,** so the loop can't fight forever over the last 1%.
- **One extension per loop,** only with a stated reason.
- **A deadlock protocol** if the limit is reached without agreement.
- **Reset and reframe commands** for when the models drift or solve the wrong problem.

## Version

This is v1.7 (April 24, 2026). Each file lists what changed from v1.6.

## License

[[LICENSE TBD: to be chosen before publishing]]
