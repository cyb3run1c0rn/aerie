# AERIE — Phase 6: PAI Integration Contract

## Purpose

This document defines the **formal interface between cognitive systems (e.g. PAI)** and the AERIE execution plane.

The goal is to enable seamless integration **without coupling**, ensuring AERIE can operate with PAI or any other cognitive system while preserving governance guarantees.

---

## Core Integration Principle

**Cognition proposes. Governance disposes.**

Upstream systems may assist humans in forming intent, but AERIE alone decides whether execution is permitted and under what constraints.

---

## Integration Boundary

### Upstream (PAI / Cognitive System)

Responsible for:

* Research and synthesis
* Planning and option generation
* Drafting structured intent proposals
* Presenting trade‑offs to the human principal

Explicitly *not* responsible for:

* Issuing execution authority
* Selecting credentials or tools
* Performing actions

---

### Downstream (AERIE Control Plane)

Responsible for:

* Validating intent envelopes
* Enforcing policy
* Issuing capability tokens
* Governing execution and audit

---

## Canonical Handoff Objects

### 1. Intent Proposal (Upstream → Human)

A non‑authoritative draft intent produced by the cognitive system.

Properties:

* Human‑readable goal description
* Suggested constraints
* Candidate actions
* Risk notes (optional)

**Note:** An Intent Proposal has *no authority* until approved and issued by a human as an Intent Envelope.

---

### 2. Intent Envelope (Human → AERIE)

The authoritative, schema‑validated intent object defined in Phase 3.

PAI may assist in drafting, but **must not submit on behalf of a human without explicit delegation**.

---

### 3. Capability Request (Upstream or Human → AERIE)

A structured request referencing a frozen Intent Envelope.

Properties:

* intent_id
* requested action
* resource scope
* justification (optional)

AERIE evaluates this request against policy.

---

## Interaction Pattern (Textual Sequence)

1. Human uses PAI to explore options and draft intent
2. Human approves and submits Intent Envelope to AERIE
3. PAI (or human) submits Capability Request
4. AERIE evaluates policy and issues or denies capability
5. Execution occurs only if capability is issued
6. Execution is recorded in the ledger

---

## Prohibited Integration Patterns

The following are explicitly disallowed:

* PAI executing tools directly
* PAI holding long‑lived credentials
* Implicit intent submission via conversation state
* Auto‑approval of execution without human involvement

Any integration that collapses cognition and execution violates AERIE design primitives.

---

## Model‑Agnosticism Guarantee

AERIE must not rely on:

* Model‑specific prompt behaviour
* Proprietary memory features
* Vendor‑specific APIs

PAI integrations must operate through:

* Structured objects
* Explicit interfaces
* Versioned contracts

---

## Extensibility

PAI is a **reference cognitive system**, not a dependency.

Other upstream systems may integrate provided they:

* Produce schema‑compliant intent objects
* Respect authority boundaries
* Accept execution denial as a valid outcome

---

## Status

Phase 6 complete once the integration contract is accepted and frozen.
Phase 7 will define non‑goals, guardrails, and long‑term constraints.
