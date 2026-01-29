# AERIE — Phase 2: Trust Boundaries & Roles

## Purpose

This document defines the actors within the AERIE architecture and establishes **explicit trust boundaries** between them.

Authority, responsibility, and accountability must be unambiguous. No actor may assume privileges that are not explicitly granted.

---

## Core Design Principle

**Authority flows downward from humans; execution flows upward from systems.**

No component is both an authority source and an execution actor.

---

## Defined Roles

### 1. Human Principal

#### Description

The Human Principal is the ultimate source of authority in the system.

#### Responsibilities

* Declare intent
* Approve execution scope
* Authorise capability issuance (directly or via policy)
* Accept accountability for outcomes

#### Explicit Powers

* Issue or revoke intent
* Approve or deny execution
* Suspend or terminate the system

#### Explicit Limitations

* Cannot bypass AERIE controls
* Cannot retroactively alter execution records

---

### 2. Cognitive System (e.g. PAI / LLM)

#### Description

The Cognitive System performs reasoning, synthesis, planning, and proposal generation. It may assist humans in formulating intent but **does not possess execution authority**.

#### Responsibilities

* Analyse context and data
* Propose plans or actions
* Translate human goals into structured intent proposals

#### Explicit Powers

* Read knowledge bases and context
* Generate structured intent drafts

#### Explicit Limitations

* Cannot execute actions
* Cannot issue capabilities
* Cannot modify intent post‑authorisation
* Cannot access execution credentials

---

### 3. AERIE Control Plane

#### Description

The AERIE Control Plane is the governance and enforcement layer that validates intent, issues capabilities, enforces policy, and records all actions.

It is **authoritative but non‑cognitive**.

#### Responsibilities

* Validate intent envelopes
* Evaluate policy
* Issue and revoke capabilities
* Enforce least privilege
* Record execution events immutably

#### Explicit Powers

* Grant or deny execution authority
* Halt execution on policy violation or failure

#### Explicit Limitations

* Cannot infer intent
* Cannot execute tools directly
* Cannot alter human‑approved intent

---

### 4. Execution Substrate

#### Description

The Execution Substrate consists of tools, APIs, scripts, infrastructure, and external systems that perform real‑world actions.

#### Responsibilities

* Execute actions when presented with valid capabilities
* Enforce scope and constraints locally

#### Explicit Powers

* Perform bounded actions as authorised

#### Explicit Limitations

* Cannot initiate actions independently
* Cannot escalate privileges
* Cannot reinterpret intent

---

## Trust Boundaries

### Boundary A — Human ↔ Cognitive System

* Trust: advisory only
* Risk mitigated: over‑reliance on model judgement

### Boundary B — Cognitive System ↔ AERIE Control Plane

* Trust: none
* Interaction via structured intent objects only

### Boundary C — AERIE Control Plane ↔ Execution Substrate

* Trust: conditional
* Enforced by capability tokens and policy

### Boundary D — Execution Substrate ↔ External World

* Trust: externalised risk
* Mitigated via least privilege and audit

---

## Authority Flow (Textual)

Human Principal
→ declares intent
→ approves execution

Cognitive System
→ proposes intent
→ assists planning

AERIE Control Plane
→ validates intent
→ issues capabilities
→ enforces policy

Execution Substrate
→ performs bounded actions
→ reports results

---

## Forbidden Authority Collisions

The following are explicitly disallowed:

* Cognitive systems executing tools
* Execution systems issuing capabilities
* Control plane inferring intent
* Humans bypassing control enforcement

Any design that collapses roles violates this phase.

---

## Status

Phase 2 complete once roles and trust boundaries are accepted and frozen.
All subsequent schemas and control flows must conform to these definitions.

