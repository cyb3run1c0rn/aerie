# AERIE — A governed AI execution plane enforcing explicit intent, least privilege, and full auditability.

## 📄 Architectural Paper

**From Policy to Enforcement: An Architectural Pattern for Governed AI Execution**

This paper proposes the **AI Execution Control Plane** — an architectural pattern for enforcing governance at the execution boundary of agentic AI systems.

AERIE is presented as a **reference architecture** instantiating this pattern using:
- Structured intent envelopes
- Capability-scoped execution authority
- Non-bypassable policy enforcement
- Immutable execution ledgers

📘 Preprint (arXiv): [ADD_ARXIV_LINK_HERE]
📂 Paper source (LaTeX): [./paper](./paper)
📑 PDF version: [From_Policy_to_Enforcement_AERIE.pdf](paper/From_policy_to_enforcement__AERIE.pdf)


## Purpose

This document establishes *what AERIE is*, *what it is not*, and *who it is for*. It is the canonical reference that prevents architectural drift and misinterpretation as the system evolves.

---

## Description

**A governed AI execution plane that lets intelligent agents act with real power, while enforcing explicit human intent, least‑privilege capabilities, and full auditability by design.**

---

## Problem Statement

Current AI agent frameworks conflate intelligence with authority. They rely on prompts, model behaviour, or inferred intent to control execution, resulting in scope drift, weak governance, and post‑hoc explanations instead of provable accountability.

Organisations need AI systems that can *act*—not just think—without sacrificing control, safety, or compliance.

---

## What AERIE Is

* A **control and governance plane** for AI execution
* A system that **separates intent, authority, and action**
* A **model‑agnostic** architecture compatible with hosted or local LLMs
* A **human‑authorised** execution layer enforcing least privilege
* An **audit‑first** design suitable for regulated environments

AERIE is designed to sit *downstream* of cognitive systems (e.g. Local LLM agents etc), receiving structured intent and deciding **if, how, and under what constraints** execution may occur.

---

## What AERIE Is Not (Explicit Non‑Goals)

AERIE is **not**:

* An autonomous agent framework
* A prompt‑driven governance solution
* A self‑healing or improvisational system
* A chatbot, copilot, or LLM wrapper
* A replacement for cognitive or knowledge systems like PAI

If a feature requires trusting model behaviour instead of enforcing policy, it is out of scope.

---

## Target Audience

Primary:

* Security engineers
* Platform and infrastructure engineers
* AI governance and risk professionals
* Architects working in regulated environments

Secondary:

* Advanced individual practitioners using Personal AI‑style systems
* Researchers exploring safe agent execution
* Standards and assurance bodies

---

## Design Ethos

AERIE prioritises:

* **Architecture over prompts**
* **Authorisation over alignment**
* **Provable behaviour over explainability theatre**
* **Replaceable models over embedded intelligence**

Where ambiguity exists, the system must halt—not infer.

---

## Relationship to PAI

AERIE is designed to **complement**, not compete with, Personal AI Infrastructure (PAI):

* PAI supports cognition, research, and synthesis
* AERIE governs execution, authority, and accountability

PAI produces *intent*. AERIE governs *action*.

---

## Success Criteria (Phase‑Independent)

AERIE is successful if:

* Execution authority can be explained without reference to prompts or conversations
* Actions can be independently reconstructed from records
* Models can be swapped without altering governance guarantees
* Failure modes default safely and return control to humans

---

## Status

Phase 0 complete once this document is approved and frozen.
Future phases may extend functionality, but must not contradict the intent set here.


## Citation

If referencing this work:

Stockdale, W. (2026). *From Policy to Enforcement: An Architectural Pattern for Governed AI Execution*. arXiv preprint.

BibTeX:

```bibtex
@article{stockdale2026policy,
  author  = {Stockdale, Warren},
  title   = {From Policy to Enforcement: An Architectural Pattern for Governed AI Execution},
  journal = {arXiv preprint},
  year    = {2026}
}
```


## Licensing (RAPTOR-Aligned)

**AERIE** is dual-licensed to ensure wide accessibility while providing a sustainable model for future development.

### Free (Non-Commercial Use)
- **Personal use**
- **Academic, research, and non-profit use**
- **Internal use and evaluation**  
  You are welcome to study, modify, and use AERIE in non-commercial environments, provided you maintain attribution.  
  **No commercial revenue generation is allowed without proper licensing.**

### Commercial Use Requires a License
- If you are selling a product or service using AERIE or its derivatives, embedding AERIE into a commercial platform, or offering paid consulting where AERIE is a core deliverable, a commercial license is required.
- For **commercial licensing**, please contact us at: **[contact@promptsmiths.space](mailto:contact@promptsmiths.space)**

For detailed licensing terms, please refer to the [LICENSE](LICENSE) and [COMMERCIAL LICENSE](LICENSES/COMMERCIAL-LICENSE.md) files.
