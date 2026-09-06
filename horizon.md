# Horizon — Personal Profile

> Last updated: 2026-09-06

## Basics

- **Name:** Horizon
- **Location:** St. Louis, MO
- **Language:** 中文/English (prefers 中文 with me)
- **Vibe:** Direct, no small talk, says what he wants

## Communication Style

- Skips pleasantries, gets to the point
- Prefers action over planning — "go write code" > "let me plan this out"
- Doesn't like guessing or hallucinated assumptions; wants to be asked when unsure
- Tolerates minimal filler, values clarity

## Technical Background

- Runs **Horisation** — a private friends platform (Flask backend, React frontend, EC2, horizonyhj.com)
- Has **Horizon Agent** framework at `Horizon_agent` — Claude Code AI agent framework with 14 personas, 12 commands, 12 skill domains, plus his personal `constitution/` and `rules/`
- Builds **HJ_YYS** — an Onmyoji (阴阳师) mobile game automation framework (image recognition + coordinate clicking against MuMu emulator windows). Actively iterated on with its own `docs/CHANGELOG.md`/`docs/DEV_LOG.md`/`docs/开发宪章_Development_Constitution.md`. Project-specific facts, current status, and standing quirks live in that project's own docs — don't duplicate them here, see [Documentation Placement](#documentation-placement) below.
- Uses GitHub Actions for auto-deploy (push main → EC2)
- Also built Bella Salon commission splitting system

## Documentation Placement

Horizon's rule for where new information should be written down (established 2026-08-11, after too many md files accumulated ad hoc). Use this test before writing anything down:

1. **About Horizon himself, or how any Claude session should collaborate with him** (communication style, standing personal preferences, what he cares about) → **this file** (`horizon.md`).
2. **A universal engineering principle that should hold across any of his codebases** (commit format, error-handling philosophy, architecture taste like "don't embed cross-cutting concerns in a business-logic function") → `constitution/coding.md`, or the relevant file under `rules/` if it's language/tool-specific.
3. **Specific to one project** (its architecture, current status, iteration history, project-specific standing quirks like HJ_YYS's "avoid the number 4" or its commit-message-file convention) → stays inside that project's own docs. Never duplicated into Horizon_agent — reference/link instead if it's worth pointing at.

This rule applies to every project of his (HJ_YYS, Horisation, and whatever comes next), not just one.

## How We Work

- Project code and project-specific facts stay in the project, not here (see Documentation Placement above)
- This file + `constitution/` + `rules/` only store: who Horizon is, how we collaborate, and universal rules that apply everywhere
- Uses WhatsApp to talk to me

## What Matters

- Quality > speed
- Security-conscious
- Don't exfiltrate private data
- Don't run destructive commands without asking
- Use `trash` over `rm`

## Agent Framework Rules

When working on Horisation or any code Horizon asks about, I should:
- Reference the rules in `Horizon_agent/rules/`
- Help maintain and evolve the skills/rules over time
- Follow the coding standards, security, and testing conventions defined there

## Notes

- Based on memory as of 2026-08-11. This file should be updated as Horizon's preferences evolve.
