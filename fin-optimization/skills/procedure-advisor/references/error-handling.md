# Error Handling and Fallback Design

Every Procedure that uses a Data Connector MUST have explicit fallback instructions. Fin Procedures do NOT automatically handle data connector failures — if a connector times out or returns an error, Fin won't retry or recover on its own. Without explicit fallback instructions, Fin may stop unexpectedly or generate responses that aren't grounded in the Procedure's configuration.

The customer should never see a Procedure "break." Every failure path should end in either a graceful message or a clean handoff to a human.

## Fallback Patterns by Failure Type

| Failure Scenario | What Happens | Recommended Fallback |
|-----------------|--------------|---------------------|
| **Connector timeout or 500 error** | The external system didn't respond in time or returned a server error | Apologise, offer to connect to a human, include the error context in the handoff note so the agent doesn't start from scratch |
| **Customer not found (404)** | The identifying information didn't match any record in the external system | Confirm the identifying information with the customer, try the lookup once more with corrected info, then hand off if it still fails |
| **Unexpected data format** | The API returned data in a format the connector doesn't expect | Don't surface raw errors to the customer — hand off with context noting what was attempted and what went wrong |
| **Partial data returned** | The API returned some fields but not all expected ones | Use what you have, clearly note what's missing, either ask the customer to fill the gap or hand off |
| **Authentication failure (401/403)** | The connector's API credentials are invalid or expired | This is an infrastructure problem, not a customer problem. Apologise, hand off, and flag internally |
| **Rate limiting (429)** | Too many requests to the external API | Apologise for the delay, suggest the customer wait a moment, or hand off |

## Writing Fallback Instructions

When writing fallbacks into Procedure instructions, use this pattern:

**Do:** "If the billing lookup returns an error or no results, say: 'I wasn't able to pull up your billing details right now. Let me connect you with a team member who can help.' Then hand off to a human with a note that includes the customer's email and what was attempted."

**Don't:** "If there's an error, handle it gracefully." (Too vague — Fin won't know what "gracefully" means in context.)

Be specific about:
1. What to say to the customer
2. Whether to retry or hand off immediately
3. What information to include in the handoff note

## Checkpoint Design for POST Connectors

POST connectors (ones that take actions like issuing refunds, changing plans, or modifying accounts) need special attention because their failures can be more consequential:

- **Always add a confirmation step** before executing a POST action: "I'm going to issue a refund of $49.99 to your card ending in 4242. Can you confirm this is correct?"
- **Consider human approval checkpoints** for high-value or irreversible actions — Fin pauses and waits for an agent to approve before proceeding
- **Handle partial success** — what if the refund API says it succeeded but the confirmation email fails? Define what Fin should tell the customer.

## Testing Fallbacks with Simulations

When running Simulations, specifically test these scenarios:
1. The happy path works
2. The connector returns an error — does Fin follow the fallback?
3. The customer provides wrong information — does Fin re-ask appropriately?
4. Multiple connectors in sequence — what happens if the second one fails but the first succeeded?
