# Kshitij request — one final DataVibe regenerated-copy test

**Status:** Draft instruction only. No message has been sent, and the test has not been run. Please send this through the existing Kshitij channel when ready.

## Copy/paste instruction

Please run **one—and only one—regenerated-copy test** for the same 10 records used in the original DataVibe comparison. This is the final technical test; do not revise the test design or the action contract.

### Frozen conditions

1. Use the **same 10 records**, original offer, original prompt, model, and settings as the original controlled comparison.
2. Use the frozen Pipeline42 verdict/action/evidence packet at `Kshitij/PASS2_PIPELINE42_VERDICTS.csv` and the **same frozen action contract**. Do not edit or enrich the input packet.
3. Do not manually edit generated copy, record facts, or verdicts during the run. Capture the raw output.
4. Recover and record the original prompt, model, and settings before starting. If any cannot be recovered exactly, label the run **exploratory, not controlled**, list what is missing, and do not imply that it is a controlled replay.
5. Do not run a second regeneration, a second set of records, or a variant prompt/settings test.

### Record the result

For every record, preserve the generated copy **before and after** the one regeneration and capture:

- the copy change (or no change),
- which supplied fact/evidence changed it and why, if applicable,
- the action-contract gate result,
- any assertion in the copy that is unsupported by the supplied facts, and
- surprises, including unexpected changes or no change where expected.

Include a short run manifest with the date, exact prompt/model/settings or an explicit note that they could not be recovered, and confirmation that no manual edits or second runs occurred.

### Keep copy separate from action status

The frozen action contract is:

- `FIX`, `REPLACE`, or `REMOVE` → **Block**
- `VERIFY` → **Review**
- `USE` → **Proceed**

It may therefore return the same **1 Blocked / 7 Review / 2 Proceed** statuses regardless of whether the generated wording changes. Report copy changes and action statuses as separate results; do not change the contract to make statuses respond to wording.

Log these known scope limitations without changing the contract:

- `USE` does not specify channel/use scope. DV-02 and DV-05 had phone-first limitations but proceeded as email under the coarse mapping.
- DV-03's `FIX → Block` result may conflate automated sequencing with permitted human verification; record the distinction as an observation only.
- DV-08's `RED / VERIFY → Review` can be coherent because severity and action are separate.
- Unsupported personalization (for example, a claim about supplier orders or stock counts) is not automatically false. Mark it **unsupported by supplied facts**; do not infer truth or falsity.

DataVibe checks whether generated copy matches the supplied facts. It does **not** independently verify the facts or establish buyer, ICP, role, or workflow actionability.

After returning this one run's outputs, freeze DataVibe and stop technical iteration. Do not revise the contract or run further tests.
