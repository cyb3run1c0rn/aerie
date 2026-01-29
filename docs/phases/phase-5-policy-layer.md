# AERIE — Phase 5: Policy & Governance Layer

## Purpose

This document defines how **rules are expressed, evaluated, and enforced** within AERIE.

Policies are the mechanism by which human governance is translated into machine‑enforceable constraints. They must be explicit, inspectable, and versioned.

---

## Core Principle

**Governance must be declarative and external to code.**

If a rule cannot be expressed as policy, it must not be enforced implicitly through prompts or model behaviour.

---

## Policy Design Goals

Policies in AERIE must be:

* **Human‑readable** — understandable without specialised tooling
* **Machine‑evaluatable** — deterministic, no probabilistic interpretation
* **Versioned** — changes tracked and auditable
* **Composable** — small rules combine into enforceable decisions
* **Fail‑closed** — ambiguity results in denial

---

## Policy Scope Types

### 1. Intent Acceptance Policies

Govern whether an Intent Envelope may be accepted at all.

Examples:

* Allowed intent issuers
* Maximum intent duration
* Prohibited goal categories

---

### 2. Capability Issuance Policies

Govern whether a Capability Token may be issued.

Examples:

* Which actions may be bound to which intent types
* Maximum resource scope
* TTL limits by action class
* Environment restrictions (prod vs non‑prod)

---

### 3. Execution Constraint Policies

Govern runtime enforcement during execution.

Examples:

* Time‑of‑day restrictions
* Rate limits
* Environmental preconditions
* Contextual safety checks

---

### 4. Revocation & Emergency Policies

Govern how and when authority may be withdrawn.

Examples:

* Kill‑switch conditions
* Automatic revocation on anomaly
* Global freeze rules

---

## Policy Evaluation Model

### Determinism

* Policies evaluate to **ALLOW** or **DENY** only
* No scoring, weighting, or confidence thresholds

### Order of Evaluation

1. Intent acceptance policies
2. Capability issuance policies
3. Execution constraint policies
4. Emergency / revocation policies (always active)

The first **DENY** halts the process.

---

## Policy Expression Format

Policies should be expressed in:

* Declarative formats (e.g. YAML / JSON / Rego‑style)
* With explicit conditions and outcomes

Each policy must include:

* `policy_id`
* `version`
* `scope` (intent | capability | execution)
* `conditions`
* `decision` (allow | deny)
* `rationale` (human‑readable)

---

## Change Management

Policy changes:

* Must be versioned
* Must record author and timestamp
* Must not retroactively alter past execution outcomes

Execution is evaluated against the policy version active at the time of decision.

---

## Forbidden Governance Patterns

The following are explicitly disallowed:

* Policies embedded in prompts
* “Soft” guidance policies (“should”, “prefer”)
* Model‑interpreted rules
* Silent policy overrides

Governance must be enforceable, not advisory.

---

## Relationship to Primitives

This phase enforces:

* Primitive #2 (explicit intent)
* Primitive #3 (least‑privilege capability issuance)
* Primitive #5 (fail‑closed behaviour)

Any policy mechanism that weakens these primitives is invalid.

---

## Status

Phase 5 complete once the policy model is approved and frozen.
Phase 6 will define the integration contract with upstream cognitive systems (e.g. PAI).
