# Elite Website Builder — Development Notes

This repo is the source of truth for the `elite-website-builder` Claude skill.
See `README.md` for what the skill does and how users install it.

## File map

- `SKILL.md` — the skill itself. The YAML frontmatter `description` drives when
  Claude auto-triggers the skill; the body is the 5-level workflow loaded into
  context when it runs.
- `references/design-principles.md` — loaded at Level 2 and during the HTML
  build phase.
- `references/teardown.md` — loaded at Level 4 (URL teardown pipeline).
- `README.md` — user-facing documentation for GitHub.

## How this skill is deployed

1. **Claude Code (this machine):** `~/.claude/skills/elite-website-builder` is a
   directory junction pointing at this repo. Edits here are live immediately —
   no copy step. Do not delete or recreate that junction casually.
2. **claude.ai / Claude Desktop:** a copy was uploaded as a skill on claude.ai
   (appears namespaced as `anthropic-skills:elite-website-builder`). It does NOT
   auto-sync — after meaningful changes, re-upload it there.
3. **GitHub:** https://github.com/joao2pf/elite-website-builder — push `main`
   after each improvement so installs via `git clone` stay current.

## Editing guidelines

- Files are UTF-8. Watch for corruption: `design-principles.md` once ended up
  with trailing NUL bytes, which makes git treat the file as binary.
- When changing `SKILL.md`'s frontmatter `description`, remember it is the
  triggering surface — keep the concrete trigger phrases ("build me a website",
  "landing page", etc.) unless intentionally retuning them.
- Keep the Design Brief section labels (`[L1]`–`[L5]`) consistent across
  SKILL.md, README.md, and the references — they cross-reference each other.
