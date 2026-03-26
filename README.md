# Anti AI Slop Editor

> A Claude Code custom skill and agent that detects and destroys AI-generated "slop" (hollow filler phrases, fake enthusiasm, recycled structures, performative depth) and rewrites your text to sound like a human with something to say.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## The Problem

AI-generated text has a recognizable smell. You have read it a thousand times: the unnecessary "delve into", the triple adjective chains, the em-dashes every other sentence, the lists that always have exactly three items. Even when the content is technically correct, it reads like a helpful assistant wrote it -- because one did.

This repo provides two ways to fix that:

- **`skill.md`** -- Install as a Claude Code custom skill (persistent, always available)
- **`agent.md`** -- Use as a Claude Code custom agent (on-demand, run when needed)

Both files contain the same detection rules. Pick whichever fits your workflow. They work in both English and German.

## What It Does

The Anti AI Slop Editor runs a **10-point mandatory checklist** against any text you give it. It checks for:

- Overuse of em-dashes
- Lists that suspiciously always have three items
- Triple adjective chains ("innovative, cutting-edge, transformative")
- Banned words and phrases (maintained in English and German blacklists)
- Passive voice overload
- Repetitive sentence openers
- Rhetorical question openers
- Fake participatory language ("Let's dive in...")
- Structural monotony
- Word frequency violations

Then it rewrites the text to sound like a real person wrote it, following concrete rewriting principles: shorter sentences, active voice, specific details instead of vague claims, and varied structure.

It also scores text on a **0-10 Slop Scale** so you can see exactly how AI-detectable your writing is.

## Quick Start

**You need Claude Code installed.** If you do not have it yet, visit [claude.ai/code](https://claude.ai/code) and follow the setup instructions.

### Option A: Install as a Skill (Recommended)

```bash
claude install-skill https://github.com/Kendo1988/anti-ai-slop-editor
```

Open any project in Claude Code and type:

```
Review this text for AI slop and rewrite it: [paste your text here]
```

### Option B: Use as an Agent

Copy `agent.md` from this repo into your project's `.claude/agents/` directory:

```bash
mkdir -p .claude/agents
curl -o .claude/agents/anti-ai-slop-editor.md https://raw.githubusercontent.com/Kendo1988/anti-ai-slop-editor/main/agent.md
```

Then run it with:

```
/agents anti-ai-slop-editor
```

That is it. Claude Code now knows how to hunt and destroy AI-generated filler.

## Installation

For detailed step-by-step installation instructions, see [INSTALLATION.md](INSTALLATION.md).

For a quick overview:

### Prerequisites

- **Claude Code** installed and working on your machine ([installation guide](https://docs.anthropic.com/en/docs/claude-code))
- A terminal or command line application
- An active Claude Code subscription or API access

### As a Skill (Global, Always Available)

```bash
claude install-skill https://github.com/Kendo1988/anti-ai-slop-editor
```

Or manually: copy `skill.md` to `~/.claude/skills/anti-ai-slop-editor/skill.md`

### As an Agent (Per-Project, On-Demand)

Copy `agent.md` into your project:

```bash
mkdir -p .claude/agents
cp agent.md .claude/agents/anti-ai-slop-editor.md
```

Or manually: create `.claude/agents/` in your project root and place the `agent.md` file there (renamed to `anti-ai-slop-editor.md`).

### Manual Skill Installation

1. Open Claude Code's configuration directory:
   - **macOS/Linux:** `~/.claude/skills/`
   - **Windows:** `%USERPROFILE%\.claude\skills\`
2. Create a new folder called `anti-ai-slop-editor`
3. Copy the `skill.md` file from this repository into that folder
4. Restart Claude Code

## Usage

Once the skill is installed, Claude Code automatically has access to it. You do not need to activate it or import it. Just describe what you want in plain language.

### Audit a Text

Paste or reference any text and ask Claude to check it:

```
Check this blog post for AI slop: [paste text]
```

```
Audit the file marketing-copy.md for AI-generated patterns.
```

Claude will run the full 10-point checklist and return a detailed report with a Slop Score (0-10).

### Rewrite a Text

Ask Claude to fix the problems it finds:

```
Rewrite this text to remove all AI slop: [paste text]
```

```
Clean up the file about-us.md -- make it sound human.
```

### Audit and Rewrite Together

```
Audit and rewrite this press release. Show me the before/after with the slop score.
```

## Before and After

**Before (Slop Score: 8/10):**

> In today's rapidly evolving digital landscape, it's worth noting that our innovative, cutting-edge, and transformative platform empowers businesses to seamlessly navigate the complexities of modern commerce. We don't just deliver solutions -- we craft experiences that resonate deeply with your audience. Let's dive into what makes our approach truly unique.

**After (Slop Score: 1/10):**

> Our platform helps online stores process orders faster. Average checkout time dropped from 4 minutes to 90 seconds for our current clients. Here is how it works.

What changed:
- "Rapidly evolving digital landscape" -- gone. Says nothing.
- "Innovative, cutting-edge, and transformative" -- three adjectives doing zero work, replaced with a concrete result.
- "Seamlessly navigate the complexities" -- vague. Replaced with a specific metric.
- "Let's dive into" -- fake participation. Replaced with a direct transition.
- Em-dash used once instead of twice.

## How It Works

For a detailed explanation of the detection system, scoring, and rewriting principles, see [HOW-IT-WORKS.md](HOW-IT-WORKS.md).

## Customization

Both `skill.md` and `agent.md` are plain Markdown. You can edit either to fit your needs.

### Add Your Own Banned Words

Open `skill.md` or `agent.md` and find the blacklist tables. Add rows to ban words or phrases specific to your industry or writing style.

### Adjust the Slop Scale Thresholds

The scoring system uses a 0-10 scale. You can edit the descriptions for each score level to make the assessment stricter or more lenient.

### Change the Language Focus

The default skill includes both English and German blacklists. If you only write in one language, you can remove the other language's section to keep things focused.

### Modify the Checklist

The 10-point checklist is the core of the skill. You can add new checks (for example, "flag any sentence over 40 words") or remove checks that do not apply to your writing.

To edit the skill file, find it in your Claude Code skills directory:
- **macOS/Linux:** `~/.claude/skills/anti-ai-slop-editor/skill.md`
- **Windows:** `%USERPROFILE%\.claude\skills\anti-ai-slop-editor\skill.md`

## Contributing

Found a phrase that screams "AI wrote this" but is not on the blacklist? Open an issue or submit a pull request. The more patterns this skill catches, the better everyone's writing gets.

## License

MIT License. See [LICENSE](LICENSE) for details.

Copyright (c) pfisterer.digital
