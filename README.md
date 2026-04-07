# ProfitLab — Find Your Winning Product

A free, single-page web app that takes your monthly profit goal and niche, then instantly returns a product recommendation, full profit breakdown, unit targets, and a 5-step action plan.

---

## Live Demo

Open `index.html` in any browser — no server, no build step, no dependencies.

---

## Features

- **Product match** — picks a recommended product from your chosen niche
- **Profit breakdown** — cost per unit, selling price, profit per unit
- **Unit calculator** — exact units needed per month and per day to hit your goal
- **Budget check** — warns you if your starting budget won't cover initial stock
- **5-step action plan** — prewritten sourcing, listing, and marketing steps per niche
- **Email sign-up bar** — slides up after results to capture leads (wire to your email service)
- **Fully responsive** — works on mobile, tablet, and desktop
- **No login, no API, no backend** — pure HTML, CSS, JavaScript

---

## Project Structure

```
profit-calculator/
├── index.html        # Entire app — markup, styles, and logic in one file
├── README.md         # This file
└── design-concept.md # Design decisions and visual language
```

---

## How to Run Locally

1. Download or clone the repo
2. Double-click `index.html` — opens directly in your browser

That's it. No `npm install`, no build process.

---

## How to Deploy

### Option 1 — GitHub Pages (free, recommended)

1. Push this repo to GitHub (see below)
2. Go to your repo → **Settings → Pages**
3. Under **Source**, select `main` branch and `/ (root)` folder
4. Click **Save** — your site will be live at `https://<your-username>.github.io/<repo-name>/`

### Option 2 — Netlify (free, drag-and-drop)

1. Go to [netlify.com](https://netlify.com) and sign in
2. Drag the entire project folder onto the Netlify dashboard
3. Netlify instantly gives you a live URL (e.g. `https://profitlab.netlify.app`)
4. To use a custom domain: **Site settings → Domain management → Add custom domain**

### Option 3 — Vercel (free)

1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click **Add New Project** → import this repo
3. Leave all settings as default — Vercel detects a static site automatically
4. Click **Deploy** — live in under 60 seconds

### Option 4 — Any Web Host (cPanel, FTP)

1. Log in to your hosting control panel
2. Open **File Manager** and navigate to `public_html`
3. Upload `index.html`
4. Visit your domain — done

---

## Replacing Placeholder Data

All product data lives in the `PRODUCTS` object inside the `<script>` tag at the bottom of `index.html`.

```js
const PRODUCTS = {
  fitness: [{
    name: "Your Product Name",
    cost: 4.80,      // what you pay per unit
    price: 21.99,    // selling price
    plan: [
      "Step 1 text (HTML allowed, use <strong> for emphasis)",
      "Step 2 text...",
      // up to 5 steps
    ]
  }],
  // repeat for each niche key...
};
```

**Niche keys:** `health`, `beauty`, `fitness`, `home`, `pets`, `tech`, `kids`, `outdoors`

You can add multiple products per niche — the app currently picks the first one. To add selection logic, swap `PRODUCTS[nicheKey][0]` with your own logic.

---

## Wiring Up the Email Sign-Up

Find the `submitSignup()` function in the script and replace the placeholder with your email service:

```js
function submitSignup() {
  const email = document.getElementById('signup-email').value.trim();
  if (!email || !email.includes('@')) return;

  // Example: Mailchimp, ConvertKit, Klaviyo, or a simple fetch() to your backend
  fetch('https://your-email-endpoint.com/subscribe', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ email })
  });

  document.getElementById('signup-form').style.display    = 'none';
  document.getElementById('signup-success').style.display = 'block';
}
```

---

## Tech Stack

| Layer  | Choice |
|--------|--------|
| Markup | HTML5  |
| Style  | CSS3 (custom properties, grid, flexbox, scroll-snap) |
| Logic  | Vanilla JavaScript (ES6+) |
| Fonts  | DM Sans via Google Fonts |
| Icons  | Inline SVG |

No frameworks. No bundler. No runtime dependencies.

---

## License

MIT — use it, modify it, ship it.
