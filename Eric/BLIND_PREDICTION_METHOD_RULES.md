# Standing Rule: Blind Prediction Method for Future Lead Data

**Status:** Reusable method rule for future blind lead-prediction reports.  
**Recorded:** 2026-10-03, at the user's request.  
**Purpose:** Reuse the method and quality controls—not Order 54's row-level judgments, assumptions, or class counts.

## 1. Core rule

Use this methodology for future datasets unless the user explicitly changes it. Treat supplied datasets as the primary evidence. Keep account-level first-call actionability, named-contact sequence actionability, and entity identity/routing as separate questions. Freeze predictions before calls or other ground-truth outcomes. Make uncertainty visible; never force a status to reach a preferred count.

**Do not carry forward Order 54's labels or counts as targets.** Its FCA 35/16/0, NCSA 1/13/2/35, and SEQ 1/47/3 counts are one dataset's frozen predictions—not quotas, thresholds, priors, or proof the method is accurate. The method transfers; each future record must be assessed from that dataset's evidence. Do not bias toward Pipeline42, prior conclusions, a previous flag rate, or presumed representativeness of restaurants (or any other segment).

If the offer/product and ICP are material but absent, ask the user for them when practical. If work must proceed without them, state a provisional assumption, keep role-fit judgments conditional on it, and do not present the result as universal.

## 2. Evidence and data-integrity rules

1. Inventory the supplied files, formats, row counts, column counts, IDs, null/placeholder conventions, and source provenance before scoring.
2. Use source row order to create stable IDs only when no stable source ID exists; state how IDs were assigned. Check duplicates and related locations, but do not merge or discard records merely because names, people, addresses, or numbers overlap.
3. Compare exports field by field. Agreement across exports is **cross-export consistency**, not independent verification unless provenance independence is known.
4. Separate dataset evidence from external verification. If external research is requested or necessary, cite and label it separately; never make a dataset-derived fact look independently verified.
5. Treat missing website, LinkedIn, contact, title, email, or enrichment as missing evidence—not as proof of a bad account. Treat populated fields, generic inboxes, profile markers, job titles, ratings, recent reviews, and Apollo stages as claims/signals, not confirmation by themselves.
6. Do not infer email deliverability, current employment, decision authority, phone ownership, or business closure from fields that do not establish those facts.
7. Preserve earlier frozen reports unchanged. Create a new version for each pre-ground-truth revision, clearly stating what it supersedes and what information was or was not used.

## 3. Three separate scoring dimensions

### FCA — First-Call Actionability (account/location level)

- **GREEN:** The supplied local business/location and main phone support a reasonable first qualification call. GREEN means *reasonable to call*, not that the number is independently verified, will connect, or will be answered.
- **YELLOW:** A first call is still reasonable, but should qualify a material entity, parent/chain/franchise, platform, outlet, purchasing-boundary, or phone-route ambiguity. YELLOW is not a do-not-call verdict.
- **RED:** Use only with positive evidence that the number is wrong/disconnected or belongs to another entity, or another comparably direct record-level disqualifier. Explain the evidence in the row. Missing data, no answer, old review activity, or an area-code difference alone is not RED.

### NCSA — Named-Contact Sequence Actionability (person/route level)

- **GREEN:** Positive evidence supports all of: an identifiable person, a current/relevant role, plausible fit to the stated or explicitly assumed offer, and a suitable route to that person. A connection, senior title, or working email alone is not enough. GREEN should be intentionally strict/rare, but never artificially limited to a chosen number.
- **YELLOW:** A person is named, but a material uncertainty remains. Use a descriptive sublabel so the issue is visible, such as **ROUTE**, **ROLE**, **SCOPE**, or **LIVENESS** (combine only when needed). Examples: an unconfirmed direct number, uncertain decision authority, parent/location scope, or old business-activity signal.
- **RED:** Positive evidence supports a material named-person role or channel mismatch for the specified/provisional offer. State the assumption and the reason; do not use RED merely because a title is not obviously senior or a channel is absent.
- **INSUFFICIENT EVIDENCE:** If no person is named, do not invent one and do not classify the person sequence as bad. Use an explicit missing-evidence label, e.g. **INSUFFICIENT EVIDENCE — MISSING NAMED CONTACT**. A stray email whose owner/role is unmapped remains insufficient evidence; it is not a named-contact match. If a person is named but their role is absent, label the actual role-evidence gap clearly.

### SEQ — conservative named-contact sequence class

Use `SEQ` instead of the former `FINAL` class label. It is a downstream sequence decision, not a replacement for FCA or NCSA. Ordinarily it follows the NCSA result. An entity-level RED may override SEQ only when positive evidence materially contaminates the identity/routing of the sequence target; write the reason in a dedicated **RED Trigger** field and retain the independent FCA and NCSA results. Make it explicit when NCSA is INSUFFICIENT EVIDENCE but SEQ is RED for entity contamination. A valid local phone can still justify a verification call even when a named-contact sequence is RED.

### Confidence

Use A–D consistently as evidence-strength confidence, not as a calibrated call-connect probability: **A** strong evidence; **B** good evidence/minor uncertainty; **C** meaningful uncertainty; **D** weak or insufficient evidence. Confidence must not silently change the classification. Explain material confidence reductions in the row.

## 4. Phone-route and liveness signals

### ContactPhone area-code mismatch

Compare a separate `ContactPhone` with the main business number. Record whether it is the same number/area code, different area code, toll-free, or unavailable. A different area code is a **routing risk**, not proof of a bad number or the contact's physical location. If a named person is present, until a different-area-code ContactPhone is confirmed to reach them, assign NCSA at least YELLOW and state the route uncertainty. If no person is named, retain NCSA INSUFFICIENT EVIDENCE and record the number's route uncertainty separately; never invent a person-level match. Never make it RED solely for an area-code mismatch. The respondent confirming that the number reaches the person resolves the route question only; it does not prove role fit or purchasing authority.

### `LastReviewDate` liveness bands

When relative review-date data are supplied, use these bands consistently:

- **LOW:** 3 months ago or more recent.
- **MEDIUM:** 4–6 months ago.
- **HIGH:** 7 months ago or older.
- **UNKNOWN:** missing or not reliably parseable.

These are business-activity signals only. They do not establish current employees, phone validity, contact freshness, actionability, or closure. Use them to temper NCSA confidence where relevant; do not change class automatically. Recent reviews do not prove a record good, and old reviews do not prove it bad. If the source has no capture date, say so and do not imply an absolute observation date.

## 5. Ground-truth call questions and scoring

For **every record**, keep these prompts in three distinct fields so outcomes can be scored independently:

1. **FCA question:** Does the listed main phone reach the stated business/location at the supplied address? If not, what is the correct business/location route? Score whether the number reaches the intended account—not whether someone answered.
2. **Entity question:** Is the named business/outlet the right operating entity, and are relevant decisions local, parent-, franchise-, or platform-controlled? Tailor this to actual entity conflicts; do not ask every respondent to validate irrelevant enrichment.
3. **NCSA question:** Is the named person current, in the stated role, relevant to the offer, and reachable via the supplied route? For an unnamed-contact record, ask who owns/operates the location and who decides on the offer; do not pretend a person is already matched.

Questions must be answerable by phone, tailored to the record, and not framed to lead the respondent. Keep FCA, entity, and person/role/route outcomes separate, even if one call establishes multiple facts. Do not ask a respondent to validate revenue, employee counts, LinkedIn attribution, or email deliverability unless the user has a specific valid verification method. A connection alone is not proof the record is good; no answer or voicemail is inconclusive, not proof the record is bad.

## 6. Prioritization and predeclared falsification

- Select a top-ten (or user-requested number) of high-information phone tests from distinct, testable risks: wrong/ambiguous entity, parent or franchise routing, mismatched ContactPhone, named-role fit, unowned email, platform enrichment, or liveness uncertainty. State why each was selected. Include useful borderline cases, not only predicted REDs.
- Do not choose the list to match a preferred flag rate. A priority order is a test plan, not an assertion that unselected records are valid.
- Before calls, define what would confirm or refute each axis and how unanswered calls will be recorded. Where useful, predeclare rough interpretation bands for FCA GREEN-vs-YELLOW error/routing rates. Choose denominators and thresholds for the current dataset; **never copy Order 54's numeric thresholds or results automatically**.
- No Stage 2 analysis or outcome-adjusted prediction report until the user provides ground-truth outcomes. Afterward, preserve the frozen prediction, score only outcome-supported facts, keep unresolved/no-answer separate, report denominators, and do not retroactively edit the frozen file.

## 7. Standard report structure and row schema

Use a versioned Markdown report with these sections unless the user requests another format:

1. Dataset integrity and source limitations.
2. Methodology, definitions, assumptions, and confidence scale.
3. Frozen prediction table plus computed class totals.
4. Prioritized phone-test list.
5. Exact, separate FCA / entity / NCSA call questions for priority records.
6. Confirmation/refutation definitions and predeclared interpretation/falsification expectations.
7. A clear STOP/awaiting-ground-truth notice.

Recommended prediction-table columns:

`Record ID`, `Company`, `Contact`, `Stated Role`, `FCA`, `FCA Confidence`, `NCSA Status`, `NCSA Confidence`, `SEQ Classification`, `SEQ Confidence`, `Entity Status`, `Contact Status`, `Role Status`, `Phone Mismatch`, `LastReviewDate`, `Liveness Risk`, `Main Risk`, `RED Trigger`, `Pipeline42 Prediction`, `Evidence`, `Why This Matters for Outreach`, `Recommended Action`, `FCA Ground-Truth Question`, `Entity Ground-Truth Question`, `NCSA Ground-Truth Question`.

Use `—` for no RED trigger; do not leave the reason implicit. For each RED, state whether it is NCSA/person-role, route, or entity-level and identify the supporting source evidence. Keep all original identifiers and ensure no source row silently disappears.

## 8. Generation and validation checklist — required before presenting

### Before generation

- [ ] Confirm the active branch/workspace and locate the exact source files; do not assume stale local copies or missing upload folders contain the data.
- [ ] Parse actual headers and row counts; inspect null/placeholder values. Assign IDs and verify any cross-file joins using keys rather than an unchecked row-order assumption.
- [ ] Create an evidence ledger/mappings for every record and define every set, function, lookup, and output column before using it. Do not rely on implicit variable names or copied snippets with undefined identifiers.
- [ ] Derive classes from evidence and the definitions above. Compute totals from row-level labels; never hard-code narrative totals independently of the table.
- [ ] Keep predictions frozen before the first ground-truth outcome. Create a new version rather than editing a prior frozen report.

### After generation, before presentation

- [ ] Confirm the output file exists and can be read back; generation errors must stop delivery rather than leave a guessed/partial file.
- [ ] Assert one prediction row per source record, exact row count, unique IDs, expected column count/order, no malformed Markdown rows, and no missing questions/statuses.
- [ ] Compute FCA, NCSA (including INSUFFICIENT EVIDENCE), and SEQ counts from the parsed output. Check that the printed summary matches those counts and that totals equal the source denominator.
- [ ] Check every RED has a nonempty, evidence-backed RED Trigger; every non-RED has the agreed empty marker. Check specific requested overrides (confidence, sublabels, priority inclusion) against parsed output.
- [ ] Search for stale `FINAL` classification labels, accidental post-call language, unrequested Stage 2 conclusions, unexplained count targets, and claims of external verification that did not happen.
- [ ] Read the beginning, representative normal and exception rows, priority questions, and ending of the rendered report. Then present the final deliverable and state the validation results.

## 9. Order 54 notes (examples only; never defaults)

Order 54's v3 demonstrated the method with FCA 35 GREEN / 16 YELLOW / 0 RED; NCSA 1 GREEN / 13 YELLOW / 2 RED / 35 INSUFFICIENT EVIDENCE; and SEQ 1 GREEN / 47 YELLOW / 3 RED. LF-11's unmatched Cheryl email remained insufficient evidence with confidence C and was included in the top ten; LF-31 remained NCSA INSUFFICIENT EVIDENCE but SEQ RED for entity contamination. These decisions document that dataset and its stated offer assumption only. Reassess every equivalent-looking record in future data from its own evidence.
