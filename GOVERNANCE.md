# AERIE — Phase 4: Control Flow (Happy Path & Failure Path)

## Purpose

This document defines AERIE’s deterministic execution lifecycle.

It specifies:

* The **happy path** from intent to action
* The **failure paths** and halt conditions
* The rules governing retries, recovery, and escalation

Where ambiguity exists, the system must halt.

---

## Core Control Principle

**Execution is a transaction.**

Each action attempt must be:

* explicitly authorised (capability)
* bounded (scope + TTL)
* recorded (ledger)
* fail‑closed (safe halt)

---

## Happy Path (End‑to‑End)

### Step 0 — Intent Draft (Cognitive System)

* Cognitive system (e.g. PAI/LLM) drafts a proposed Intent Envelope.
* Human Principal reviews and edits.

**Output:** Proposed Intent Envelope (unexecuted)

---

### Step 1 — Intent Submission (Human → Control Plane)

* Human Principal submits an Intent Envelope to AERIE.

**Control Plane checks:**

* Schema validation
* Issuer verification
* Expiry validity
* Policy compliance (high level)

**Output:** Accepted or rejected Intent Envelope

---

### Step 2 — Intent Freeze (Control Plane)

* Upon acceptance, the control plane computes integrity hash and stores the intent.
* The intent becomes the authoritative reference.

**Output:** Frozen Intent Envelope (immutable for execution)

---

### Step 3 — Capability Request (Cognitive System or Human)

* A Capability Token request is made referencing the frozen intent.

**Request must include:**

* desired action
* target resource scope
* intended tool category (optional)
* required conditions

---

### Step 4 — Capability Issuance (Control Plane)

* Control plane evaluates policy and either issues or denies.

**Issuance rules:**

* deny by default
* least privilege
* short TTL
* revocable

**Output:** Capability Token (or denial)

---

### Step 5 — Execution Attempt (Execution Substrate)

* Execution substrate receives:

  * Capability Token
  * Tool invocation request

**Execution substrate must:**

* validate capability token
* enforce resource scope
* enforce conditions
* refuse if invalid

**Output:** Tool execution result

---

### Step 6 — Record & Commit (Ledger)

* AERIE records the attempt as an Execution Record.
* Execution Record is appended to the ledger.

**Record binds:**

* intent_id
* capability_id
* tool invoked
* inputs/outputs (or hashes)
* result

---

### Step 7 — Capability Expiry & Closure

* Capability token expires naturally or is revoked.
* System returns to idle state.

---

## Failure Paths & Halt Conditions

### F1 — Intent Rejected

**Trigger:** invalid schema, expired intent, unverified issuer, policy conflict.

**System response:**

* reject intent
* record rejection event (non‑ledger or ledger event, depending on implementation)
* no capabilities can be issued

---

### F2 — Capability Denied

**Trigger:** policy disallows action/scope/conditions.

**System response:**

* deny capability
* return explicit denial reason
* no execution occurs

---

### F3 — Capability Invalid at Execution

**Trigger:** expired token, revoked token, signature mismatch, wrong scope.

**System response:**

* refuse execution
* record refused attempt

---

### F4 — Tool / Substrate Failure

**Trigger:** tool error, timeout, unexpected response, environment mismatch.

**System response:**

* halt action chain
* record failure with explicit reason
* do not retry automatically

---

### F5 — Policy Violation Detected Mid‑Flight

**Trigger:** condition not met, resource drift, suspicious behaviour.

**System response:**

* fail closed
* revoke outstanding capabilities as required
* record violation event

---

### F6 — Ambiguity / Missing Context

**Trigger:** unclear target, incomplete parameters, untrusted input.

**System response:**

* halt
* request renewed explicit intent or clarifying input
* no inference allowed

---

## Retry & Recovery Rules (Primitive #5 Enforcement)

### Automatic retries

**Forbidden.**

### Manual retry

Allowed only when:

* Human Principal issues renewed intent or explicit retry authorisation
* New capability token is issued
* The retry is recorded as a new execution attempt

### Alternative approach / fallback tool

Allowed only when:

* intent explicitly permits alternate tools/paths
* policy allows
* new capability issued

---

## Sequencing Guarantees

* Every execution attempt must map 1:1 to an Execution Record.
* No tool call without a valid capability.
* No execution chain continues after a halt event.

---

## Status

Phase 4 complete once control flow is approved and frozen.
Phase 5 will define the policy layer used in capability issuance and enforcement.
