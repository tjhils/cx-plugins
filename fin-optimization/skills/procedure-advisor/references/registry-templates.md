# Registry Templates

Use these templates when helping the user build their Procedure Registry and Data Connector Registry. Adapt the depth of collection to the user's situation — a team with 2 Procedures doesn't need a formal inventory exercise; a team with 15 does.

## Procedure Registry Template

For each existing Procedure, capture:

| Field | Description | Example |
|-------|-------------|---------|
| **Procedure Name** | The name as it appears in Intercom | "Billing Lookup" |
| **Category** | The broad support topic it belongs to | Billing, Onboarding, Account Management, Troubleshooting |
| **Problem It Solves** | One sentence describing the customer problem | "Customer wants to check their current plan, billing date, or recent invoices" |
| **Trigger** | How/when Fin activates this Procedure | Customer asks about billing, invoices, or subscription details |
| **Data Connectors Used** | Which connectors this Procedure calls (cross-reference the Data Connector Registry) | "Get Subscription Details", "Get Invoice List" |
| **Sub-Procedures Used** | Any shared sub-procedures it calls | "VerifyCustomerIdentity" |
| **Channels** | Which channels it's active on | Chat, Email, WhatsApp |
| **Handoff Points** | When/why it routes to a human | Billing disputes, refund requests over $100 |
| **Estimated Volume** | Roughly how often it fires per day/week | ~80/day |
| **Status** | Live, in testing, draft, or deprecated | Live |
| **Known Issues** | Any problems the team has noticed | "Sometimes fails to find subscription when customer uses a secondary email" |
| **Last Updated** | When the Procedure was last revised | 2026-01-15 |

### Tips for Collecting the Procedure Registry

- If the user has Procedures but doesn't know the details, encourage them to open each one in Intercom and walk through it together. Even a rough inventory is better than none.
- Focus on the fields they can answer quickly first (name, category, problem it solves, status) and note the gaps for later.
- If starting from scratch with no Procedures, skip the registry — the prioritised candidate list from the scoring phase becomes the seed of their registry.

## Data Connector Registry Template

For each existing Data Connector, capture:

| Field | Description | Example |
|-------|-------------|---------|
| **Connector Name** | The name as it appears in Intercom | "Get Subscription Details" |
| **System** | The external system it connects to | Stripe, Salesforce, internal API |
| **Method** | GET (read) or POST (action) | GET |
| **Inputs** | What data it needs to make the call | customer_email, subscription_id |
| **Outputs** | What data it returns | plan_name, status, next_billing_date, amount |
| **Input Source** | Where the inputs come from | Intercom user attributes, conversation, previous connector |
| **Error Behaviour** | What happens when it fails (if known) | Returns 404 if customer not found; times out after 10s |
| **Status** | Live, in development, or planned | Live |
| **Used In** | Which Procedures currently use it (cross-reference the Procedure Registry) | "Billing Lookup", "Cancellation Flow" |

### Tips for Collecting the Data Connector Registry

- Teams consistently underestimate what they already have. A connector built for one Procedure often unlocks two or three others.
- If the team has no connectors yet, ask what external systems they use daily (billing, CRM, product database, internal tools) and whether those systems have APIs. Build a "planned connectors" list that feeds into scoring.
- Connector names should be action-oriented and specific: "Get Subscription Details" not "Stripe Connector."

## Cross-Reference Patterns

Once both registries are populated, look for these patterns:

### Connector Reuse Opportunities

- **Same system, different endpoint:** A team with a "Get Subscription" connector to Stripe likely has the auth and infrastructure to quickly add "Get Invoices" or "Create Refund."
- **Same input, different context:** If one connector already takes customer_email as input, any new Procedure that starts with identifying the customer can chain from there.
- **Shared outputs as inputs:** If connector A returns subscription_id, and a planned connector B needs subscription_id as input, they chain naturally.

### Dependency Mapping

- Which Procedures depend on a single connector? (Single point of failure risk)
- Which connectors are used by multiple Procedures? (High-value infrastructure — invest in reliability)
- Which Procedures have no connectors? (Conversation-only — lowest risk, most portable)

### Orphan Detection

- Connectors not used by any Procedure → potential waste, or a signal that a Procedure was removed but the connector wasn't
- Procedures that reference connectors not in the registry → documentation gap

## Registry Maintenance Schedule

- **After launching a new Procedure** → add it to the Procedure Registry with all fields
- **After building a new Data Connector** → add it to the Data Connector Registry; update the "Used In" field
- **After updating a Procedure** → update "Last Updated" and any changed fields
- **After deprecating a Procedure** → mark as deprecated, don't delete (history is useful)
- **After a known issue is reported** → add to "Known Issues" immediately
- **Quarterly** → review both registries end-to-end, rerun gap analysis, re-score candidates that were previously "not ready"

## Registry Health Check Questions

Ask these periodically:

1. Do any Procedures have a "Last Updated" date older than 6 months? → Schedule reviews
2. Are there connectors with no Procedures using them? → Clean up or repurpose
3. Are there Procedures with "Known Issues" that haven't been addressed? → Prioritise fixes
4. Has the team's top 5 support topics changed since the last gap analysis? → Rerun the coverage map
