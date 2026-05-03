---
name: dev-log
description: "Use this skill whenever the user asks to update, maintain, or create a development log (dev log). Triggers include: '更新开发日志', '更新dev log', 'update dev log', 'update development log', '记录这次迭代', 'log this iteration', 'add to dev log', or any request to track development progress, iteration history, technical decisions, or lessons learned in a structured persistent document. Also triggers when the user says '开发日志' or 'development log' in the context of recording work done. Do NOT use for general note-taking, meeting minutes, or changelogs that follow conventional commit/release formats."
---

# Development Log Skill

Maintain a structured, append-only development log that tracks iterations, technical decisions, and reusable lessons across a long-lived project.

## When This Skill Activates

The user wants to record development progress into a persistent markdown log. This is NOT a one-time document — it's a living file that grows over many sessions. The core contract: **never rewrite or delete old content; only append and update the status header.**

## Log File Location

Ask the user where their dev log lives. Common patterns:
- A file path they provide (e.g., `docs/DEV_LOG.md`)
- An uploaded file in `/mnt/user-data/uploads/`
- If no log exists yet, create one using the Template below

## Update Protocol

Every update MUST do exactly three things:

### 1. Update the Current Status header (top of file)

Replace the content under `## 0. Current Status` with:
- **Last Updated**: today's date (YYYY-MM-DD)
- **Completed**: what's now done
- **In Progress**: what's actively being worked on
- **Blocked / Not Solved**: anything stuck
- **Latest Summary**: one sentence summarizing this update (中英文均可，跟随用户语言)
- **Next Immediate Step**: the single highest-priority next action

### 2. Append Technical Decisions (if any)

If this iteration involved a meaningful technical choice (library selection, architecture change, schema design, workaround adoption), add a row to the `## 1. Technical Decisions` table:

```
| YYYY-MM-DD | Decision | Reason | Trade-off |
```

Skip this if the iteration was purely feature work with no notable decisions.

### 3. Prepend a new Iteration Record

Add the new record at the TOP of `## 3. Iteration History` (newest first). Every record MUST contain ALL of these sections — no exceptions, no shortcuts:

```markdown
### YYYY-MM-DD - [Descriptive Title]

#### Goal
What this iteration set out to accomplish.

#### Trigger / Context
Why now? What prompted this work? (bug report, user request, refactor need, etc.)

#### Problem & Root Cause
If fixing a bug: describe symptom → investigation → root cause.
If feature work: write "无明显 bug，本次为功能开发/结构优化" and explain the development motivation.

#### Solution
What was actually done. Be specific — mention function names, config changes, query modifications. Include brief code snippets if they clarify the approach.

#### Changed Files
List every file touched, with a one-line note on what changed in each.

#### Result
Observable outcome: what works now that didn't before, or what's new.

#### Testing
Specific steps taken to verify the change. NOT just "已测试".
Good: "在 Oracle dev 环境执行 trading_limit_calc.sql，验证 3 个品种的限额计算结果与手动计算一致。检查 alert 触发条件：将测试头寸设为超限值，确认邮件在 2 分钟内发出。"
Bad: "测试通过" / "已验证"

#### Lessons Learned
Write as a reusable pattern others (or future-you) can apply. Format:
- **Symptom**: what you saw
- **Root Cause**: why it happened
- **Reusable Solution**: what to do next time

If no bug was encountered, still capture a process or design insight. Examples:
- "When adding a new Oracle column with a NOT NULL constraint to a live table, always use a default value to avoid locking."
- "Dropdown 联动逻辑放在 onChange 回调里而非 useEffect 里，可避免初始化时的无效触发。"

#### Remaining Issues / Next Step
What's still open. Feed this back into the Current Status header.
```

## Reusable Patterns Section

If a Lesson Learned is particularly valuable and generalizable, also add it to `## 2. Reusable Patterns / Lessons Learned` as a named pattern:

```markdown
### Pattern N: [Descriptive Name]
- **Symptom**: ...
- **Root Cause**: ...
- **Reusable Solution**: ...
```

## Template for New Logs

When creating a dev log from scratch, use this structure:

```markdown
# Development Log

## 0. Current Status
Last Updated: YYYY-MM-DD

### Current Working Version
- Completed:
- In Progress:
- Blocked / Not Solved:

### Latest Summary
（一句话总结）

### Next Immediate Step
（下一步最优先事项）

---

## 1. Technical Decisions

| Date | Decision | Reason | Trade-off |
|---|---|---|---|
| | | | |

---

## 2. Reusable Patterns / Lessons Learned

（随迭代积累）

---

## 3. Iteration History

（最新记录在最上方）
```

## Critical Rules

1. **Append-only**: Never delete or modify old iteration records unless the user explicitly asks to archive or consolidate.
2. **Date format**: Always YYYY-MM-DD.
3. **Language**: Follow the user's language. Mixed Chinese-English is fine and expected.
4. **Completeness**: Every iteration record must have all 9 sub-sections. If a section genuinely doesn't apply, write a brief explanation why rather than leaving it blank.
5. **Testing specificity**: "已测试" or "tested" alone is never acceptable. Describe what was tested, how, and the observed result.
6. **Lessons must be reusable**: Write them so that someone encountering a similar situation can directly apply the insight without knowing your project's context.
7. **Current Status coherence**: The "Remaining Issues / Next Step" of the latest iteration and the "Current Status" header must be consistent — they describe the same state.

## Information Gathering

When the user says "更新 dev log" or similar, gather the following before writing:

1. What did you work on? (Goal)
2. What triggered this work? (Context)
3. Was there a bug or problem? What was the root cause? (Problem)
4. What did you change? Which files? (Solution + Changed Files)
5. How did you verify it works? (Testing)
6. What did you learn that's reusable? (Lessons)
7. What's left to do? (Remaining Issues)

If the user provides all this information upfront (e.g., in a paste or a detailed message), proceed directly. If information is missing, ask — but batch your questions into one round, not a drawn-out interview.

## Edge Cases

- **First entry in a new log**: Create the full template, then add the first iteration record.
- **Multiple iterations in one update**: Create separate iteration records for each, ordered newest-first.
- **User provides partial info**: Fill in what you can, mark unknowns with `[待补充]`, and note what's missing so the user can fill gaps.
- **Conflicting info between old records and new update**: Trust the new update; old records are historical and immutable.