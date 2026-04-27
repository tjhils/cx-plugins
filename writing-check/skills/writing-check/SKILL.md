---
name: writing-check
description: >
  Scan writing for AI-generated patterns and drift from the user's own voice.
  Use when the user says "writing check", "slop check", "check for AI writing",
  "de-slop this", "does this sound like AI", "review for AI tells",
  "scan my draft", "clean up AI writing", or asks to review a draft for
  robotic or formulaic language.
version: 0.1.0
---

# Writing Check

Scan a draft for AI writing tells, the statistical patterns that automated AI detection tools (GPTZero, WalterAI, Originality.ai) flag, and drift from the user's voice. This is a final-pass editorial tool, not a rewrite engine. Flag problems, let the user decide what to fix.

The skill runs entirely off bundled reference files. No network calls.

## Process

### 1. Check for a voice profile

Before scanning anything, look for the user's voice profile in this order:

1. `${CLAUDE_PROJECT_DIR}/.writing-check/voice-profile.md` (project-local, takes precedence)
2. `${HOME}/.claude/writing-check/voice-profile.md` (user-global)

If neither exists, run the first-run setup flow before doing anything else. Do not skip this. The voice profile is what makes this check more than a generic spell-checker.

**First-run setup:**

Read `${CLAUDE_PLUGIN_ROOT}/skills/writing-check/references/voice-profile-setup.md` and follow it end to end. The setup will:

- Explain what's needed (3+ writing samples, 300+ words each).
- Ask where to save the profile (project-local or user-global).
- Collect and validate the samples.
- Analyze the samples for sentence rhythm, vocabulary, humor, analogies, structural patterns, and what the writer avoids.
- Generate a `voice-profile.md` using the template at `${CLAUDE_PLUGIN_ROOT}/skills/writing-check/templates/voice-profile-template.md`.
- Save the profile to the chosen location.

After setup completes, continue with the slop check using the freshly generated profile.

If the user explicitly asks to "redo" or "rebuild" their voice profile, run setup from scratch even if a profile already exists. If they ask to "update" or "refine" it, follow the targeted-update flow described in the setup reference.

### 2. Load the checklist and the voice profile

Read `${CLAUDE_PLUGIN_ROOT}/skills/writing-check/references/ai-slop-checklist.md` for the checklist of AI writing patterns.

Read the user's voice profile (project-local or user-global, per Step 1) for voice calibration.

Both are required. The checklist catches AI tells. The profile catches drift from how the user actually writes.

### 3. Scan the draft

Run these checks against the draft text. The checklist has full details and examples for each category.

**Vocabulary and phrasing:**
- Vocabulary clusters (3+ AI vocabulary words in a section)
- Inflated significance phrases
- Promotional / travel-brochure language
- Unearned profundity ("Something shifted.", "But here's the thing.")
- Vapid openers and closers ("In today's fast-paced world...", "The possibilities are endless...")

**Sentence and paragraph patterns:**
- Superficial -ing phrases that restate what the sentence already said
- Sentence monotony: uniform sentence and paragraph lengths (low burstiness)
- Self-answered rhetorical questions used as a repeating structural formula
- Over-hedging: excessive qualifiers as a reflex rather than genuine uncertainty

**Structural tells:**
- Formulaic transitions ("moreover", "furthermore", "it's important to note")
- Meta-commentary and signposting ("Now that we've explored X, let's turn to Y", "Let's dive in")
- Negative parallelism overuse ("not just X, it's Y" appearing repeatedly)
- Rule of three (every list has exactly three items)
- Copula avoidance ("serves as" instead of "is")
- Elegant variation (cycling through synonyms for the same thing)
- Cohesion without coherence: reads smoothly but doesn't build an argument or go anywhere
- Challenges-and-future formula ("Despite... Despite...")
- Templated conclusions that mirror the intro or zoom to vague significance
- Repetitive subheadings ("Understanding X", "The Importance of Y", "The Role of Z")

**Formatting tells:**
- Excessive boldface
- Title Case In Every Heading (compare against the user's profile for case preference)
- The "**Term:** Description" bullet pattern everywhere
- Emoji decoration
- Unicode formatting artifacts or markdown leaking into plain text

**Hard evidence:**
- Em dashes (check the voice profile for the user's stance)
- Chatbot leakage: "I hope this helps!", unfilled placeholders, ChatGPT reference codes, utm_source=chatgpt.com in links
- Generic analogies that could apply to anything vs. the writer's lived-experience comparisons (per profile)

**Vague authority.** Flag attributions to unnamed experts or studies. Real cites or no cite at all.

**Voice alignment.** Compare the draft against the loaded voice profile:
- Does it sound like the writer's voice as documented in the profile?
- Are there specific details where generic ones could go (per the profile's "leans into" list)?
- Does the draft use any moves the profile lists under "what this writer avoids"?
- Are there structural or formatting patterns that conflict with the profile?
- Run the "quick check for staying in voice" questions from the profile.

### 4. Detection-tool scan

Run a second pass focused on the statistical patterns that automated detectors measure. The checklist has full details in the "Detection-Tool Patterns" section. This is separate from the surface-level scan because a draft can read well to a human editor and still get flagged.

**Perplexity check.** Scan each paragraph for word-choice predictability. Flag passages where every word is the most statistically probable next word. Look for: generic collocations ("plays a crucial role"), absence of specific nouns (tool names, brand names, people's names), and stretches where the casual or colloquial vocabulary documented in the user's voice profile is conspicuously absent.

**Burstiness check.** Measure sentence-length variation across the full piece. Flag sections where sentences cluster in the 15 to 25 word range with no short punches (under 6 words) or long winding sentences. Check paragraph-length variation too. Flag uniform 3 to 4 sentence paragraphs throughout. Compare against the rhythm patterns documented in the user's profile.

**Texture check.** Flag sections where the writing stays in a single mode (explanation, analysis, or instruction) for too long without shifting. Look for the absence of: anecdotes, parenthetical asides, humor, self-correction, or register shifts. A piece that maintains one consistent tone throughout will flag as AI even if the individual sentences are good.

**Semantic predictability check.** Evaluate whether the overall structure follows the most obvious path for the topic. Flag pieces that follow the definition-importance-challenges-future template. Flag sections where the main point of each paragraph could be predicted from its heading alone.

For each detection-tool finding, explain what pattern would trigger the flag and suggest a specific fix. Fixes should increase perplexity (more specific word choices), burstiness (more rhythmic variation), and texture variation (mode shifts, personality, anecdotes).

### 5. Report findings

Present findings organized by severity:

**Rewrite needed.** Patterns that clearly read as AI output. Vocabulary clusters, formulaic structure, promotional language stacked together, chatbot leakage, cohesion-without-coherence problems.

**Detection-tool risks.** Patterns that would likely trigger automated AI detectors even if they read fine to a human. Low perplexity stretches, flat burstiness, uniform texture, predictable structure. For each, explain what the detector would see and provide a concrete rewrite that addresses the statistical pattern.

**Worth a second look.** Individual hits that might be intentional but are worth the author checking. A single AI vocabulary word, one "not X, it's Y" construction, a generic analogy, etc.

**Voice notes.** Places where the draft drifts from the user's documented voice profile even if no specific AI tell is present. Too formal, too vague, missing stakes the profile says the user usually includes, missing humor opportunities the profile suggests would fit, sentence rhythm out of band from the profile's documented range.

For each finding, quote the specific text from the draft, explain what triggered the flag, and suggest a concrete alternative where possible. Keep suggestions consistent with the user's voice profile.

End with an overall detection assessment: given the patterns found, estimate whether this draft is likely to pass or fail automated detection tools. Be direct about the risk level.

### 6. Iterate

After presenting the report, ask the user if they want to:
- Fix specific items (offer to rewrite flagged passages in their voice).
- Run the check again after edits.
- Accept the draft as-is.
- Update the voice profile if the report surfaces patterns the user thinks are wrong (the profile may have miscalibrated on some dimension).

Do not auto-rewrite. Show the findings, let the user drive.
