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

**Dark throughout.**
Both sections share the same dark palette. Depth comes from elevation — slightly lighter darks on darker darks — not from a jarring colour switch between sections. This is the standard used by Linear, Vercel, Resend and other premium SaaS tools.

---

## Layout & Structure

### Two Full-Viewport Sections

The page is split into two deliberate, full-screen sections using CSS scroll-snap:

```
Section 1 (100svh) — Hero / Marketing
Section 2 (100svh) — App / Calculator
```

`100svh` (small viewport height) is used instead of `100vh` to fix the iOS Safari address-bar bug where `100vh` includes the browser chrome, hiding content behind it.

Scroll-snap makes the transition feel intentional — like flipping between two screens in a native app rather than scrolling a webpage. Disabled below 860px on mobile, where natural scroll is more comfortable.

### Section 1 — Hero

- **Purpose:** Communicate the product's value in under 5 seconds. Generate enough trust to scroll.
- **Layout:** Two-column grid. Left = copy. Right = product preview card.
- **Background:** Dark base (`#0c0c10`) with a single top-centre radial ambient glow — brand purple at ~18% opacity, fading to transparent. One light source. No orbs, no grid, no texture. This is the Linear/Vercel standard: sophisticated colour layering over ornamental decoration.
- **Preview card:** A white card on the dark background — the intentional contrast focal point. Built with real HTML/CSS so it always matches the live output. Labelled "SAMPLE" to set honest expectations. Floating chips above and below reinforce specific data points (profit match, margin) without cluttering the copy.
- **Nav:** Always dark frosted glass (`rgba(12,12,16,.75)` + `blur(20px)`). Consistent across both sections — no morph needed since the palette is unified.

### Section 2 — App

- **Purpose:** Do the job. Fast, clear, no distractions.
- **Layout:** Three layers:
  1. **Top bar** — thin toolbar with section label and a "Back to home" button. Signals context switch into the tool.
  2. **Form panel (left, fixed 360px)** — always visible. Compact inputs, quick-pick niche chips for speed, single action button.
  3. **Results panel (right, fluid)** — starts with a shimmer-animated skeleton so the panel never looks empty. Fills in on submit with a fade-up animation.
- **Background:** `#0f0f14` — barely lighter than the hero base, creating separation without a colour jump. Panels are elevated slightly further (`#141420`), inputs and cards one step more (`#1a1a28`).

---

## Colour System

The palette uses a 4-step dark elevation system. Depth is communicated by surface lightness, not by colour change.

| Token           | Value                      | Usage                                         |
|-----------------|----------------------------|-----------------------------------------------|
| `--base`        | `#0c0c10`                  | Page base / hero background                   |
| `--app-bg`      | `#0f0f14`                  | App section background                        |
| `--surface-1`   | `#141420`                  | Panels, top bar                               |
| `--surface-2`   | `#1a1a28`                  | Inputs, stat cards, plan items                |
| `--surface-3`   | `#222232`                  | Hover states, elevated cells                  |
| `--brand`       | `#7c5cff`                  | Primary actions, accents, target box          |
| `--brand-dark`  | `#6440f0`                  | Button hover states                           |
| `--brand-glow`  | `rgba(124,92,255,.18)`     | Ambient glow, focus rings, chip backgrounds   |
| `--green`       | `#4ade80`                  | Profit numbers, success badges (dark-optimised) |
| `--green-dim`   | `rgba(74,222,128,.15)`     | Badge backgrounds                             |
| `--border`      | `rgba(255,255,255,.08)`    | Default dividers and card borders             |
| `--border-med`  | `rgba(255,255,255,.13)`    | Hover / focused borders                       |
| `--text`        | `#f0f0f5`                  | Primary text                                  |
| `--text-2`      | `rgba(240,240,245,.6)`     | Secondary text, body copy                     |
| `--text-muted`  | `rgba(240,240,245,.32)`    | Labels, placeholders, captions                |

**Preview card exception:** The hero preview card is always white (`#ffffff`). Its internal colours are hardcoded light-mode values (`#09090b` text, `#71717a` muted, `#f4f4f6` stat backgrounds) since CSS custom properties from the dark palette would make text invisible on a white surface.

**Green is brighter on dark:** `#4ade80` (vs the lighter-bg standard `#16a34a`) — the higher luminosity is needed for sufficient contrast against dark surfaces.

**Intentional restraint:** Only two hues — purple (brand/action) and green (profit/success). Everything else is a cool-neutral dark. This keeps the UI calm and makes numbers stand out without visual competition.

---

## Typography

**Font:** [DM Sans](https://fonts.google.com/specimen/DM+Sans) — a geometric sans-serif with optical sizing support (9–40px). Chosen for:
- Clean, minimal personality — no quirks, no decorative details
- Excellent legibility at small sizes (form labels, stat captions)
- Strong weight contrast between 400 and 800, used to create hierarchy without multiple typefaces
- Widely used in modern SaaS and fintech — feels at home in a tool context

**Scale:**
- Hero headline: `clamp(2.6rem, 4vw, 4rem)` / weight 800 / tracking `-2px`
- Section headlines: `1.05rem` / weight 800
- Body / plan text: `0.85–0.9rem` / weight 400–500
- Labels / captions: `0.65–0.75rem` / weight 600 / uppercase + letter-spacing

No serif. No italic. Hierarchy is built entirely through size, weight, and colour.

---

## Component Decisions

### Preview Card (Hero)
A white card on the dark hero background — the deliberate contrast focal point. Intentionally uses hardcoded light-mode colours internally so the white surface reads correctly. Floating chips (`+$17.19 / unit`, `Profit Match`) add data-point callouts without cluttering the copy.

### Hero CTA Button
The `⚡ Find Winning Product` button uses a slow left-to-right gradient shimmer animation (`background-position` over 3s). On hover, the glow ring expands. Designed to feel active and energetic — the button is the single most important tap target on the page.

### Niche Chips
Quick-pick buttons beneath the niche dropdown. Tapping a chip selects the dropdown value and vice versa — they stay in sync. Reduces the click count for common niches from 2 interactions to 1.

### Skeleton / Waiting State
The results panel never starts empty. A shimmer-animated skeleton preview gives the right column visual weight and signals where results will appear. Hidden on small mobile screens where vertical space is limited.

### Target Box (Results)
The units-needed calculation is the core value of the tool. It gets the most visual weight — a full-width gradient purple card with large type, breaking out of the stat grid to draw the eye first.

### Sign-Up Bar
- **Fixed position, bottom of viewport** — doesn't interrupt the flow
- **Triggered by results, not by time** — only appears 1.2s after value is delivered
- **Dismissable** — a single × removes it
- **Consistent with the dark theme** — uses `--surface-1` background, seamlessly part of the page rather than a jarring overlay

---

## Interaction Model

```
Land on page
  → Hero: understand the product (~5 sec)
  → Click "⚡ Find Winning Product" / scroll down
  → App section: fill 3 fields (~15 sec)
  → Click "Find Winning Product"
  → Results appear in-place, right panel, fade-up animation (instant)
  → 1.2s later: sign-up bar slides up from bottom
  → User saves plan or dismisses
```

No modals. No page reloads. No scroll jumps. Every state change is in-place.

---

## Responsive Strategy

| Breakpoint | Behaviour |
|---|---|
| > 860px | Full two-column hero + two-panel app. CSS scroll-snap active. |
| 540–860px | Hero stacks vertically (preview card visible). App panels stack (form above results). Scroll-snap disabled. |
| < 540px | Hero preview card hidden — headline and CTA take full focus. Niche chips and buttons get 44px+ touch targets. Stat grid 2-column, profit spans full row. Skeleton hidden to save space. |

**`100svh` instead of `100vh`** — used on both sections to fix the iOS Safari address-bar bug.

**Scroll-snap disabled on mobile** — full-height snapping feels claustrophobic on small screens. Natural scroll is used below 860px.

**Preview card hidden on small phones** — on screens under 540px the card pushes the headline and CTA below the fold. Removing it keeps the most important content (the hook and the button) front and centre.

---

## What Was Intentionally Left Out

- **Dark/light mode toggle** — the unified dark palette is a deliberate choice, not a default. A toggle would add complexity without adding value for an MVP.
- **Multiple fonts** — one font, multiple weights. Clean.
- **Gradient orbs / mesh backgrounds** — the single top-centre ambient glow is the only decorative background element. Everything else is flat dark.
- **Loading states / spinners** — the calculation is synchronous and instant. A spinner would add perceived latency where there is none.
- **Animations beyond fade, shimmer, and float** — no parallax, no page transitions, no entrance sequences. Speed and clarity over spectacle.
- **Multiple products per niche in the UI** — the data supports it but the selection logic is intentionally deferred. The MVP validates whether users want the tool at all before adding comparison features.
