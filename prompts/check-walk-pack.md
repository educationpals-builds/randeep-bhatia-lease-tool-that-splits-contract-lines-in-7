# Lease Duty-Splitting Auditor — Five-Check Prompt Pack

Use these five standalone prompts to audit any lease duty-splitting tool. Each check ends with the measurement it demands. Paste one prompt at a time into any chat model, supply your failing inputs, and record the score.

---

## Check 1: Unowned

**Prompt:**

I'm auditing a lease tool that splits contract lines into separate duties. The tool is failing on lines with "provided that" clauses—it merges two duties so the wrong party looks responsible.

Here are three real failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Unowned check:** When a duty line fails to split correctly, is there a named owner who sees the error and is accountable for fixing it?

Walk through each failing input above. For each one, answer:
- Who currently owns catching this failure?
- If no one owns it, what happens to the error?

**Measurement demanded:** Count how many of the three failing inputs have a named owner responsible for catching the split error. Report as X/3 with owner names or "unowned."

---

## Check 2: Copies

**Prompt:**

I'm auditing a lease tool that splits contract lines into separate duties. The tool is failing on lines with "provided that" clauses—it merges two duties so the wrong party looks responsible.

Here are three real failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Copies check:** When the tool produces a merged output, how many downstream copies of that wrong assignment exist before someone catches it?

Walk through the first failing input ("Tenant shall repair the roof provided that Landlord funds materials within 10 days"). Trace what happens after the tool merges the two duties:
- Where does the merged output go?
- How many systems, documents, or summaries receive a copy before review?
- Who sees each copy?

**Measurement demanded:** Report the number of downstream copies created before the error is caught. If unknown, state "unknown" and explain what you'd need to find out.

---

## Check 3: Room

**Prompt:**

I'm auditing a lease tool that splits contract lines into separate duties. The tool is failing on lines with "provided that" clauses—it merges two duties so the wrong party looks responsible.

Here are three real failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Room check:** How much slack exists between when the tool produces a wrong merge and when it causes real harm (a partner signs a summary that puts repair duty on the wrong side)?

Walk through the second failing input ("Fees accrue daily; provided, however, that the cap in §4.2 still applies"). If the tool merges these duties incorrectly:
- How long until someone acts on the wrong output?
- What review steps exist between tool output and signature?
- Is there time to catch and fix the error?

**Measurement demanded:** Report the time window (hours, days, or steps) between wrong output and irreversible action. State whether this window is sufficient for review.

---

## Check 4: Stitch

**Prompt:**

I'm auditing a lease tool that splits contract lines into separate duties. The tool is failing on lines with "provided that" clauses—it merges two duties so the wrong party looks responsible.

Here are three real failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Stitch check:** When the tool merges duties that should be separate, does the system stitch together outputs in a way that hides the original error or makes it harder to trace?

Walk through the first failing input ("Tenant shall repair the roof provided that Landlord funds materials within 10 days"). The tool merges "Tenant shall repair the roof" with "Landlord funds materials within 10 days" into one duty line:
- Does the merged output preserve any signal that two duties existed?
- Can a reviewer tell from the output that a merge happened?
- Does downstream formatting or summarization further obscure the merge?

**Measurement demanded:** Report whether the merge is visible, hidden, or partially obscured in the final output. Score as: visible (reviewer can see two duties were merged), partially obscured (some signal remains), or hidden (no trace of the merge).

---

## Check 5: Ablation

**Prompt:**

I'm auditing a lease tool that splits contract lines into separate duties. The tool is failing on lines with "provided that" clauses—it merges two duties so the wrong party looks responsible.

Here are three real failing inputs from Harbor Lease sample contracts:

> Tenant shall repair the roof provided that Landlord funds materials within 10 days.
> Fees accrue daily; provided, however, that the cap in §4.2 still applies.
> Notice is deemed given when posted, unless the parties agree otherwise in writing.

**Ablation check:** If you removed or disabled the "provided that" merge logic entirely, what would break? What depends on the current (wrong) behavior?

Consider what happens if the tool stops merging any duty pairs separated by "provided that" and outputs them as two lines by default:
- What downstream processes expect a single merged line?
- Would any reports, summaries, or integrations fail?
- Are there cases where merging is actually correct?

**Measurement demanded:** List each downstream dependency that would break if the merge logic were disabled. Report count and severity (blocking vs. inconvenient).

---

## Sample Asks

A stranger auditing their own lease duty-splitting tool can paste these inputs:

**Stranger input 1:**
> Lessee shall maintain insurance coverage provided that Lessor approves the carrier within 30 days of policy renewal.

**Stranger input 2:**
> Rent increases annually; provided, however, that increases shall not exceed 3% without written consent.

**Stranger input 3:**
> Subletting is permitted when Landlord provides written approval, unless the original lease prohibits assignment.

Use these with any of the five check prompts above. Replace the Harbor Lease examples with your own failing inputs and run each check.

---

## Scoring Reference

After running all five checks, record scores:

| Check | Score | Notes |
|-------|-------|-------|
| Unowned | _/3 owners named | |
| Copies | _ downstream copies | |
| Room | _ time window | |
| Stitch | visible / partially obscured / hidden | |
| Ablation | _ dependencies would break | |

**Top crack for this specimen:** Stitch (score: 4) — the merge hides the original two-duty structure, making errors hard to trace.

**Ship call:** Ship with conditions: disable auto-merge for any duty pair separated by "provided that" and output them as two lines by default, flagged for manual confirmation. Priya owns confirming the flagged lines; reopens if confirmation backlog exceeds 20 leases.

**Tripwire:** Watch wrong-party rate on signed summaries containing "provided that" — even one per week means the merge fix didn't hold. Priya reviews weekly and reopens the hold if it recurs.
