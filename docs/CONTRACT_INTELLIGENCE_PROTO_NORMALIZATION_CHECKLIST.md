# Contract Intelligence Proto Normalization Checklist

## Purpose

This checklist captures the remaining normalization work for the `contract_intelligence` protobuf compatibility package.

It exists so the remaining deltas are captured in-repo and do not depend on chat history.

## Canonical references

Normalize the protobuf package against all of the following:

1. `SocioProphet/socioprophet-standards-storage/docs/standards/interfaces/tritrpc-contract-intelligence.md`
2. `SocioProphet/socioprophet-standards-storage/schemas/json/contract-intelligence/`
3. `SocioProphet/socioprophet-standards-storage/schemas/avro/contract-intelligence/`
4. `SocioProphet/TriTRPC` transport posture for stable TritRPC v1 / Path-A

## Package under normalization

- `proto/socioprophet/contract_intelligence/v1/types.proto`
- `proto/socioprophet/contract_intelligence/v1/service.proto`
- `proto/socioprophet/contract_intelligence/v1/query.proto`
- `proto/socioprophet/contract_intelligence/v1/evaluation.proto`

## Current status

The package exists and is useful, but it should still be treated as a compatibility/developer-facing surface until the following items are normalized.

## Checklist

### A. Types parity

- [ ] Confirm `DocumentArtifact` fields match the canonical JSON and Avro families where the compatibility layer intends a 1:1 mirror.
- [ ] Confirm `ProfileResolution` fields match canonical pack-selection and resolver-evidence fields.
- [ ] Confirm `ContractClause`, `ContractObligation`, `InterpretationEvidence`, `ReviewerFeedback`, `BenchmarkCase`, and `EvaluationReport` stay aligned with the canonical families.
- [ ] Document any intentional compatibility-only deviations.

### B. Command service parity

`service.proto`

- [ ] Confirm `IngestDocument` request shape matches the intended command-plane surface.
- [ ] Confirm `ResolveProfile`, `ParseDocument`, `ExtractClauses`, `ExtractObligations`, `ApplyReviewerFeedback`, and `RecomputeExtraction` remain aligned with the interface standard.
- [ ] Ensure recomputation explicitly supports pack references where required.
- [ ] Ensure request/response naming is stable and not drifting from the shared interface terminology.

### C. Query service parity

`query.proto`

- [ ] Confirm retrieval methods match the query-plane surface from the interface standard.
- [ ] Confirm `GetInterpretationEvidence` request semantics are explicit enough for document and artifact-level retrieval.
- [ ] Confirm artifact listing methods remain compatible with canonical artifact identity/version posture.

### D. Evaluation service parity

`evaluation.proto`

- [ ] Add or confirm an explicit benchmark-suite selector where required.
- [ ] Ensure benchmark requests preserve enough information to tie runs to benchmark cases and pack versions.
- [ ] Ensure `ApprovePromotion` includes enough artifact identity to avoid ambiguous approvals.
- [ ] Ensure `ReplayRun` preserves explicit replay references expected by the interface standard.
- [ ] Determine whether `ReplayRunResponse` should carry an `EvaluationReport` or equivalent replay result surface.

### E. TriTRPC binding clarity

- [ ] Keep the protobuf package clearly documented as compatibility-facing.
- [ ] Avoid implying protobuf is the normative on-wire format if upstream TriTRPC Path-A remains Avro-aligned.
- [ ] Preserve a clear distinction between logical service contracts and wire/transport authority.

### F. Verification

- [ ] Run the repository’s generation/build workflow for the normalized package.
- [ ] Verify generated artifacts/build outputs are updated if required by repo conventions.
- [ ] Add a small compatibility example or smoke fixture if helpful.

## Completion condition

This protobuf compatibility package can be treated as normalized when:

- the checklist above is complete,
- any intentional deviations are documented,
- and the package is clearly framed as compatible with the canonical upstream JSON/Avro/TriTRPC posture.
