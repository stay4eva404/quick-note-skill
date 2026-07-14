<div align="center">

**English** | [中文](README.md)

# ⚡ QuickNote

> **A "workflow-non-interrupting" universal note-taking Skill**

When you spot something during coding, product thinking, research, or daily life
that needs follow-up later, but you don't want to switch context to handle it now --
**QuickNote records it quickly, in a structured way, with status flow and retrieval.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skill](https://img.shields.io/badge/Skill-QuickNote-blueviolet)]()
[![Status](https://img.shields.io/badge/Status-Production_Ready-success)]()
[![Scenes](https://img.shields.io/badge/Scenes-Universal-orange)]()
[![Platform](https://img.shields.io/badge/Platform-Universal_Agent-blue)]()
[![Version](https://img.shields.io/badge/Version-v1.0.0-informational)]()

**Capture fast, return to the task at hand immediately.**

</div>

---

## 📖 Table of Contents

- [🤔 Why You Need It](#-why-you-need-it)
- [🚀 Quick Start](#-quick-start)
- [✨ Features](#-features)
- [🔄 Status Flow](#-status-flow)
- [💾 Storage Conventions](#-storage-conventions)
- [📄 File Structure](#-file-structure)
- [🎮 Usage Examples](#-usage-examples)
- [🧱 Design Principles](#-design-principles)
- [📁 Project Structure](#-project-structure)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

---

## 🤔 Why You Need It

QuickNote is a lightweight note-taking tool: when you notice something that needs follow-up but don't want to switch context right away, one sentence to the AI records it in a structured format with status flow and retrieval -- so you can review and process on your own rhythm.

Moments like these happen all the time at work:

| Scenario | Inner Monologue |
|------|---------|
| Spot a potential bug while coding | _"I'm in the middle of changing something else, don't want to context-switch"_ |
| A product idea pops up during a discussion | _"Want to note it, but not expand on it right now"_ |
| A question to confirm comes up during research | _"Leave it for later, keep going"_ |
| A random todo suddenly comes to mind in life | _"Note it down, don't interrupt what I'm doing"_ |

- Handle it on the spot -> **interrupts your workflow**
- Do nothing -> **easy to forget**

QuickNote is designed for exactly these "note it now, look at it later" moments.

---

## 🚀 Quick Start

### Installation

QuickNote is a **universal Agent Skill** following the [Anthropic Agent Skills](https://github.com/anthropics/agent-skills) spec, usable in any AI coding assistant that supports SKILL.md loading.

#### Install Path

Drop it into the global skills directory of your platform:

| Platform | Path |
|------|------|
| Claude Code / Codex | `~/.claude/skills/` or `~/.codex/skills/` |
| Trae / Cursor / OpenCode | `~/.trae/skills/`, `~/.cursor/skills/`, `~/.opencode/skills/` |
| Other Agents | Generally `~/.<agent>/skills/` |

---

Copy SKILL.md into the global or project-level skills directory of your platform:

```bash
# 1. Clone the repo
git clone https://github.com/stay4eva/quick-note-skill.git

# 2. Global install (Claude Code example; replace the path prefix for other platforms)
mkdir -p ~/.claude/skills/quicknote
cp quick-note-skill/SKILL.md ~/.claude/skills/quicknote/SKILL.md

# 3. Or project-only use
mkdir -p ./.claude/skills/quicknote
cp quick-note-skill/SKILL.md ./.claude/skills/quicknote/SKILL.md
```

Restart your Agent session after installing; the skill auto-loads.

> 💡 **Universality note**: This skill depends only on the SKILL.md file itself -- no platform-specific APIs, MCP tools, or scripts -- so it runs on any agent that supports the SKILL spec. Trigger-word recognition may vary slightly across platforms, but the core features (create / update / retrieve / edit / delete) all work.

---

#### 🤖 Let the Agent Install It for You

If you'd rather not do it manually, just copy the following to your AI Agent:

```markdown
Download SKILL.md from https://github.com/stay4eva/quick-note-skill
and place it under a quicknote/ subdirectory in the current agent's global skills directory
(Claude Code -> ~/.claude/skills/, Codex -> ~/.codex/skills/,
Trae -> ~/.trae/skills/, Cursor -> ~/.cursor/skills/).
No other dependencies needed. Briefly confirm when done.
```

### Trigger Words

| Type | Trigger Examples |
|:----:|---------|
| ➕ Create | "jot this down" · "make a note" · "quick note" · "note this for later" · "note an idea" · "brainstorm" · "remind me" |
| 🔄 Update Status | "mark xxx as in-progress" · "xxx is resolved" · "start working on xxx" · "I've looked at xxx" |
| ✏️ Edit Body | "change xxx's description to ..." · "add a related file to xxx" · "rename xxx to ..." |
| 🔍 Retrieve | "list quicknotes" · "show unresolved" · "show my todos" · "find notes about xxx" |
| 🗑️ Delete | "delete xxx" · "remove xxx quicknote" · "trash xxx" · "I don't need this entry anymore" |

> 💡 **Bilingual**: Chinese trigger words (记一下 / 记个待办 / 先记下来 / 列出 quicknote / 把 xxx 标记为已解决 / 删除 xxx ...) work equally well. The skill auto-adapts to your conversation language.

### 30-Second Onboarding

```
👤 You: The login timeout error isn't handled here-jot it down, I'll look at it later
🤖 AI: Saved to docs/quicknote/2026-07-02-1430_LoginTimeoutUnhandled.md 📝 (status: to-review)

👤 You: I've started working on the login timeout one
🤖 AI: Updated 2026-07-02-1430_LoginTimeoutUnhandled.md: to-review -> in-progress ✅

👤 You: list unresolved quicknotes
🤖 AI:
       - [in-progress] 2026-07-02-1430_LoginTimeoutUnhandled.md - LoginTimeoutUnhandled (medium)
       - [to-review] 2026-07-02-1505_ResearchCompetitorPricing.md - ResearchCompetitorPricing (low)
       2 total (to-review 1 / in-progress 1)
```

> More examples in [🎮 Usage Examples](#-usage-examples).

---

## ✨ Features

- 🌐 **Universal scenes** - Not limited to code: bugs / ideas / research / life / inspiration all welcome
- 🌐 **Language-adaptive** - Follows your conversation language; generates Chinese or English quicknotes
- 🔄 **Five-state machine** - `to-review -> reviewed -> in-progress -> resolved / ignored`
- 🎯 **Five operations** - Create · Update status · Edit body · Retrieve · Delete
- 🔨 **Batch update** - Filter then batch-transition (requires user confirmation)
- 🔍 **Fuzzy matching** - No need to remember filenames; auto-locates by title / keyword
- ✏️ **Editable body** - Any field editable under explicit user instruction; the AI never edits on its own
- 📜 **Status history** - Each transition is logged in `history`; full lifecycle is traceable
- 👤 **Creator attribution** - Records `author` (user) and `created_by` (AI)
- ⚡ **Lightweight confirmation** - A brief reply after each action, then back to work; no expansion, no follow-up questions

---

## 🔄 Status Flow

```
                   ┌──────────────┐
                   │   to-review  │  ← default on create
                   └──────┬───────┘
                          ↓
                   ┌──────────────┐
                   │   reviewed   │
                   └──────┬───────┘
                          ↓
                   ┌──────────────┐
                   │  in-progress │
                   └──────┬───────┘
                          ↓
              ┌───────────┴───────────┐
              ↓                       ↓
       ┌──────────────┐        ┌──────────────┐
       │   resolved   │        │   ignored    │
       └──────────────┘        └──────────────┘
```

| Rule | Description |
|------|------|
| ⏩ Jumps allowed | Any state can jump directly to `resolved` or `ignored` |
| ◀️ Rollback allowed | `in-progress` can roll back to `reviewed` |
| 🔁 Reopen allowed | `resolved` / `ignored` can be restored to any state |
| 🗣️ Colloquial mapping | "done"->`resolved`, "park it"->`ignored`, "working on it"->`in-progress` |

---

## 💾 Storage Conventions

| Project Type | Default Directory | Notes |
|:--------:|:--------:|------|
| Any project | `docs/quicknote/` | 🌟 Recommended default; visible to agents on `ls`, easier to consult |
| Existing `.quicknote/` | `.quicknote/` | ↩️ Backward compatible; auto-reused |

**Filename Rules**

```
Format: YYYY-MM-DD-HHmm_short-title.md
Example: 2026-07-02-1430_LoginTimeoutUnhandled.md
```

- Special characters auto-sanitized: `/ \ : * ? " < > |` and spaces -> underscore `_`
- Auto-truncated if longer than 40 characters
- Same-minute conflicts auto-append a sequence: `_2.md`, `_3.md`

---

## 📄 File Structure

```markdown
---
type: <bug|optimization|tech-debt|idea|todo|to-research|other>
status: <to-review|reviewed|in-progress|resolved|ignored>
priority: <high|medium|low>
scene: <code|product|idea|research|life|other>
author: <creator username>
created_by: <agent name / model name>
created: <YYYY-MM-DD HH:mm>
updated: <YYYY-MM-DD HH:mm>
tags: []
history: []
---

# <title>

## Context
<the context>

## Description
<detailed description>

## Related Files
- `<file path>`           ← optional for non-code scenes

## Initial Thoughts
<brief root-cause guesses, investigation directions, possible fix ideas>

## Notes
<additional notes>
```

### Field Notes

| Field | Value Rules |
|------|---------|
| `author` | Auto from `git config user.name` -> system username -> `unknown` |
| `created_by` | Filled in by the AI, format `<agent name> / <model name>` (e.g. `Trae Agent / GLM-5.2`) |
| `history` | Appends `{ time, from, to }` on each status update; preserves the full transition trail |
| `tags` | Empty array by default; not auto-extracted; only filled when the user explicitly provides them |
| `created`/`updated` | User's local timezone, format `YYYY-MM-DD HH:mm`; falls back to system timezone, then `UTC` |

---

## 🎮 Usage Examples

### 1️⃣ Create

```
👤 You: The login timeout error isn't handled here-jot it down, I'll look at it later

🤖 AI  : Saved to docs/quicknote/2026-07-02-1430_LoginTimeoutUnhandled.md 📝
         (status: to-review)
```

### 2️⃣ Update Status

```
👤 You: I've started working on the login timeout one

🤖 AI  : Updated 2026-07-02-1430_LoginTimeoutUnhandled.md
         to-review -> in-progress ✅
```

### 3️⃣ Edit Body

```
👤 You: Update the login timeout one's description, add "reproduces on weak networks"

🤖 AI  : Modified 2026-07-02-1430_LoginTimeoutUnhandled.md: updated Description ✏️
```

> 📌 **Editing principle**: Modified only under explicit user instruction; the AI never suggests or rewrites on its own.
> A vague instruction (e.g. "improve the description") triggers one follow-up question for the specific text, never free expansion.

### 4️⃣ Fuzzy Match with Multiple Candidates

```
👤 You: Mark the login one as resolved

🤖 AI  : Found multiple matches, please choose:
         - [in-progress] 2026-07-02-1430_LoginTimeoutUnhandled.md - LoginTimeoutUnhandled
         - [to-review] 2026-07-02-1500_LoginPageStylingBroken.md  - LoginPageStylingBroken

👤 You: the first one

🤖 AI  : Updated 2026-07-02-1430_LoginTimeoutUnhandled.md
         in-progress -> resolved ✅
```

### 5️⃣ Retrieve

```
👤 You: list unresolved quicknotes

🤖 AI  :
         - [in-progress] 2026-07-02-1430_LoginTimeoutUnhandled.md - LoginTimeoutUnhandled (medium)
         - [to-review] 2026-07-02-1505_ResearchCompetitorPricing.md - ResearchCompetitorPricing (low)

         2 total (to-review 1 / in-progress 1)
```

> 📌 **Shows unresolved by default** (`to-review` + `reviewed` + `in-progress`)<br>
> Resolved/ignored entries require "including resolved" or "show all" to appear.

### 6️⃣ Batch Update

```
👤 You: Mark all bugs as ignored

🤖 AI  : Will batch-update to "ignored", 3 items:
         - 2026-07-02-1430_LoginTimeoutUnhandled.md
         - 2026-07-02-1500_LoginPageStylingBroken.md
         - 2026-07-02-1510_FormValidationCrash.md
         Confirm?

👤 You: confirm

🤖 AI  : Updated 3 items -> ignored ✅
```

### 7️⃣ Delete

```
👤 You: Delete the form validation one

🤖 AI  : Confirm delete 2026-07-02-1510_FormValidationCrash.md (FormValidationCrash)?
         This cannot be undone.

👤 You: confirm

🤖 AI  : Deleted 2026-07-02-1510_FormValidationCrash.md 🗑️
```

---

## 🧱 Design Principles

<table>
<tr>
<td width="50%" valign="top">

**⚡ Workflow-non-interrupting**

Recording and transitions are minimal; return to the current task immediately after each action.

</td>
<td width="50%" valign="top">

**🚧 The AI doesn't overstep**

Only records / updates / retrieves / briefly confirms, but the "Initial Thoughts" section should proactively offer valuable root-cause guesses and analysis -- this is QuickNote's core value. It doesn't expand into a full solution discussion or follow up with the user.

</td>
</tr>
<tr>
<td width="50%" valign="top">

**🔒 Bounded edits**

All fields (body + metadata) are editable under **explicit** user instruction; the AI never suggests or rewrites on its own. `status`/`history` go through the status-update operation.

</td>
<td width="50%" valign="top">

**🗑️ Delete requires confirmation**

Deleting quicknote files is supported, but only with explicit user confirmation. Use `ignored` to archive; use delete only when you truly want it gone.

</td>
</tr>
<tr>
<td colspan="2" align="center">

**🗂️ Each project is independent**

No cross-project retrieval; each project's quicknotes live under that project and don't interfere.

</td>
</tr>
</table>

---

## 📁 Project Structure

```
quicknote-skill/
├── 📄 README.md         # This doc (Chinese, for humans)
├── 📄 README.en.md      # English doc
└── 📄 SKILL.md          # Skill definition (the AI reads this to activate the skill)
```

---

## 🤝 Contributing

Issues and Pull Requests welcome.

- 🐛 Bug reports: describe the trigger scenario, expected behavior, and actual behavior
- 💡 Feature suggestions: explain the use case and expected effect
- 📝 Doc improvements: wording, examples, and formatting all welcome

---

## 📄 License

[MIT License](LICENSE) © stay4eva

---

<div align="center">

**Made with ⚡ by [stay4eva](https://github.com/stay4eva)**

If this Skill helped you, a ⭐ Star is appreciated

</div>
