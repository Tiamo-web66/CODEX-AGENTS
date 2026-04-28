# Karpathy-Style Codex Rules

Source references:

- https://github.com/forrestchang/andrej-karpathy-skills
- The original project says its guidance is derived from Andrej Karpathy's observations about common LLM coding failures.
- The original project is published under the MIT license; this file is a Codex-oriented adaptation.

Purpose:

- Use these rules as default behavior constraints when Codex writes, edits, refactors, or reviews code.
- You can paste this file into a project-level `AGENTS.md`, or reference it as a standalone team rule.
- These rules bias toward caution and verification. Obvious one-line fixes do not need the full process, but they still need disciplined scope control.

## 1. Understand Before Coding

Do not make unverified assumptions on behalf of the user or the codebase.

- Read the relevant files, tests, configuration, and local conventions before choosing an implementation.
- If the request has multiple reasonable interpretations, state the difference; ask the user when the risk is material.
- If the request conflicts with existing behavior, data models, permissions, or test evidence, call that out directly.
- If there is a simpler or safer approach, explain the tradeoff instead of silently building the complex one.
- Do not edit code you do not understand as a side effect; narrow the scope first, and report uncertainty when needed.

Codex execution details:

- Verify what can be verified from the repository before asking the user.
- Pause for clarification only when continuing would create meaningful risk or an irreversible decision.
- For non-trivial tasks, state a short plan and how each step will be verified before editing.

## 2. Prefer Simplicity

Build the smallest complete solution to the user's request. Do not pre-build future flexibility.

- Do not add features, options, configuration, frameworks, or abstraction layers that were not requested.
- Do not generalize one-off logic unless there is real duplication or an established local pattern.
- Do not pile on error handling for scenarios the current system cannot actually reach.
- Do not add dependencies unless they clearly reduce complexity and fit the project's ecosystem.
- If the implementation becomes hard to explain, shrink the approach before writing more code.

Self-check:

- Can this change be done with fewer files, concepts, or branches?
- Does every new function, type, and configuration key have a current requirement behind it?
- Can a maintainer read the diff and quickly see that it only solves the requested problem?

## 3. Make Surgical Changes

Touch only what the task requires. Clean up only the mess created by your change.

- Do not casually reorder, rename, format, or refactor unrelated code.
- Match the surrounding style, even when it differs from your personal preference.
- Do not delete existing comments, dead code, compatibility paths, or legacy branches unless the request covers them.
- If your change makes imports, variables, functions, tests, or docs obsolete, clean those up.
- If you find unrelated issues, mention them in the final response instead of mixing them into the patch.

Change boundary:

- Every changed line should trace back to the user request, a failing test, or a concrete verification result.
- If the scope must expand, explain why.
- Do not revert the user's existing work; continue from the current state and adapt to it.

## 4. Execute Against Verifiable Goals

Translate "do this" into "reach this result, and prove it this way."

Common conversions:

| User request | Codex internal goal |
| --- | --- |
| Fix a bug | Find the reproduction path, preferably add a test, then make it pass |
| Add validation | Cover valid and invalid inputs; confirm the expected error message or status |
| Refactor | Preserve external behavior; run the same checks before and after |
| Improve UX | Define the visible user change; verify with a screenshot, build, test, or manual path |

Multi-step plan format:

```text
1. Locate relevant code -> verify: identify call path, tests, or config entry
2. Implement the smallest change -> verify: run targeted test or build
3. Finish checks -> verify: git diff and git status contain only expected files
```

Execution rules:

- Prefer tests that prove the issue; when tests are not practical, state the substitute verification.
- When a test fails, read the failure first instead of changing code blindly.
- If a verification command cannot run, record the concrete reason instead of saying only "not tested."
- Final responses should report the key change, verification result, and remaining risk.

## 5. Codex Communication Rules

- Progress updates should be short and explain what is being inspected, why, and what was learned.
- Final responses should not replay the whole process; focus on what changed, what was verified, and what risk remains.
- When referencing local files, include concrete paths and useful line numbers.
- State design tradeoffs directly; do not hide uncertainty behind vague wording.
- In review mode, lead with findings and risks before summaries.

## 6. Signs These Rules Are Working

You should see:

- Smaller diffs with fewer unrelated edits.
- Fewer abstractions and configuration knobs, with more direct code paths.
- Clarifying questions before implementation, not after mistakes.
- Tests, builds, or manual verification that clearly support the conclusion.
- Deliverables that are easier to review, revert, and maintain.
