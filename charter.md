# Audit: Lease tool that splits contract lines into separate duties

## Specimen under review

**Tool:** Lease tool that splits contract lines into separate duties

**What goes wrong if this never gets fixed:** A partner signs a summary that puts repair duty on the wrong side

**Standard for success:** Each duty lands on its own line with the right party named

---

## Real inputs tested

**Source:** Harbor Lease sample contracts

**Usage reality:** Old scanned leases with nested "provided that" lines

### Pasted failing inputs

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

---

## Check findings

| Check | Rating | Notes |
|-------|--------|-------|
| Unowned | 1 | Low concern |
| Copies | 1 | Low concern |
| Room | 2 | Moderate concern |
| Stitch | 4 | **Deciding check** — highest severity |
| Ablation | 0 | No concern |

### Deciding check: Stitch

The stitch check scores 4 — the highest rating in this audit. The tool merges duties that should remain separate when a "provided that" clause appears. Two distinct obligations get stitched into one line, making it impossible to tell which party owns which duty.

---

## Call

**Ship with conditions:** disable auto-merge for any duty pair separated by "provided that" and output them as two lines by default, flagged for manual confirmation. Priya owns confirming the flagged lines; reopens if confirmation backlog exceeds 20 leases.

---

## Tripwire

Watch wrong-party rate on signed summaries containing "provided that" — even one per week means the merge fix didn't hold. Priya reviews weekly and reopens the hold if it recurs.

---

## Audit summary

This lease duty splitter fails the stitch check at severity 4. When contract lines contain "provided that" clauses, the tool merges two separate duties into one line, obscuring which party is responsible for what. The fix ships with conditions: disable auto-merge for duty pairs separated by "provided that," output them as two lines flagged for manual confirmation. Priya owns the confirmation queue. If the confirmation backlog exceeds 20 leases, the condition reopens. Post-release, watch the wrong-party rate on signed summaries containing "provided that" — one occurrence per week triggers a hold.
