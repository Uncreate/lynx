# LYNX --- Phase 2 Work Handoff

## Purpose

This package transfers Lynx from the Phase 1 design conversation into an
implementation workspace.

**`docs/CONSTITUTION.md` is the authoritative behavioral
specification.**

If implementation convenience conflicts with the Constitution, **the
Constitution wins**. Do not silently weaken a constitutional property to
simplify implementation.

## Project vision

Lynx is a locally hosted, open-source orchestration and cognition system
intended to understand the user's environment over time, maintain an
evidence-backed temporal world model, delegate work to appropriate
experts, mediate capabilities through deterministic governance, verify
outcomes, and remain accountable to the sovereign user.

Lynx is **not** merely a chatbot, model router, Home Assistant
assistant, or agent framework.

Chat is one interface into Lynx.

## Non-negotiable project constraints

-   Open source.
-   Locally hostable.
-   Privacy first; need-to-know information flow.
-   Local operation must not depend on a proprietary cloud cognition
    service.
-   External experts/services may be optional capabilities when
    authorized.
-   The sovereign user remains the ultimate authority.
-   Critical governance cannot rely solely on an LLM following a prompt.
-   Evidence, provenance, temporal history, verification, and
    auditability are first-class concepts.
-   Lynx should make autonomous forward progress inside established
    intent and authority without consuming the user's attention for
    ceremonial approvals.

## Known current environment

### Utility Pi

-   Hosts the current Lynx prototype.
-   Debian 13 / ARM64.
-   Tailscale address previously observed: `100.109.227.45`.
-   Current project location: `~/lynx`.
-   Current service: Dockerized Python/FastAPI application.
-   Current persistence: SQLite.
-   Current exposed port: `8080`.

### Control Center

-   Windows host.
-   Tailscale address previously observed: `100.81.99.78`.
-   Intel Core i9-12900K.
-   NVIDIA RTX A4000 16 GB.
-   32 GB system RAM.
-   Hosts Ollama/local models.

### Local model context observed during prototype work

Models have included: - `mistral-small3.2:latest` - `qwen3:8b` - earlier
Home Assistant-oriented Ollama models and experiments.

**Important:** Treat model names and host state as environment
observations, not permanent architectural requirements. Verify current
state before relying on them.

## Existing implementation status

The existing `~/lynx` application should be treated as a **prototype and
historical starting point**, not as the target architecture.

Its conceptual loop has been approximately:

`user message → router/model selection → Ollama generation → response → conversation persistence`

Useful pieces may survive, including FastAPI plumbing, persistence work,
Ollama integration, containerization, and UI pieces.

The current routing/chat architecture must **not** dictate the Phase 2
design.

Do not rewrite the project merely for cleanliness. First inspect what
exists, identify reusable pieces, and justify changes against the
Constitution.

## Architectural boundary established in Phase 1

Conceptually:

``` text
SOVEREIGN USER
      |
ROOT OF TRUST
      |
DETERMINISTIC GOVERNANCE / POLICY ENFORCEMENT
      |
LYNX COGNITION
      |
EXPERT SELECTION / DELEGATION
      |
CAPABILITY MEDIATION
      |
TOOLS / SYSTEMS / REAL WORLD
      |
OBSERVATION / EVIDENCE / VERIFICATION
      |
TEMPORAL KNOWLEDGE + AUDIT
```

### Critical distinction

**Probabilistic cognition may propose, reason, plan, hypothesize, and
recommend. Deterministic governance decides whether a capability may
actually be exercised.**

The LLM is not the security model.

## External OpenAI relationship

The intended relationship is conceptually:

`Sovereign user ↔ external OpenAI interface ↔ Lynx ↔ local experts/tools/systems`

External OpenAI is an optional intermediary/expert interface. It is not
Lynx and does not inherit sovereign authority merely by being connected.

Delegated user intent must retain provenance.

## Phase 2 minimum objective

Do **not** begin by integrating every system or building a large agent
framework.

The first Phase 2 milestone should prove the constitutional architecture
on the smallest useful environment:

-   Utility Pi
-   Control Center / Ollama
-   Lynx itself

The minimum useful kernel should support:

1.  Root-of-trust/identity abstraction.
2.  Authority and policy evaluation.
3.  Temporal event/evidence model with provenance.
4.  Capability registry.
5.  Delegation envelope.
6.  Read-only observation capabilities.
7.  Verification semantics.
8.  Append-oriented audit records.
9.  World-model updates that preserve historical state.
10. Clear separation between cognition and capability enforcement.

Only after read-only discovery and reasoning are working should
controlled mutation be introduced.

## Phase 2 proof scenario

A successful early Lynx should be able to:

-   discover authorized facts about Utility Pi and Control Center;
-   represent their relationship;
-   record how and when each fact was learned;
-   distinguish observation from inference;
-   notice meaningful changes over time;
-   investigate an anomaly without needing a chat prompt;
-   select/use an expert when justified;
-   keep expert context need-to-know;
-   verify the expert's result independently where practical;
-   update its temporal knowledge;
-   explain afterward, from recorded provenance, what it knew,
    concluded, delegated, did, and verified.

## First assignment for ChatGPT Work

**Do not modify code immediately.**

1.  Inspect the complete existing Lynx repository.
2.  Read `docs/CONSTITUTION.md` in full.
3.  Produce a gap analysis between the prototype and Constitution v0.2.
4.  Identify:
    -   components that can be retained;
    -   components that should be refactored;
    -   components that should be retired;
    -   missing constitutional enforcement mechanisms;
    -   security/privacy boundaries that currently exist only as
        prompt-level assumptions.
5.  Propose the smallest staged implementation plan that reaches the
    Phase 2 proof scenario.
6.  Identify any architectural decision that genuinely requires
    sovereign-user judgment.
7.  Do **not** ask for ceremonial approval on decisions already
    established by the Constitution.
8.  Do **not** begin a broad rewrite until the gap analysis is reviewed.

## Explicit non-goals for the first implementation pass

-   Building a polished replacement chat UI.
-   Adding dozens of integrations.
-   Creating a swarm of agents because an agent framework makes it easy.
-   Giving experts unrestricted shell/API access.
-   Treating a vector database as "memory" without temporal/provenance
    semantics.
-   Treating successful tool return values as verified outcomes.
-   Sending broad household/system context to every expert.
-   Making external OpenAI the orchestrator of local systems.
-   Replacing deterministic authorization with prompt instructions.
-   Prematurely optimizing model routing.
-   Rewriting working prototype code without a constitutional reason.

## Repository workflow

Until Phase 2 begins, preserve the current prototype as historical
evidence.

Recommended sequence once the existing `~/lynx` tree is available in
Git:

1.  Import the existing prototype without architectural cleanup.
2.  Commit it as the historical baseline.
3.  Add the Phase 1 documentation package.
4.  Tag the untouched prototype baseline: `prototype-pre-phase2`.
5.  Perform Phase 2 work through focused branches/commits.
6.  Keep constitutional changes explicit and separately reviewable.

Do not pretend the documentation commit is the original prototype state
if it was added afterward; preserve accurate commit history.

## Documentation hierarchy

-   `docs/CONSTITUTION.md` --- authoritative behavioral/governance
    baseline.
-   `LYNX_HANDOFF.md` --- implementation handoff and current Phase 2
    assignment.
-   `docs/ARCHITECTURE.md` --- architectural properties derived from the
    Constitution; evolves during implementation.
-   `docs/DECISIONS.md` --- Architecture Decision Records/index or
    concise decision log.
-   `docs/THREAT_MODEL.md` --- adversarial assumptions and enforcement
    boundaries.
-   `README.md` --- project-facing overview; not the governing
    specification.

## Working principle

**Experts advise. Evidence adjudicates. Lynx conducts. The user
governs.**
