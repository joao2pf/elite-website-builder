---
name: elite-website-builder
description: >
  Progressive 5-level workflow that turns a basic website brief into a rich,
  specific design spec — then generates a distinctive, non-generic HTML prototype.
  Use this skill whenever the user wants to build or redesign a website, landing
  page, or web UI and quality matters. Trigger for: "build me a website", "create
  a landing page", "design a web app", "my site looks too generic", "make it look
  like X", "build me a SaaS landing page", or any web design request. Also trigger
  when the user mentions visual references, screenshots of sites they like, or
  URLs they want to clone or draw from. If someone asks to build ANY web UI and
  hasn't invoked this skill, invoke it — the output will be substantially better.
---

# Elite Website Builder

A 5-level progressive workflow that builds up a rich, specific design brief — then
generates a distinctive HTML prototype that actually has a visual identity.

**The core problem:** Claude produces generic output when given vague prompts.
Without direction, it fills in gaps with the statistical average of its training
data: purple gradients, Tailwind card grids, Inter font, zero personality. Each
level of this workflow eliminates a different source of genericness.

**The pattern:** All sources are gathered upfront in a single Intake step — one
round of questions at most. Then Levels 1–5 run in order, accumulating context
into a single growing Design Brief without stopping to ask for new inputs. The
final consolidation step synthesizes everything into a coherent Final Design
Spec. Then you build.

**Reference files in this skill:**
- `references/design-principles.md` — design methodology used at Level 2 and for building
- `references/teardown.md` — site analysis pipeline used at Level 4

---

## The Design Brief

Maintain a single growing document throughout the workflow. Show the current
state at the end of each level. Add sections as you complete each level:

```
## [L1] Core Intent
## [L2] Design Direction
## [L3] Visual References       (if not skipped)
## [L4] Teardown Intelligence   (if not skipped)
## [L5] Components              (if not skipped)
```

---

## Intake — Gather All Sources Upfront

This step runs ONCE, at the very start, before any level. Its job is to collect
everything the workflow needs so the levels can run end-to-end without
interrupting the user again.

**1. Scan the initial message** for the four source types:

| Source | Feeds | What counts as "provided" |
|---|---|---|
| Intent | Level 1 | What / Who / Goal / Framework (see Level 1) |
| Screenshots | Level 3 | Attached images of sites or designs the user likes |
| Reference URL(s) | Level 4 | Any URL of a site to learn design techniques from |
| Components | Level 5 | Pasted code or links from 21st.dev, CodePen, etc. |

**2. If anything is missing, ask ONE grouped message** covering all gaps at once:
- Any missing intent fields (What / Who / Goal / Framework)
- *"Do you have screenshots of sites you like? Attach them (Dribbble,
  awwwards.com, godly.website, Pinterest...) — or say **skip**."*
- *"Is there a site whose design you want me to learn from? Paste the URL — or
  say **skip**."*
- *"Do you have specific components to integrate (21st.dev, CodePen...)? Paste
  the code or links, and tell me where each goes — or say **skip**."*

Make clear that screenshots, URLs, and components are all optional — a run with
only the intent still produces substantially better output than a raw prompt.

**3. If the initial message already contains all sources** (or the user has
explicitly skipped the optional ones), do NOT ask anything — proceed directly.

After Intake, run Levels 1–5 **in order**, each applying its full instructions to
the material collected here. Do not stop between levels to request new inputs.
The only acceptable mid-flow questions are genuine clarifications where the
instructions cannot be applied without a user decision (e.g., a material style
conflict at Level 5 that the consolidation rules cannot resolve).

---

## Level 1 — The Raw Prompter

Capture the user's intent cleanly before adding any design direction — design
decisions imposed before the intent is clear just anchor the wrong things.

From the Intake material, extract:
- **What**: The page/product type (landing page, dashboard, portfolio, SaaS, etc.)
- **Who**: Target audience
- **Goal**: The page's primary job (signups, showcasing, selling, informing)
- **Framework**: Plain HTML/CSS/JS, React, Next.js — or no preference

All four should already be answered at Intake. If the user declined to specify
one, choose a sensible default and note it in the brief — do not re-ask.

Write **[L1] Core Intent** in the Design Brief and move to Level 2.

---

## Level 2 — Design Education

This level runs automatically without user input. Read `references/design-principles.md`
for the full methodology. Apply it to produce a compact token system.

**What to produce:**

**1. Ground it in the subject.** Before touching colors or fonts, name the
subject's world: its materials, instruments, vernacular, or cultural context.
This is where distinctive choices come from. "SaaS productivity app" is not a
world — "dispatch software for independent freight brokers" is.

**2. Compact token system:**
- **Color**: 4–6 named hex values with clear roles. Name each (e.g., "Void
  background #0A0A0F", "Ice accent #B8D4E8"). Don't describe them — commit to them.
- **Typography**: 2+ typeface roles with specific faces from Google Fonts or
  Fontshare. Name the display face and body face explicitly. Avoid Inter, Roboto,
  and any font you'd reach for by default for a generic project.
- **Layout concept**: One-sentence description of the structural logic of the page.
- **Signature element**: The one thing this page will be remembered for — an
  unusual hero treatment, a distinctive animation, a typographic moment, an
  unexpected structural choice.

**3. Self-critique for generic defaults.** The three AI defaults to watch for:
  (1) warm cream + terracotta + high-contrast serif, (2) near-black + acid-green
  or vermilion accent, (3) broadsheet newspaper + hairline rules. If your token
  system echoes one of these without a specific reason from the L1 brief, revise
  that axis and explain what you changed and why.

Write **[L2] Design Direction** in the Design Brief. Show the user the token system
and the critique in a concise summary, then move to Level 3.

---

## Level 3 — Visual Director (optional)

**If no screenshots were provided at Intake:** Write "Level 3 skipped" in the
brief and move to Level 4.

**If the user attached screenshots**, analyze each one:

- **Palette**: Dominant and accent colors (estimate hex where possible)
- **Typography style**: Serif vs. sans, weight contrast, size hierarchy
- **Layout pattern**: How sections are arranged, use of whitespace, grid logic
- **Key effects**: Animations, scroll behaviors, glassmorphism, parallax, etc.
- **Mood**: The overall feeling (editorial, playful, premium, raw, minimal, etc.)

**For multiple screenshots:**
- Extract the **common thread**: what runs through all of them that the user
  clearly responds to?
- Note **divergences**: where they conflict in style. Flag these — the
  consolidation step will resolve them.

Write **[L3] Visual References** in the Design Brief. Show the user a crisp
summary of what you extracted, then move to Level 4.

---

## Level 4 — The Cloner

**If no reference URL was provided at Intake:** Write "Level 4 skipped" and move
to Level 5.

**If the user provided a URL**, follow the pipeline from `references/teardown.md`
(Steps 1–4) to analyze the site. The goal is not to clone it wholesale — it's
to understand *how* it works so you can borrow techniques intelligently.

1. **Fetch the HTML** (WebFetch the URL). Extract section structure, class names,
   image/video paths, and links to the main JS and CSS files.

2. **Fetch the main JS file** (WebFetch). Extract animations, scroll behaviors,
   interaction handlers, GSAP usage, and any library initializations. Focus on
   techniques relevant to the user's L1 goal.

3. **Fetch the main CSS file** (WebFetch). Extract colors, @font-face declarations,
   spacing system, keyframes, and custom properties.

From these three sources, write a **Teardown Summary** for the Design Brief:

```
### [Site name]
Tech stack: [framework, libraries]
Colors confirmed from CSS: [list]
Fonts confirmed from @font-face: [list]
Key effects worth borrowing:
- [Effect]: [1-sentence explanation of how it actually works]
- ...
Reusable patterns: [layout or structural logic worth adapting]
```

Be specific — "GSAP ScrollTrigger with scrub:true on the hero, scaling from 1.2
to 1.0" is useful. "Uses scroll animations" is not.

Write **[L4] Teardown Intelligence** in the Design Brief, then move to Level 5.

---

## Level 5 — Component Sniper

**If no components were provided at Intake:** Write "Level 5 skipped" and move
to Final Consolidation.

**For each component provided**, do three things:

1. **Identify it**: What is it (nav, hero, card, button, testimonial, etc.)? What
   design language does it have (colors, fonts, borders, shadows)?

2. **Check compatibility**: Does it conflict with the existing Design Brief?
   Conflicts mean: different color system, different font treatment, or a design
   language that doesn't fit the Level 1 brief's world. If there's a conflict,
   name it clearly and resolve it yourself by default: **adapt the component to
   fit the existing brief** (keep the brief's tokens, change the component's
   surface). Only ask the user — *adopt this component's style* vs. *adapt it* —
   when the component's design language seems to be the very reason the user
   chose it and adapting would destroy what they wanted from it.

3. **Plan the adaptation**: Note what needs to change to make it fit (swap the
   hardcoded colors for the brief's palette, change the font, adjust spacing, etc.).

**⚠ Frankenstein Trap:** Components from different design systems — a brutalist
nav, a glassmorphic card, a flat button — produce a site that looks assembled,
not designed. Before Level 5 is done, confirm that all components share the same
token system from the Design Brief. Beautiful parts, ugly whole is a real failure
mode. Catch it here, not after the prototype is built.

Write **[L5] Components** in the Design Brief with each accepted component, its
source, and the adaptation plan, then move to Final Consolidation.

---

## Final Consolidation

This is the most important step. A high-quality prototype follows from a coherent
spec; a fragmented spec produces a Frankenstein site even with good components.

Synthesize the full Design Brief into a single **Final Design Spec** document.

**Consolidation rules:**

**1. Level 1 owns the intent.** The product, audience, and goal are non-negotiable.
Nothing from later levels can change what the site IS, who it's FOR, or what it
DOES. A meditation app stays a meditation app even if the Level 4 teardown is from
a gaming site.

**2. Later levels win on visual decisions.** For any design choice — color,
typography, effects, layout, components — the priority order is:
L5 > L4 > L3 > L2. Each level added more specific, curated visual intelligence.
Trust the specificity of what the user deliberately chose.

**3. Resolve all conflicts explicitly.** Don't carry conflicts into the build.
If L3 shows a serif editorial style and L5 brings a stark geometric component,
choose one direction, adapt everything else to match, and explain your choice.

**4. One source of truth per design decision.** Remove duplicate instructions.
If both L2 and L4 specify colors, L4 wins — keep only the L4 values.

**5. Check for Frankenstein.** Are all components adapted to share the same
palette and typefaces? If not, add explicit adaptation instructions to the spec.

Present the Final Design Spec as a clean, structured summary, then proceed
directly to building the HTML prototype — do not wait for approval. The user
reviews the spec alongside the finished prototype and can request adjustments
to either.

---

## HTML Prototype

Generate a **self-contained single-file HTML prototype** that implements the
Final Design Spec.

Read `references/design-principles.md` before building — it contains principles
that significantly affect output quality. In particular:

**Hero = thesis.** The hero section should open with the most characteristic
element of the product's world — not a big headline + subheadline + CTA button
grid. That's the template answer. Only use it if no better option exists.

**Typography = personality.** Import the specified typefaces. Set a clear type
scale. Use the display face with restraint and intention. The type treatment
itself should be part of the design, not a neutral container.

**Structure = information.** Every structural device (numbered markers, dividers,
section labels) should encode something true about the content. If the content
isn't a sequence, don't number it.

**One signature moment.** Spend the design's boldness in one place. Make the
signature element (specified in L2) actually do its job. Keep everything around
it disciplined and quiet.

**Motion.** If the spec includes animations: page-load sequence with staggered
reveals, scroll-triggered classes (IntersectionObserver), or hover micro-interactions.
Prefer orchestrated single moments over scattered effects. Always respect
`prefers-reduced-motion`.

**Copy.** Don't use Lorem Ipsum. Write real copy that fits the product's world,
audience, and voice. A label labels, a headline headlines — no filler.

**Build quality floor:** Responsive to mobile, visible keyboard focus, semantic
HTML.

After generating: do a brief self-critique. Does anything read like a generic AI
default? Does the signature element actually stand out? If yes to either, revise
before presenting.

Present the file and offer next steps:
- Iterate on specific sections
- Adjust the signature element
- Replace components with alternatives
- Add another level of refinement on any axis (new screenshots, another
  teardown URL, or additional components can be provided at any time)