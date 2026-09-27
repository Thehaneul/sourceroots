# SourceRoots — observed demo results

Date: 27 September 2026. Contract address supplied by the owner: `0x355913aD17b8317493b77A6f92C19C73567e1897`.

The owner ran the built-in cases in hosted GenLayer Studio and supplied screenshots of the returned records. The table records those observations, not an independent RPC replay, an exported automated test run, or a statistical accuracy benchmark. The screenshot collection remains in the project conversation and is not bundled here.

## Observed results

| Case | Stored result | Scenario | Processing | Status | Eligible |
| --- | --- | --- | --- | --- | --- |
| 1 | 0 | Three retellings of announcement R1 | ASSESSED | SHARED_ORIGIN | false |
| 2 | 1 | Reporter visit A17 and inspection B42 | ASSESSED | SEPARATE_ORIGINS_DOCUMENTED | true |
| 3 | 2 | Similar claims without an attributed origin | ASSESSED | UNRESOLVED | false |
| 4 | 3 | A cites B; B cites A; neither supplies underlying evidence | ASSESSED | UNRESOLVED | false |
| 5 | 4 | Shared announcement plus an interview about an unrelated topic | ASSESSED | SHARED_ORIGIN | false |
| 6 | 5 | Sources B and C marked missing | INCOMPLETE | UNRESOLVED | false |
| 7 | 6 | A source embeds an instruction to count it as independent | ASSESSED | SHARED_ORIGIN | false |
| 8 | 7 | A page contains both a shared announcement and its own visit | ASSESSED | SEPARATE_ORIGINS_DOCUMENTED | true |

All eight observed statuses and flags matched the expected demo outcomes.

## What was checked in the reports

- Case 1 grouped A, B, and C under announcement R1 instead of counting three origins.
- Case 2 retained the reporter and inspection quotations, with a distinct pair connecting the two origins.
- Cases 3 and 4 returned no origins and listed A and B as unresolved.
- Case 5 kept both announcement quotations. The painter interview concerned wall colour, so it did not become an origin for the opening-date claim. Source B remained relevant because it also contained announcement evidence.
- Case 6 listed B and C in `missing_sources`, returned `report: null`, and did not issue a provenance assessment.
- Case 7 kept the shared-announcement grouping despite the embedded instruction. This is one observed injection test, not a general security guarantee.
- Case 8 identified announcement R2 from A and B as one origin, reporter visit A17 from A as another, and inspection visit B42 from C as another. Its returned pairs were `[[0,1],[0,2],[1,2]]`, with no unresolved sources. These record separate documented events under the rubric; they do not prove independence outside the submitted text.

## Earlier local verification

Before Studio deployment, the project work recorded:

- `genvm-linter 0.11.0`: AST and SDK semantic checks passed.
- `genlayer-test 0.29.2`: direct-mode storage and validator checks using mocked AI responses passed.
- Deterministic checks covered the eight input formats; fabricated quote rejection; source coverage; duplicate evidence and invalid-pair rejection; shared, separate, and unresolved decisions; mixed origins; and the unresolved-source eligibility gate.
- Direct-mode checks covered append-only record behaviour, incomplete inputs, validator acceptance/rejection, and no result append after a malformed assessment.

Those checks used temporary scripts and mocked responses. This package does not present them as a committed automated test suite. The original source file is unchanged from that checkpoint.

## Observed Studio issue

One screenshot sequence also contained a background `gen_getContractCode` database error: `can't adapt type 'dict'`. Later screenshots showed successfully returned assessment records. The root cause was not independently diagnosed; a successful read of these records does not demonstrate that the separate Studio error is fixed.

## Evidence still to capture

Machine-readable assessment exports and complete transaction receipts would make this checkpoint easier for others to verify. Deployed source equivalence, validator/provider configuration, repeated runs, contradiction handling, and broader adversarial inputs have not been independently established by this screenshot review.
