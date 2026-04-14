# Prospect 360 — B2B sales intelligence

End-to-end **prospect research** for B2B sellers: from a single URL (site, LinkedIn, Instagram, etc.) to a **meeting-ready** Markdown report plus optional self-contained HTML.

## Who it is for

- SDRs, AEs, founders, and consultants preparing **first meetings** or **outbound** with a specific company.
- Teams that want **one structured document**: company card, digital presence, stakeholders, pains, competitive context, ROI framing, and **ready-to-send** messages (email, DM, WhatsApp, LinkedIn).

## Prerequisites

| Requirement | Why |
|-------------|-----|
| **Claude Code** (or compatible agent runtime) | Skill is authored for agent execution with tools. |
| **`web-search` skill** | Open-web research (required). |
| **`npx` / Node** | To install skills from this repository. |
| **Optional: context-mode MCP** (`ctx_batch_execute`) | Parallel research batches when available. |
| **Optional: `competitor-teardown` skill** | Richer competitive analysis in research round 4. |
| **Optional: Superpowers + Superpowers Chrome** | Browser automation for gated or complex pages; use `/superpowers:using-superpowers` per plugin docs. |

No API keys are required **by this skill itself**; `web-search` may use your inference.sh / Tavily / Exa setup as documented in that skill.

## Install

```bash
npx skills add inference-sh/skills@prospect-360-b2b -g -y
```

Install dependencies:

```bash
npx skills add inference-sh/skills@web-search -g -y
# optional
npx skills add inference-sh/skills@competitor-teardown -g -y
```

Full plugin (all skills):

```bash
npx skills add inference-sh/skills
```

## Configure

- **WebSearch**: Must be available in the session. If missing, the skill stops with install instructions.
- **Superpowers**: Install the plugin and Chrome extension; complete any login in the browser when the agent requests it. Do not put passwords into the chat.
- **context-mode**: Add the MCP server in Claude Code settings if you want parallel `ctx_batch_execute` batches.

## Usage examples

**Full dossier (default flow)**

```text
Run prospect-360-b2b for https://www.example.com — they are a mid-market logistics company in Brazil.
```

**With urgency keywords** (skill may auto-detect urgent mode)

```text
Urgent: meeting tomorrow with Acme Corp, LinkedIn company page https://linkedin.com/company/acme
```

**After install in Claude Code**, invoke the skill the way your client loads skills (e.g. natural language with triggers like *prospect 360*, *sales prep*, *analyze this company*).

The skill will ask for:

1. Output language  
2. What you sell and the outcome for clients  
3. Your name and company (for templates)  
4. Mode: Full / Lite / Urgent  

Then it runs research rounds and writes `PROSPECT_[COMPANY]_[YYYYMMDD].md` and a matching `.html` in the working directory.

## Output modes

| Mode | Research | Sections |
|------|----------|----------|
| **Full** | Up to 6 rounds | Full template including call script and action plan |
| **Lite** | Subset of rounds | Priority brief + core sections |
| **Urgent** | Fast path | Minimal sections for same-day meetings |

## Limitations & good practices

- **Confidence**: Sections are labeled High/Medium/Low; prefer refreshing the file after ~30 days for live markets.
- **Compliance**: Use only public information and ethical outreach; respect GDPR/LGPD and platform terms.
- **Gated sites**: If WebSearch is not enough, enable Superpowers and follow `/superpowers:using-superpowers` — never share credentials in prompts.
- **Competitors**: For deep teardowns, install `competitor-teardown`; otherwise the skill falls back to manual search queries.

## Related skills

```bash
npx skills add inference-sh/skills@web-search
npx skills add inference-sh/skills@competitor-teardown
npx skills add inference-sh/skills@llm-models
```

## License

Same as the parent [inference-sh/skills](https://github.com/inference-sh/skills) repository (MIT).

## Authoring note

Contributions should keep `SKILL.md` self-contained and update this README when behavior or prerequisites change.
