# Intervention Types — Detailed Reference

Use this reference when helping the user understand each intervention type in depth. The main SKILL.md has the quick summary; this file has the detail needed to actually write and implement each type.

## Guidance

Natural language rules that shape Fin's behavior during AI reasoning. Think of these as coaching instructions for a new agent — they change how Fin acts, not what it knows.

### Four Categories

- **Communication Style** — Tone, terminology, brand voice. Use when Fin has the right information but presents it wrong.
- **Context & Clarification** — When and how Fin should ask follow-up questions before answering. Use when Fin is guessing instead of asking.
- **Content & Sources** — Which knowledge sources Fin should prioritise for specific topics. Use when correct content exists but Fin picks the wrong source.
- **Other/Policy** — Company rules, escalation triggers, special handling. Use for business logic that doesn't fit the other categories.

### Writing Effective Guidance

- **Write as if talking directly to Fin:** "Always ask for the invoice number" not "Fin should ask for the invoice number."
- **Keep rules single-turn.** If the fix requires a multi-step workflow, you need a Procedure, not Guidance.
- **Tell Fin what to convey, not how to word it.** Give the information and let Fin handle phrasing. Say "Explain that Standard Payouts take 1-2 business days domestically" not "Say: Your Standard Payout will arrive in 1-2 business days."
- **Use conditional language:** "if," "when," "then" to define when the rule applies.
- **Be cautious with blanket escalation rules.** If they trigger too broadly, they'll tank resolution rate. Make escalation rules situational and specific.
- **Avoid super-narrow rules tied to one exact phrase.** Think about the category of behavior, not just the specific instance. Customers express the same idea many different ways.
- **Test before shipping.** Use Intercom's built-in Preview panel with real customer questions before enabling.

### Common Guidance Mistakes

- Writing Guidance when the real problem is missing content (Guidance can't add knowledge)
- Making escalation rules too broad ("if the customer seems frustrated, escalate" → tanks resolution rate)
- Writing rules that conflict with each other ("always be concise" + "always provide detailed explanations")
- Being too vague ("handle this gracefully" — Fin won't know what that means)

---

## Snippets

Short-form, private knowledge that only Fin can see. Customers see "AI answers are generated based on public and private sources" instead of a direct source link.

### Best For

- Temporary information (known bugs, outages, workarounds) that will be removed soon
- Small facts that don't justify a full article
- Internal-only information that shouldn't be customer-facing but Fin needs to know
- Quick fixes when speed matters — Fin picks up Snippets almost instantly

### Not For

Information that should be publicly discoverable by customers. Intercom recommends public articles over Snippets when possible because articles are more scalable and maintainable, and Fin weights them equally.

### Writing Effective Snippets

- **Title should be the question a customer would ask.** "How do I reset my password?" not "Password Reset Process."
- **Body should be the answer Fin should give.** Write it in clear Q&A format.
- **Keep it focused.** One Snippet per topic. If you're writing more than a few paragraphs, it should probably be an article.
- **Include a review date.** Snippets created as temporary fixes tend to become permanent. Set a reminder to review or promote to an article.

---

## Help Center Articles (Public)

Customer-facing knowledge base articles. Both customers and Fin can access them. Fin uses these as a primary knowledge source and can link customers directly to them.

### Best For

- Information customers should be able to find on their own (self-serve)
- Permanent, stable knowledge that won't change frequently
- Content that benefits from structure (sections, steps, screenshots)
- Scalable documentation — one article serves both Fin and direct customer access

### Not For

Internal policies, temporary workarounds, or information you don't want customers to see directly.

### Key Advantage Over Snippets

Scalability and maintenance. Articles live in a structured help center, are searchable by customers, and are easier to keep up to date over time. Intercom recommends using articles over Snippets whenever the information is appropriate for customer self-service.

---

## Internal Articles

Structured knowledge content that Fin can reference but won't link to customers. A middle ground between Snippets and public articles.

### Best For

- Detailed troubleshooting steps that are too complex for a Snippet but shouldn't be public
- Internal policies and procedures Fin needs to know about
- Technical reference material (error code lookups, system architecture details)
- Detailed process documentation for Fin to follow without exposing it to customers

### When to Use Instead of Snippets

If the content is more than a paragraph or two, has internal structure (sections, lists of steps), or is likely to be maintained long-term, use an Internal Article. Snippets are better for quick, small facts.

---

## Custom Answers

Guaranteed exact responses that trigger before Fin's AI reasoning. When a Custom Answer matches a customer's question, Fin uses it verbatim — no AI synthesis, no other content considered.

### Best For

- High-stakes questions where variation is unacceptable (legal, compliance, safety)
- Well-defined, specific questions with one correct answer
- Situations where you need 100% control over the exact response

### Risks

- **Broad triggers cause misfires** — the Custom Answer matches questions it shouldn't and gives irrelevant responses. This is the hardest problem to avoid.
- **Rigid and high-maintenance** — any change to the answer requires manually updating the Custom Answer.
- **Bypasses Fin's intelligence** — Fin can't adapt, clarify, or combine information when a Custom Answer fires.

### When NOT to Use

Most problems are better solved with content + Guidance, which lets Fin's AI reasoning work while still shaping the output. Only reach for Custom Answers when you genuinely need a guaranteed identical response every time.

### Common Custom Answer Mistakes

- Making triggers too broad (matching questions the answer isn't relevant to)
- Using Custom Answers as a shortcut instead of creating proper content
- Forgetting to maintain them when the underlying information changes
- Creating too many Custom Answers, which reduces Fin's ability to use its AI reasoning

---

## Procedures

Multi-step workflows defined in a document-style editor. Procedures let Fin collect information, make conditional decisions, and take different actions based on outcomes. Can include code and Data Connectors.

### Best For

- Processes that require information collection → decision → action sequences
- Workflows with conditional branching ("if X, do A; if Y, do B")
- Tasks that need external data lookups or system integrations
- Complex issues where Guidance alone can't capture the logic

### Not For

Simple behavioral adjustments (use Guidance) or knowledge gaps (use content).

### The Handoff to Procedure Advisor

If the decision framework leads to "this needs a Procedure," the Fin Procedure Advisor skill provides the full framework for deciding which Procedures to build, scoring them, sequencing the build order, and writing effective Procedure instructions. The Content Advisor identifies that a Procedure is needed; the Procedure Advisor helps you build the right one.
