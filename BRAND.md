# Lune — Visual Identity Specification (v2.0)

**Brand:** Lune  
**Tagline:** *Your universe. Your media.*  
**Aesthetic:** Calm, cinema-first minimalism — neutral obsidian surfaces, monochrome Lunar Silver chrome, and uniform neo-grotesque typography so artwork carries the color.

---

## 1. Logo System (Horizon Mark)

The **Horizon** mark depicts a serene moon rising above a widescreen horizon with three progressively tapering reflection bars, rendered in a refined Lunar Silver-to-White metallic gradient (and Graphite-to-Obsidian on light surfaces).

| Asset | File | Intended Use |
|---|---|---|
| Primary Mark (Dark) | [lune-mark.svg](svg/lune-mark.svg) | Web headers, hero branding, dark UI |
| Primary Mark (Light) | [lune-mark-light.svg](svg/lune-mark-light.svg) | Web headers, hero branding, light UI |
| App Icon (SVG) | [lune-app-icon.svg](svg/lune-app-icon.svg) | Scalable pre-rounded app icon |
| App Icon (PNG) | [lune-app-icon-1024.png](png/lune-app-icon-1024.png) (`512`, `192`) | Pre-rounded raster app icons (web, PWA, Unraid) |
| Full-Bleed Square Avatar (SVG & PNG) | [lune-avatar.svg](svg/lune-avatar.svg) · [lune-avatar-1024.png](png/lune-avatar-1024.png) (`512`) | Unmasked square for GitHub orgs, iOS, and adaptive icon crops |
| Favicon (Optical Small) | [lune-favicon.svg](svg/lune-favicon.svg) | Browser tabs (16–32px); slightly thicker reflection bars & higher lower-bar opacity for crisp subpixel rendering |
| Horizontal Lockup (Dark) | [lune-lockup-dark.svg](svg/lune-lockup-dark.svg) | Navigation bars, docs, README dark mode |
| Horizontal Lockup (Light) | [lune-lockup-light.svg](svg/lune-lockup-light.svg) | Light documentation, print, README light mode |
| Mono Light | [lune-mark-mono-light.svg](svg/lune-mark-mono-light.svg) | 1-colour dark surfaces, watermarks |
| Mono Dark | [lune-mark-mono-dark.svg](svg/lune-mark-mono-dark.svg) | 1-colour light surfaces, stamps |

### Clearspace & Minimum Size
- Maintain clearspace equal to at least **25% of the mark height** on all sides.
- Minimum rendered size: **16px** (`lune-favicon.svg`) or **20px** (`lune-mark.svg`).
- Do not rotate the mark, add drop-shadow glow filters behind the wordmark, or combine with play buttons / film icons.

---

## 2. Colour System

Defined in [tokens.css](tokens.css) and [tokens.json](tokens.json). Neutral dark mode (`#09090B`) is the primary product canvas so posters, stills, and backdrops provide all ambient color.

| Token | Hex | Role | Contrast vs `#09090B` |
|---|---|---|---|
| Obsidian | `#09090B` | Primary canvas | — |
| Graphite | `#141417` | Cards, panels, navigation | 1.1:1 |
| Charcoal | `#1E1E22` | Elevated modals, hover surfaces, secondary buttons | 1.3:1 |
| Hairline | `#2C2C31` | Structural dividers & borders | 1.6:1 |
| Pure White | `#FFFFFF` | Primary action CTA fill & progress bars (pair with `#09090B` ink) | 19.8:1 (AAA) |
| Lunar Silver | `#F5F5F7` | Primary text & wordmark | 18.2:1 (AAA) |
| Silver Muted | `#A1A1A6` | Secondary copy & metadata | 7.6:1 (AAA) |
| Silver Subtle | `#7C7C82` | Captions, hints, subtle labels | 4.8:1 (AA) |
| Lunar Blue | `#64D2FF` | Restrained telemetry, live playback & Dual Audio accents | 11.7:1 (AAA) |
| Healthy | `#30D158` | Service/node healthy & active state | 10.1:1 (AAA) |
| Warning | `#F5C451` | Degraded / attention state | 12.1:1 (AAA) |
| Danger | `#FF6961` | Auth failure / blocked / error / favorite heart | 7.2:1 (AAA) |

---

## 3. Typography

- **Uniform Interface & Display:** Native system neo-grotesque with `Inter` cross-platform fallback (`-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'SF Pro Text', 'Inter', system-ui, sans-serif`).
- **Wordmark & Display:** SemiBold / Bold (`600`–`700`), `-0.025em` to `-0.03em` tracking.
- **Metadata, Badges & Numerals:** Always use the same sans-serif family with `font-variant-numeric: tabular-nums` for `4K`/`HDR`/`DUAL` pills, durations, episode codes, bitrates, and timestamps.
- **Monospace (Admin Only):** System monospace (`ui-monospace, 'SF Mono', Menlo, monospace`) is reserved strictly for raw file paths, invite URLs, IP addresses, and audit payloads in the Admin Console.
