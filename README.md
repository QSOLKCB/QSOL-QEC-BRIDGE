# QSOL-QEC-BRIDGE

**QSOL-QEC-BRIDGE is the conformance airlock between experimental QSOLQEC work and the canonical QSOLKCB/QEC repository.**

QSOLQEC is intentionally permissive: it exists to try new state representations, decoders, observers, compute backends, sonification paths, compression schemes, and other research ideas without forcing those ideas into QEC's stricter proof and release lineage.

This repository exists so those two environments never have to be coupled directly.

```text
QSOLQEC
experimental research
    |
    | promoted candidate
    v
QSOL-QEC-BRIDGE
translation / conformance / reproduction
    |
    | validated integration artifact
    v
QSOLKCB/QEC
canonical proof stack
```

## Purpose

The bridge will eventually provide a controlled path for moving a mature QSOLQEC result toward QEC without granting QSOLQEC code, schemas, claims, or runtime behavior any automatic authority inside QEC.

A result entering this repository is still a **candidate**.

The bridge must independently determine whether the candidate can be represented, reproduced, and validated under the QEC contracts that apply at the time of integration.

## Non-goals

QSOL-QEC-BRIDGE is not:

- an experimental playground;
- a second implementation of QSOLQEC;
- a shortcut around QEC governance;
- an authority that can promote a result merely because QSOLQEC produced it;
- a place to copy entire donor repositories;
- a quantum-hardware claim layer.

If translation or conformance cannot be demonstrated, the candidate remains outside QEC.

## Intended flow

### 1. Candidate export

QSOLQEC exports a bounded candidate package containing only what is required to reproduce the result, for example:

- module identity and version;
- source commit;
- experiment specification;
- declared capabilities;
- input fixtures;
- output artifacts;
- numerical contract;
- approximation/error declaration;
- benchmark method;
- provenance;
- claim boundary.

### 2. Schema translation

The bridge translates experimental QSOLQEC structures into an explicit bridge schema.

Translation must be loss-aware. Unsupported or ambiguous fields fail closed rather than being silently normalized.

### 3. Independent reproduction

The bridge reproduces the candidate from the declared source and fixtures.

A QSOLQEC receipt is evidence about the QSOLQEC experiment; it is not accepted as proof of bridge reproduction.

### 4. Conformance checks

Candidate behavior is checked against the relevant QEC expectations, which may include:

- deterministic experiment identity;
- canonical serialization;
- hash stability;
- replay behavior;
- oracle/candidate separation;
- numerical tolerances;
- claim boundaries;
- decoder or representation invariants;
- provenance requirements;
- benchmark reproducibility.

### 5. Integration artifact

If the candidate survives reproduction and conformance, the bridge emits a bounded integration artifact suitable for review by QEC.

The artifact should contain enough evidence for QEC to validate it without trusting the bridge's conclusions.

### 6. QEC review

QSOLKCB/QEC remains the final authority over whether anything is adopted into its canonical lineage.

Bridge success means **eligible for QEC review**, not **accepted by QEC**.

## Proposed repository structure

```text
QSOL-QEC-BRIDGE/
├── README.md
├── docs/
│   ├── BRIDGE_CONTRACT.md
│   ├── TRANSLATION_RULES.md
│   ├── CONFORMANCE.md
│   └── PROMOTION_BOUNDARY.md
├── schemas/
│   ├── candidate/
│   └── integration/
├── adapters/
│   ├── qsolqec/
│   └── qec/
├── fixtures/
├── validators/
├── receipts/
└── tests/
```

This is a plan, not an assertion that those components already exist.

## Candidate maturity

QSOLQEC may use an experimental maturity ladder such as:

```text
E0  sketch
E1  executes
E2  deterministic fixture
E3  oracle-compared
E4  benchmarked
E5  independently replicated
E6  candidate for bridge evaluation
```

The bridge should normally accept only explicitly promoted candidates. Reaching E6 does not imply QEC compatibility.

## Design principles

1. **No direct QSOLQEC -> QEC integration.**
2. **Translation is explicit and loss-aware.**
3. **External evidence is reproduced, not trusted.**
4. **Candidate claims never expand during translation.**
5. **Approximation remains approximation.**
6. **Simulation evidence remains evidence about the declared model.**
7. **Optimization does not become correctness authority.**
8. **Bridge acceptance is not QEC acceptance.**
9. **The current QEC contract wins if QSOLQEC and QEC disagree.**
10. **Failure to conform is a valid research result, not a reason to weaken QEC.**

## Initial implementation plan

### B0 - Documentation boundary

- Freeze the purpose and non-goals of the bridge.
- Define the QSOLQEC -> Bridge -> QEC direction of authority.
- Keep the repository implementation-free until QSOLQEC has a real promotion candidate.

### B1 - Candidate package schema

- Define the minimum candidate manifest.
- Bind source revision, module identity, experiment identity, fixtures, outputs, numerical contract, and claims.
- Reject undeclared mutable dependencies.

### B2 - QSOLQEC adapter

- Parse an exported QSOLQEC candidate package.
- Validate internal identity and required artifacts.
- Preserve unsupported fields rather than discarding them silently.

### B3 - Reproduction harness

- Re-run the exported experiment under a declared environment.
- Compare outputs under the candidate's numerical contract.
- Emit independent bridge receipts.

### B4 - QEC conformance adapter

- Map reproduced evidence to the current QEC integration contract.
- Keep QEC-specific invariants out of QSOLQEC.
- Fail closed when no valid mapping exists.

### B5 - Integration package

- Emit a minimal QEC-facing package.
- Include source lineage, reproduction evidence, translation record, validation results, and unchanged claim boundaries.

### B6 - Cross-repository integration tests

- Pin exact QSOLQEC and QEC revisions.
- Test known-compatible, known-incompatible, and ambiguity cases.
- Ensure a change in either side cannot silently change bridge semantics.

## Status

**Current phase: B0 - Documentation boundary.**

No QSOLQEC module has been promoted through this bridge yet, and no bridge artifact should be interpreted as part of QSOLKCB/QEC unless QEC explicitly adopts it.
