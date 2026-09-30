# website-audit-rebuild

An [Agent Skill](https://agentskills.io) for Claude, Codex CLI, Gemini CLI, Cursor, opencode and other harnesses that read `SKILL.md`.

Audit an existing publicly accessible website and produce a complete redevelopment plan — page/content/feature inventory, sitemap, multi-area audit (UI, UX, mobile, accessibility, performance, SEO, security, branding, content, architecture, analytics), a client-facing audit report, a technical redevelopment specification with content migration plan, and a concise (≤3 page) redevelopment proposal with tasks, conservative timeline and budget, and recommended tech stack. Use this skill whenever the user asks to audit, review, analyze, assess, redesign, rebuild, modernize, migrate, or "look at" an existing website or URL; wants a website proposal, quote, or scope for improving a client's site; asks "what's wrong with this site"; or wants to document a site before redeveloping it. Trigger even if the user only pastes a URL and asks for feedback on the site.


## Install

With the [skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add brianitsup/website-audit-rebuild
```

Manually (user scope for Codex, Gemini, Cursor, opencode):

```bash
git clone https://github.com/brianitsup/website-audit-rebuild.git ~/my-skills/website-audit-rebuild
ln -s ../../my-skills/website-audit-rebuild ~/.agents/skills/website-audit-rebuild
```

For Claude, upload the folder as a skill in Settings → Capabilities, or place it in `~/.claude/skills/website-audit-rebuild` for Claude Code.

## License

MIT
