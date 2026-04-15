# Contract Intelligence Compatibility Note

## Purpose

This document explains the role of the `contract_intelligence` protobuf package in `api-contracts`.

## Role of this package

The files under:

- `proto/socioprophet/contract_intelligence/v1/`

provide a **developer-facing compatibility surface** for service definitions and local tooling.

They are useful for:

- service stubs
- local integration code
- compatibility-oriented SDK generation
- developer ergonomics

## Canonical source of truth

The canonical structural and transport-adjacent sources of truth live outside this repository:

- **Contract-domain canon**: `SocioProphet/contractforge`
- **Cross-repo interface standard**: `SocioProphet/socioprophet-standards-storage/docs/standards/interfaces/tritrpc-contract-intelligence.md`
- **Canonical JSON schema family**: `SocioProphet/socioprophet-standards-storage/schemas/json/contract-intelligence/`
- **Canonical Avro payload family**: `SocioProphet/socioprophet-standards-storage/schemas/avro/contract-intelligence/`
- **Normative transport / wire posture**: `SocioProphet/TriTRPC`

## Transport posture

The `contract_intelligence` family uses **TriTRPC / TritRPC v1** as the transport/RPC authority.

Under the current stable upstream posture, the wire-adjacent payload path is aligned to the upstream TriTRPC Path-A model.

Accordingly, the protobuf files in this repository should be treated as a **compatibility mirror**, not an independent truth surface.

## Required reconciliation rule

Any change to the protobuf package should be reconciled against:

1. the upstream interface standard,
2. the canonical JSON contracts,
3. the canonical Avro payload family,
4. the current TriTRPC transport posture.

If there is any conflict, upstream standards and transport authority take precedence over the convenience IDL in this repository.

## Near-term expectation

The current `contract_intelligence` protobuf package should be normalized field-by-field against the canonical upstream payloads before it is treated as complete.

## Status

This note captures the intended role of the `api-contracts` `contract_intelligence` package as of `v0.1`.
