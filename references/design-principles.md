---
name: frontend-design
description: Design methodology for producing distinctive, intentional web interfaces. Guides aesthetic direction, typography, layout, and the process of moving from brief to build without defaulting to generic patterns.
---

# Frontend Design

Design as if every project deserves its own visual language. Generic output is not a tool limitation — it's a direction problem. Every axis left unspecified gets filled with the statistical average of training data. Your job is to leave no axis unspecified.

## Ground it in the subject

Before choosing a color or font, identify the subject's world: its materials, textures, instruments, rituals, and vocabulary. That world is where original choices come from. A legal firm and a music label can both use dark backgrounds and strong type — what differentiates them is whether the visual vocabulary comes from the world of law or the world of sound.

If the brief doesn't name a subject clearly, name it yourself before designing. State it in one sentence: what it is, who uses it, and what the page's single job is. Build every design decision from that sentence outward. If there's anything in your memory about this person's past projects, preferences, or context, use it — a returning context is richer than a blank brief.

## Design principles

**The hero is an argument.** The first thing someone sees should make the clearest, most characteristic statement you can make about the subject. An image that could belong to any competitor, or a headline + subheadline + CTA button in three rows, is not an argument — it's a template. The hero earns its position by being specific. A large number with a small label and a gradient accent is a default; only use it when there's no better option for this particular brief.

**Typography carries identity.** Choose typefaces that belong to this brief, not to the category. Pair a display face used with restraint against a complementary body face. Define a clear type scale with intentional weights and spacing. The type treatment should be part of what makes the page recognizable — not a neutral container for content.

**Structure encodes meaning.** Every structural device — numbered markers, dividers, eyebrow labels, section breaks — should communicate something true about the content. Numbered sections imply sequence; use them only when the content is actually sequential. Decoration that pretends to be structure is noise.

**Motion should earn its place.** Consider where animation genuinely serves the subject: an orchestrated page-load reveal, scroll-triggered transitions, ambient atmosphere, micro-interactions on hover. A single well-placed animated moment lands harder than scattered effects. Motion that exists to signal effort rather than serve the design reads as AI-generated. Sometimes stillness is the stronger choice.

**Complexity should match the vision.** A maximalist direction needs elaborate, controlled execution. A minimal direction needs precision in spacing, type, and proportion. The goal in both cases is executing the chosen vision well — not picking something in between.

**Copy is a design material.** When the brief doesn't provide real content, write it — but treat it with the same intentionality as spacing or color. Copy that could belong to any competitor makes the design feel generic regardless of how original the visual execution is. See the writing section below.

## Process: plan first, build second

Work in two passes. The first pass is planning only — no code. The second pass is building, following the plan exactly.

**Pass 1 — Design plan.** Produce a compact token system:

- **Color**: 4–6 named hex values with explicit roles. Name each one ("Ink #1A1A2E", "Frost #E8F4F8", "Signal #FF5733"). Don't describe — commit.
- **Typography**: 2 or more typeface roles with specific faces from Google Fonts or Fontshare. Name the display face and the body face explicitly. If a utility face is needed for captions or data, name that too. Avoid reaching for the same families you'd use for any project in this category.
- **Layout concept**: One sentence describing the structural logic of the page — how sections relate to each other, what the reading flow prioritizes.
- **Signature element**: The one thing this page will be remembered for. An unusual compositional choice, a typographic moment, an unexpected structural device, an animation that belongs only to this brief.

**Pass 2 — Self-critique before building.** Read the plan as a stranger would. Ask: could this token system belong to an unrelated brief in the same category? If the answer is yes for any axis, revise that axis. State what you changed and why. Only after that confirmation should you write any code.

When writing CSS, watch for selector specificity conflicts. It's easy to generate classes that override each other — especially between section-level selectors (`.section`) and element-level ones (`.cta`). This often surfaces as padding or margin inconsistencies between sections.

Do the planning and revision in your thinking. Show the user a direction only when you have high confidence it will land well.

## Three AI defaults to actively avoid

Three design directions appear in AI output regardless of subject. All three are valid when the brief genuinely calls for them — the problem is when they appear without being called for:

1. **Warm off-white** background (around #F4F1EA or similar) paired with a high-contrast serif display face and a terracotta, ochre, or clay accent.
2. **Near-black surface** with a single electric accent — acid green, vivid orange, or vermilion — on an otherwise dark palette.
3. **Editorial newspaper grid** with hairline rules, zero border-radius, and dense text columns.

If your plan resembles one of these and the brief didn't point you there, treat it as a signal to revise that axis.

## Restraint and self-critique

Concentrate the design's risk in one place. Choose the signature element and execute it well. Keep everything around it disciplined and quiet. Decoration that doesn't serve the brief dilutes the impact of the element that does.

A minimal direction isn't less work — it demands more precision. Restraint is a quality floor: responsive to mobile, keyboard-accessible, respectful of `prefers-reduced-motion`. Build to that floor without announcing it.

Before finalizing, remove one element you're uncertain about and see if the design improves. If it does, it didn't belong.

If your environment supports screenshots, take them during the build — visual feedback catches things that reading the code doesn't. Keep a brief note of what you've tried so you don't repeat the same choices in future iterations.

## Writing in design

Words in a design exist for one reason: to make the experience easier to understand and navigate. They are not decoration. Bring the same intention to copy that you bring to spacing and color.

Write from the user's side of the screen. Name things by what people recognize and control, not by how the system is built. "Manage notifications" not "configure webhooks." Describe what something does in plain terms rather than positioning it.

Active voice by default. Controls should say exactly what happens when used: "Save changes" not "Submit." An action keeps the same name through the entire flow — the button that says "Publish" produces a confirmation that says "Published." Consistency is how people learn to navigate.

Be specific rather than clever. Errors say what went wrong and how to fix it, without apology and without vagueness. Empty states are invitations to act, not acknowledgments of emptiness.

Match register to audience. Plain verbs, sentence case, no filler. Each element does one job: a label labels, an example demonstrates, nothing does both quietly.