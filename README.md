# Cytron Tutorial Writing Guide

Live page: https://marketingcytron.github.io/Cytron-Tutorial-Writing-Rules/

This repo holds the Cytron Tutorial Guide page and the **`cytron-tutorial-rules` AI skill**. The skill has the same rules
as the guide page, in a form AI tools can follow. Use it to draft, revamp or self-check a my.cytron.io tutorial.

## What's here

| Path | What it is |
|---|---|
| `index.html` + `videos/` | The Cytron Tutorial Guide page for staff and interns |
| `skills/cytron-tutorial-rules/SKILL.md` | The skill: the tutorial rules for AI tools |
| `cytron-tutorial-rules.zip` | The same skill, zipped, ready to upload |

**Downloads (always the latest version):**

- Skill zip: https://github.com/MarketingCytron/Cytron-Tutorial-Writing-Rules/raw/main/cytron-tutorial-rules.zip
- SKILL.md file: https://github.com/MarketingCytron/Cytron-Tutorial-Writing-Rules/raw/main/skills/cytron-tutorial-rules/SKILL.md

## Add the skill to your AI tool

### Claude (claude.ai or the desktop app)

1. Download the **skill zip** above. Don't unzip it.
2. Go to **Customize > Skills**, click **+**, then **Create skill**, then **Upload a skill**.
3. Choose `cytron-tutorial-rules.zip` and make sure the skill is switched on.

### Claude Code

Clone this repo once and link the skill, so `git pull` keeps it up to date:

```bash
git clone https://github.com/MarketingCytron/Cytron-Tutorial-Writing-Rules.git ~/Cytron-Tutorial-Writing-Rules
mkdir -p ~/.claude/skills
ln -s ~/Cytron-Tutorial-Writing-Rules/skills/cytron-tutorial-rules ~/.claude/skills/cytron-tutorial-rules
```

On Windows, copy the `skills/cytron-tutorial-rules` folder into `%USERPROFILE%\.claude\skills\` instead.

### ChatGPT

- **Business, Enterprise or Edu:** in the sidebar open **Plugins**, then the **Skills** tab. Click **Create**, then
  **Upload from your computer**, and upload the unzipped `cytron-tutorial-rules` folder.
- **Free, Plus, Pro, or if you don't see Skills:** create a **Project** and add the **SKILL.md file** to its files. In the
  project instructions, write: *"Follow the Cytron Tutorial Writing Rules in SKILL.md for every tutorial I draft or check."*

### Gemini app (gemini.google.com)

The Gemini app doesn't load skills. Create a **Gem**, upload the **SKILL.md file** as its knowledge, and use the same
one-line instruction as for ChatGPT Projects.

### Codex

Clone this repo, then link or copy the skill folder into `~/.agents/skills/` (all projects) or `.agents/skills/` inside one
project:

```bash
mkdir -p ~/.agents/skills
ln -s ~/Cytron-Tutorial-Writing-Rules/skills/cytron-tutorial-rules ~/.agents/skills/cytron-tutorial-rules
```

### Gemini CLI

```bash
gemini skills install https://github.com/MarketingCytron/Cytron-Tutorial-Writing-Rules --path skills/cytron-tutorial-rules
```

Or copy the folder into `~/.gemini/skills/`. Run `/skills list` to check it's there.

### Antigravity

Copy (or link) the `skills/cytron-tutorial-rules` folder into `.agents/skills/` in your project, then ask the agent
*"What skills do you have?"* to check.

### Any other AI tool

Attach or paste the **SKILL.md file** and say: *"Use these rules for my tutorial."*

## How to use it

- *"Draft a tutorial for [project] using [board] and [parts], following the Cytron tutorial rules."*
- *"Check my draft against the Cytron tutorial rules before I submit."* Paste the HTML from the WebAdmin **Source** view.
  AI tools usually can't open my.cytron.io pages.
- *"Which Telegram banner do I use for a Raspberry Pi project?"*

**Never paste real Wi-Fi passwords, bot tokens or API keys into any AI tool.** Use placeholders such as
`YOUR_WIFI_PASSWORD`. The AI's check doesn't replace the Marketing team's review.

## Keeping it up to date

The Marketing team updates the skill in this repo whenever the rules change. The links above always give the latest version.

- **Claude Code, Codex, Gemini CLI, Antigravity** (linked to a clone of this repo): run `git pull` in
  `~/Cytron-Tutorial-Writing-Rules`. Gemini CLI users who used `gemini skills install` can run the same command again.
- **Claude, ChatGPT, Gemini app** (uploaded copies don't update by themselves): download the zip or SKILL.md again, delete
  the old skill or file, and upload the new one.

The date at the top of SKILL.md ("Writer edition, …") tells you which version you have.

---

### For maintainers

Do not edit this repo directly. It is a published copy. The source lives in the private Cytron-Build-Tutorial hub at
`projects/tutorial-writing-guide/` and is pushed here with `publish.sh`. Any change made here is overwritten on the next
publish.

Last published from hub commit `bdc0c37`.
