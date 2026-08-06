# Lease tool that splits contract lines into separate duties

A lease tool is supposed to split contract lines into separate duties. On lines with "provided that", it still merges two duties so the wrong party looks responsible.

## Verdict

**Ship with conditions:** disable auto-merge for any duty pair separated by "provided that" and output them as two lines by default, flagged for manual confirmation. Priya owns confirming the flagged lines; reopens if confirmation backlog exceeds 20 leases.

## Tripwire

Watch wrong-party rate on signed summaries containing "provided that" — even one per week means the merge fix didn't hold. Priya reviews weekly and reopens the hold if it recurs.

## The problem

Old scanned leases with nested "provided that" lines get merged incorrectly. A partner signs a summary that puts repair duty on the wrong side.

**Standard:** Each duty lands on its own line with the right party named.

## Failing examples (Harbor Lease sample contracts)

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

## One-paste rebuild block

```
CONDITIONAL SPLIT FIX

1. Detect "provided that" / "provided, however" in any contract line
2. Split into two separate duty lines at the conditional boundary
3. Preserve party attribution on each resulting line
4. Flag both lines for manual confirmation
5. Route flagged pairs to Priya for review

Backlog threshold: 20 leases
Escalation: If confirmation backlog exceeds 20 leases, reopen hold
```

## Deciding check

The **stitch** check scored highest (4) — the tool merges duties that should stay separate when conditional language appears.

## Using this audit

Point this auditor at your own lease-splitting setup. Describe what it's supposed to do, paste three real lines where it fails, and walk the five checks. You'll get findings with measurements, a call with an owner, and a tripwire with a number that means trouble.

See [charter.md](charter.md) for the full audit. See [METHOD.md](METHOD.md) for the five-check framework.

<!-- educationpals-build-verified -->
