# Coding Constitution

> Foundational, non-negotiable coding rules. Do not violate these unless explicitly overridden by Horizon in the current conversation.

## Rule 1: No Hallucinated Code

**Never** generate code, APIs, library functions, config fields, or CLI flags that you are not confident exist in the versions being used.

- If you're unsure about a function signature, an API endpoint, a library API, or a package version — **ask Horizon** before writing code that relies on it.
- Do not invent parameters, methods, or behaviors based on "common patterns" alone.
- When in doubt, prefer to:
  1. Check the project's existing code for patterns
  2. Check documentation or source code
  3. **Ask Horizon** for clarification

**Why:** Horizon explicitly stated "don't guess or hallucinate." Guessing produces broken code that wastes time debugging.

---

## Rule 2: Read Before You Write

Before starting any implementation or change in a directory, **first read the nearest README.md** that documents that module, function, or feature.

- Horizon maintains a pattern of placing `README.md` files both at the project root AND inside individual subdirectories/modules when a feature needs local documentation or design rationale.
- These READMEs serve as the **local design doc, changelog, or specification** for that component.
- Do not assume you understand a module's intent until you've read its README.
- If a directory has no README, check parent directories for context.

**Why:** Avoids misinterpreting the purpose of a module and writing code that doesn't fit Horizon's intent.

---

## Rule 3: Commit Convention (Conventional Commits)

Follow the **Conventional Commits** format derived from the `git-commit.skill` in Horisation:

```
<type>(<scope>): <summary>

<body>
<footer>
```

- **Summary line**: ≤ 72 characters, imperative mood
- **Types**: `feat`, `fix`, `refactor`, `docs`, `style`, `test`, `chore`
- **Scope**: primary module/component affected (short, 1-2 words)
- **Body**: 2-4 sentences, concise, wraps at 72 chars
- The dev log (`log.md` or similar) is the single source of truth for commit messages

## Rule 4: Comments — Concise, Supplement with README

- Keep code comments **brief and minimal** (言简意赅)
- Detailed design rationale, architecture decisions, and usage notes go in **README.md** files (local or project-level)
- Only write more comments when the function/module is **complex with many sub-parts**

## Rule 5: Error Handling — Let It Crash

Prefer the **let it crash** approach:

- Don't over-engineer defensive checks for every edge case
- Handle errors at natural boundaries (request handlers, service boundaries)
- Don't pollute business logic with excessive try/except or if-nil checks

## Rule 6: Type Annotations — Optional

Python/TypeScript type annotations are **optional**:

- Use them when it genuinely improves clarity or catches bugs
- Don't require them everywhere

## Rule 7: Testing — Core Functions Must Be Tested

Testing is not universal, but there's a hard rule:

- **Core / bottom-layer functions** — the ones that other functions depend on for correctness — **must have tests**.
- If a function is wrong, it cascades and breaks many things above it → that's the bar.
- Simple CRUD, prototypes, one-off scripts: no tests needed.
- When unsure whether something needs tests, ask Horizon.

---

*Rules are append-only. Add new ones as needed, keeping the numbering sequential.*
