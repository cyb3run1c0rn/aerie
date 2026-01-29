# AERIE — Phase 1: Design Primitives (The Constitution)

## Purpose

This document defines AERIE’s non‑negotiable design primitives.

These primitives are **constraints**, not preferences. If a proposed feature violates a primitive, the feature is out of scope (or the primitive set must be explicitly revised with a recorded rationale).

---

## Primitive 1 — The AI should install the system, not become the system

### Statement

**The AI should install the system, not become the system.**

### Rationale

AERIE’s behaviour must be anchored in inspectable, versioned artefacts (code, configuration, policies, schemas, runbooks), not in model state, conversational history, or prompt drift. This ensures reproducibility, auditability, and model replaceability.

### Enforced by

* Source of truth lives in repositories and artefacts (not hidden prompts)
* Behavioural rules promoted to policy/config files
* Reproducibility tests on fresh environments

### Anti‑patterns forbidden

* “Prompt soup” architectures where logic lives in conversations
* Systems that only function with a specific model’s memory/personality
* Hidden governance logic embedded in prompt templates

---

## Primitive 2 — Intent must be explicit, externalised, and immutable at the point of execution

### Statement

**Intent must be explicit, externalised, and immutable at the point of execution.**

### Rationale

Execution authority must come from declared human intent, not inferred interpretation. Once execution begins, intent must not drift. This prevents scope creep, goal substitution, and post‑hoc rationalisation.

### Enforced by

* Structured Intent Envelope objects with identifiers and integrity checks
* Explicit constraints and expiry
* Freeze/lock semantics at execution start

### Anti‑patterns forbidden

* “The agent decided…” goal drift
* Implicit intent inferred from context
* Mid‑flight re‑interpretation of objectives

---

## Primitive 3 — Execution must be constrained by explicitly issued, least‑privilege capabilities

### Statement

**Execution must be constrained by explicitly issued, least‑privilege capabilities—never by trust in the model.**

### Rationale

Understanding is not permission. Agents must have no ambient authority. Power is delivered via scoped capabilities: narrow, time‑bound, revocable permissions to perform specific actions on specific resources.

### Enforced by

* Capability tokens with scope, TTL, conditions, and revocation
* Tool gateways that enforce capabilities regardless of model output
* Deny‑by‑default posture

### Anti‑patterns forbidden

* Reliance on “policy prompts” to prevent harmful actions
* Over‑broad credentials shared with agents
* Long‑lived tokens with unclear scope

---

## Primitive 4 — All agent actions must be immutably recorded and independently reconstructable

### Statement

**All agent actions must be immutably recorded in an append‑only ledger, sufficient for independent reconstruction and audit.**

### Rationale

Once agents can act, accountability becomes mandatory. The system must be able to reconstruct what happened, under what authorisation, and with what outcomes—without relying on model explanations.

### Enforced by

* Append‑only, tamper‑evident execution ledger
* Records binding: Intent ID + Capability ID + Tool invocation + result
* Hashing of sensitive inputs/outputs where needed

### Anti‑patterns forbidden

* Ephemeral logs that can be edited/deleted
* “Trust the agent’s explanation” after the fact
* Unlogged side‑effects

---

## Primitive 5 — Failure must be safe, bounded, and explicitly recoverable

### Statement

**Failure must be safe, bounded, and explicitly recoverable—never silent, cascading, or self‑healing by improvisation.**

### Rationale

Safe systems assume failure. When policy checks fail, tools error, or context is missing, execution must halt cleanly. Recovery requires renewed human intent and (where applicable) new capabilities.

### Enforced by

* Fail‑closed tool gateways
* Explicit error states and halt semantics
* Recovery pathways that require re‑authorisation

### Anti‑patterns forbidden

* Silent retries or hidden backoff loops
* Automatic scope expansion (“try something else”)
* Goal substitution during recovery

---

## Primitive Change Control

These primitives may only be changed if:

* The change is proposed in writing
* The trade‑off is explicitly documented
* The decision is recorded and versioned

If primitives change, downstream schemas, policies, and control flows must be reviewed for consistency.

---

## Status

Phase 1 complete once this document is approved and frozen as `DESIGN_PRIMITIVES.md` in the repo root.
