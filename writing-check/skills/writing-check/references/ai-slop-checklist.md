# AI Writing Tells: Self-Review Checklist

Adapted from [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), which catalogs patterns statistically overrepresented in LLM output. Use this as a final pass to catch robotic phrasing that slipped through.

This checklist is **descriptive, not prescriptive**. A few of these patterns appear naturally in good human writing. The signal is density: one "pivotal" is fine; five AI vocabulary words in two paragraphs is a rewrite.

When the checklist references "the user's voice," compare against the voice profile generated during first-run setup (`.writing-check/voice-profile.md` project-local, or `~/.claude/writing-check/voice-profile.md` user-global). If neither exists, treat the voice notes as advisory and flag voice questions for the user.

---

## Vocabulary and Phrasing

### Overused AI vocabulary

Words that spiked in frequency after 2023, corroborated by peer-reviewed studies. Scan for clusters of these:

> additionally, align with, comprehensive, crucial, delve, emphasizing, endeavour, enduring, enhance, fostering, garner, highlight (verb), interplay, intricate/intricacies, key (adjective), landscape (abstract), leverage, multifaceted, nuanced, pivotal, realm, showcase, tapestry (abstract), testament, underscore (verb), unpack, valuable, vibrant, vital

One or two in a full post is fine. A cluster of three or more in a section means the LLM was on autopilot.

### Inflated significance

LLMs inflate importance with a small repertoire of phrases. Scan for:

- "stands as a testament"
- "plays a vital/significant/crucial/pivotal role"
- "underscores its importance"
- "watershed moment" / "key turning point"
- "indelible mark"
- "setting the stage for"
- "evolving landscape"
- "deeply rooted"
- "enduring/lasting legacy"

**The fix:** Say what actually happened. Specific facts beat vague significance.

### Promotional language

Words that read like a travel brochure or sales deck:

> breathtaking, stunning, nestled, in the heart of, boasts a, vibrant, rich (figurative), profound, groundbreaking (figurative), renowned, showcasing, exemplifies, commitment to, natural beauty, rich cultural tapestry/heritage

If the user's voice is enthusiastic, it should still be specific. "The terminal felt like home" beats "a vibrant and rich developer experience."

### Unearned profundity

Phrases that sound meaningful but carry no actual insight:

- "Something shifted."
- "Everything changed."
- "But here's the thing."
- "And that changes everything."
- "This is bigger than most people realize."

**The tell:** These phrases attempt dramatic weight without earning it through specifics. They substitute tone for substance.

### Vapid openers and closers

Opening lines that could start any article on any topic:

- "In today's fast-paced world..."
- "In today's rapidly evolving landscape..."
- "As technology continues to evolve..."
- "Unlock your full potential..."

Closing lines that zoom out to vague significance nobody asked for:

- "Only time will tell..."
- "As we look to the future..."
- "The possibilities are endless..."

**The fix:** Start with the specific thing the piece is actually about. End when the point has been made.

---

## Sentence and Paragraph Patterns

### Superficial -ing phrases

LLMs tack present participle phrases onto sentences as fake depth:

- "...ensuring a seamless experience"
- "...highlighting its importance"
- "...emphasizing the need for"
- "...reflecting broader trends"
- "...contributing to the ecosystem"
- "...fostering a sense of community"

**The fix:** If the -ing clause adds no information the reader didn't already have, cut it.

### Sentence monotony (low burstiness)

Human writing naturally varies sentence length. A short punch. Then a longer sentence that carries more nuance and lets the idea breathe. AI tends to produce sentences of similar length (15 to 25 words) paragraph after paragraph.

**How to check:** Eyeball a paragraph. If every sentence is roughly the same length, that's a flag. Same goes for paragraph length: if every paragraph is three to four sentences with no variation, the rhythm is mechanical.

### Self-answered rhetorical questions

AI uses questions as structural hooks and immediately answers them in the next sentence:

- "What does this mean for developers? It means..."
- "So why does this matter? Because..."
- "But is that really the case? As it turns out..."

A question now and then is fine. The tell is the pattern repeating multiple times in a piece.

### Over-hedging

AI defaults to softening language with excessive qualifiers:

- "It might be worth considering..."
- "One could argue..."
- "It's perhaps important to note..."
- "This could potentially..."

Hedging is appropriate when the writer is genuinely uncertain. As a reflex to avoid taking a position, it reads as AI.

---

## Structural Tells

### Formulaic transitions

These transitions read like a five-paragraph essay:

> moreover, furthermore, in addition, on the other hand, in contrast, it's important to note, it is worth mentioning, no discussion would be complete without

Most human writers use casual transitions or no transition at all. Compare against the user's voice profile for their typical transition style.

### Meta-commentary and signposting

AI narrates its own structure instead of just making the next point:

- "Now that we've explored X, let's turn to Y."
- "As mentioned earlier..."
- "Let's dive in."
- "With that context in mind..."
- "In summary..."
- "In this section, we'll cover..."

A piece that announces what it's about to say repeatedly is signposting too hard.

### Negative parallelism overuse

The "not X, it's Y" construction:

- "It's not just about X, it's about Y"
- "Not only... but also..."
- "It isn't X, it's Y"

**Nuance:** This pattern can be used deliberately and sparingly. The tell is when every other paragraph uses it, or when it creates false profundity from obvious contrasts.

### Rule of three

LLMs default to grouping things in threes:

- "convenient, efficient, and innovative"
- "keynote sessions, panel discussions, and networking opportunities"

When every list has exactly three items, it's suspicious. Vary the count. Two items is fine. Four is fine. One is fine.

### Copula avoidance

LLMs replace "is" with fancier verbs:

- "serves as" instead of "is"
- "stands as" instead of "is"
- "represents" instead of "is"
- "marks" instead of "is"
- "boasts" instead of "has"
- "features" instead of "has"

Sometimes the fancy verb is right. Usually "is" is better.

### Elegant variation

LLMs use increasingly elaborate synonyms to avoid repeating a word:

> the tool → the solution → the platform → the offering → the ecosystem

If the piece is about a specific tool, name it again. Readers don't mind repetition of concrete nouns. They notice when a writer cycles through thesaurus entries.

### Cohesion without coherence

AI output can read smoothly paragraph by paragraph but not actually build an argument. The pieces connect syntactically but don't go anywhere logically.

**How to check:** After reading the full piece, can a reader state what argument it made or what they should do differently? If the answer is vague ("it's about the importance of X"), the piece has cohesion without coherence. It sounds organized but says nothing.

### Challenges-and-future formula

The rigid "Despite its success, X faces challenges... Despite these challenges, X continues to thrive" sandwich. If "despite" appears twice in a paragraph, restructure.

### Templated conclusions

AI conclusions mirror the introduction too closely or zoom out to "bigger picture" significance. If the conclusion could be swapped with the intro with minor edits, it's templated.

### Repetitive subheadings

Section headers following a pattern like:

- "Understanding X"
- "The Importance of Y"
- "The Role of Z"
- "Key Considerations for W"

Vary the structure. Not every heading needs to be a noun phrase starting with "The."

---

## Formatting Tells

- **Excessive boldface:** bolding every key term mechanically, "key takeaways" style.
- **Title Case In Every Heading:** check the user's voice profile for case preference.
- **Bullet + bold header + colon:** the "**Term:** Description of term" pattern in every list.
- **Emoji decoration:** emoji before every section heading or bullet point.
- **Random Unicode formatting:** use of special Unicode bold/italic characters, arrows (→), multiplication signs (×) in running prose.
- **Markdown artifacts:** asterisks for bold/italic leaking into plain text or published content.

---

## Em Dash Overuse

LLMs use em dashes (—) at two to three times the rate of human writers. They substitute them for commas, parentheses, and colons in a formulaic, "punched up" style.

Em dashes are not inherently AI-generated. Many human writers use them well. But density matters: a paragraph with three em dashes is suspicious regardless of who wrote it. Check the user's voice profile for their stance on em dashes.

---

## Vague Authority

LLMs attribute claims to phantom experts:

- "Industry reports suggest..."
- "Observers have cited..."
- "Experts argue..."
- "Some critics contend..."
- "Several publications have noted..."

**The fix:** Name the person or drop the attribution. Cite real people, real projects, real numbers.

---

## Chatbot Leakage

Phrases that leak from the conversational AI context into published drafts:

- "I hope this helps!"
- "Let me know if you need anything else."
- "As of my last training update..."
- "Great question!"
- Unfilled placeholders: "[Subject's Name]", "[URL of source]", "[Your Company]"
- ChatGPT reference codes: "citeturn0search0", "contentReference[oaicite:0]"
- Tracking parameters in links: "utm_source=chatgpt.com"

These are hard evidence of AI generation. Any occurrence is a flag.

---

## Generic Analogies

AI generates metaphors that are plausible but not specific. They gesture at meaning without landing because they lack cultural specificity or personal connection.

**Example of AI analogy:** "Think of it like building a house: you need a solid foundation before you add the walls."

**The tell:** generic analogies that could apply to anything, with no detail rooted in the writer's actual experience.

**The fix:** swap the generic analogy for one drawn from the writer's lived experience. Compare against the user's voice profile for their typical analogy style and source domains.

---

## Detection-Tool Patterns

The categories above catch surface tells visible to a human editor. This section covers the deeper statistical patterns that automated detectors (GPTZero, WalterAI, Originality.ai) actually measure. A draft can pass every check above and still get flagged by these tools.

### Perplexity (word predictability)

Detectors run a language model over the text and measure how "surprised" it is by each word choice. Low perplexity means the text picked the most statistically probable next word at every step, which is exactly what LLMs do. GPTZero considers text with perplexity above 85 as more likely human.

**What triggers low perplexity:**

- Choosing the default word when a more specific one exists. "The tool provides a comprehensive solution" is maximally predictable. "The tool fills the gap between X and Y" is less so.
- Relying on common collocations. "Plays a crucial role," "paves the way for," "sheds light on" are phrases where every word is the most probable completion of the previous one.
- Avoiding unusual or domain-specific vocabulary. Casual or colloquial words, brand names, tool names, and people's names register as high-perplexity (human) because they're not the statistically safest choice.

**How to check:** Read a paragraph and ask: could an autocomplete engine have written this sequence of words? If every word feels like the "obvious" next word, the perplexity is too low.

**The fix:** Swap generic phrases for specific ones. Use concrete nouns (tool names, place names, people's names). Let casual or colloquial vocabulary in where it fits the user's voice profile. The goal isn't randomness; it's specificity. A single brand name or lived-experience detail in a paragraph can shift its perplexity score.

### Burstiness (variation across the document)

Burstiness measures how much the perplexity varies from sentence to sentence across the whole piece. Human writing naturally oscillates: a simple declarative sentence, then a long compound one with a parenthetical aside, then a two-word fragment. AI tends to write at a consistent "medium" complexity throughout.

**What triggers low burstiness:**

- Every sentence is 15 to 25 words long.
- Every paragraph is three to four sentences long.
- The emotional register stays flat: no moments of humor, frustration, or candor punctuating the even tone.
- Sentence structure follows the same pattern: subject-verb-object, subject-verb-object, subject-verb-object.

**How to check:** Scan the piece for rhythm. Does it feel like it was written at a constant pace, or does it speed up and slow down? Look for the absence of: very short sentences (under 6 words), long winding sentences with embedded clauses, sentence fragments, parenthetical asides, or shifts in register.

**The fix:** If a draft is rhythmically flat, inject variation. Break a long sentence into a short one followed by a longer one. Add a parenthetical aside. Drop in a one-sentence paragraph. Let a sentence fragment stand on its own. Match the rhythm patterns documented in the user's voice profile.

### Uniform texture

Detectors also flag text that maintains a consistent "feel" across sections. Human writing shifts texture as it moves between explanation, opinion, narrative, and instruction. AI text often reads like one continuous mode.

**What triggers uniform texture:**

- Every section has the same density of ideas per paragraph.
- The writing never shifts between modes (narrative, analysis, instruction, aside).
- There are no moments where the author's personality breaks through: no dry humor, no specific anecdotes, no "here's what actually happened" tangents.
- The hedging level is constant throughout. AI either hedges everything or nothing. Humans hedge selectively based on actual confidence.

**How to check:** Read the piece quickly and mark where the "energy" changes. If you can't find shifts, the texture is too uniform.

**The fix:** Make sure the piece contains at least a few of these: a concrete anecdote or example from experience, a moment of candor or self-correction, a shift from explaining to advising, a sentence that's clearly the user's personality coming through (per the voice profile). These break the uniform texture that detectors measure.

### Semantic predictability

Beyond individual word choice, detectors measure whether the overall argument follows the most expected path. AI text tends to cover a topic the way a well-organized encyclopedia entry would: definition, importance, challenges, future outlook. Human writing takes less predictable paths.

**What triggers high semantic predictability:**

- The piece follows a template: introduce topic, explain why it matters, list benefits, acknowledge challenges, conclude with optimism.
- Each paragraph's main point could be predicted from the heading alone.
- There are no surprises, contradictions, or moments where the author changes their mind or reveals something unexpected.

**The fix:** Let the piece take a turn the reader wouldn't predict. Lead with the counterintuitive finding. Start from a specific experience instead of a general definition. Skip the "why this matters" section if the reader already knows why. The strongest human writing often starts from a specific, unexpected angle rather than the obvious framing.

---

## How to Use This Checklist

1. Finish the draft first. Don't self-censor while writing.
2. Read through once scanning for vocabulary clusters.
3. Read through again checking structural patterns (parallelism density, list uniformity, transition formality, sentence length variation).
4. Run the detection-tool checks: scan for perplexity (are word choices too predictable?), burstiness (is the rhythm too uniform?), texture (does the piece stay in one mode?), and semantic predictability (does the argument follow the most obvious path?).
5. Check the overall arc: Does the piece actually go somewhere, or does it just sound like it does?
6. For each hit: Is this a deliberate rhetorical choice, or did the LLM default to it? If the writer can't articulate why the fancy version is better, use the plain one.
7. When in doubt, read it aloud. If it sounds like a press release, rewrite it. If it sounds like something the writer would actually say, keep it.
