# AERIE — Phase 7: Non‑Goals, Guardrails & Long‑Term Constraints

## Purpose

This document defines **what AERIE will deliberately never become**.

Its role is to prevent scope creep, accidental autonomy, and future design decisions that undermine the foundational primitives. These constraints protect the system from well‑intentioned but unsafe extensions.

---

## Core Guardrail Principle

**AERIE must remain a governance and execution control plane, not an autonomous agent system.**

Any feature that weakens human authority, explicit intent, or deterministic enforcement is out of scope.

---

## Explicit Non‑Goals

AERIE will **not**:

* Become a general‑purpose agent framework
* Support self‑directed or self‑initiated execution
* Perform long‑running autonomous loops
* Infer or reinterpret intent from context
* Rely on model behaviour for safety or compliance
* Optimise for speed at the expense of auditability
* Embed business logic in prompts or conversations
* Provide silent self‑healing or improvisational recovery

If a capability requires trusting the model to “do the right thing,” it is a non‑goal.

---

## Authority Guardrails

The following boundaries are absolute:

* Humans remain the sole originators of intent
* Capability issuance is explicit, scoped, and revocable
* Execution never occurs without a valid capability
* All actions are logged immutably

No feature may collapse these boundaries for convenience.

---

## Anti‑Patterns to Actively Resist

The project must actively resist:

* “Just one autonomous shortcut” features
* Prompt‑based safety controls
* Implicit retries or fallback behaviour
* Hidden escalation paths
* Model‑specific optimisations that erode portability

These patterns are considered architectural regressions.

---

## Change Control Discipline

Future enhancements must:

* Explicitly state which design primitives they rely on
* Demonstrate they do not violate any primitive
* Document new risks introduced

If a change weakens a primitive, the primitive must be formally revised first.

---

## Long‑Term Constraints

AERIE must remain:

* Model‑agnostic
* Human‑authorised
* Deterministic in enforcement
* Auditable without model introspection

Emerging AI capabilities may be integrated only if these constraints are preserved.

---

## Relationship to Standards & Regulation

AERIE is designed to align naturally with:

* Least privilege principles
* Separation of duties
* Audit and assurance requirements
* Regulated execution environments

It must not adopt patterns that would make independent assurance impossible.

---

## Status

Phase 7 complete once these guardrails are accepted and frozen.
Phase 8 will define the development handoff to implementation tooling (e.g. Claude Code).
