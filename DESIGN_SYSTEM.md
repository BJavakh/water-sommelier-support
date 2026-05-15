# Water Sommelier - Design System

Reference for the brand's visual language, used by the landing page (`index.html`)
and intended as a single source of truth for future surfaces (in-app marketing
modules, App Store screenshots, social cards, etc.).

## Files

| File | Purpose |
|---|---|
| `tokens.css` | CSS custom properties. Two layers: a hand-curated **editorial brand layer** at the top (use these), and the full auto-generated palette below for reference. |
| `tokens.json` | Same data as machine-readable JSON. For Figma plugin import, Style Dictionary pipelines, etc. |
| `index.html` | The live landing page. Already uses the editorial-layer values inline. |

## Aesthetic Direction

**Editorial Sommelier Magazine.** The app's name is literally "sommelier" — a
curator of taste. Most water apps look clinical; this one is curated, refined,
and feels like a small magazine. Warm cream paper, real editorial typography,
restrained palette, one dark spread for visual rhythm.

## Colour

The editorial layer is what you should reach for first. The auto-generated
50-900 scale is included as a reference for shading needs not yet covered by
the curated tokens.

### Editorial layer

| Token | Hex | Use |
|---|---|---|
| `--brand-paper` | `#F4EFE5` | Primary background. Warm cream, magazine-stock feel. |
| `--brand-paper-warm` | `#EAE3D2` | Alt sections (premise, support). |
| `--brand-paper-deep` | `#DDD3BC` | Deepest cream — pull-quote ground if needed. |
| `--brand-ink` | `#15182A` | Primary text. Not pure black. |
| `--brand-ink-soft` | `#3D4256` | Secondary text (lede paragraphs). |
| `--brand-ink-faint` | `#717890` | Tertiary text, metadata. |
| `--brand-water` | `#3D6FB8` | Primary accent. Used on italic words, links, primary CTAs. |
| `--brand-water-bright` | `#5990D5` | Hover state, gradient highlights. |
| `--brand-navy` | `#1E3A5F` | Phone gradients, deeper accents. |
| `--brand-copper` | `#A85F3C` | Eyebrow labels, numerals, chapter numbers. Use SPARINGLY — copper is the spice. |
| `--brand-copper-soft` | `#C77B58` | Lighter copper variant for hover. |
| `--brand-night` | `#0B0E1C` | The single dark spread ("Inside" section). |
| `--brand-rule` | `#C9BFA6` | Hairline rules separating editorial sections. |

### Auto-generated scale

For each primary, secondary, and neutral color you get a 50-900 scale plus a
`DEFAULT`. Useful for picking a tint or shade not in the editorial layer.

```css
var(--colors-primary-500)     /* default water-blue scale */
var(--colors-neutral-700)     /* default neutral gray scale */
var(--colors-semantic-success-base)   /* #10B981 — success */
var(--colors-semantic-warning-base)   /* #F59E0B — warning */
var(--colors-semantic-error-base)     /* #EF4444 — error */
```

## Typography

| Token | Family | Where |
|---|---|---|
| `--font-display` | `Fraunces` | All headlines, hero, italics. Variable font - use `font-variation-settings` to control optical sizing and SOFT axis (warmth). For display sizes set `opsz 144`; for body italic `opsz 18`. For "wonky" italic emphasis on accent words add `WONK 1`. |
| `--font-body` | `Manrope` | Body copy, navigation, UI. |
| `--font-mono` | `JetBrains Mono` | Numerical readouts, technical labels ("brand_match", mineral values, FAQ Q.01). |

Display weights typically 400 (regular) or 500 (medium); avoid heavy weights —
editorial typography is set lighter than SaaS typography.

## Spacing

Standard `--spacing-*` tokens follow an 8pt grid: 0, 4, 8, 12, 16, 24, 32, 48, 64, 96, 128, 192 (px).

## Motion

Three named easings cover most needs:

```css
var(--ease-out)    /* cubic-bezier(0.16, 1, 0.3, 1)        — most reveals  */
var(--ease-snap)   /* cubic-bezier(0.34, 1.56, 0.64, 1)    — overshoot     */
var(--ease-fluid)  /* cubic-bezier(0.65, 0, 0.35, 1)       — symmetrical   */
```

Standard durations: `--animation-duration-fast` 150ms, `--animation-duration-DEFAULT` 250ms, `--animation-duration-slow` 350ms.

## Shadows

Three editorial shadows tuned for paper-on-paper:

```css
var(--shadow-paper)   /* 0 1px 2px rgba(21,24,42,0.06)             — subtle card lift */
var(--shadow-soft)    /* 0 20px 60px -20px rgba(21,24,42,0.18)      — phone/float card */
var(--shadow-deep)    /* 0 50px 120px -30px rgba(21,24,42,0.32)     — hero device */
```

## Regenerating tokens

The auto-generated palette comes from the design-system skill. To re-run with a
different brand color or style:

```
cd <project root>/.claude/skills/ui-design-system/scripts
python3 design_token_generator.py "#3D6FB8" classic css > tokens.css
python3 design_token_generator.py "#3D6FB8" classic json > tokens.json
```

Other style presets: `modern`, `playful`. Other formats: `json`, `scss`.

**After regenerating, re-add the editorial brand layer at the top of `tokens.css`**
(the script overwrites everything). The editorial choices are not derivable from
the algorithm.

## How `index.html` uses these

The live page (`index.html`) currently inlines its CSS variables in the
`<style>` block rather than importing `tokens.css`. This keeps the single-file
landing fast and dependency-free. If/when the site grows beyond one page, swap
to `<link rel="stylesheet" href="tokens.css">` and reference variables by name.
