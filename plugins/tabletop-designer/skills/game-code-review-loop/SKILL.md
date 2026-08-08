---
description: Run an iterative second-opinion review after changing a card/board game's engine, rules, state-management, or API/content-loading code -- spawn the game-code-reviewer subagent, apply its fixes, and repeat until it reports no more issues. Use this automatically whenever you finish editing game logic or engine code, not for pure content-data edits (e.g. a JSON stat tweak or a new card added via an existing schema) unless asked to review those too.
---

# Game code review loop

Whenever you finish making a code change to a card/board game's engine, rules logic, state management, or API/content-loading code, run this loop before considering the change done.

## The loop

1. **Make the code change** as normal.
2. **Spawn the reviewer.** Invoke the `game-code-reviewer` subagent (shipped in this same plugin) via the Agent tool. Give it the specific files you changed, a short description of what the change was supposed to do, and enough surrounding context (related files, the parallel code paths it should check) to actually verify correctness rather than just reading the diff in isolation.
3. **Apply real findings yourself.** If the reviewer reports confirmed bugs, inefficiencies, or mistakes, fix them directly in the code — don't just relay the list back to the user and stop there.
4. **Re-run the reviewer** on the updated code.
5. **Repeat steps 3–4** until the reviewer reports no further issues.
6. **Report to the user** what changed and, if it's worth mentioning, what the review loop caught along the way (for example: "the reviewer caught that the solo-path fix wasn't mirrored in the group path — fixed that too").

## Guardrails

- **Bound the loop.** If you're still getting new findings after roughly 4 rounds, stop, apply what you're confident is correct, and tell the user the remaining disagreement or uncertainty explicitly rather than looping indefinitely — that usually means the underlying requirement is ambiguous, not that the reviewer needs another pass.
- **A clean first pass is a legitimate outcome**, not a sign you under-prompted the reviewer — as long as you gave it the changed files and the intent behind the change, not just a vague "check my code."
- **This is a code-quality gate, not a design review.** The reviewer checks whether the code does what was intended; it has no opinion on whether the intended mechanic is a good idea. Route design/balance questions to `game-designer` instead, separately.
- **Skip it for pure content/data edits** with no logic change — adding a card entry through an existing, already-validated schema, or tweaking a stat number in JSON. Run it whenever the change touches actual code: engine functions, API routes, validators, state-management logic, or UI logic that drives game state.
