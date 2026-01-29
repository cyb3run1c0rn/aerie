# AERIE — Phase 3: Core Objects & Data Models

## Purpose

This document defines the **canonical objects** that carry authority, intent, and accountability through AERIE.

These objects are the system’s *mechanical truth*. Control, enforcement, and audit depend on them being explicit, minimal, and immutable where stated.

---

## Design Rules (Non‑Negotiable)

* All authority is expressed via **objects**, not prompts or conversations
* Objects are **schema‑validated** and versioned
* Object identifiers are globally unique
* Integrity is verifiable (hashes / signatures)

---

## 1. Intent Envelope

### Description

The Intent Envelope represents **explicit human intent** authorised for potential execution. It is immutable once execution begins.

### Required Fields

* `intent_id` — globally unique identifier
* `issuer` — human principal (or delegated authority reference)
* `declared_goal` — plain‑language objective
* `constraints` — scope, limits, prohibitions
* `requested_actions` — abstract action types (not tools)
* `expiry` — time‑bound validity
* `created_at` — timestamp
* `integrity_hash` — hash of full envelope

### Properties

* Immutable at execution start
* Human‑readable
* Machine‑verifiable

### Notes

The Intent Envelope does **not** grant execution authority. It only declares what *may* be attempted.

---

## 2. Capability Token

### Description

A Capability Token grants **bounded execution authority** for a specific action on a specific resource under defined conditions.

### Required Fields

* `capability_id` — globally unique identifier
* `intent_id` — reference to originating Intent Envelope
* `action` — permitted operation
* `resource_scope` — bounded target (resource, API, system)
* `conditions` — contextual constraints (time, state, environment)
* `ttl` — explicit expiry
* `issued_by` — control plane reference
* `revocation_handle` — mechanism for invalidation

### Properties

* Least‑privilege by design
* Time‑limited
* Revocable

### Notes

Capabilities are **consumed**, not trusted. Tools must enforce capability checks regardless of model output.

---

## 3. Execution Record

### Description

An Execution Record captures a **single action attempt** performed under a capability.

### Required Fields

* `execution_id` — globally unique identifier
* `intent_id` — reference
* `capability_id` — reference
* `tool_invoked` — execution target
* `inputs` — values or cryptographic hashes
* `outputs` — results or cryptographic hashes
* `timestamp` — execution time
* `result` — success | failure | partial
* `failure_reason` — required if not success

### Properties

* Append‑only
* Sufficient for reconstruction

### Notes

If an action is not recorded, it is considered **not authorised**.

---

## 4. Execution Ledger

### Description

The Execution Ledger is an **append‑only, tamper‑evident log** of Execution Records.

### Required Properties

* Ordered entries
* No deletion or mutation
* Cryptographic linkage (hash chaining or equivalent)

### Required Capabilities

* Verify integrity
* Reconstruct execution sequences
* Support independent audit

### Notes

The ledger is a system of record, not a debugging aid.

---

## Object Relationships (Textual)

Human Principal
→ issues Intent Envelope

AERIE Control Plane
→ validates Intent Envelope
→ issues Capability Token(s)

Execution Substrate
→ consumes Capability Token
→ produces Execution Record

Execution Ledger
→ stores Execution Records immutably

---

## Explicit Non‑Objects

The following are **not** authority‑carrying objects:

* Prompts
* Conversations
* Model memory
* Tool responses

They may inform cognition, but never execution.

---

## Status

Phase 3 complete once schemas are approved and frozen.
Subsequent phases may extend fields, but core semantics must remain intact.
