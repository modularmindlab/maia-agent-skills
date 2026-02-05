# Agent Skills

A collection of skills for AI coding agents. Skills are packaged instructions and scripts that extend agent capabilities.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### automating-with-maia

Offload complex backend automations to Maia, a multi-agent AI assistant. Teaches coding agents how to generate workflow prompts that users can deploy via webhooks.

**Use when:**
- Building websites or apps that need backend operations
- Implementing data processing, web scraping, or document generation
- Setting up API integrations without building them yourself
- Creating scheduled tasks or multi-step workflows

**Capabilities covered:**
- Data Retrieval (web search, maps, website browsing, document processing)
- Content Generation (documents, PDFs, single-page websites, data visualizations)
- Native Integrations (Gmail, Google Calendar, Docs, Drive, Sheets)
- Custom Actions (any API endpoint via HTTP)
- Deployment (webhooks with flexible JSON input, scheduled execution)

**How it works:**
1. Agent identifies backend operations to offload
2. Generates a natural language prompt for the user to pass to Maia
3. Specifies the expected webhook response payload format
4. User deploys the workflow in Maia and provides the webhook URL
5. Agent embeds the webhook URL into the website/app

**Example use cases:**
- Booking systems with Google Calendar availability checks
- Lead capture forms with Gmail follow-ups and Sheets logging
- Dashboard reports with data visualizations and PDF export
- Web research workflows that scrape sites and compile findings

## Installation

### Option 1: CLI Install (Recommended)

Use [npx skills](https://github.com/vercel-labs/skills) to install skills directly:

```bash
# Install all skills
npx skills add modularmindlab/agent-skills

# Install specific skills
npx skills add modularmindlab/agent-skills --skill automating-with-maia

# List available skills
npx skills add modularmindlab/agent-skills --list
```

This automatically installs to your `.claude/skills/` directory.

### Option 2: Claude Code Plugin

Install via Claude Code's built-in plugin system:

```bash
# Add the marketplace
/plugin marketplace add modularmindlab/agent-skills

# Install all skills
/plugin install agent-skills
```

### Option 3: Clone and Copy

Clone the entire repo and copy the skills folder:

```bash
git clone https://github.com/modularmindlab/agent-skills.git
cp -r agent-skills/skills/* .claude/skills/
```

### Option 4: Git Submodule

Add as a submodule for easy updates:

```bash
git submodule add https://github.com/modularmindlab/agent-skills.git .claude/agent-skills
```

Then reference skills from `.claude/agent-skills/skills/`.

### Option 5: Fork and Customize

1. Fork this repository
2. Customize skills for your specific needs
3. Clone your fork into your projects

### Option 6: SkillKit (Multi-Agent)

Use [SkillKit](https://github.com/rohitg00/skillkit) to install skills across multiple AI agents (Claude Code, Cursor, Copilot, etc.):

```bash
# Install all skills
npx skillkit install modularmindlab/agent-skills

# Install specific skills
npx skillkit install modularmindlab/agent-skills --skill automating-with-maia

# List available skills
npx skillkit install modularmindlab/agent-skills --list
```

## Usage

Once installed, just ask your AI coding agent to help with backend automation tasks:

```
"Build a booking page that checks my Google Calendar availability
and creates events when someone books a slot"
→ Uses automating-with-maia skill (Google Calendar integration)

"I need a dashboard that pulls sales data from my Google Sheets
and generates weekly PDF reports with charts"
→ Uses automating-with-maia skill (Sheets + document generation)

"Create a lead capture form that sends personalized follow-up emails
via Gmail and logs contacts to a Google Sheet"
→ Uses automating-with-maia skill (Gmail + Sheets integration)

"Build a research tool that scrapes competitor websites and
compiles findings into a formatted report"
→ Uses automating-with-maia skill (web scraping + content generation)
```

You can also invoke skills directly:

```
/automating-with-maia
```

## Skill Structure

Each skill contains:
- `SKILL.md` - Instructions for the agent

## License

MIT
