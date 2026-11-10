# Agent Action Security Lab

**Inspect the action before it reaches the world.**

An agent may propose a legitimate action and later change its destination or payload. Action Security Lab asks what the server can actually execute after approval.

Built by **Mohammed Abumtary** · TypeScript · React · Hono · PostgreSQL · policy and approval contracts

![Agent Action Security Lab — working demonstration](media/overview.png)

[Demo guide](docs/DEMO.md) · [Engineering notes](docs/ENGINEERING.md) · [Verification & boundaries](docs/VERIFICATION.md) · [Recorded walkthrough](media/walkthrough.mp4)

## The experience

Choose a scenario → inspect proposal → approve or deny → inspect the receipt.

Controlled proposals, two fictional tenants and sandbox actions. No real messages, refunds or external exports are sent.

## Where the engineering matters

### Bind approval to one exact action

An approval contract includes payload digest, destination, tenant, authorization revision, policy and expiry.

### Revalidate while consuming the approval

Execution checks the current identity and policy inside a transaction, consumes the single-use contract and writes a durable receipt.

### Compare against an observable baseline

A deliberately permissive sandbox runner makes the effect of the protected boundary measurable without contacting real services.

## Verified in the demonstration

- 12 database regressions and five browser checks passed in the current verification pass.
- The recorded synthetic evaluation covers 36 legitimate/adversarial scenarios with protected and baseline outcomes.
- Replay, changed payload, stale permission and cross-tenant cases are part of the documented boundary tests.

## Explore the work

This private repository is a presentation package: screenshots, walkthrough media and engineering notes. Application source, credentials and customer records are not included. The interactive demonstration runs in a separate local review environment; access can be arranged for a walkthrough.

[Read the guided demo](docs/DEMO.md) · [View my portfolio](https://mohammed-ab.github.io/)

## Scope

This is evidence about the tested application boundary. Fixture proposals do not measure how often a live model follows an injection, and the result is not a universal security claim.

Reviewed 10 November 2026. Results describe the recorded build and stated test scope.
