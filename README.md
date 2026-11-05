# KBH1 DESIGN — tokens + one-pager

Open `index.html` through any local server (the Adobe Fonts kit needs http, not `file://`), e.g.

```bash
python3 -m http.server 4173 --directory Output
```

Press **g** (or add `?spec` to the URL) to overlay the column grid in the guides' cyan.

## Files

| File | Role |
|---|---|
| `css/tokens/primitives.css` | **Private** raw values (`--_*`). Never used by components. |
| `css/tokens/semantic.css` | **Public** role tokens. Re-pointed per breakpoint and per surface. |
| `css/base.css` | Reset, typographic roles (`.t-*`), cap-height/baseline trim. |
| `css/layout.css` | Section frame, 4/8/12-col grid, `.figure` local artboards, spec overlay. |
| `css/components.css` | Header, menu, button, link, card, step, device mock, footer. |
| `css/compositions.css` | The one-pager's section compositions, mobile first. |
| `css/kbh1.css` | Entry; declares cascade layers `reset → tokens → base → layout → components → compositions`. |

## The system, as found in the InDesign masters

**One ratio.** The 390 mobile master is the 1920 desktop master × **8/9**, for type *and* space:
18→16 body · 24→21.33 heading/lead/title · 60→53.33 display · 14→12.44 label · 45→40 · 90→80 · 30→27 · 55→49 control height.

**Space is measured cap-height → baseline**, as the cyan markers measure it. Every `.t-*` role trims its box with
`text-box: trim-both cap alphabetic` (metrics-based negative-margin fallback where it isn't supported), so a 45 in CSS is a 45 on the guide.

| Semantic token | Mobile | Tablet / Desktop | Use |
|---|---|---|---|
| `--space-page` | 20 | 45 | outer margin |
| `--space-gutter` | 20 | 30 | column gap |
| `--space-section` | 40 | 45 | section edge → cap / baseline |
| `--space-stack-tight` | 27 | 30 | label → title, display → text |
| `--space-stack` | 40 | 45 | title → body, text → actions, between buttons |
| `--space-stack-loose` | 80 | 90 | heading → content, card → card |
| `--space-head-min` | 0 | 105 | desktop "content line": content cap sits 105 below heading cap (150 from section top) |

**Type** — Helvetica Neue LT Pro 55/65/75 + Octin Spraypaint, from Adobe Fonts kit `ioc6bqt`.

| Role | Face | Desktop | Leading | Tracking |
|---|---|---|---|---|
| `heading` | 75 Bold, caps | 24 | 1 | −0.008em |
| `lead` | 65 Medium | 24 | 1.25 (30) | −0.008em |
| `title` | 65 Medium | 24 | 1 | −0.008em |
| `display` | 65 Medium, caps | 60 | 1 | −0.008em |
| `body` | 55 Roman (+75 Bold lead-ins) | 18 | 1.333 (24) | +0.008em |
| `action` | 65 Medium | 18 | 1 | +0.008em |
| `label` | 65 Medium, caps | 14 | 1 | +0.064em |
| `stencil` | Octin Spraypaint | 174 @1920 / 100 @390 (vw) | 1 | −0.008em |

Tracking was calibrated by fitting browser word positions to InDesign's exported word positions over every multi-word line in both masters (spread < 0.0001em).

**Colour** — ink `#111111`, paper `#FFFFFF`, mist `#F2F2F2` (light type, light panel, button rule), spray `#E1E1E1` (stencil type), cool `#E3E7EA` and steel `#8C99A3` (image fallbacks). Sections set `data-surface="ink|paper|mist|cool"`; components read `--color-fg / --color-bg / --color-rule`.

**Breakpoints** — mobile < 48em (390 master) · tablet 48–89.99em (derived; mobile type scale below 64em / 1024, desktop type scale from there) · desktop ≥ 90em / 1440 (1920 master: each section is one 16:9 screen on a 12-column grid).

## Known gaps

- `Book a 20-minute call`, LinkedIn, Instagram, Listen to LNX, See the visual work use `href="#"` — real URLs needed.
- Client logos are 1.33× raster crops from a LinkedIn graphic; SVG logos would be sharper on retina.
- Desktop line breaks match the guide exactly. On mobile a handful differ by a word, because InDesign's Paragraph Composer balances whole paragraphs; `text-wrap: pretty` is the browser's closest equivalent.
