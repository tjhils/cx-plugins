# Common Procedure Candidates for B2B SaaS

Use these as reference points when the user is brainstorming or evaluating candidates. Adjust typical scores based on the user's specific context, Procedure Registry, and Data Connector Registry.

## Subscription Lookup and Invoice History

**Typical score: 14-15**

This is the classic confidence builder. Very high frequency, clear process, strong APIs in most billing systems (Stripe, Chargebee, Recurly, etc.). Low complexity with obvious handoff points — billing disputes go to humans. Excellent first Procedure IF the billing API is accessible.

- **Connectors needed:** GET subscription details, GET invoice list
- **Sub-procedures:** Identity verification (reusable)
- **Cost note:** High volume — do the ROI math. If agents handle 100 of these a day at 3 minutes each, the $99/day Outcome cost replaces 5 hours of agent time.
- **Watch out for:** Secondary email addresses, multiple subscriptions per customer, legacy plans not in the billing system

## Lead Qualification

**Typical score: 14-15**

The best first Procedure for teams with limited technical access, because it needs NO Data Connectors — it's purely conversation-driven. Most teams already have qualification criteria documented. It also extends Fin beyond support into commercial value, which gets leadership attention.

- **Connectors needed:** None (optionally a CRM write to log the qualified lead)
- **Sub-procedures:** None typically needed — the whole flow is linear
- **Watch out for:** Teams trying to qualify across too many dimensions at once. Start with the top 3-4 criteria.

## Product Setup and Onboarding Questions

**Typical score: 11**

High impact but process clarity often needs work. Moderate branching (different plans, integrations, error states). The common mistake is scoping this as "onboarding" — start with one specific setup flow.

- **Connectors needed:** Often GET account details to determine plan/configuration
- **Tip:** Start with the single most common onboarding question, not "onboarding" as a category
- **Watch out for:** Different setup paths for different plan tiers, integration-specific flows, and error states that need troubleshooting

## Account or User Management

**Typical score: 12-13**

Common in B2B SaaS — adding/removing users, changing roles, updating account details. Process is usually well-defined but may need API access to the product's admin system. Good second or third Procedure once billing-related ones are live.

- **Connectors needed:** GET account details, possibly POST to update user roles
- **Caution:** POST connectors that modify data need careful checkpoint design — adding a human approval step before Fin changes someone's access level
- **Watch out for:** Permission hierarchies, admin-only actions, audit trail requirements

## Troubleshooting a Known Issue

**Typical score: 10-12**

Works well when scoped to a single, well-documented issue with a clear resolution path. Falls apart completely when scoped too broadly ("troubleshoot any product issue"). The score depends almost entirely on how well the troubleshooting steps are documented.

- **Connectors needed:** Varies — may need product status checks, log lookups
- **Tip:** If you don't have a written troubleshooting doc for this issue, write one first. The Procedure IS the doc.
- **Watch out for:** Teams wanting to build one "master troubleshooting Procedure" — this never works. Build one per issue.

## Password Reset / Access Recovery

**Typical score: 13-14**

Very common, usually well-documented, low branching. The main complexity is identity verification — which is a reusable sub-procedure. Often doesn't need Data Connectors if it's routing to a self-service flow.

- **Connectors needed:** Potentially GET to check account status, but often just conversational
- **Sub-procedures:** Identity verification (reusable across many Procedures)
- **Watch out for:** SSO-managed accounts where the password reset process is different, expired accounts, accounts with MFA complications

## Cancellation Requests End-to-End

**Typical score: 8-9**

HIGH impact but LOW readiness — this is the classic "wrong first Procedure." Teams pick it because it's painful and visible, but it has massive complexity, inconsistent processes, and difficult handoff design. Should be built much later, after the process is standardised.

- **Connectors needed:** Multiple — subscription details, usage data, potentially offer engine
- **Reality check:** Ask the user to list every path a cancellation can take. If the list exceeds 6-8 branches, it's not ready.
- **Common traps:** Retention offers that vary by customer segment, proration logic, contract terms, annual vs. monthly differences, team vs. individual plans

## Refund or Credit Requests

**Typical score: 9-11**

Similar trap to cancellation — sounds simple, usually isn't. Score improves dramatically when scoped to specific, clear-cut scenarios (e.g. "duplicate charge refund" vs. "any refund request").

- **Connectors needed:** GET transaction details, POST to issue refund/credit
- **Caution:** POST connectors that move money need checkpoints for human approval
- **Watch out for:** Different refund policies by product/plan, partial refunds, credits vs. refunds, tax implications, currency differences

## Upgrade or Plan Change Requests

**Typical score: 11-13**

Often overlooked but increasingly common as SaaS pricing gets more complex. Works well when plan options are clearly defined and the billing system has good APIs for plan changes.

- **Connectors needed:** GET current plan details, GET available plans, potentially POST to change plan
- **Sub-procedures:** Identity verification, possibly billing information collection
- **Watch out for:** Proration logic, feature access timing, team plans where one user can't change for everyone, annual commitment restrictions

## Status Check or Order Tracking

**Typical score: 13-14**

Very straightforward when the underlying system has good APIs. Customer wants to know the status of something (order, request, application, etc.) and the answer lives in an external system.

- **Connectors needed:** GET status from the relevant system
- **Sub-procedures:** Identity verification
- **Watch out for:** Multiple status systems that don't agree, statuses that require interpretation or context ("processing" means different things for different request types)
