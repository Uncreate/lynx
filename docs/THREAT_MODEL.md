# Lynx Threat Model --- Phase 2 Seed

This is a seed document for Work to refine after repository inspection.

## Threat classes already established

-   Prompt injection in webpages, logs, email, documents, tool output,
    retrieved memory, and expert responses.
-   Rogue or compromised expert operating inside or outside its
    delegated envelope.
-   Confused-deputy privilege laundering.
-   Replay of previously legitimate instructions.
-   Stolen/compromised user credentials.
-   Tool lying about execution or verification.
-   Shared failure domain between executor and verifier.
-   Memory/evidence poisoning.
-   Stale evidence represented as current fact.
-   Privacy leakage through derivation or aggregation.
-   Credential leakage in otherwise approved context.
-   External recipient retention outside Lynx's enforceable control.
-   Autonomous retry/cascade/oscillation.
-   Rollback causing more harm than stabilization.
-   Split-brain or stale delegation after environmental change.
-   Compromise of Lynx cognition itself.
-   Self-optimization weakening verification/governance.
-   Audit tampering by the component being audited.
-   Governance service failure.
-   Resource exhaustion causing unsafe shortcuts.
-   Malicious plugins/capabilities.
-   Recovery after downtime with stale world state.

## Core defense principle

The reasoning model is assumed to be fallible and potentially
manipulable. Critical authority, privacy, capability, replay,
root-of-trust, and audit-integrity boundaries must therefore have
enforcement outside probabilistic cognition.
