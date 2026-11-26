# AGENTS.md — `LuneServer/lune-brand` (Visual Identity & Design Tokens)

This document describes the architecture, asset inventory, brand rules, and downstream sync workflow for **Lune Brand** (`github.com/LuneServer/lune-brand`).

> **Mandatory Branch Workflow:** Never commit directly to `main` or pile unrelated changes onto an existing branch. Start every distinct task (asset, token, or doc change) on its own branch from an up-to-date local `main` (fetch and fast-forward `main` first, then `git switch -c <type>/<short-topic> main`, e.g. `feat/mono-mark`; if uncommitted changes prevent fast-forwarding `main`, use the freshly fetched `origin/main` as the start point instead). For parallel or concurrent work, or when the working tree already holds uncommitted changes from another task, use a separate worktree (`git worktree add ../lune-brand-<topic> -b <type>/<topic> main`) instead of switching branches in place. Keep each branch scoped to one concern, run `git status` before editing to confirm what you're building on, and when a task spans repos (`lune`, `lune-web`, `lune-brand`), use a same-named branch in each. Do not merge, rebase onto, or push unless the user asks.

> **Mandatory Maintenance Rule:** Whenever you add, rename, or modify logos, icons, color tokens, typography rules, or radii in this repository, **you must update this `AGENTS.md` and [`BRAND.md`](BRAND.md) in the same change**, and keep `tokens.css` and `tokens.json` strictly in sync. Remember to propagate updates to downstream consumers (`lune-web`, `lune`, and future native clients).

---

## 1. Lune Platform Ecosystem

`lune-brand` is the **single source of truth** for visual identity across all Lune repositories:

| Repo | Local Path | How It Consumes `lune-brand` |
|---|---|---|
| **`LuneServer/lune-brand`** (this repo) | `../lune-brand` | Canonical brand spec (`BRAND.md`), design tokens (`tokens.css`, `tokens.json`), vector marks (`svg/`), and raster icons (`png/`). |
| **`LuneServer/lune-web`** | `../lune-web` | Copies `tokens.css` -> `src/tokens.css`, mirrors semantic palette colors in `src/index.css` (`@theme`), and copies `svg/lune-mark.svg` & `svg/lune-favicon.svg` -> `public/`. |
| **`LuneServer/lune`** | `../lune` | References `png/lune-avatar-512.png` in `deploy/unraid/lune.xml` and uses the canonical brand name & tagline (*"Your universe. Your media."*) in `GET /api/v1/system/info`. |
| Future native apps (`lune-ios`, `lune-tv`, `lune-android`) | — | Will consume `tokens.json` (W3C Design Tokens format) and `png/lune-avatar-1024.png` / `svg/` assets. |

---

## 2. Repository Layout

```text
lune-brand/
├── BRAND.md                        # Visual Identity Specification (v2.0)
├── tokens.css                      # CSS custom properties (--lune-*) for dark default & [data-theme="light"]
├── tokens.json                     # W3C Design Tokens format (palette, dark/light semantic roles, typography, radii)
├── svg/
│   ├── lune-mark.svg               # Primary Horizon mark (Lunar Silver gradient, dark UI)
│   ├── lune-mark-light.svg         # Primary Horizon mark (Graphite-to-Obsidian gradient, light UI)
│   ├── lune-favicon.svg            # Optically adjusted mark for 16-32px favicons
│   ├── lune-app-icon.svg           # Scalable pre-rounded app icon
│   ├── lune-avatar.svg             # Full-bleed unmasked square avatar (GitHub, iOS, adaptive icons)
│   ├── lune-lockup-dark.svg        # Horizontal mark + wordmark for dark surfaces
│   ├── lune-lockup-light.svg       # Horizontal mark + wordmark for light surfaces
│   ├── lune-mark-mono-light.svg    # 1-color light mark for dark surfaces / watermarks
│   └── lune-mark-mono-dark.svg     # 1-color dark mark for light surfaces / stamps
└── png/
    ├── lune-app-icon-1024.png      # Pre-rounded raster app icons (web, PWA, Unraid)
    ├── lune-app-icon-512.png
    ├── lune-app-icon-192.png
    ├── lune-avatar-1024.png        # Full-bleed square raster avatars
    └── lune-avatar-512.png
```

---

## 3. Core Brand & Design Invariants

### Brand Identity
- **Name:** `Lune`
- **Tagline:** *Your universe. Your media.*
- **Aesthetic:** Calm, cinema-first minimalism — neutral obsidian surfaces, monochrome Lunar Silver chrome, and uniform neo-grotesque typography so media artwork carries the color.

### Horizon Mark Rules
- Depicts a serene moon rising above a widescreen horizon with three progressively tapering reflection bars in a Lunar Silver-to-White gradient (Graphite-to-Obsidian on light surfaces).
- **Clearspace:** Maintain at least **25% of mark height** on all sides.
- **Minimum size:** `16px` (`lune-favicon.svg`) or `20px` (`lune-mark.svg`).
- **Prohibited modifications:** Never rotate the mark, add drop-shadow glow filters behind the wordmark, or combine the mark with play buttons or film-strip icons.

### Color & Accessibility System
- Neutral dark mode (`#09090B` Obsidian) is the primary product canvas; light theme is supported via `[data-theme="light"]`.
- **Palette anchors:**
  - Surfaces: Obsidian `#09090B` (canvas), Graphite `#141417` (surface), Charcoal `#1E1E22` (elevated), Hairline `#2C2C31` (structural border)
  - Text: Lunar Silver `#F5F5F7` (primary), Silver Muted `#A1A1A6` (secondary), Silver Subtle `#7C7C82` (muted)
  - Accents: Pure White `#FFFFFF` (primary CTA & progress bars — pair with `#09090B` ink on solid fills), Lunar Blue `#64D2FF` (restrained telemetry/live/Dual Audio accent)
  - Status tones: Healthy `#30D158`, Warning `#F5C451`, Danger `#FF6961`
- Any new or adjusted color token must meet WCAG AA contrast (prefer AAA for text and telemetry tones) against its intended surface.

### Typography
- **Uniform UI & Display:** `-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'SF Pro Text', 'Inter', 'Segoe UI', system-ui, sans-serif`.
- **Metadata & Numerals:** Keep the same sans-serif with `tabular-nums` across badges (`4K`, `HDR`, `DUAL`), durations, episode numbers, and media specs.
- **Monospace (Admin Only):** System monospace (`ui-monospace, 'SF Mono', Menlo, monospace`) is reserved strictly for raw file paths, invite URLs, IP addresses, and audit payloads in the Admin Console.

---

## 4. Change & Downstream Sync Checklist

Whenever updating assets or tokens in `lune-brand`:

1. **Keep token formats synchronized:** Update both `tokens.css` and `tokens.json` together, and reflect any new roles or hex changes in `BRAND.md`.
2. **Keep raster exports synchronized:** If `svg/lune-app-icon.svg` or `svg/lune-avatar.svg` changes, regenerate all corresponding sizes in `png/` (`1024`, `512`, `192`).
3. **Propagate to `../lune-web`:**
   - Copy `tokens.css` -> `../lune-web/src/tokens.css` and update `@theme` colors in `../lune-web/src/index.css` if palette hexes changed.
   - Copy updated `svg/lune-mark.svg` -> `../lune-web/public/lune-mark.svg`, `svg/lune-mark-light.svg` -> `../lune-web/public/lune-mark-light.svg`, and `svg/lune-favicon.svg` -> `../lune-web/public/favicon.svg`.
4. **Check `../lune` references:** Preserve stable filenames referenced externally (e.g., `png/lune-avatar-512.png` used in `../lune/deploy/unraid/lune.xml`).
5. **Update this `AGENTS.md`:** Document any added asset variants, token categories, or new consumer repositories.
