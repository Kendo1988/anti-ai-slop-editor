# Installation Guide

This guide walks you through installing the Anti AI Slop Editor for Claude Code. You can install it as a **skill** (global, always available) or as an **agent** (per-project, on-demand). No prior experience with custom skills or agents is required.

---

## What You Will Need

Before you start, confirm you have the following:

1. **Claude Code** installed and running on your machine.
   If you do not have Claude Code yet, install it first by following the [official Claude Code documentation](https://docs.anthropic.com/en/docs/claude-code). Come back here once you can open Claude Code and run a basic prompt.

2. **A terminal application.**
   - **macOS:** Terminal (built-in) or iTerm2
   - **Windows:** PowerShell, Windows Terminal, or Git Bash
   - **Linux:** Any terminal emulator

3. **Internet access** to download the skill from GitHub.

---

## Method 1: Install via CLI (Recommended)

This is the fastest method. One command, and you are done.

### Step 1: Open your terminal

Launch your terminal application. You can be in any directory -- it does not matter.

### Step 2: Run the install command

```bash
claude install-skill https://github.com/Kendo1988/anti-ai-slop-editor
```

You should see output confirming the skill was installed. It looks something like:

```
Skill "Anti AI Slop Editor" installed successfully.
```

### Step 3: Verify the installation

Skip ahead to the [Verification](#verification) section below.

---

## Method 2: Install Manually

If the CLI method does not work, or if you prefer to see exactly what gets installed, use this method.

### Step 1: Find your Claude Code skills directory

Claude Code stores custom skills in a specific folder on your machine. Find the right path for your operating system:

| Operating System | Skills Directory Path |
|---|---|
| macOS | `~/.claude/skills/` |
| Linux | `~/.claude/skills/` |
| Windows | `%USERPROFILE%\.claude\skills\` |

If the `skills` folder does not exist yet, create it. This is normal for first-time skill users.

**macOS/Linux:**
```bash
mkdir -p ~/.claude/skills
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills"
```

### Step 2: Create a folder for this skill

Inside the `skills` directory, create a new folder called `anti-ai-slop-editor`:

**macOS/Linux:**
```bash
mkdir -p ~/.claude/skills/anti-ai-slop-editor
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills\anti-ai-slop-editor"
```

### Step 3: Download the skill file

Download the `skill.md` file from this repository and place it in the folder you just created.

**Option A: Using curl (macOS/Linux):**
```bash
curl -o ~/.claude/skills/anti-ai-slop-editor/skill.md \
  https://raw.githubusercontent.com/Kendo1988/anti-ai-slop-editor/main/skill.md
```

**Option B: Using PowerShell (Windows):**
```powershell
Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/Kendo1988/anti-ai-slop-editor/main/skill.md" `
  -OutFile "$env:USERPROFILE\.claude\skills\anti-ai-slop-editor\skill.md"
```

**Option C: Manual download:**
1. Go to the [skill.md file on GitHub](https://github.com/Kendo1988/anti-ai-slop-editor/blob/main/skill.md)
2. Click the "Raw" button
3. Right-click the page and choose "Save As..."
4. Save the file as `skill.md` (not `skill.md.txt`) in the skills folder from Step 2

### Step 4: Restart Claude Code

Close Claude Code completely and reopen it. Claude Code loads custom skills at startup, so you need to restart it after installing manually.

### Step 5: Verify the installation

Continue to the next section.

---

## Verification

After installation, confirm the skill is working with this simple test.

### Step 1: Open Claude Code

Launch Claude Code in any project directory.

### Step 2: Run a test prompt

Type or paste the following:

```
Audit this text for AI slop:

"In today's rapidly evolving landscape, it's worth noting that our innovative,
cutting-edge, and transformative solution empowers organizations to seamlessly
navigate the complexities of digital transformation. Let's delve into what
makes this truly unique."
```

### Step 3: Check the response

If the skill is working correctly, Claude will:

1. **Run the 10-point checklist** -- you should see it checking for em-dashes, triple adjective chains, banned words, and the other items.
2. **Flag specific problems** -- it should catch "rapidly evolving landscape", "innovative, cutting-edge, and transformative", "seamlessly", "delve into", and "Let's... " as violations.
3. **Assign a Slop Score** -- the test text above should score high (7 or above out of 10).
4. **Offer a rewrite** or automatically rewrite the text, depending on how you phrased the prompt.

If you see this behavior, the skill is installed and working.

---

## Troubleshooting

### "Skill not found" or Claude does not seem to know about AI slop detection

**Cause:** The skill file is not in the right location, or Claude Code has not loaded it yet.

**Fix:**
1. Confirm the file exists at the correct path:
   - macOS/Linux: `~/.claude/skills/anti-ai-slop-editor/skill.md`
   - Windows: `%USERPROFILE%\.claude\skills\anti-ai-slop-editor\skill.md`
2. Confirm the file is named exactly `skill.md` (not `skill.md.txt` or `Skill.md`)
3. Restart Claude Code completely (close and reopen, do not just start a new conversation)

### The file downloaded as `skill.md.txt`

**Cause:** Your browser or OS appended `.txt` to the filename.

**Fix:** Rename the file to remove the `.txt` extension:

macOS/Linux:
```bash
mv ~/.claude/skills/anti-ai-slop-editor/skill.md.txt ~/.claude/skills/anti-ai-slop-editor/skill.md
```

Windows (PowerShell):
```powershell
Rename-Item "$env:USERPROFILE\.claude\skills\anti-ai-slop-editor\skill.md.txt" "skill.md"
```

### Claude responds but does not run the 10-point checklist

**Cause:** The skill may be installed but Claude might not be using it for your specific prompt.

**Fix:** Be explicit in your prompt. Use phrases like:
- "Use the Anti AI Slop Editor skill to audit this text"
- "Run the AI slop checklist on this text"
- "Check this text for AI-generated patterns using the slop detection skill"

### The install command fails with a network error

**Cause:** Your machine cannot reach GitHub.

**Fix:**
1. Check your internet connection
2. Try opening `https://github.com` in your browser
3. If you are behind a corporate firewall or VPN, try Method 2 (manual installation) instead

### I want to uninstall the skill

Delete the skill folder:

macOS/Linux:
```bash
rm -rf ~/.claude/skills/anti-ai-slop-editor
```

Windows (PowerShell):
```powershell
Remove-Item -Recurse -Force "$env:USERPROFILE\.claude\skills\anti-ai-slop-editor"
```

Then restart Claude Code.

---

## Alternative: Install as an Agent

If you prefer per-project control instead of a global skill, install as an agent instead.

### Step 1: Navigate to your project

Open your terminal and go to the project where you want to use the editor.

### Step 2: Create the agents directory

```bash
mkdir -p .claude/agents
```

**Windows (PowerShell):**
```powershell
New-Item -ItemType Directory -Force -Path ".claude\agents"
```

### Step 3: Download the agent file

**macOS/Linux:**
```bash
curl -o .claude/agents/anti-ai-slop-editor.md \
  https://raw.githubusercontent.com/Kendo1988/anti-ai-slop-editor/main/agent.md
```

**Windows (PowerShell):**
```powershell
Invoke-WebRequest `
  -Uri "https://raw.githubusercontent.com/Kendo1988/anti-ai-slop-editor/main/agent.md" `
  -OutFile ".claude\agents\anti-ai-slop-editor.md"
```

### Step 4: Use the agent

In Claude Code, run:

```
/agents anti-ai-slop-editor
```

Then give it your text to audit or rewrite.

### Skill vs. Agent: When to Use Which

| | Skill | Agent |
|---|---|---|
| **Scope** | Global (all projects) | Per-project |
| **Activation** | Automatic (Claude picks it up) | Manual (`/agents` command) |
| **Best for** | Daily use across everything | Specific projects or one-off audits |
| **Install location** | `~/.claude/skills/` | `.claude/agents/` in your project |

---

## Next Steps

- **Learn what it checks for:** Read [HOW-IT-WORKS.md](HOW-IT-WORKS.md)
- **See usage examples:** Read the Usage section in [README.md](README.md)
- **Customize it:** Edit `skill.md` or `agent.md` directly -- both are plain Markdown. See the Customization section in the README.
