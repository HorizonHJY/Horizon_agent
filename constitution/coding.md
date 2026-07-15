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

*Add more rules below. Each rule gets a number and a clear rationale.*
