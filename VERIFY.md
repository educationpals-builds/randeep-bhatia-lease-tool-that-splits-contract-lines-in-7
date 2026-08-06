# Verification: Lease tool that splits contract lines into separate duties

## Purpose

Confirm the auditor surfaces the **stitch** finding (the deciding check) and demands a numeric measurement when a stranger runs their own lease-splitting setup through `/play`.

---

## Stranger verification steps

### 1. Open `/play` with a failing lease splitter

A stranger pastes their own lease tool setup — one that is supposed to split contract lines into separate duties but fails on conditional clauses.

### 2. Walk the five checks

The auditor walks all five checks conversationally. For each check, it proposes a finding and names the measurement that would confirm it.

### 3. Confirm the deciding-check finding surfaces

The tool must surface the **stitch** finding — the check that decides whether the tool merges duties that should stay separate.

For the builder's specimen, this means:

> Lines with "provided that" still merge two duties so the wrong party looks responsible.

The auditor must not skip this finding or bury it. It should appear as the top crack in the scored audit.

### 4. Demand a numeric measurement

The auditor must demand a specific number for the stitch finding — not a vague "check if it works."

Example numeric measurement for the builder's specimen:

- **Wrong-party rate on signed summaries containing "provided that"**
- Danger line: even one per week means the merge fix didn't hold

### 5. Confirm the call includes an owner

The audit result must include a call with conditions and an owner:

> Ship with conditions: disable auto-merge for any duty pair separated by "provided that" and output them as two lines by default, flagged for manual confirmation. Priya owns confirming the flagged lines; reopens if confirmation backlog exceeds 20 leases.

### 6. Confirm the tripwire has a number, danger line, and watcher

> Watch wrong-party rate on signed summaries containing "provided that" — even one per week means the merge fix didn't hold. Priya reviews weekly and reopens the hold if it recurs.

---

## Pass criteria

| Requirement | Pass |
|-------------|------|
| Stitch finding surfaces as the deciding check | ☐ |
| Numeric measurement demanded for stitch finding | ☐ |
| Call names an owner (Priya) on conditions | ☐ |
| Tripwire includes number (one per week), danger line, and watcher (Priya) | ☐ |

All four boxes must be checked for verification to pass.

---

## Sample stranger input for testing

A stranger with a similar lease-splitting tool might paste:

> "My contract parser is supposed to separate obligations into individual line items. When a clause contains 'subject to' or 'except where', it combines both obligations into one line and assigns them to whichever party appears first."

The auditor should walk the five checks, surface the stitch finding (merging obligations that should stay separate), and demand a numeric measurement (e.g., wrong-assignment rate on contracts containing conditional language).
