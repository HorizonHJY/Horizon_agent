---
name: project-docs-scaffold
description: "Use this skill whenever a new project or repo is being started and needs its documentation foundation laid down — before or alongside the first code. Triggers include: '新项目', '搭一下文档', '把 docs 结构建起来', '先写文档', 'set up the docs', 'scaffold the project docs', 'start a new repo', 'write the CLAUDE.md', 'I'm starting X, help me structure it', or any request to create a README / CLAUDE.md / development constitution / docs folder for a project that doesn't have one yet. Also use when an existing project has accumulated code but no durable documentation and the user wants to retrofit the structure. Do NOT use for writing a single document (one README, one design doc) into a project that already has this structure — just write that document."
---

# Project Docs Scaffold

Lay down the documentation foundation for a new project: a README that states what the
thing is and what it deliberately isn't, a CLAUDE.md that constrains how it gets built,
and a `docs/` set that makes decisions and definitions findable six months later.

## Why this exists

The failure mode this prevents is specific: three months in, nobody can say why a piece
of code chose one behavior over another, and the "obvious" thing gets silently rewritten
into something subtly different. Code answers *what*; these documents answer *why* and
*which one did we pick*. Writing them after the code means writing them from memory,
which is when they stop being true.

The second failure mode is scope creep. A project without a written "we do not do this"
list accumulates features that each seemed reasonable alone.

## Before writing anything: interview

Don't guess these. Wrong answers here produce documents that get ignored, which is worse
than no documents.

1. **One-sentence positioning.** What single question does this project answer? Push for
   specificity — "a trading dashboard" is not an answer; "which of my holdings caused
   today's P&L" is.
2. **The exclusion list.** What will this deliberately *not* do, even though it would be
   easy? This is usually the most valuable part of the whole scaffold. Ask directly:
   "what's the adjacent thing you're worried you'll drift into?"
3. **Companion repos.** Is there a library, package, or sibling project this one depends
   on or feeds? If yes, the boundary between them needs a written rule (see below).
4. **Ambiguous domain terms.** Are there terms in this domain where two reasonable people
   would compute different numbers from the same words? Finance, billing, scheduling,
   permissions, and analytics almost always have these. If yes, the project needs a
   definitions document; if no, skip it.
5. **Audience.** Solo project or team? Solo projects can drop contribution guides and
   onboarding, and should — unused documents rot and mislead.

## What to create

Adjust to the project. A solo script does not need nine files; a two-repo system does.
The default set:

| File | Job |
|---|---|
| `README.md` | What it is, why it exists, **范围边界 (what it deliberately won't do)**, stack, how to run, doc index |
| `CLAUDE.md` | The constitution — hard constraints, boundaries, mandatory process. Not a tutorial |
| `docs/QUICK_REF.md` | The single file to read at session start. Positioning, current status, layering, key file map, the rules most often broken |
| `docs/ARCHITECTURE.md` | Layering, module responsibilities, data flow, directory structure |
| `docs/DEV_LOG.md` | Current status + decision table + session log |
| `docs/CHANGELOG.md` | Version-tagged change history |
| `docs/TODO.md` | Blocked / near-term / idea pool |
| `docs/<DOMAIN>.md` | **Only if step 4 said yes.** The authority on ambiguous definitions |

Drop anything that won't be maintained. A stale ARCHITECTURE.md is a liability.

## The parts that carry the weight

Most of these files are ordinary. Three of them are where the value actually is.

### CLAUDE.md is constraints, not documentation

It should say what is *not allowed*, and why. If a line in CLAUDE.md doesn't rule
something out, it probably belongs in ARCHITECTURE.md or QUICK_REF.md instead.

Include, when applicable:
- **Exclusion list** — the "do not build this" items from the interview, with 🚫 markers
- **Dependency boundary** — if there's a companion repo, the rule for what goes where.
  A one-sentence test beats a paragraph: *"if it would still make sense for someone else,
  it goes in the library; if it's only true for me, it stays here."*
- **Capability vs policy** — when a companion library implements something configurable,
  the library provides parameterized capability with documented defaults, and this repo
  decides which parameters to use. Without this rule the two repos drift and nobody
  notices until numbers disagree.
- **Single source of truth** — name the file that wins when code and docs disagree, and
  say which one gets changed (usually: change the code).
- **Change tracking** — the requirement to log changes, and where.
- **The chain-effect checklist** — see the `chain-check` skill; CLAUDE.md should carry a
  short version and point at the fuller treatment.
- **Coding constraints** that are specific to this domain, not general style. Things like
  "no binary floats for money", "dates always carry an explicit timezone", "never
  silently fill missing data" earn their place. "Use meaningful variable names" does not.

### QUICK_REF.md is the session entry point

The premise: someone (or some model) starting a session reads exactly one file. It needs
positioning, current status, what's blocked, the layer diagram, a file map, and the three
to five rules most easily violated. Keep it current — this is the file most worth the
maintenance.

### The definitions document, if the domain needs one

Number every open question (`D-1`, `D-2`, …) and keep a summary table at the bottom with
status. Mark undecided ones clearly and say what the leaning is without pretending it's
decided. The rule that makes this work: **when something is marked undecided, stop and
ask rather than picking a default** — a silently chosen default is exactly the thing that
becomes unexplainable later.

## Handling open questions

New projects have unknowns. Don't paper over them and don't let them block the scaffold.
Give every unknown an ID, a leaning, and a home in the summary table, then keep building
around it. A document that says "⚠️ D-7 undecided, leaning toward X, needs confirmation"
is far more useful than one that quietly assumes X, and far more useful than a blank.

## Writing style

Match the language the user writes in. Prefer tables to prose for anything enumerable.
State the reason next to any rule that looks arbitrary — a rule whose rationale is
written down survives; one that isn't gets deleted by a future reader who assumes it was
cargo cult.

Write dates as absolute (`2026-09-06`), never "last week".

## Finishing

Verify before declaring done:
- Every cross-document link resolves to a file that exists
- Every numbered open question appears in both the body and the summary table
- The README's doc index lists every file actually created
- `.gitignore` covers whatever is private (real data, credentials, build output,
  dependencies) — and note that `data/` excludes the whole directory, so a later
  `!data/example.csv` exception won't work; write `data/*` when an exception is needed

Then record the scaffold itself as the first CHANGELOG entry, so the log starts at the
project's actual beginning.
