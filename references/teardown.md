---
name: site-teardown
description: "Reverse engineer any website into a complete build blueprint. Analyzes the HTML structure, fetches and extracts all animation/interaction code from the site's JavaScript, and pulls the complete design system from the CSS. Outputs a structured teardown document with tech stack, every visual effect and how it's implemented, design tokens, assets needed, and a section-by-section build plan. Use this skill whenever the user wants to analyze how a website was built, reverse engineer a site, clone or recreate a website, understand what tech stack or animations a site uses, do a site teardown, deconstruct a page, figure out how an effect works on a website, or says things like 'steal this website', 'break down this site', 'how did they build this', 'website blueprint', 'analyze this site for me', or gives you a URL and asks you to figure out how it works. Also trigger when the user pastes raw HTML source code and asks what's going on or how to recreate it."
---

# Site Teardown

Reverse engineer any website into a complete build blueprint — tech stack, every visual effect with implementation details, full design system, and a section-by-section build plan. The output should be thorough enough that someone could hand it to Claude Code in a fresh session and build a clone without ever visiting the original site.

## When This Skill Activates

**Activate when the user wants to:**
- Analyze how a website was built
- Reverse engineer or deconstruct a site
- Clone or recreate a website's design and animations
- Understand what tech stack, libraries, or animation techniques a site uses
- Get a build blueprint for a website they want to recreate
- Understand how a specific effect on a website works (and the site hasn't been analyzed yet)

**Example triggers:**
- "Tear down this site: https://example.com"
- "How did they build this website?"
- "Analyze this site for me"
- "Reverse engineer this page"
- "I want to steal this website's design"
- "Clone this site analysis"
- "Website blueprint for [URL]"
- "Break down this page"
- "Deconstruct this site"
- `/site-teardown`
- `/site-teardown [URL]`
- User pastes raw HTML and asks how to recreate it

## Pipeline

### Step 1 — Get the HTML

The HTML is the foundation. It tells you what's on the page — the elements, the classes, the structure, the image/video paths, the SVGs.

**If the user pastes raw HTML source code:**
- Use it directly. Pasted HTML is more complete than a WebFetch for large pages because WebFetch processes content through a sub-model that may summarize details.
- Scan the HTML and extract key structural information:
  - All section/component class names
  - Image and video source paths
  - SVG elements (logos, icons, decorative shapes)
  - Form structures
  - Navigation structure
  - Meta tags (author, description, title)
  - Any inline styles or inline scripts

**If the user only provides a URL:**
- Use WebFetch on the URL with this prompt: "Return the complete HTML structure of this page. Include all class names, element hierarchy, image/video src paths, SVG elements, meta tags, script src paths, stylesheet href paths, and any inline styles or scripts. Preserve the exact class names and data attributes. Do not summarize the structure — return as much detail as possible."
- Note to user: for the most complete analysis, they can paste the raw HTML (Ctrl+U → Ctrl+A → Ctrl+C on the page).

### Step 2 — Find the JS and CSS File Paths

From the HTML, locate the main application JavaScript and CSS files. These are what contain the actual behavior and styling.

**Look for:**
```html
<!-- CSS - usually in <head> -->
<link rel="stylesheet" href="/path/to/main.css">

<!-- JS - usually before </body> -->
<script src="/path/to/main.js"></script>
<script type="module" src="/dist/assets/app.js"></script>
```

**Filter out third-party scripts** — skip these, they're not the site's custom code:
- Google Tag Manager, Google Analytics, gtag
- Cookie consent (iubenda, OneTrust, CookieBot)
- reCAPTCHA, hCaptcha
- CDN-hosted libraries (cdnjs, unpkg, jsdelivr) — don't fetch them
- Social media widgets, chat widgets
- WordPress core scripts (`/wp-includes/js/`)

**Keep the main application files**

### Step 3 — Fetch the JavaScript

Use WebFetch on the main JS file. Extract every interaction, animation, and behavior on the site.

### Step 4 — Fetch the CSS

Use WebFetch on the main CSS file. Extract the complete design system.

### Step 5 — Assemble the Teardown Document

Combine findings from all three sources into a structured markdown file.
