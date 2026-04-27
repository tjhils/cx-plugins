# writing-check

A Claude Code plugin that scans your drafts for AI writing tells, statistical patterns that automated detectors flag, and drift from your own voice. The first time you use it, it walks you through a one-time setup that builds a voice profile from samples of your own writing. Every check after that compares the draft against your profile, not someone else's idea of "good writing."

## What it does

Two scans, run together:

1. **Surface tells.** Vocabulary clusters, inflated significance phrases, formulaic transitions, rule-of-three bullet lists, copula avoidance, em dash overuse, chatbot leakage, generic analogies, vague authority, and the rest of the recognizable AI-output patterns. Adapted from the Wikipedia "Signs of AI writing" page and supplemented with patterns specific to recent model output.

2. **Detection-tool patterns.** The deeper statistical patterns that automated tools (GPTZero, WalterAI, Originality.ai) measure: perplexity, burstiness, uniform texture, semantic predictability. A draft can pass a human editorial scan and still get flagged on these.

Findings are reported by severity. The plugin does not auto-rewrite. It tells you what's wrong and lets you decide what to fix.

## How the voice profile works

On first use, the plugin asks you to provide three samples of your own writing, at least 300 words each. Different formats are fine and encouraged: a blog post, an email, a Slack thread, a strategic memo. The plugin reads them and writes a `voice-profile.md` file that captures your sentence rhythm, humor patterns, analogy style, what you avoid, and the voice cues a draft should match.

The profile is stored in one of two places:

- **Project-local:** `.writing-check/voice-profile.md` in your current project root. Use this if you write in different voices for different work.
- **User-global:** `~/.claude/writing-check/voice-profile.md`. Use this for a single voice across all projects.

If both exist, project-local wins. You can edit the profile by hand any time. Delete it to redo setup.

## No API calls

The plugin runs entirely off bundled reference files. No network requests. Useful if you're working offline, behind a firewall, or just don't want a tool reaching out to the internet for an editorial pass.

## Components

- **Skill `writing-check`.** Triggers on phrases like "writing check", "check for AI writing", "de-slop this", "does this sound like AI", "review for AI tells", "scan my draft".
- **Command `/writing-check`.** Quick invocation. Pass a file path or paste text directly.

## Installation

This plugin lives in the [cx-plugins](https://github.com/tjhils/cx-plugins) repo. Clone the repo (or download just this folder) and copy the plugin into your project:

```bash
git clone https://github.com/tjhils/cx-plugins.git
cp -R cx-plugins/writing-check /path/to/your/project/
```

The skill and `/writing-check` slash command will be available to Claude when working in that project.

## Usage

```
/writing-check my-draft.md
```

Or in conversation:

> "Can you writing-check this?"

If you haven't set up a voice profile yet, the plugin will prompt you through it before running the scan.

## Reference files

- `skills/writing-check/references/ai-slop-checklist.md`: the bundled checklist of AI writing patterns and detection-tool patterns.
- `skills/writing-check/references/voice-profile-setup.md`: the first-run setup flow.
- `skills/writing-check/templates/voice-profile-template.md`: the template the plugin fills in based on your samples.

## License

MIT — see [LICENSE](../LICENSE).
