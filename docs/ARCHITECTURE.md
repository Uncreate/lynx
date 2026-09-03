# Lynx Architecture --- Phase 2 Starting Constraints

This document is intentionally a starting constraint set, not a finished
architecture.

## Required separations

1.  **Cognition vs. governance** --- an LLM may request an action;
    deterministic policy decides whether it is allowed.
2.  **Capability vs. authority** --- possessing a
    tool/credential/network path is not permission to use it.
3.  **World model vs. audit ledger** --- current knowledge may be
    consolidated; material history must remain reconstructable.
4.  **Observation vs. inference** --- derived beliefs retain evidence
    provenance.
5.  **Expert execution vs. verification** --- success claims should be
    verified through an independent path when practical.
6.  **Identity vs. authorization** --- authentication establishes a
    principal; policy establishes allowed actions.
7.  **User authority vs. intermediary transport** --- intermediaries can
    carry authenticated intent without inheriting sovereignty.

## Engineering requirements derived from red-team review

-   Replay-resistant authorization semantics.
-   Delegation envelopes with temporal validity.
-   Cumulative-action/cascade limits.
-   Loop/oscillation detection for autonomous recovery.
-   Event time and observation/ingestion time as distinct concepts.
-   Source/evidence freshness appropriate to the fact being represented.
-   Dependency/provenance graph sufficient to reevaluate beliefs after
    corrections.
-   Privacy classification that follows derived information and
    aggregate disclosures.
-   Secret/credential handling through capability boundaries;
    deterministic secret scanning where appropriate.
-   Expert reputation based on verified outcomes and contextualized by
    domain/task difficulty.
-   Audit records sufficient to reconstruct consequential decisions
    without requiring unnecessary duplication of sensitive payloads.
-   Governance failure defaults toward narrower authority.
-   Stronger authentication for exceptional sovereignty-level or highly
    anomalous destructive operations.

## Open architecture work

The implementation team should propose concrete mechanisms after
inspecting the prototype. Database choice, message bus, policy engine,
cryptographic scheme, event schema, model framework, and service
decomposition are not constitutionally predetermined.
