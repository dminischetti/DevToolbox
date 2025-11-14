# DevToolbox - A Developer’s Personal Lab

> Thoughtful tools. Minimal surface area. Engineered to stay out of your way.

DevToolbox is an offline-capable, framework-free toolbox containing fourteen micro-apps designed around clarity, speed, and developer ergonomics. Every module runs entirely client-side - no telemetry, no servers, no build steps. Just clean ES modules, a small router, and a cohesive UI shell.

![Hero preview](./assets/cover.svg)

---

## Live Demo

Deploy on any static host (GitHub Pages, Netlify, S3, local file server).
The entry point is [`index.html`](./index.html). Routing is hash-based, so deep links like:

```
#/tools/regex
#/tools/json-schema
#/tools/contrast
```

work immediately without server configuration.

---

## Tools Included

| Tool | Description |
| --- | --- |
| **Regex Explorer** | Highlight matches, capture groups, and flags. |
| **JSON Doctor** | Validate, format, sort, and clean JSON. |
| **JWT Lens** | Decode JWTs safely and offline. |
| **Base64 Studio** | Encode/decode with UTF-8 awareness. |
| **UUID Generator** | Stream secure `crypto.randomUUID()` values. |
| **Hash Forge** | Hash text using Web Crypto (SHA-1/256/384/512). |
| **Cron Poet** | Turn cron expressions into human phrasing. |
| **Time Atlas** | Compare dates/times across zones. |
| **HTTP Whisperer** | Search HTTP status codes with guidance. |
| **SQL Formatter** | Clean whitespace + uppercase keywords. |
| **Diff Canvas** | Visualize line-level differences. |
| **Markdown Renderer** | Preview sanitized Markdown. |
| **JSON Schema Validator** | Validate JSON against simple schemas. |
| **Contrast Lab** | Evaluate color contrast against WCAG. |

---

## Why DevToolbox?

DevToolbox is intentionally minimal to highlight:

### 🧱 Framework-free architecture
Each tool is a standalone ES module with predictable structure, wired into a shared shell. No React, no build chains, nothing to hide behind.

### 🔌 Offline-first thinking
A service worker precaches the shell and opportunistically caches tool modules so the toolbox still works on planes, trains, and spotty cafés.

### ♿ Accessibility as a default
High-contrast palette, consistent focus states, full keyboard support, and readable typography.

### 🔐 Security mindfulness
- Strict CSP
- JWT decoded locally only
- No eval, no dynamic HTML injection
- Sanitized Markdown
- Same-origin service worker

---

## Setup

No bundlers, pipelines, or node-based build steps required. Just serve the folder:

```bash
# (optional) install dev dependencies for tests
npm install

# quick local server
npx serve .
# or
python -m http.server 8000
```

Then open:
```
http://localhost:8000
```

## Testing
Unit tests use Vitest and cover shared utilities such as:
- string helpers
- date/time utilities
- color math
- base64 and JWT helpers

Run tests:

```bash
npm test
```

Tests mirror the structure of `js/utils/` and live under `tests/utils/`.

## Architecture

Core components
- **Vanilla ES Modules** - Every page and tool is imported lazily.
- **Router** - Hash-based, zero config, handles deep linking cleanly.
- **State module** - Tool metadata + persisted favorites.
- **Service worker** - Offline shell caching + safe fallback behavior.
- **UI shell** - Shared layout, shortcuts, drawers, toasts, and tool framing.

## Styling
- Tailwind via CDN for utilities
- Custom CSS for animations, typography, spacing, and transitions
- Small, predictable classnames and zero runtime styling complexity

## Helpers
Shared utilities handle:
- localStorage-safe persistence
- color + contrast math
- time/duration helpers
- sanitization + escaping
- error formatting

## Structure
```bash
js/
├── app.js           # Bootstraps router, shortcuts, layout framing
├── router.js        # Hash router with lazy-loading
├── state.js         # Tool metadata + persisted favorites
├── tools/           # Each micro-app (Regex, JSON Doctor, etc.)
└── pages/           # Home, tools hub, study notes
```

## UX & Accessibility

- Unified dark theme with neutral grays
- Focus states that glow and remain visible
- Keyboard shortcuts:
```
/ - focus search
Cmd/Ctrl + Enter - run action
Esc - clear or close
g t - go to Tools hub
g s - open Study page
```
- Micro-animations: pulses, tilts, and toasts designed to be calm rather than noisy

## Adding a Tool

- Create js/tools/<slug>.js exporting a default render function.
- Use toolPage(tool, { workspace, output, actions, notes }) to inherit the layout.
- Register metadata in js/state.js.
- Add sample data in data/ if needed.
All tools should run offline and avoid side effects outside their own DOM subtree.

## Privacy & Security
- No telemetry
- No external APIs after initial page load
- Strict CSP (self + required CDNs)
- All parsing/formatting done locally
- No leaking of user-provided payloads
- Service worker respects same-origin rules
- Sanitized Markdown & escaped HTML outputs

License
MIT - free to use, modify, and extend.
