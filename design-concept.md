# ProfitLab — Design Concept

## Overview

ProfitLab is designed to feel like a focused SaaS tool, not a generic landing page with a form attached. Every decision — layout, colour, typography, interaction — is made to reduce friction and get the user from "I have a goal" to "I have a plan" in under 30 seconds.

---

## Design Philosophy

**Show, don't tell.**
The hero section doesn't describe the tool — it shows the output. A live-looking sample result card sits beside the headline so users immediately understand what they're getting before they scroll.

**App-first, not marketing-first.**
Most calculators look like blog posts with a form dropped in. ProfitLab is structured as a two-panel web app: inputs on the left, results on the right — always visible together. The form never disappears and results never require a page jump.

**Earn the sign-up.**
The email capture appears only after the user has received value (the result). It slides in from the bottom — visible but not intrusive, and always dismissable.

---

## Layout & Structure

### Two Full-Viewport Sections

The page is split into two deliberate, full-screen sections using CSS scroll-snap:

```
Section 1 (100vh) — Hero / Marketing
Section 2 (100vh) — App / Calculator
```

Scroll-snap makes the transition feel intentional — like flipping between two screens in a native app rather than scrolling a webpage.

### Section 1 — Hero

- **Purpose:** Communicate the product's value in under 5 seconds. Generate enough trust to scroll.
- **Layout:** Two-column grid. Left = copy. Right = product preview card.
- **Background:** Near-black (`#09090b`). The dark background isolates the preview card, making it the focal point of the page.
- **Preview card:** A static, styled recreation of the actual tool output. Not a mockup screenshot — real HTML and CSS — so it looks exactly like what the user will receive. Labelled "SAMPLE" to set honest expectations.
- **Floating chips:** Two small cards that float above/below the preview card, calling out specific data points (profit match, margin). They reinforce the output without cluttering the headline area.
- **Nav:** Starts transparent over the dark hero. On scroll to Section 2, it morphs to a frosted-glass white bar. This signals to the user that they've moved from "marketing" to "tool" without any hard cut.

### Section 2 — App

- **Purpose:** Do the job. Fast, clear, no distractions.
- **Layout:** Three layers:
  1. **Top bar** — thin toolbar with section label, status text, and a "Back to home" button. Signals a context switch into the app.
  2. **Form panel (left, fixed 360px)** — always visible. Compact inputs, quick-pick niche chips for speed, a single action button.
  3. **Results panel (right, fluid)** — starts with a skeleton/waiting state so the panel never looks empty. Fills in on submit with a fade-up animation.
- **Background:** Light grey (`#f4f4f6`) for the outer section, white for both panels. Creates a clear container feel without heavy shadows.

---

## Colour System

| Token          | Value     | Usage                                      |
|----------------|-----------|--------------------------------------------|
| `--brand`      | `#6c47ff` | Primary actions, accents, links, badges    |
| `--brand-dark` | `#5535d4` | Hover states on brand elements             |
| `--brand-lite` | `#ede9ff` | Backgrounds for brand-tinted elements      |
| `--green`      | `#16a34a` | Profit numbers, success states, "recommended" badge |
| `--green-lite` | `#dcfce7` | Badge backgrounds                          |
| `--ink`        | `#09090b` | Hero background, primary text, nav (dark)  |
| `--bg`         | `#f4f4f6` | App section background                     |
| `--border`     | `#e4e4e7` | All dividers and card borders              |
| `--muted`      | `#71717a` | Secondary text, labels, placeholders       |

**Intentional restraint:** Only two hues — purple (brand) and green (profit/success). Every other colour is a neutral. This keeps the UI calm and makes the brand and profit numbers stand out without competition.

---

## Typography

**Font:** [DM Sans](https://fonts.google.com/specimen/DM+Sans) — a geometric sans-serif with optical sizing support (9–40px). Chosen for:
- Clean, minimal personality — no quirks, no decorative details
- Excellent legibility at small sizes (form labels, stat captions)
- Strong weight contrast between 400 and 800, used to create hierarchy without needing multiple typefaces
- Widely used in modern SaaS and fintech — feels at home in a tool context

**Scale:**
- Hero headline: `clamp(2.6rem, 4vw, 4rem)` / weight 800 / tracking `-2px`
- Section headlines: `1.05rem` / weight 800
- Body / plan text: `0.85–0.9rem` / weight 400–500
- Labels / captions: `0.65–0.75rem` / weight 600 / uppercase + letter-spacing

No serif. No italic. Type hierarchy is built entirely through size, weight, and colour.

---

## Component Decisions

### Preview Card (Hero)
Built with the same CSS classes as the real results card, not a static image. This means it always matches the live output and costs zero extra maintenance.

### Niche Chips
Quick-pick buttons beneath the niche dropdown. Tapping a chip selects the dropdown option and vice versa — they stay in sync. Reduces the click count for the most common niches from 2 to 1.

### Skeleton / Waiting State
The results panel never starts empty. A shimmer-animated skeleton preview gives the right column weight and signals to the user where results will appear. This prevents the jarring "half a page is blank" feel common in split-panel tools.

### Target Box (Results)
The units-needed calculation is the core value of the tool. It gets the most visual weight — a full-width purple card with large type, breaking out of the card grid to draw the eye first.

### Sign-Up Bar
- **Fixed position, bottom of viewport** — doesn't interrupt the flow
- **Triggered by results, not by time** — only appears after value is delivered
- **Dismissable** — a single × removes it without guilt
- **Dark themed** — echoes the hero background, visually distinct from the light app section so it reads as a separate system message

### Nav Morphing
The navigation uses an `IntersectionObserver` on the hero section. When the hero exits the viewport, the nav switches from `class="nav dark"` (transparent, white text) to `class="nav light"` (frosted white, dark text). No scroll event listeners, no jank — just a clean CSS class swap driven by the browser's native intersection API.

---

## Interaction Model

```
Land on page
  → Hero: understand the product (5 sec)
  → Click "Find my product" / scroll
  → App section: fill 3 fields (15 sec)
  → Click "Find Winning Product"
  → Results appear in-place, right panel, fade-up (instant)
  → 1.2s later: sign-up bar slides up from bottom
  → User saves plan or dismisses
```

No modals. No page reloads. No scroll jumps. Every state change is in-place.

---

## Responsive Strategy

| Breakpoint | Behaviour |
|---|---|
| > 900px | Full two-column hero + two-panel app. Scroll-snap active. |
| 600–900px | Hero stacks vertically. App panels stack (form above results). Scroll-snap disabled. |
| < 600px | Nav collapses to logo + CTA only. Form padding tightened. Stat grid goes 2-column. Floating chips hidden. |

Scroll-snap is **disabled on mobile** — stacked panels that snap feel trapped on small screens. Natural scroll is more comfortable.

---

## What Was Intentionally Left Out

- **Animations beyond fade/slide** — no parallax, no page transitions, no loading spinners. Speed > spectacle.
- **Dark mode toggle** — the two-section dark/light contrast is a deliberate design choice, not a default. Adding a toggle would undermine it.
- **Multiple fonts** — one font, multiple weights. Clean.
- **Decorative backgrounds** — no gradient orbs, no grid overlays, no mesh gradients. The data and typography carry the visual weight.
