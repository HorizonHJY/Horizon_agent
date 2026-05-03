---
name: git-commit
description: "Use this skill whenever the user asks to commit code, submit changes, push code, or generate commit messages based on a dev log. Triggers include: 'commit code', 'commit this', '提交代码', '帮我commit', 'push changes', 'generate commit message', '提交这次改动', 'commit from log', or any request that involves reading a development log (log.md / DEV_LOG.md) to produce a git commit with a well-structured commit message. Also triggers when the user says 'commit and update log' or '提交并更新日志'. Do NOT use for general git operations like branching, merging, rebasing, or repo setup."
---

# Git Commit from Dev Log

Read a local dev log, verify the scope of changed files, generate a structured commit message from the log's description, execute the commit, and optionally update the log with commit metadata.

## When This Skill Activates

The user wants to commit code changes and wants the commit message derived from their dev log (e.g., `log.md`, `DEV_LOG.md`, or a similar file). The core value: **the dev log is the single source of truth for what changed and why — the commit message is a condensed, well-formatted extraction from it, not something written from scratch.**

## Prerequisites

- A git repository (the working directory must be inside a git repo)
- A dev log file that describes the current iteration's changes
- Uncommitted changes in the working tree or staging area

## Workflow

### Step 1: Locate and Read the Dev Log

Ask the user for their log file path if not already known. Common locations:
- `log.md` or `DEV_LOG.md` in the project root
- `docs/DEV_LOG.md`
- A path provided by the user
- An uploaded file in `/mnt/user-data/uploads/`

Read the **latest iteration record** from the log. Extract:
- **Goal**: what this iteration set out to accomplish
- **Solution**: what was actually done
- **Changed Files**: the list of files touched
- **Result**: observable outcome

### Step 2: Verify Changed File Scope

Run `git status` and `git diff --name-only` (or `git diff --staged --name-only` if files are already staged) to get the actual list of changed files in the repo.

**Cross-reference** the log's "Changed Files" list with the actual git diff:

- **Files in log but NOT in git diff**: Warn the user — the log may be outdated, or those files were already committed.
- **Files in git diff but NOT in log**: Warn the user — there are uncommitted changes the log doesn't describe. Ask whether to include them (and if so, get a brief description) or exclude them from this commit.
- **Match**: Proceed.

If there are significant discrepancies, pause and confirm with the user before proceeding. Minor differences (e.g., auto-generated files like `.pyc`, lock files) can be noted but don't need to block the commit.

### Step 3: Stage Files

If files are not yet staged, stage them based on the verified scope:

```bash
git add <file1> <file2> ...
```

Only stage files that are within the agreed-upon scope. If the user wants to commit everything, use `git add -A`, but confirm first.

### Step 4: Generate the Commit Message

Construct the commit message using the **Conventional Commits** format, derived from the dev log content:

```
<type>(<scope>): <summary>

<body>

<footer>
```

**Rules:**
- **Summary line**: ≤ 72 characters. Extracted from the log's Goal + Result. Use imperative mood ("add", "fix", "refactor", not "added", "fixed").
- **Type**: Infer from the log content:
  - `feat` — new feature or capability
  - `fix` — bug fix
  - `refactor` — code restructuring without behavior change
  - `docs` — documentation only
  - `style` — formatting, whitespace, no logic change
  - `test` — adding or updating tests
  - `chore` — build, config, tooling changes
- **Scope**: Infer from the Changed Files — the primary module, component, or area affected. Keep it short (1-2 words).
- **Body**: 2-4 sentences summarizing the Solution from the log. Mention key technical details (function names, config changes, query modifications) but keep it concise. Wrap at 72 characters per line.
- **Footer** (optional): Reference issue IDs, breaking changes, or link to the log entry date.

**Example:**

```
feat(alert-system): add email mapping for trading limit alerts

Implement user-to-email mapping table in Oracle for the automated
alert system. New stored procedure maps trader IDs to notification
groups based on desk and commodity assignments.

Log-ref: 2025-05-03
```

Show the generated commit message to the user and **ask for confirmation** before executing.

### Step 5: Execute the Commit

```bash
git commit -m "<commit message>"
```

Report the result: commit hash, branch name, number of files changed, insertions/deletions.

### Step 6: Update the Dev Log (Optional)

If the user agrees, update the dev log's latest iteration record with commit metadata:

- Add the **commit hash** (short form, 7 chars) to the iteration record
- Add the **commit date** if different from the iteration date
- Update the "Result" section to note the commit was made
- Update `## 0. Current Status` if the commit marks a milestone

**Important**: Follow the dev-log skill's append-only principle — don't rewrite old content. Only amend the latest iteration record's metadata fields.

### Step 7: Post-Commit Check (Optional)

If the user wants, run:
- `git log --oneline -5` to show recent commit history
- `git status` to confirm a clean working tree

## Commit Message Style Guide

1. **言简意赅 (concise and precise)**: The summary line is the most important part. If someone reads only that line, they should understand what this commit does.
2. **Reuse log language**: Don't reinvent descriptions — extract and condense from the dev log. The log is authoritative.
3. **Technical but readable**: Include function names and file references in the body, but don't dump raw code.
4. **One logical change per commit**: If the log describes multiple unrelated changes, suggest splitting into multiple commits.
5. **Language**: Follow the user's language preference. Mixed Chinese-English is fine. But the commit type and scope should always be in English (they're git conventions).

## Edge Cases

- **No dev log exists**: Ask the user to describe the changes verbally. Generate the commit message from their description, but suggest creating a dev log for future use (reference the dev-log skill).
- **Log describes changes not yet made**: The log is aspirational, not reflective. Only commit what's actually changed in git. Note the discrepancy.
- **Multiple commits needed**: If the log's iteration covers multiple logical changes, propose a commit plan (which files go in which commit, in what order) and execute sequentially.
- **Merge conflicts or dirty state**: If `git status` shows conflicts or other issues, address those first before attempting to commit. Don't silently ignore them.
- **User wants to amend the last commit**: Support `git commit --amend` if explicitly requested, and regenerate or edit the commit message accordingly.

## Permissions and Boundaries

This skill **CAN**:
- Read the dev log
- Run `git status`, `git diff`, `git add`, `git commit`, `git log`
- Suggest edits to the dev log's latest iteration record (commit metadata only)

This skill **CANNOT**:
- Push to remote (`git push`) — always leave this to the user unless explicitly asked
- Force-push, rebase, or rewrite history
- Delete branches or tags
- Modify files other than the dev log

## Quick Reference: Common Flows

**Standard commit:**
```
User: "帮我 commit"
→ Read log → git status → cross-check files → generate message → confirm → commit → update log
```

**Commit specific files only:**
```
User: "只 commit alert 相关的文件"
→ Read log → filter changed files by keyword/path → stage subset → generate message → confirm → commit
```

**Dry run:**
```
User: "先看看 commit message 长什么样"
→ Read log → git status → cross-check → generate message → show to user → stop (don't commit)
```