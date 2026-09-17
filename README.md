# Sentinel Manual Testing Academy

An interactive, single-file web application for training new manual testers on the Sentinel OTP testing workflow — from triggering a verification code to recording and reporting the final result.

Built with plain HTML, CSS, and JavaScript. No build step. No dependencies. No backend. Just open it and start learning.

![Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Dependencies](https://img.shields.io/badge/dependencies-none-success)
![Build](https://img.shields.io/badge/build-none-lightgrey)

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Course Structure](#course-structure)
- [Demo](#demo)
- [Getting Started](#getting-started)
- [Deployment](#deployment)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Design System](#design-system)
- [Browser Support](#browser-support)
- [Privacy & Security](#privacy--security)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

Sentinel Manual Testing Academy is a **12-section interactive training course** that teaches the complete manual testing cycle for OTP-based verification systems.

The workflow it teaches:

1. A tester enters a phone number (MSISDN) into an app
2. The app triggers an SMS or voice-call OTP
3. The message travels through a mobile operator's network
4. A probe catches it and reports the result
5. The tester observes the real result in TestTrig
6. The result is recorded and reported

The academy teaches this end-to-end through plain-language explanations, clickable diagrams, a step-by-step walkthrough, a hands-on practice simulation, and a 12-question knowledge check.

> **Educational only.** This app does not connect to any real Sentinel system. The practice simulation is entirely self-contained.

---

## Features

- **12 structured learning modules** — from core vocabulary to a full test cycle
- **Fully interactive** — clickable flow diagrams, accordions, tabs, steppers, and a practice simulation
- **Progress tracking** — visited sections, completion percentage, and best quiz score saved to `localStorage`
- **Light & dark mode** — respects OS preference, with a manual toggle
- **Responsive design** — desktop sidebar, mobile hamburger menu
- **Accessible** — semantic HTML, keyboard navigable, high-contrast palette
- **Zero dependencies** — no npm, no framework, no build step
- **Single file** — the entire app is one `index.html`

---

## Course Structure

| # | Module | What You'll Learn |
|---|--------|-------------------|
| 1 | **Dashboard** | Course overview and progress tracking |
| 2 | **Start Here** | What Sentinel manual testing is, and the 9-step journey from app to report |
| 3 | **Core Concepts** | MSISDN, OTP, Brand, Operator, Probe — plus SMS vs Call vs No Result vs Error |
| 4 | **Tools** | Chrome, Notepad, Manual Testing Tracker, TestTrig, Redash, Manual Testing Sheet, Testbench |
| 5 | **Complete Test Cycle** | An 8-step walkthrough, a practice simulation, and the "Expected vs Actual" lesson |
| 6 | **Results & Reporting** | How to interpret the four outcomes and turn them into report rows |
| 7 | **Unconventional Apps** | Why some apps need different registration flows |
| 8 | **Troubleshooting** | CAPTCHA, cooldowns, resend, country/VPN issues, timezones, browser vs mobile |
| 9 | **Quick Reference** | All core terms in one scannable cheat sheet |
| 10 | **Knowledge Check** | 12 questions with explanations and a final workflow recap |

### The Core Mental Model

```
TRIGGER  →  RECORD  →  OBSERVE  →  VERIFY  →  REPORT
```

Every test follows this pattern. The academy reinforces it throughout.

---

## Demo

Open `index.html` in your browser, or serve it locally:

```bash
# Python 3
python -m http.server 8000

# Node.js
npx serve

# PHP
php -S localhost:8000
```

Then visit `http://localhost:8000`.

---

## Getting Started

### Prerequisites

None. You only need a modern web browser.

### Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/sentinel-manual-testing-academy.git
   cd sentinel-manual-testing-academy
   ```

2. Open `index.html` in your browser:

   ```bash
   # macOS
   open index.html

   # Windows
   start index.html

   # Linux
   xdg-open index.html
   ```

That's it. No installation, no server, no configuration.

---

## Deployment

Because it's a single static HTML file, you can host it anywhere.

### GitHub Pages

1. Push the repository to GitHub
2. Go to **Settings → Pages**
3. Under **Source**, select `main` branch and `/ (root)` folder
4. Click **Save**
5. Your site will be live at `https://your-username.github.io/sentinel-manual-testing-academy/`

### Netlify

1. Drag and drop the repository folder onto [Netlify Drop](https://app.netlify.com/drop)
2. Done

### Vercel

1. Import the repository at [vercel.com/new](https://vercel.com/new)
2. Framework preset: **Other**
3. Deploy

### Cloudflare Pages

1. Connect your repository at [pages.cloudflare.com](https://pages.cloudflare.com)
2. Build command: *(leave empty)*
3. Build output directory: `/`
4. Deploy

---

## Project Structure

The entire application is a single HTML file with three logical layers:

```
sentinel-manual-testing-academy/
├── index.html          # The entire application
├── README.md           # This file
└── LICENSE             # MIT license
```

Inside `index.html`:

```
index.html
├── <style>             # All CSS (design tokens, layout, components)
├── <body>              # Minimal shell (sidebar, topbar, content container)
└── <script>            # Data + rendering logic
    ├── PAGES           # Navigation registry
    ├── ICONS           # Inline SVG icon library
    ├── MODULES         # Dashboard module cards
    ├── START_FLOW      # "Start Here" flow steps
    ├── CONCEPTS        # Core concept cards
    ├── RESULT_TYPES    # SMS / Call / No Result / Error
    ├── TOOLS           # Tool reference data
    ├── APPS            # Unconventional apps
    ├── TROUBLESHOOTING # Troubleshooting accordions
    ├── REFERENCE       # Quick reference terms
    ├── CYCLE_STEPS     # Complete test cycle walkthrough
    ├── QUIZ            # Knowledge check questions
    └── state           # App state + render functions
```

### Architecture Notes

- **Data-driven rendering.** Every page is generated from a JavaScript data structure. To change content, edit the data — not the HTML.
- **No framework.** State is a plain object, rendering uses template literals, and events use inline `onclick` handlers.
- **No router.** Navigation is a simple `state.page` string and a `switch` statement.

### LocalStorage Keys

| Key | Value | Purpose |
|-----|-------|---------|
| `sma_visited` | `string[]` | Visited section keys |
| `sma_quiz_best` | `{score, total}` | Best quiz score |
| `sma_theme` | `"light" \| "dark"` | Theme preference |

---

## Customization

### Changing Content

All content lives in the data objects at the top of the `<script>` block:

```js
const CONCEPTS = [
  {
    key: 'msisdn',
    icon: 'phone',
    tag: 'The number under test',
    name: 'MSISDN',
    simple: 'MSISDN is the mobile phone number used for the test.',
    how: ['MSISDN', 'Test Phone Number', 'SIM', 'Mobile Network'],
    example: '...'
  },
  // ...
];
```

To add a new tool, append to `TOOLS`. To add a quiz question, append to `QUIZ`. To add an unconventional app, append to `APPS`.

### Adding a New Section

1. Add an entry to `PAGES`:

   ```js
   { key: 'my-section', label: 'My Section', icon: 'book' }
   ```

2. Add a render function:

   ```js
   function renderMySection() {
     return `<h1 class="page-h">My Section</h1><p class="body-text">...</p>`;
   }
   ```

3. Add a case to the `render()` switch:

   ```js
   case 'my-section': c.innerHTML = renderMySection(); break;
   ```

4. If needed, add a new icon to `ICONS`.

### Rebranding

- **Colors:** edit the CSS custom properties in `:root` (and `:root[data-theme="dark"]`)
- **Name:** search for `Sentinel Academy` and `Sentinel Manual Testing Academy`
- **Fonts:** update the Google Fonts `<link>` and `--font-ui` / `--font-mono` tokens

### Full Offline Mode

Remove the Google Fonts `<link>` tags and use system fonts:

```css
--font-ui: system-ui, -apple-system, sans-serif;
--font-mono: ui-monospace, SFMono-Regular, Menlo, monospace;
```

---

## Design System

### Color Tokens

| Token | Light | Dark | Purpose |
|-------|-------|------|---------|
| `--bg` | `#FFFFFF` | `#0A0F1C` | Page background |
| `--surface` | `#F8FAFC` | `#111827` | Sidebar, cards |
| `--text` | `#0F172A` | `#E7EBF7` | Primary text |
| `--text-muted` | `#5B6B85` | `#9AA6C3` | Secondary text |
| `--primary` | `#4338CA` | `#818CF8` | Accent, buttons |
| `--success` | `#0D9488` | `#2DD4BF` | Completed states |
| `--warning` | `#B45309` | `#FBBF24` | Cautions |
| `--danger` | `#DC2626` | `#F87171` | Errors, warnings |

### Typography

- **UI:** [Inter](https://fonts.google.com/specimen/Inter), weights 400–800
- **Code / chips:** [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono), weights 400–600
- **Body line height:** 1.65–1.7 for readability

### Spacing & Radius

- Border radius: `14px` (cards), `9px` (small elements), `99px` (pills)
- Shadows: soft, layered, low-opacity
- Content max-width: `900px` (standard) / `1040px` (wide pages)

---

## Browser Support

| Browser | Supported |
|---------|-----------|
| Chrome / Edge | ✅ Last 2 versions |
| Firefox | ✅ Last 2 versions |
| Safari | ✅ Last 2 versions |
| Mobile Safari | ✅ iOS 14+ |
| Chrome for Android | ✅ |
| Internet Explorer | ❌ Not supported |

Requires JavaScript enabled. Uses `localStorage` for progress — if unavailable, the app still works but won't remember progress.

---

## Privacy & Security

- **No analytics.** No tracking scripts, no cookies, no telemetry.
- **No network calls** except for Google Fonts (which can be removed for full offline use).
- **No backend.** All data stays in your browser's `localStorage`.
- **Educational only.** The app does not connect to any real Sentinel system.

---

## FAQ

**Q: Do I need to install anything?**
No. Just open the HTML file in a browser.

**Q: Does it work offline?**
Yes, after the first load (fonts are cached). For fully offline use, remove the Google Fonts links.

**Q: Can I use this for my own team?**
Yes. It's a single HTML file — copy it, rebrand it, and customize the content.

**Q: How do I add more quiz questions?**
Append objects to the `QUIZ` array. Each needs `q`, `opts`, `a` (index of correct answer), and `explain`.

**Q: Can I change the color scheme?**
Yes. Edit the CSS custom properties in `:root`. The entire app is themed through those tokens.

**Q: Why doesn't the app remember my progress?**
Check that `localStorage` is enabled in your browser. Private browsing modes sometimes disable it.

**Q: How do I reset my progress?**
Open the browser console and run:

```js
localStorage.removeItem('sma_visited');
localStorage.removeItem('sma_quiz_best');
localStorage.removeItem('sma_theme');
location.reload();
```

**Q: Can I host this on GitHub Pages?**
Yes — see the [Deployment](#deployment) section.

---

## Contributing

Contributions that improve clarity, accessibility, or content accuracy are welcome.

1. Fork the repository
2. Create a feature branch:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. Commit your changes:

   ```bash
   git commit -m "Add: short description of change"
   ```

4. Push to your fork:

   ```bash
   git push origin feature/your-feature-name
   ```

5. Open a pull request

### Content Guidelines

- Use plain language — explain jargon on first use
- Include a concrete example for every concept
- Keep quiz explanations educational, not just "correct/incorrect"
- Never invent test results or fabricate capabilities
- Mark anything outside the source guide as "not covered"

### Code Guidelines

- Keep the data-driven approach — edit the data arrays, not the render functions
- Test in both light and dark mode
- Verify on mobile viewport sizes
- Maintain the existing design tokens; don't hardcode colors

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

The content is based on Sentinel manual testing procedures. All examples, brand names (TikTok, Amazon, PayPal, etc.), and operator names (Smart, Cellcard, Metfone) are used illustratively for training purposes only.

---

<div align="center">

**Sentinel Manual Testing Academy**

*From OTP trigger to test report.*

`TRIGGER → RECORD → OBSERVE → VERIFY → REPORT`

</div>
