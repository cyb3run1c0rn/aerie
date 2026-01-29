# AERIE Policy Layer

This directory contains declarative governance policies enforced by the AERIE Control Plane.

Policies in AERIE:
- are human-readable
- are deterministic (ALLOW or DENY)
- are versioned and auditable
- are external to code and models
- fail closed on ambiguity

If a rule cannot be expressed as policy, it must not be enforced implicitly.

Example policies live in `policies/examples/`.
