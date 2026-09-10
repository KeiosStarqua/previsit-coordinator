# Documentation

- Domain documentation, design briefs, and project concepts for PreVisit Call‑E Coordinator.

## Purpose

Maintain durable project references, user journey specifications, safety constraints, and hackathon build requirements.

## Ownership

- Files in this folder document product intent, safety rules, system boundaries, and architectural guidelines.
- Runtime code and test suites belong in `previsit-coordinator/`.

## Local Contracts

- Do not alter or contradict non-diagnostic safety guidelines or clinical terminology defined in `CONTEXT.md` and `doc/project_purpose.md`.
- Keep documentation aligned with real implementation status in `previsit-coordinator/`.
- Reference repositories under `Sources/` (such as legacy OpenMRS or CALL‑E integration guides) are external reference materials and must not be committed as project code.

## Work Guidance

- When modifying architectural or functional documentation, ensure all technical references (e.g. Java version, endpoints, case statuses) reflect actual codebase capabilities.
- Keep documentation clear, succinct, and structured.

## Verification

- Ensure relative markdown links between docs resolve properly.
- Verify terminology adheres to `CONTEXT.md`.

## Child DOX Index

(No child directories exist under `doc/`)
