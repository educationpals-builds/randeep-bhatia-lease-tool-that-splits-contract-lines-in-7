# Lease Tool That Splits Contract Lines Into Separate Duties — Conversational Auditor

## What this auditor does

A stranger pastes a description of their own lease-duty-splitting tool that is failing, along with three real contract lines where it breaks. The auditor walks five checks conversationally, proposes findings with the measurement that would confirm each, and returns a scored audit with a severity story, a call, and a tripwire.

---

## The specimen this auditor was built from

**Broken tool:** Lease tool that splits contract lines into separate duties

**What goes wrong if this never gets fixed:** A partner signs a summary that puts repair duty on the wrong side

**How you know it's fixed:** Each duty lands on its own line with the right party named

**Real inputs look like:** Old scanned leases with nested "provided that" lines

**Source:** Harbor Lease sample contracts

---

## Failing inputs (worked example)

```
Tenant shall repair the roof provided that Landlord funds materials within 10 days.
Fees accrue daily; provided, however, that the cap in §4.2 still applies.
Notice is deemed given when posted, unless the parties agree otherwise in writing.
```

---

## Five-check audit walk

The auditor walks each check in order, proposes a finding, and names the measurement that would confirm it.

| Check | Rating | What to measure |
|-------|--------|-----------------|
| unowned | 1 | Count duty lines with no party named in output |
| copies | 1 | Count duplicate duty assignments across summaries |
| room | 2 | Count lines where split created ambiguous scope |
| stitch | 4 | Count "provided that" lines merged into single duty with wrong party |
| ablation | 0 | Remove splitter; count duties that still route correctly |

**Top crack:** stitch

---

## Findings

### Severity story

The "stitch" check is the decider. When the tool encounters "Tenant shall repair the roof provided that Landlord funds materials within 10 days," it merges both duties into one line. The summary then shows repair duty assigned to whichever party appeared first—often the wrong one. A partner signs that summary believing the other side owns the repair.

### Call

Ship with conditions: disable auto-merge for any duty pair separated by "provided that" and output them as two lines by default, flagged for manual confirmation. Priya owns confirming the flagged lines; reopens if confirmation backlog exceeds 20 leases.

### Tripwire

Watch wrong-party rate on signed summaries containing "provided that" — even one per week means the merge fix didn't hold. Priya reviews weekly and reopens the hold if it recurs.

---

## How a stranger uses this auditor

1. **Paste your specimen:** Describe the lease-duty-splitting tool you rely on and what it's supposed to do.
2. **State the stakes:** What goes wrong when duties land on the wrong party?
3. **Paste three failing lines:** Real contract text where your tool merges or misassigns duties.
4. **Walk the five checks:** The auditor asks about each check, proposes a finding, and names the measurement.
5. **Receive your audit:** A scored result with the top crack identified, a ship/hold call with conditions and owner, and a tripwire with a number, danger line, and watcher.

---

## Sample asks

A stranger with their own lease-splitting tool might paste:

> "Our duty parser handles most clauses but fails on lines with 'notwithstanding' — it assigns both obligations to the first party mentioned. Here are three lines from our Riverside Commercial portfolio:
> 
> Landlord shall maintain HVAC notwithstanding Tenant's obligation to replace filters monthly.
> Tenant pays utilities notwithstanding any cap negotiated in Exhibit B.
> Insurance proceeds go to repairs notwithstanding Landlord's right to terminate."

The auditor walks all five checks against this stranger's specimen, proposes findings with measurements, identifies the top crack, and returns a call with owner and tripwire with number and watcher—applying the same discipline used on the Harbor Lease "provided that" failure.
