---
name: decision-record
description: "Use this skill when a technical choice gets made that someone will later wonder about — library or framework selection, architecture boundaries, data model shape, settling an ambiguous definition, or reversing an earlier decision. Triggers include: '记一下这个决定', '这个决策要留痕', '为什么当初选的这个', 'record this decision', 'write an ADR', 'add a decision record', 'why did we pick X', 'we're changing our mind about X', or any moment where an option was chosen over a viable alternative. Also use it proactively right after helping the user choose between approaches — that is exactly when the reasoning is still available and cheap to capture. Do NOT use for logging what work was done (that's a dev log or changelog entry), or for choices with no real alternative."
---

# Decision Record

Capture *why* a choice was made, while the reasoning still exists.

## Scope of this skill

This is about the **content and lifecycle** of a decision — whether something is worth
recording, how to write a trade-off that's actually useful, and what to do when a
decision gets reversed.

**Where it gets written is a separate concern.** If the project has a dev log with a
technical-decisions table, that format is authoritative — follow it and don't invent a
parallel structure. Two places defining "how we record decisions" is precisely the drift
this whole practice exists to prevent. Look for `docs/DEV_LOG.md`, `docs/decisions/`, or
whatever the project's `CLAUDE.md` names, and write there.

## What counts as a decision worth recording

The test: **would a competent person six months from now wonder why it isn't the other
way?** If yes, record it.

Worth recording:
- Choosing between viable alternatives (this library over that one, this boundary here)
- Deliberately *not* doing something reasonable
- Settling an ambiguous definition, or picking a non-default parameter
- Accepting a known cost for a benefit
- Reversing an earlier decision

Not worth recording:
- Following the framework's obvious convention
- Choices with no real alternative
- What work was done — that's a changelog or dev-log entry, not a decision

When in doubt: if writing the trade-off is hard because there isn't one, it probably
wasn't a decision.

## The four parts

Every record needs a date, the decision, the reason, and the trade-off. The last two are
where records succeed or fail.

### Reason — what forced this, not what's nice about it

Weak: *"FastAPI is modern and fast."*

Strong: *"pydantic's validation is what enforces the money-and-timezone constraints the
project requires; getting that from Flask would mean hand-rolling it."*

The difference is that the strong version names the specific pressure. It also tells a
future reader when the reason has expired — if that pressure goes away, the decision is
open for review. Generic praise never expires and therefore never informs anything.

Numbering the reasons (① ② ③) helps when several independent pressures pointed the same
way, because later one of them may fall away while the others hold.

### Trade-off — what this genuinely costs

This is the part people skip, and skipping it makes the record nearly worthless. A record
with no trade-off reads as "we picked the obviously right thing", which tells a future
reader nothing about when to revisit it.

Weak: *"Slightly more code."* — nobody has ever revisited a decision over this.

Strong: *"Two codebases instead of one; needs an npm build step; a single-user tool now
carries a full frontend project to maintain."*

If you cannot name a real cost, that's a signal — either it wasn't a decision, or the
cost hasn't been thought through. Say which.

Costs that are worth naming: ongoing maintenance burden, things now harder to change,
new failure modes, work deferred onto future-you, capability given up.

## Reversing a decision

Decisions get overturned. How that's recorded determines whether the log stays trustworthy.

**Never delete the old record.** Strike it through, mark it superseded, and point at the
one that replaced it:

```
| ~~ADR-003~~ | 2026-09-05 | ~~Treat the library as an external dependency~~ | — | **Superseded by ADR-007** |
```

Then the new record explains not just the new choice, but *what was wrong with the
reasoning that produced the old one*. That's the part with lasting value — the same
faulty reasoning will otherwise recur.

Strong: *"The first version's error was equating 'code lives in another repo' with 'this
is a third-party dependency'. Ownership is the actual criterion — a package you own needs
no defensive adapter layer, and that layer was pure overhead."*

That sentence prevents the mistake next time. "We changed our mind" does not.

## Recording decisions that are still open

Sometimes the right move is to record that a decision is *pending*, with the leaning and
what it's blocked on. Give it an ID so other documents can reference it, state the
leaning honestly as a leaning, and say what would settle it.

This is more useful than either silence or a fake decision, and it stops the same
question being re-litigated every few weeks.

## When to write one

Immediately, while the alternatives are still in your head. A decision record written a
week later reconstructs the reasoning, and reconstructed reasoning is systematically
cleaner and more confident than what actually happened — which strips out the doubt that
would have told a future reader where the soft spots are.

If a decision came out of a conversation with the user, write it before the topic
changes. If several decisions were made at once, record each separately — bundled
decisions get reversed as a bundle, which is rarely what anyone wants.
