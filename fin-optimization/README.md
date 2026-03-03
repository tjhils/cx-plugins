# Fin Optimization Plugin

Decision frameworks for optimizing your Intercom Fin AI agent. Two complementary skills that cover the full loop — from diagnosing bad answers to planning your automation roadmap.

## Skills

### content-advisor

A decision framework for choosing the right way to fix or improve Fin's answers. When Fin gets something wrong, there are six levers available (Guidance, Snippets, Help Center Articles, Internal Articles, Custom Answers, Procedures) — this skill helps you pick the right one and use it effectively.

**Use when:** Fin gave a wrong answer, you're deciding between Guidance and a Snippet, you want to audit Fin's content, or you need to figure out which lever to pull.

**Example usage:**

```
Fin keeps telling customers our Standard plan includes priority support, but it doesn't. How do I fix this?
```

The skill will walk you through the content hierarchy, diagnose the root cause (knowledge gap vs. behavior problem), recommend the right intervention type, and help you implement it.

**Bundled references:**

- `intervention-types.md` — Detailed breakdown of each intervention type with writing tips and common mistakes
- `decision-examples.md` — Six worked examples plus a quick decision cheat sheet

### procedure-advisor

An interactive framework for deciding which Fin Procedures to build and in what order. Uses a structured Inventory → Filter → Score → Sequence → Build → Test process.

**Use when:** You're deciding what to automate with Fin, choosing which Procedure to build first, reviewing your existing Procedures, or planning your automation roadmap.

**Example usage:**

```
We want to automate our refund process with Fin. Is that a good idea?
```

The skill will gather context about your setup, build registries of your existing Procedures and Data Connectors, run gap analysis, score candidates across five dimensions, and recommend a build sequence with cost estimates.

**Bundled references:**

- `registry-templates.md` — Procedure Registry and Data Connector Registry templates with cross-referencing patterns
- `candidates.md` — 10 common B2B SaaS Procedure candidates with typical scores and traps to avoid
- `error-handling.md` — Fallback patterns, checkpoint design for POST connectors, and simulation testing guidance

## How the Skills Work Together

The **Content Advisor** is reactive — Fin got something wrong, which lever do I pull? The **Procedure Advisor** is proactive — I know I need Procedures, which ones should I build?

When the Content Advisor's decision framework leads to "this needs a Procedure," it hands off to the Procedure Advisor for the full scoring and sequencing framework. One diagnoses the problem; the other plans the solution.

## Version

1.0.0
