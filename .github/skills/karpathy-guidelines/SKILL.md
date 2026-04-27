---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, surface assumptions, and define verifiable success criteria. Derived from Andrej Karpathy's observations on LLM coding pitfalls (https://github.com/forrestchang/andrej-karpathy-skills, MIT).
license: MIT
---

# Karpathy Guidelines

Four principles that target the most common LLM coding failure modes: silent assumptions, overcomplication, drive-by edits, and vague execution.

**Tradeoff:** These bias toward caution over speed. For trivial tasks (typos, one-liners), use judgment.

---

## 1. Think Before Coding
**Don't assume. Don't hide confusion. Surface tradeoffs.**

- State assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them — don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

**Anti-pattern:** "Add export feature" → silently picks JSON, all users, file location, fields.
**Fix:** List the ambiguities (scope, format, fields, volume), propose the simplest default, ask.

## 2. Simplicity First
**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If 200 lines could be 50, rewrite it.

Ask: *"Would a senior engineer say this is overcomplicated?"* If yes, simplify.

**Anti-pattern:** Strategy pattern + config class + 30 lines of setup for one discount calc.
**Fix:** One function. Refactor only when a second use case actually appears.

## 3. Surgical Changes
**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that **your** changes made unused.
- Don't remove pre-existing dead code unless asked.

**The test:** Every changed line should trace directly to the user's request.

**Anti-pattern:** "Fix empty-email crash" diff also reformats quotes, adds type hints, tightens username rules.
**Fix:** Change only the lines that fix the empty-email case.

## 4. Goal-Driven Execution
**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

## Applying to this project (single-file `index.html`)
- **Think:** Before edits, name which slide(s) and which CSS variables / animation are affected.
- **Simplicity:** No new build tools, no frameworks, no helper abstractions for one-off effects.
- **Surgical:** Don't reformat unrelated CSS or rename existing variables when adding a feature.
- **Goal-driven:** Verify visually at 375 / 768 / 1280 / 1920 px, and confirm `prefers-reduced-motion` still works after motion changes.

## Working signals
The skill is working when diffs show:
- Only requested changes (no drive-by refactors).
- Simple-first code (no premature abstraction).
- Clarifying questions **before** implementation, not after.
- Plans with explicit verification steps for non-trivial work.
