# Agent Action Security Lab: engineering notes

An agent may propose a legitimate action and later change its destination or payload. Action Security Lab asks what the server can actually execute after approval.

## System path

~~~mermaid
flowchart LR
  UntrustedContent --> AgentProposal
  AgentProposal --> PolicyCheck
  PolicyCheck --> ExactApproval
  ExactApproval --> TransactionalRecheck
  TransactionalRecheck --> SandboxAction
  SandboxAction --> Receipt
~~~

This diagram describes the demonstrated system boundary, not a production deployment topology.

## Decisions and tradeoffs

### Bind approval to one exact action

An approval contract includes payload digest, destination, tenant, authorization revision, policy and expiry.

### Revalidate while consuming the approval

Execution checks the current identity and policy inside a transaction, consumes the single-use contract and writes a durable receipt.

### Compare against an observable baseline

A deliberately permissive sandbox runner makes the effect of the protected boundary measurable without contacting real services.

## Review questions

- What evidence demonstrates **bind approval to one exact action**, and what would fail without it?
- What evidence demonstrates **revalidate while consuming the approval**, and what would fail without it?
- What evidence demonstrates **compare against an observable baseline**, and what would fail without it?

## Verification boundary

12 database regressions and five browser checks passed in the current verification pass. The recorded synthetic evaluation covers 36 legitimate/adversarial scenarios with protected and baseline outcomes. Replay, changed payload, stale permission and cross-tenant cases are part of the documented boundary tests.

This is evidence about the tested application boundary. Fixture proposals do not measure how often a live model follows an injection, and the result is not a universal security claim.
