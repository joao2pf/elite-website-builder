# Elite Website Builder

A Claude skill for creating distinctive, non-generic websites — one design layer at a time.

## The Problem It Solves

Claude produces generic output when given vague prompts. Without direction, it fills the gaps with the statistical average of its training data: purple gradients, Tailwind card grids, Inter font, zero personality. The result looks like every other AI-generated site.

**Elite Website Builder** solves this by guiding you through 5 progressive levels, each adding a layer of specificity to your design brief. By the time you hit "build", Claude has enough context to produce something with a real visual identity.

## How It Works

The skill collects all your inputs upfront in a single **Intake** step — your intent, screenshots, reference URLs, and components — then runs 5 levels in sequence without interrupting you again. Each level eliminates a different source of genericness:

| Level | Name | What It Does |
|---|---|---|
| 1 | **The Raw Prompter** | Captures your intent: what, who, goal, framework |
| 2 | **Design Education** | Auto-generates a token system (palette, typography, signature element) and self-critiques for AI defaults |
| 3 | **Visual Director** | You attach screenshots of sites you like → the skill extracts visual patterns and adds them to the brief |
| 4 | **The Cloner** | You provide a URL → the skill teardowns its HTML, CSS, and JS to extract design techniques |
| 5 | **Component Sniper** | You paste components from 21st.dev or CodePen → the skill integrates them and prevents the Frankenstein trap |

At the end, the skill consolidates all layers into a coherent **Final Design Spec**, resolves conflicts (Level 1 owns the intent, later levels own the visual), and generates a self-contained HTML prototype.

## Installation

### Via Plugin Marketplace (Claude Code)

```bash
/plugin marketplace add joao2pf/elite-website-builder
/plugin install elite-website-builder@elite-website-builder
```

### Manual Installation

```bash
git clone https://github.com/joao2pf/elite-website-builder.git ~/.claude/skills/elite-website-builder
```

### Via Cowork

Download the `.skill` file from the [Releases](../../releases) page and click **Save skill** in the Cowork interface.

## Usage

Invoke the skill and describe what you want to build:

```
/elite-website-builder

> "I want a landing page for a sleep tracking app called Dormio.
>  Goal: waitlist signups. Audience: adults 25–40 with sleep issues.
>  Plain HTML, no framework."
```

At the start, the skill asks one grouped question for anything missing: screenshots of sites you like, a reference URL to tear down, and components to integrate. Answer (or `skip` any of them) and the whole pipeline runs to completion — no further prompts.

**Power move:** put everything in your first message — intent, screenshots attached, reference URL, pasted components — and the skill goes straight from your prompt to a finished prototype with zero questions.

### Level 2 is always automatic

You don't need to know anything about design for Level 2. The skill reads the `design-principles.md` reference and produces a token system (palette, typefaces, layout concept, signature element) — then critiques it for generic defaults before showing you the result.

### Optional sources

You decide how deep to go. A run with only your intent (Levels 1 + 2) still produces substantially better output than a raw prompt. The optional sources are for when you want to push further:

```
Screenshots (Level 3) → attach from Dribbble, awwwards.com, godly.website, or Pinterest
Reference URL (Level 4) → a site whose design you admire, torn down for techniques
Components (Level 5) → paste from 21st.dev, CodePen, or similar
```

## What Makes the Final Output Different

### No Frankenstein sites

Level 5 includes a compatibility check: if you paste components from different design systems, the skill flags conflicts and adapts them to share a common token system before building. Beautiful parts assembled wrongly still look wrong.

### Intent vs. visual priority

The consolidation step follows a clear rule: **Level 1 owns what the site IS and WHO it's for. Later levels own what it LOOKS like.** A meditation app stays a meditation app even if the Level 4 teardown came from a gaming site.

### Self-critique before building

The skill includes an explicit step where it checks whether the token system resembles the three most common AI defaults:
1. Warm cream background + terracotta + high-contrast serif
2. Near-black + acid-green or vermilion accent
3. Broadsheet newspaper + hairline rules + dense columns

If the output resembles one of these without a specific reason from the brief, the skill revises that axis before building.

## Bundled References

The skill ships with two reference files used internally:

- **`references/design-principles.md`** — Design methodology for Level 2 and the HTML build phase. Covers token systems, self-critique process, motion, typography, and copy principles.
- **`references/teardown.md`** — Site analysis pipeline for Level 4. Covers how to fetch and extract HTML structure, JS animations, and CSS design tokens from any URL.

## Requirements

- [Claude Code](https://claude.ai/claude-code) CLI or Anthropic Cowork
- No additional dependencies — the HTML output is a single self-contained file

## Philosophy

Most people using AI for web design aren't bad at design — they just don't have a process for communicating visual direction to an AI. This skill gives you that process.

The five levels map to how good designers actually work: they start with intent, define a visual language, gather references, study what they admire, and curate specific components. The skill just makes that workflow explicit and AI-native.

## Credits

- **[Chase AI](https://www.youtube.com/@chaseaio)** — The 5-level framework is based on his video [The 7 Levels of Building ELITE Websites with Claude Code](https://www.youtube.com/watch?v=1PXFAFMgdns). The site teardown methodology (`references/teardown.md`) is also his work, originally distributed through the Chase AI community.

## License

MIT — Use it, modify it, share it.
