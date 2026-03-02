# SEO Superpowers — Claude Code Plugin

## What This Is

A Claude Code plugin providing 16 SEO workflow skills. Modeled after [obra/superpowers](https://github.com/obra/superpowers) but for SEO instead of software development.

## How to Work on This Project

### Reference material

- Study the superpowers plugin structure at `~/.claude/plugins/cache/claude-plugins-official/superpowers/` for the canonical skill format
- Each skill lives in `skills/<skill-name>/SKILL.md`
- Plugin metadata is in `.claude-plugin/plugin.json`
- The README.md contains the full skill catalog

### Architecture

- **Session-start hook** injects `seo-triage` router into every session via `hooks/session-start`
- **seo-triage** is the router skill — it lists all skills and routes users to the right one
- Skills check MCP integrations first (analytics-mcp for GA4, WebFetch, WebSearch), then fall back to asking users for CSV exports
- Cross-skill references use the format `seo-superpowers:skill-name`
- When invoking a skill, briefly announce which skill is being used

### Writing skills

Each SKILL.md needs:
1. **Frontmatter** — `name` and `description` (description defines the auto-trigger)
2. **Overview** — what the skill does
3. **Iron Law** — the one non-negotiable rule for this skill
4. **Checklist** — numbered steps that become tasks
5. **Process Flow** — graphviz dot diagram (only if there are decision diamonds; skip for linear flows)
6. **The Process** — detailed instructions per step
7. **Red Flags + Rationalizations** — common ways of cutting corners and why they're wrong
8. **Key Principles** — governing rules

### SEO Plan file

- `seo-brainstorming` creates `seo-plan.md` in the user's working directory from `seo-plan-template.md`
- Other skills **read** the plan on start for context and **update** their section on completion
- Skills write compact summaries (5-10 lines), not full reports — full analysis stays in conversation
- Re-running a skill **replaces** its section; the Action Log is **append-only**
- If `seo-plan.md` doesn't exist, skills skip integration silently — never create it unprompted

### Key rules

- Skills are **workflows with decision points**, not flat checklists
- Skills should be **tools-agnostic** — describe what to analyze, not which SEO tool to use
- Every skill must end with **concrete, prioritized, actionable output**
- Keep skills **independently useful** — they can reference each other but shouldn't depend on each other
- Triggers in the description should be specific enough to avoid false activations but broad enough to catch relevant tasks
- Technical findings use a **standard severity classification**: Critical / High / Medium / Low tied to actual ranking impact
