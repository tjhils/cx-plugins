# Voice Profile Setup

This file describes the first-run flow that the `writing-check` skill executes when no voice profile is found. The output is a `voice-profile.md` file that subsequent slop checks compare against.

## When to run setup

Setup runs automatically when the skill is invoked and neither of these files exists:

- `${CLAUDE_PROJECT_DIR}/.writing-check/voice-profile.md` (project-local, takes precedence if present)
- `${HOME}/.claude/writing-check/voice-profile.md` (user-global)

If only the user-global profile exists, use it. Project-local always wins over global.

A user can rerun setup any time by deleting their profile file or by saying "redo my voice profile" / "rebuild my writing voice."

## Setup flow

### Step 1: Explain what's needed

Tell the user, before they paste anything:

> Before I can scan a draft against your voice, I need to learn what your voice sounds like. Please give me **three samples of your own writing**, **at least 300 words each**. The more variety the better: a blog post, an email to a colleague, a Slack thread, a strategic memo, a piece of personal writing, anything that you wrote and that sounds like you. Mix formal and informal if both apply.

Then ask:

> Where would you like the voice profile saved? Project-local (in `.writing-check/voice-profile.md` in the current project) or user-global (in `~/.claude/writing-check/voice-profile.md`)? Project-local is useful if you write in different voices for different work. User-global covers all your projects with one profile.

### Step 2: Collect samples

Accept samples in any of these forms:

- Pasted text directly into the conversation.
- File paths the skill can read (`Read` tool).
- A folder of writing samples (point at the folder; collect everything readable).

Validate before continuing:

- **Count:** at least three distinct samples.
- **Length:** each sample at least 300 words. If short, ask the user for more before moving on.
- **Authorship:** ask the user to confirm they wrote each piece. If a sample is co-authored or heavily edited by someone else, flag that and ask whether to include it.

If the samples come up short, do not proceed. Tell the user what's missing and ask for more. Pushing through with insufficient signal produces a generic profile that defeats the purpose.

### Step 3: Analyze the samples

Read all samples and extract patterns across these dimensions. Use the template at `templates/voice-profile-template.md` as the structure.

**Sentence rhythm.**
- What's the typical sentence length range? Where does the writer go shorter or longer?
- Do they use sentence fragments? Where?
- Do they use parenthetical asides? How often?
- Are there one-sentence paragraphs?

**Vocabulary and register.**
- Formal vs. casual register. Where does the writer shift?
- Casual or colloquial words that show up consistently (e.g., "gnarly," "noodling," "y'all," "wicked," etc.)?
- Industry or technical jargon they use confidently? Avoid?
- Profanity: yes, no, sparing?

**Humor.**
- Is humor present? What kind: dry, absurdist, self-deprecating, observational, wordplay?
- Does humor come from concrete details or from setup-punchline structures?
- When does the writer use humor (rapport-building, breaking tension, illustrating a point) and when do they not?

**Analogies and metaphors.**
- What domains does the writer pull comparisons from (cooking, sports, parenting, programming, etc.)?
- Are analogies grounded in lived experience or abstract?
- Frequency: heavy user of analogy, occasional, almost never?

**Honesty and stance.**
- How do they handle uncertainty? Hedge, state directly, qualify with specifics?
- How do they handle disagreement? Direct pushback, soften, sidestep?
- Do they admit limits of their own knowledge?

**Structural patterns.**
- Headers / no headers / sentence-case / title-case?
- Bullet usage: heavy, light, formatted with bold prefixes, plain?
- Bold and italic usage?
- Em dashes: yes, no, sometimes?
- Emoji: yes, no, sometimes?

**What they avoid.**
- Phrases or constructions that never appear in their samples.
- Vocabulary that would feel out of character.
- Tone they don't use (corporate jargon, hype, condescension, etc.).

**What they lean into.**
- Specific moves that recur across samples and clearly characterize the voice (specific details, anticipating reader objections, candor about trade-offs, etc.).

### Step 4: Generate the profile

Fill in the template at `templates/voice-profile-template.md` using the analyzed patterns. Quote actual phrases from the samples wherever possible. The profile is more useful with concrete examples than with abstract descriptions.

If a section has no clear signal from the samples (e.g., humor isn't present in any of them), say so explicitly: "No humor pattern detected in samples; treat as neutral." Do not invent patterns.

### Step 5: Save the profile

Write the completed profile to the location the user chose in Step 1.

- Project-local: ensure `${CLAUDE_PROJECT_DIR}/.writing-check/` exists, then write `voice-profile.md` inside it.
- User-global: ensure `${HOME}/.claude/writing-check/` exists, then write `voice-profile.md` inside it.

After saving, confirm the path back to the user and tell them they can edit it directly any time. They can also delete it to redo setup from scratch.

### Step 6: Proceed with the original request

If the setup was triggered by a slop-check request, run the slop check now using the freshly generated profile. Do not ask the user to rerun.

## Updating an existing profile

If a profile already exists and the user asks to "update" or "refine" their voice profile, do not overwrite from scratch. Instead:

1. Read the existing profile.
2. Ask which sections feel off or out of date.
3. Collect new samples targeting those sections specifically.
4. Update only the affected sections.

This preserves accumulated calibration. Full regeneration should only happen when the user explicitly asks to "redo" or "rebuild" the profile.
