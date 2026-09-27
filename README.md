# SourceRoots

**Trace the documented origins behind a claim, using GenLayer Intelligent Contracts.**

Three articles can repeat one announcement. One article can contain several evidence origins. SourceRoots examines the supplied text for a specific claim, groups explicitly shared origins, and records documented separate evidence-producing events with exact quotations.

This is version 0.1: a controlled-text prototype with eight fictional examples. It does not fetch URLs, authenticate pages, establish factual truth, prove hidden independence, or approve publication.

## Current demo

| Item | Recorded value |
| --- | --- |
| Environment | Hosted GenLayer Studio development environment |
| Contract address | `0x355913aD17b8317493b77A6f92C19C73567e1897` |
| Rubric | `sourceroots-controlled-text-0.1` |
| Observation date | 27 September 2026 |
| Evidence | Owner-provided Studio screenshots; full address supplied by owner |
| Demo outcomes | Eight returned results matched the expected statuses and eligibility flags |

The screenshots show Normal (Full Consensus) mode, Simulation Mode unchecked, and results read from Accepted state. This package does not contain an independently retrieved transaction receipt or an on-chain source comparison. Studio observations are not a production-network deployment claim.

See [DEMO_RESULTS.md](DEMO_RESULTS.md) for the result-by-result review and [deployment.json](deployment.json) for machine-readable deployment metadata.

## How it works

1. Validate a claim and two to five submitted source texts.
2. If any source is marked missing, record an incomplete result without an AI assessment.
3. Ask a leader model to identify relevant origins, quote evidence, group shared origins, and describe documented separation.
4. Check the output structure, exact quotation matching, source coverage, and pair indexes in code.
5. Have validators audit the full proposed report against the same input and rubric through GenLayer's custom equivalence mechanism.
6. Compute the demo policy in code and append the result to contract storage.

Each record includes the original inputs, rubric version, submitter, and a SHA-256 input fingerprint. The fingerprint binds the record to its submitted inputs; it does not authenticate those inputs.

`eligible_for_review` is true only when at least one distinct origin pair is documented and no relevant source material is unresolved. A missing source always produces false. This flag triggers no payment or publication action.

## Run the examples

For the existing deployment, use its current Studio session. To reproduce in a separate instance:

1. Open [GenLayer Studio](https://studio.genlayer.com/).
2. Use **Add From File** to import `sourceroots.py`, open it, and select **Run and Debug**.
3. Deploy with no constructor parameters. Preserve the dependency header in the file.
4. Call `get_count` and note the current number, N.
5. Under Write Methods, call `run_demo` with a `case_id` from 1 through 8. Send once and wait for the transaction to finish.
6. Check the execution outcome and refresh `get_count`. If exactly one result was appended, read `get_result(N)` and inspect the response.

Finalization by itself is not proof that an assessment succeeded. If the count did not advance, inspect the transaction error before retrying. With concurrent submissions, verify that a returned record contains your intended input and submitter.

Case IDs start at 1. Stored result IDs start at 0. The `case_id - 1` mapping applies only when all cases were run once, in order, on a fresh instance.

`get_result` returns a JSON string, so escaped quotes in Studio are normal. `get_demo` previews a fixture without saving an assessment.

## Methods

| Method | Kind | Purpose |
| --- | --- | --- |
| `get_count()` | Read | Number of stored results |
| `get_demo(case_id)` | Read | Fictional input for case 1–8 |
| `get_result(result_id)` | Read | Stored assessment as a JSON string |
| `run_demo(case_id)` | Write | Assess and store a fictional example |
| `assess(claim, sources_json)` | Write | Assess and store custom submitted text |

For `assess`, use a claim of 1–500 characters and a JSON array of 2–5 source objects with exactly `id`, `status`, and `text`. Source IDs must be unique and use 1–16 letters, digits, underscores, or hyphens. Available text must have at least 20 characters after trimming its outer whitespace and be at most 3,000 characters in total. Missing text must be empty. The entire source JSON string is limited to 25,000 characters.

Example fictional input for the claim `Alder's depot was receiving deliveries on Monday.`:

```json
[
  {"id":"A","status":"AVAILABLE","text":"Our reporter visited Alder's depot on Monday and observed deliveries being received; visit record A17."},
  {"id":"B","status":"AVAILABLE","text":"Our inspection team made its own Monday visit to Alder's depot and observed deliveries being received; inspection record B42."}
]
```

Inputs and results are public in the deployment environment. Use fictional or suitable public material.

## Verification and limits

The original file passed local GenVM linting and direct-mode checks with mocked AI responses before the owner ran the eight Studio examples. Those local checks and screenshot observations are distinct forms of evidence; details are in the demo report. The original source bytes are preserved. Its opening comments describe the earlier, pre-deployment checkpoint; this README and demo report record the later Studio results.

Eight selected fictional examples do not establish general accuracy, repeated-run reliability, or general prompt-injection resistance. Exact quote matching catches fabricated excerpts but cannot by itself guarantee that an interpretation is correct. Multiple validators can also share mistakes.

Next development priorities are reproducible result/receipt exports, broader and repeated evaluation, a readable result interface, and a separately versioned URL-capture workflow with explicit handling for unavailable material.

## References

- [Loading a contract in Studio](https://docs.genlayer.com/developers/intelligent-contracts/tools/genlayer-studio/loading-contract)
- [Equivalence principle](https://docs.genlayer.com/developers/intelligent-contracts/equivalence-principle)
- [Contract storage](https://docs.genlayer.com/developers/intelligent-contracts/storage)

This package is prepared for GitHub; creating a repository or publishing a builder contribution is a separate step.
