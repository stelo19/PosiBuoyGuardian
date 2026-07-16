# Design System Specification — Smart Eco-Mooring Buoy

Two surfaces share this system: the **Boater App** (mobile, outdoor, glare, wet hands, quick decisions) and the **Guardian Dashboard** (desktop, indoor, data-dense, monitoring). Same tokens, different density.

## 1. Design Principles

- **Read at a glance, act with one thumb.** The boater is on a moving boat, often in direct sun. Every screen answers one question fast: free or taken, safe or not, paid or not.
- **The sea, not a spreadsheet.** Even the data-heavy dashboard should feel like water and light, not enterprise software — but never at the cost of legibility.
- **Status is never color-only.** Free/taken/illegal must be readable by someone color-blind and by someone squinting at a phone in full sun — icon + label + color, always together.
- **The buoy is the hero.** The map pin is not a generic marker; it's a living status chip that already tells the story (see Signature Element, §5).

## 2. Color

| Token | Hex | Use |
|---|---|---|
| `sea-ink` | `#0E2A2E` | Primary text, dashboard background (dark mode panels) |
| `posidonia` | `#2F6E58` | Primary brand color — headers, active states, "healthy" data |
| `seafoam` | `#EAF4F1` | App background, light surfaces |
| `deep-water` | `#0B4A57` | Secondary brand, map water fill, dashboard chrome |
| `sun-amber` | `#E8A33D` | Primary CTA, booking confirmation, solar/power indicators |
| `coral-alert` | `#E15B43` | Illegal anchoring, pollution alert, errors — always paired with an icon |
| `slate-40` | `#7C8C8A` | Secondary text, disabled states, captions |

Rules:
- `coral-alert` is reserved for genuine alerts. Never use it decoratively.
- Free/taken status uses `posidonia` (free) and `slate-40` (taken) rather than pure green/red, plus a check/dot vs. cross glyph — this keeps it legible under glare and safe for color-blind users.
- Backgrounds stay cool (seafoam/deep-water family) — avoid warm neutral backgrounds, which read as generic and fight the marine subject.

## 3. Typography

| Role | Typeface | Notes |
|---|---|---|
| Display (pitch deck, app splash, section headers) | **Fraunces** (serif) | Used sparingly — headlines only, never body copy |
| UI / body (app, dashboard) | **Inter** | High x-height, tested for outdoor/small-size legibility |
| Data / sensor readouts | **IBM Plex Mono** | Temperature, pH, coordinates, timestamps — anything numeric that benefits from fixed-width alignment |

Scale (mobile base 16px): 12 / 14 / 16 / 20 / 28 / 40. Dashboard can add a 12px "dense" step for tables.

## 4. Iconography & Motion

- Line icons, 2px stroke, rounded caps — buoy, anchor, wind, droplet, thermometer as the core custom set (rest can come from a standard line-icon library for consistency).
- No filled/solid icon style mixed in; keep one weight system-wide.
- Motion is functional only: a soft pulse on a buoy pin signals "new alert," a fade-in on booking confirmation. No ambient/decorative animation. Respect reduced-motion settings.

## 5. Signature Element

**The buoy pin is the data.** Instead of a plain map marker plus a separate info panel, each pin is a small ring: fill color = occupancy status, ring thickness/pulse = environmental alert present or not. Tapping expands it in place rather than navigating away. This keeps the boater's mental model simple — one glance at the map *is* the status check — and gives the Guardian dashboard the same visual language at a denser scale (a grid of these rings instead of a map, when zoomed to fleet view).

## 6. Layout Concepts

**Boater App** — map-first, single thumb-reachable action per screen:
```
┌─────────────────┐
│      MAP         │  ← buoy rings, current position
│                  │
├─────────────────┤
│ Bay: Porquerolles │  ← bottom sheet, swipe up for detail
│ Morning ● 3 free  │
│ [ Reserve ]       │
└─────────────────┘
```

**Guardian Dashboard** — map + data panel side by side, density over charm:
```
┌───────────┬─────────────┐
│            │ Water Temp   │
│    MAP     │ pH           │
│  (ring     │ Turbidity     │
│   grid)    │ Occupancy %   │
│            │ Alerts (list) │
└───────────┴─────────────┘
```

## 7. Spacing, Radius, Elevation

- 8px base grid throughout.
- Corner radius: 12px for cards/sheets (app), 6px for dashboard panels (denser, less "toy-like").
- Elevation kept minimal — one soft shadow level for the bottom sheet, flat panels elsewhere. Avoid heavy drop shadows; they read poorly in bright sunlight photography/screenshots.

## 8. Accessibility

- Minimum contrast 4.5:1; target 7:1 for anything read outdoors (app primary text, status labels).
- Status never conveyed by color alone — always icon + text label.
- Touch targets ≥ 44×44pt (wet hands, gloves, boat motion).
- Reduced-motion respected system-wide.

## 9. Voice & Tone

- Plain, active verbs: "Reserve," not "Submit." "Booked," not "Confirmed successfully."
- Errors state what happened and what to do — no apologies, no vagueness: "No free buoys in this slot. Try afternoon or a nearby bay."
- Dashboard copy can be more technical/dense; app copy stays short enough to read in one glance while underway.
