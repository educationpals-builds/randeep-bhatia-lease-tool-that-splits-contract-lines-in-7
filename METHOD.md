# The PRISM Method for Auditing Duty-Splitting Tools

When a lease tool fails to split contract lines correctly—merging duties so the wrong party looks responsible—you need a systematic way to find where the logic breaks. PRISM provides five checks that surface the real failure point.

---

## The Five Checks

### P — Partition the Space

Does the tool divide the input into distinct, non-overlapping regions before processing?

For duty-splitting: Does it recognize that "provided that" creates a boundary between two separate obligations, or does it treat the whole clause as one unit?

### R — Run in Parallel

Can each partitioned region be evaluated independently, without one region's result contaminating another?

For duty-splitting: When the tool encounters "Tenant shall repair the roof provided that Landlord funds materials," can it process the tenant's duty and the landlord's duty as separate tracks?

### I — Individuate the Pattern

Does the tool identify the specific pattern that marks each duty—party name, verb, object—without blending adjacent patterns together?

For duty-splitting: Does it correctly tag "Tenant shall repair" as one duty-pattern and "Landlord funds materials" as another, or does it merge them into a single malformed pattern?

### S — Stitch the Spectra

When reassembling output, does the tool preserve the boundaries it found, or does it collapse distinct duties back into one line?

For duty-splitting: After identifying two duties separated by "provided that," does the output show two lines with correct party assignments, or does it stitch them into one line that misattributes responsibility?

### M — Map What Each Head Sees

Can you trace exactly which input fragment led to which output assignment?

For duty-splitting: If the summary says "Tenant: repair roof, fund materials," can you trace back to see why "fund materials" was assigned to Tenant instead of Landlord?

---

## The Collapse-to-Monochrome Anti-Pattern

The most common failure mode: the tool recognizes complexity in the input but flattens it to a single output.

**What it looks like:**
- Input has two parties, two duties, one conditional link
- Tool detects all three elements
- Output merges them: one line, one party, combined duty

**Why it happens:**
- The stitching step defaults to "merge when uncertain"
- Conditional language ("provided that," "unless," "however") triggers merge logic instead of split logic

**How to catch it:**
- Feed the tool a sentence with an explicit conditional
- Check whether the output preserves the party boundary the conditional creates
- If both duties land on one party's line, the tool collapsed to monochrome

---

## Using PRISM on Your Specimen

Rate each check 0–4:
- **0** = Not tested / unknown
- **1** = Fails outright
- **2** = Partial / inconsistent
- **3** = Mostly works
- **4** = This is where it breaks (the deciding check)

The check rated 4 is your top crack—the specific failure that determines your ship/hold call. Your audit builds from that finding.
