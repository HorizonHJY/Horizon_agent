---
name: chain-check
description: "Use this skill before calling any non-trivial change finished — it catches the derived artifacts that go stale when code changes: changelogs, decision logs, definition docs, file maps, dependency manifests, cross-repo version pins, and leftover references to renamed things. Triggers include: '收工', '改完了', '提交前检查', '连锁检查', '还有什么要更新的', 'anything else to update', 'before I commit', 'wrap this up', 'is this ready to commit', or finishing a feature, refactor, rename, or dependency change. Also run it proactively at the end of your own multi-file changes without being asked. Do NOT use for verifying code correctness — build, type, lint, and test gates are a different concern; this is about documents and references drifting out of sync with the code."
---

# Chain Check

Before a change is finished, find what else the change invalidated.

## The problem this solves

Code changes are visible; their consequences are not. Rename a module and the code still
compiles while the file map in the docs now points at nothing. Change how a number is
computed and the definition document still describes the old formula — and the document
is what someone will trust in six months. Add a dependency and the next person's install
fails.

None of this is caught by builds, types, lint, or tests. Those verify the code is
*correct*. This checks whether everything *derived from* the code is still *true*.

## How to run it

Go through the list below. For each item, either do the update or state why it doesn't
apply — don't skip silently, because "didn't apply" and "forgot" look identical later.

Do this without being asked. If the user has to remind you, the check has already failed
at the thing it's for.

### The checklist

1. **Changelog updated.** Every non-trivial change gets an entry. Include what was wrong,
   what was done, which files it touched, and how it was verified.

2. **Definitions document, if a rule or formula moved.** If the change altered how
   something is computed, classified, or validated, the document that defines it must
   change in the *same commit*. Split across commits, the two drift immediately.

3. **Decision log, if a choice was made.** Selecting a library, changing architecture,
   settling an open question — record it with the reason *and* the trade-off. See the
   `decision-record` skill for what makes these worth reading.

4. **File map / quick reference, if modules were added or renamed.** Any doc that lists
   "where things live" is now wrong. Counts are file maps too: a README or profile that
   says "12 commands, 9 skill domains" goes quietly false the moment you add one, and
   nothing will ever fail to warn you — so grep for the inventory line, not just the
   path list.

5. **Dependency manifest, if imports changed.** Add the dependency *and* a note on why
   the existing ones weren't sufficient. Watch for platform-conditional dependencies —
   something that works on one OS because the system provides it may need an explicit
   package elsewhere.

6. **Ignore rules, if new artifact types appeared.** New build output, caches, dependency
   directories, or private data files. Two things reliably get missed: the second
   language's artifacts in a polyglot repo, and the fact that ignoring a whole directory
   makes later negation patterns for files inside it not work.

7. **Grep for the old name after any rename.** Search the entire repo — including docs,
   comments, config, scripts, and commit-message templates. Zero residual references, or
   an explicit note about why a reference is deliberately kept (a superseded decision
   record, for instance, should still name the old thing).

8. **Cross-repo changes: both sides.** If the change spans repositories, commit on both
   sides referencing each other, publish the dependency before pinning it downstream, and
   update the version constraint.

9. **Generic logic in the wrong repo.** If the change added something reusable to an
   application repo when a library repo exists, it's in the wrong place. "I'll move it
   later" is how it never moves.

10. **Removed logic: check why it existed.** Before deleting a workaround or a special
    case, read the changelog history for why it was added. If the reason still holds,
    don't delete it. If it doesn't, say so in the new entry — otherwise the next person
    re-adds it.

11. **New lessons go into the checklist.** If this change surfaced a consequence not
    listed above, append it here rather than leaving it in chat. That's what keeps this
    list worth reading.

## Adapting to the project

Read the project's `CLAUDE.md` or equivalent first — most projects that use this have
their own checklist, and the project's version wins. Treat the list above as the
starting set to merge with, not a replacement.

If the project has no such list, offer to add a short version to its `CLAUDE.md`,
tailored to what actually exists there. A checklist referencing files the project doesn't
have gets ignored wholesale.

## Reporting

Say what you checked and what you changed. A bare "checked everything" is not useful —
the value is in the reader being able to spot the item you got wrong.

Prefer:

> Updated CHANGELOG and the file map (two new modules). Grepped `old_name` — zero hits.
> No definition changes, so DOMAIN.md untouched. Added `tzdata` to requirements with a
> note on why it's required on Windows.

Over:

> Ran the chain check, all good.

When something doesn't apply, one clause is enough. The point is that the reader can see
you considered it.
