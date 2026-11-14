---
name: simplify
description: Review the changed code for reuse, simplification and efficiency, then apply the fixes. Quality only; it does not hunt for bugs.
argument-hint: Optional file paths or focus
---

# Simplify

Review the code changed in the working tree and apply cleanups. Behavior must stay the same.

Scope: $ARGUMENTS

If no scope is given, use `git diff` and `git diff --cached`. Without any diff, use the most recent commit.

## Checks

1. **Reuse**: A helper, utility or existing abstraction in the repository already does what the new code does. Replace the duplicate with it.
2. **Simplification**: Remove dead code, needless indirection, redundant conditions, unused parameters and variables, and abstractions with a single caller.
3. **Efficiency**: Remove repeated work, avoidable allocations, N+1 access patterns, and sequential awaits that could run in parallel.
4. **Altitude**: Each function should work at one level of abstraction. Extract or inline until the level is consistent.
5. **Comments**: Delete comments that restate the code. Keep comments that explain a non-obvious reason.

## Procedure

1. Read the diff, then read the surrounding code of each changed file.
2. Search the repository for existing code that overlaps with the new code before proposing a new helper.
3. Apply each fix with a minimal edit. Follow the naming and style of the surrounding code.
4. Run the project's build, type check, linter and existing tests. Do not change the tests to make them pass.
5. Report what changed and why, one line per change. Mention findings you left alone and the reason.

## Boundaries

- Do not change public interfaces, outputs or side effects.
- Do not fix bugs here. Report a bug you notice, and leave the code as it is.
- Do not touch code outside the scope unless a fix requires it.
