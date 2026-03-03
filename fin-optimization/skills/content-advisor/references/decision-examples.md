# Decision Examples

Worked examples showing how to diagnose Fin problems and choose the right intervention. Use these as reference when coaching users through similar situations.

## Example 1: Custom Answer Misfiring

**Situation:** "Fin keeps giving customers a canned response about withdrawal timing, even when they're asking about something completely different like invoice payments."

**Diagnosis:** This is a Custom Answer problem. A Custom Answer with broad trigger conditions is matching questions it shouldn't. Because Custom Answers fire before AI reasoning, no amount of content or Guidance will help — the Custom Answer intercepts first.

**Fix:** Review the Custom Answer's trigger conditions. Either narrow the triggers to be more specific (only match when the customer explicitly asks about withdrawals) or disable the Custom Answer entirely and let Fin handle it through content + Guidance instead.

**Key lesson:** Always check for Custom Answer misfires first. They're the most common "invisible" cause of bad answers because they bypass everything else in Fin's stack.

---

## Example 2: Wrong Tone, Right Information

**Situation:** "Fin is giving customers accurate information about our API rate limits, but it's using super technical language and the customer-facing team thinks it sounds robotic."

**Diagnosis:** This is a behavior problem, not a knowledge problem. Fin has the right information but is presenting it in the wrong way. The content source (likely a technical doc) is accurate but written for developers, not end users.

**Two options:**

1. **Guidance rule (faster):** Write a Communication Style rule like: "When explaining technical limitations like rate limits, API errors, or system requirements, use plain language that a non-technical user would understand. Avoid jargon like 'HTTP 429' or 'rate limiting' — instead, describe the impact in user terms."

2. **Content update (more durable):** Rewrite the customer-facing article about rate limits to use plain language. This fixes it at the source so Fin naturally uses better language.

**Best approach:** Do both. The Guidance rule handles the general tone issue across all technical topics. The content update fixes this specific article.

---

## Example 3: Guidance vs. Snippet Decision

**Situation:** "We just discovered a bug where exports are failing for customers on the Basic plan. We need Fin to tell affected customers about the workaround while engineering fixes it."

**Diagnosis:** This is a temporary knowledge gap. Fin doesn't know about this bug or the workaround. Since the information is temporary and internal, a Snippet is the right call.

**Fix:** Create a Snippet titled "Why are my exports failing?" with the body explaining the known issue and the workaround. Set a calendar reminder to remove or update the Snippet when engineering ships the fix.

**Why not Guidance?** Guidance changes behavior, not knowledge. You can't teach Fin about a new bug with a Guidance rule — it needs content to draw from.

**Why not an article?** The issue is temporary. Creating a public article for a bug that'll be fixed in a week adds noise to the help center and creates a maintenance burden (you'll need to remember to remove it).

---

## Example 4: When It's Actually a Procedure

**Situation:** "When a customer asks to change their billing address, Fin gives them a link to their account settings. But some customers are on legacy accounts where they can't change it themselves — an agent has to do it. Fin doesn't know which type of account the customer has."

**Diagnosis:** This starts as a knowledge/behavior problem but is actually a process problem. The resolution depends on customer-specific data (legacy vs. current account) that Fin can't determine from a static article. The fix requires: check account type → if legacy, collect new address → hand off to agent with context; if current, direct to self-service.

**Fix:** This needs a Procedure, not content or Guidance. A Guidance rule can't look up account type. A Snippet can't branch based on customer data. Only a Procedure can: check external data → make a decision → take different actions based on the outcome.

**Handoff:** This is where the Fin Procedure Advisor skill takes over — it'll help score whether this Procedure is ready to build, what Data Connectors it needs, and where it fits in the build sequence.

---

## Example 5: Content Audit — Overlapping Sources

**Situation:** "We have three different articles about pricing — a pricing page, a FAQ, and a 'plans comparison' article. Fin sometimes mixes information from all three and gives confusing answers."

**Diagnosis:** This is a content architecture problem. Fin is finding multiple relevant sources and synthesising them, but because the sources overlap (or worse, slightly contradict each other), the synthesis is confused.

**Fix:** Consolidate the overlapping content. Designate ONE article as the authoritative source for plan details and pricing. The other articles should either be removed from Fin's content sources, or rewritten to clearly reference the authoritative article without duplicating the details.

**Optional Guidance addition:** If the content can't be consolidated immediately, add a Content & Sources Guidance rule like: "When answering questions about pricing or plan features, prioritise the 'Plans Comparison' article as the primary source."

**Key lesson:** Sometimes the best intervention isn't adding something new — it's cleaning up what's already there.

---

## Example 6: Escalation Logic Gone Wrong

**Situation:** "We added a Guidance rule that says 'if the customer mentions legal action, immediately escalate to a human.' Now Fin escalates every time someone says 'terms' or 'policy' because it interprets those as legal-adjacent."

**Diagnosis:** The Guidance rule is too broad. Fin is interpreting "legal action" more expansively than intended, catching routine questions about terms of service and privacy policy.

**Fix:** Rewrite the Guidance rule to be more specific: "If the customer explicitly threatens legal action, mentions a lawsuit, or says they want to speak with your legal department, escalate to a human agent. Do NOT escalate for routine questions about terms of service, privacy policy, or account agreements — these are normal support questions."

**Key lesson:** Guidance rules about escalation need careful scoping. Tell Fin what NOT to escalate on, not just what to escalate on. Test with edge cases like "what's your privacy policy?" and "I'm going to sue you" to make sure the rule catches the right things.

---

## Quick Decision Cheat Sheet

| Symptom | Likely Root Cause | Intervention |
|---------|-------------------|-------------|
| Fin gives a canned, irrelevant response | Custom Answer misfiring | Fix or disable the Custom Answer |
| Fin has the right info but sounds wrong | Behavioral issue | Guidance (Communication Style) |
| Fin guesses instead of asking | Missing clarification logic | Guidance (Context & Clarification) |
| Fin cites the wrong article | Source prioritisation | Guidance (Content & Sources) |
| Fin doesn't know something (temporary) | Knowledge gap | Snippet |
| Fin doesn't know something (permanent) | Knowledge gap | Help Center Article or Internal Article |
| Fin needs to check data or branch | Process issue | Procedure |
| Fin escalates too much or too little | Broad/missing escalation rule | Rewrite Guidance or add Procedure step |
| Fin mixes conflicting sources | Content overlap | Consolidate content, optionally add Guidance |
| Fin cites outdated information | Stale content | Update or remove the source |
