# Cozendagen Design System Specification

This is the canonical reference for the Cozendagen visual identity. When any rule stated here conflicts with a CSS comment, a styleguide label, or an older document, this file wins. Hand this to any tool that will produce web pages, emails, PDFs, or print material for Cozendagen.

The companion files are a visual styleguide (`styleguide.html`), a component library (`COMPONENTS.md`), a CSS implementation (`assets/cozendagen.css`), an icon library (`assets/folk-icons.css` + `ICONS.md`), and a set of pre-themed SVG assets under `assets/icons/`.

---

## 1. Palette

Seven colours. No red, ever. No dark neutral (no black, no charcoal, no slate). Nothing outside these seven may be introduced.

### Primary — the four bold accents

| Name | Hex | CSS token |
|---|---|---|
| Flame | #DBA80D | `--cz-gold` |
| Valentine | #CD3684 | `--cz-magenta` |
| Sunset | #DE8426 | `--cz-orange` |
| Dusk | #14607F | `--cz-teal` |

### Tertiary — warm neutrals and grounds

| Name | Hex | CSS token |
|---|---|---|
| Snow | #F3E6D8 | `--cz-cream` |
| Toffee | #5C3317 | `--cz-maroon` |
| Bread | #D9A66A | `--cz-camel` |

### Semantic roles

- **Default ink on snow:** dusk (`#14607F`, 5.69:1 contrast).
- **Muted text:** dusk at 72% alpha (`--cz-ink-soft`). This is not an eighth colour — it keeps the palette at seven.
- **Borders and outlines:** toffee (`#5C3317`). Softer border: toffee at 28% alpha.
- **Accent on dark grounds:** flame replaces dusk for links and emphasis when the band is dusk or valentine.
- **Scrim / modal backdrop:** toffee at 82% alpha. Never black — there is no dark neutral.
- **Error state:** sunset. On dark bands (dusk, valentine), error flips to flame for contrast.
- **Success state:** dusk. On dark bands, success flips to snow.

### Contrast matrix (WCAG 2.1 AA)

Body text (4.5:1) pairings that pass: dusk on snow (5.69:1), toffee on snow (10.06:1), toffee on bread (5.65:1), toffee on flame (5.65:1).

Pairings that work for large text / display only (3:1): valentine on snow (3.84:1), sunset on toffee (4.37:1), dusk on bread (3.19:1), dusk on flame (3.20:1).

**Sunset and valentine are accent grounds** — body copy on them goes inside a snow panel. Flame similarly fails AA for body text against snow.

---

## 2. Typography

Two typefaces. Two weights. Nothing else.

### Typefaces

- **Germania One** — display headings. One weight (400). Decorative skeleton, uncomfortable below ~22px. Used for h1 and h2 only.
- **Futura** (web substitute: Jost via Google Fonts) — everything else. Two weights only: **400 (regular)** and **700 (bold)**. No 300, no 500, no 600, no 800. This is a hard rule.

### Heading hierarchy

| Level | Font | Weight | Case | Notes |
|---|---|---|---|---|
| h1 | Germania One | 400 | uppercase | Display headings |
| h2 | Germania One | 400 | sentence case | Deliberate break from all-caps for visual distinction |
| h3 | Futura/Jost | 700 | uppercase, tracked | A visual bridge between display and body tiers |
| h4 | Futura/Jost | 700 | normal | |
| h5 | Futura/Jost | 700 | normal | |
| h6 | Futura/Jost | 700 | uppercase, tracked | |

### Body copy

Futura/Jost 400 at 17px (Jost runs small, which is why the base is 17 not 16). Line height 1.5 (`--cz-leading-body`), max-width 55ch (`--cz-measure`). Lead paragraphs: larger, tighter leading, capped at 60ch.

### Eyebrow

The small tracked label above a heading. Always Futura/Jost 700, uppercase, tracked. Never Germania One.

---

## 3. Layout: the band rule

A page is a vertical stack of full-width bands. Two ground types, alternated:

- **Light bands:** snow background. Ink is dusk (default), valentine, or sunset. Toffee is for borders and structural accents, never headline ink on its own.
- **Colour bands:** dusk, valentine, flame, or sunset background. Snow text.

**Never use bread or toffee as a band background.**

All band content is centred by default. Body copy is set at max-width (68ch) and centred within the container.

### Outlines, not shadows

The brand is flat colour with confident outlines (scherenschnitte / paper-cut aesthetic). Surfaces are separated by 2px borders, never by drop shadows or elevation. There is exactly one `box-shadow` in the system and it is a focus ring. Do not add more.

---

## 4. Buttons

Four types, three sizes. **One primary button per view.**

- **Primary:** toffee background, snow text. Hover inverts to snow-on-toffee (not a darkened shade — there is no darker brown in the palette). Contrast stays at 10:1 in both states.
- **Secondary:** ghost button with a toffee border. Hover fills with snow.
- **Flame:** flame background, toffee text. For the main call to action when you want warmth.
- **Tertiary:** text-only, no border. For low-emphasis actions.

On dark bands (dusk, valentine), secondary and tertiary flip to snow-outlined / snow-text variants.

---

## 5. Cards

Bordered containers with an optional icon, heading, and body. Three variants:

- **Default:** snow fill, toffee border.
- **Filled:** same as default but explicit.
- **Link card:** the whole card is an anchor. Hover turns the border flame.

Badge cards are a variant: a circular badge image above a heading, centred, for essentials grids.

---

## 6. Icons — folk art library

58 flat folk-art SVG graphics in the scherenschnitte (paper-cut) style. No gradients, no strokes, no shading.

### The three load-bearing rules

1. **Never use an emoji as an icon, anywhere, for any reason.** The library exists so you never have to. If no graphic fits, leave a placeholder and flag it — an emoji is never the fallback.
2. **Never write inline `<svg>`, `<symbol>`, `<use>`, or `<path>` markup.** A sprite-based approach was evaluated and rejected. `<img src>` is the only integration point.
3. **Never edit the SVGs to change colour.** Colour comes from choosing a different colourway folder. If a needed combination doesn't exist, say so rather than improvising.

### Integration

```html
<img src="assets/icons/<colourway>/<slug>.svg" alt="" class="folk-icon">
```

### Colourways

Eight folders, one per palette colour plus `full/` (original seven-colour artwork):

| Folder | Body colour | Best on | Soft but usable on |
|---|---|---|---|
| `full/` | seven-colour | snow, bread, white | — |
| `maroon/` | toffee | bread, snow, sunset, flame, white | dusk |
| `teal/` | dusk | bread, snow, flame, white | toffee, valentine |
| `magenta/` | valentine | snow, white | dusk, sunset |
| `orange/` | sunset | toffee | valentine |
| `camel/` | bread | dusk, toffee | snow |
| `gold/` | flame | dusk, toffee | snow |
| `cream/` | snow | dusk, toffee, valentine | bread, flame |

**Never place `full/` on a saturated ground** — the artwork contains flame, sunset, valentine, and dusk, which will collide with the background.

`camel/` and `gold/` are nearly identical in luminance, so neither works on the other's ground and both go soft on snow — they need a dusk, toffee, or valentine section.

### The campfire rule

The campfire icon contains both logs and flames. **Logs and flames must never be the same colour.** When placing the campfire, ensure the colourway provides enough contrast between its structural elements. This principle extends to any icon with functionally distinct parts that should read separately.

### The emblem

`assets/icons/full/emblem.svg` is the Cozendagen seal. **Fixed colours, never recoloured** — only the `full/` version exists. Its snow disc carries its own ground, so it sits on any palette colour. **160px is a hard floor** — below that the curved wordmark is unreadable. Use for header, footer, and print. Not an inline icon.

### Circular badges

Five self-contained disc graphics (`badge-house`, `badge-moose`, `badge-socks`, `badge-sweater`, `badge-teacup`). The circle is part of the artwork. In `full/` each disc is a different palette colour, which makes a row work as a set without further choices. Floor: 48px.

---

## 7. Folk circles — icons inside coloured discs

A folk circle is an icon centred inside a filled palette disc. The circle supplies its own visual ground, so the icon colourway contrasts with the circle's fill, not with the band behind the circle.

### Pair guide

| Circle background | Icon colourway |
|---|---|
| Dusk | cream |
| Valentine | cream |
| Toffee | cream |
| Flame | maroon |
| Snow | teal |
| Sunset | maroon |

Default size: 160px. In-band size: 136px. Never below 100px — the folk detail degrades.

The icon sits at 44% of the disc diameter. One object illustration per section is usually plenty — they are visually loud.

### Per-icon centering corrections

Every icon has asymmetric transparent padding in its SVG. Geometric centering looks off. Each icon requires its own translate nudge and sometimes a size override. These are defined in `cozendagen.css` as `.cz-folk-circle--<slug>` classes. The corrections exist for: kettle, teacup, coffee-pot-01, coffee-pot-02, moka-pot, typewriter, campfire, stove (also 30% smaller), slippers, sweater (also 20% bigger), open-book (also 20% bigger), house (25% smaller for 01/02), house-03, moose (15% bigger), tree (20% smaller), tree-02, tree-03, sewing-machine.

**Never rely on pure CSS centering for folk icons.** Every placement needs its correction class applied. If an icon has no correction class defined, visually verify placement and add one.

---

## 8. Corner ornaments

Two botanical flourishes (`corner-01`, `corner-02`) drawn for the top-left corner. Four mirrored copies surround a block. Applied via the `.cz-band--cornered` class.

### Rules

- **Corners appear only on snow bands**, coloured to match the headline ink. On colour bands (dusk/valentine/flame/sunset), use snow-coloured corners.
- **Corners and patterns are mutually exclusive.** Never combine corner ornaments and pattern textures on the same band.
- Corners are at z-index 1; text flows over them at z-index 2. Text is not pushed away from corners — it overlaps naturally.
- At mobile (≤640px), corners scale down to ~110px and the inset reduces.
- Never use toffee corners unless that IS the headline colour.

---

## 9. Pattern textures

Four seamless raster tiles (600px, with @2x for retina). Pattern colourways name the *ink* colour, not the ground — the ground is always baked in (snow for most, dusk for the `cream/` folder).

### Pattern-ground rule

**Never place bare text directly on a pattern background.** Always use the snow panel (`.cz-pattern-ground__panel`) for body copy over any pattern. The panel's border and text colour automatically match the parent band's background fill via `--cz-band-bg`.

### Pattern opacity

Patterns are rendered at low opacity (10–18%) as subtle texture behind content. The pattern-ground component uses `--cpg-opacity` to control this.

### URL resolution gotcha (web implementation)

When setting `--cpg-src` via inline style and consuming it in an external CSS file, the `url()` resolves relative to the CSS file, not the HTML document:

- **Correct:** `style="--cpg-src:url('patterns/teal/pattern-01.png')"`
- **Wrong:** `style="--cpg-src:url('assets/patterns/teal/pattern-01.png')"`

---

## 10. Photography treatments

Five approved treatments, each serving a distinct layout role. Photos come from past Cozendagen events.

### 10a. Showstopper (full-bleed hero)

Full-viewport photo backgrounds. Two height variants: tall (80vh min 500px) and mid (50vh min 360px). Snow text on a dark scrim. Two scrim options: bottom gradient (for text at the foot) and centre vignette (for centred text).

### 10b. Duotone bands

Photo desaturated and tinted with a palette colour via multiply blend, plus a dark scrim (35% black) for text legibility. Three approved tints: toffee, bread, valentine. Follows all normal band layout rules.

**Never add folk circles, icons, or corner ornaments to a duotone photo band.** Too busy.

### 10c. Storyteller (arch trio)

Three arch-shaped photos side by side, each with a small headline and one line of body copy underneath. For apples-to-apples comparison of three similar items. Always used in a group of three. The arch has a bread border. Extra spacing between the photo bottom and the headline matches the headline-to-body gap.

### 10d. Gallery

Two sub-types:

- **Split:** a photo and a text block side by side (50/50). Reversible. Text side can be snow, dusk, toffee, or bread.
- **Asymmetric editorial grid:** a CSS grid with one hero slot, one tall slot, one wide slot, and two small slots. Gap: 8px. Rounded corners on all items.

### 10e. Accent (pattern-ink border)

A square photo framed by a band of pattern tile. Two sizes only: **medium (280px)** and **large (360px)**. No small size — it's too small for the pattern to read. Border is approximately 32px of pattern tile.

---

## 11. Frames

Five portrait border compositions with an empty centre for wrapping content. The content box is small relative to the frame (27–52% of width). Frames suit a pull quote, a short heading, or a small image. **They will not hold body copy.** One frame per page at most — they are the largest files in the kit (300–440 KB each).

---

## 12. Ornaments

Eight decorative florals: dividers, garlands, sprays, and a mark (tiny tulip). Usage:

- **Section dividers:** `divider-01` centred at 200–320px wide.
- **Heavy breaks:** `garland-01/02/03` at 320–520px.
- **Bullet glyphs / list markers:** `mark-01` at 20–24px.
- **Corner flourishes / card headers:** `spray-01/02/03` at 48–120px.
- **Above a heading:** `garland-03` (arched) over centred display type.

Ornaments are quieter than object illustrations and can repeat. One object illustration per section is plenty.

---

## 13. Forms and validation

Inputs have a toffee border, snow fill, Futura/Jost body text. General focus ring: 3px `currentColor` outline with 2px offset (adapts to whatever ground it sits on). Form inputs also get a dusk focus glow (`box-shadow: 0 0 0 3px rgba(20,96,127,0.35)`) — this is the only `box-shadow` in the system besides the focus outline.

- **Error:** sunset border (thickened), sunset helper text. On dark bands, error flips to flame.
- **Success:** dusk helper text. On dark bands, success flips to snow.
- **Placeholders:** dusk at 72% alpha.

---

## 14. Sizing and spacing

The system uses a geometric spacing scale from 4px (`--cz-1`) to 128px (`--cz-10`). Common values: `--cz-4` (16px), `--cz-5` (24px), `--cz-6` (32px), `--cz-7` (48px), `--cz-8` (64px), `--cz-9` (96px), `--cz-10` (128px).

Border radius: `--cz-radius-sm` (3px), `--cz-radius` (5px), `--cz-radius-lg` (10px), `--cz-radius-pill` (999px).

Border widths: `--cz-border` (2px), `--cz-border-thick` (3px).

Layout tokens: `--cz-measure` (55ch body max line length), `--cz-container` (max content width), `--cz-gutter` (inline padding).

---

## 15. Callouts and pull quotes

### Callouts

Bordered asides with a left rule and an optional icon slot. No red in this palette, so the usual colour conventions are adjusted: sunset carries error, dusk carries information/success, flame carries emphasis.

### Pull quotes

Large italic text with a flame left border. Citation below in muted text. On dark bands, the accent stays flame and the citation inherits the band's text colour at reduced opacity.

---

## 16. Tables

Toffee header with bold text and a thick bottom border. Body rows separated by soft (28% toffee) horizontal rules. Left-aligned by default.

---

## 17. Modals and dialogs

Toffee scrim at 82% alpha (never black). Modal box has snow fill, toffee border, rounded corners. Close button in the top-right corner.

---

## 18. Navigation and footer

### Header / Navigation

Snow background, dusk text, with a soft bottom border. Mobile: hamburger toggle reveals a vertical menu.

### Footer

Toffee background, snow text. Flame links and accents. Footer headings use Futura/Jost 700.

---

## 19. Additional components

### Tabs

`.cz-tabs` wraps a role="tablist" of `.cz-tab` buttons that toggle `.cz-tabpanel` visibility. Active tab gets a toffee border, snow fill, and dusk text. Inactive tabs have muted text.

### Accordion

Native `<details>`/`<summary>` styled via `.cz-accordion`. Summary gets a flame chevron marker. Open state shows the panel with standard body-copy styling.

### Timeline

`.cz-timeline` is a vertical sequence of events. A soft toffee left-hand rule connects `.cz-timeline__date` and `.cz-timeline__title` entries. Mark-01 tulip glyphs (toffee colourway) serve as dot markers; override via `--cz-marker`.

### Pagination and breadcrumbs

`.cz-pagination` is a row of page numbers. Active page: toffee fill, snow text. `.cz-breadcrumbs` is a slash-separated path; separators are flame.

### Tooltips

`.cz-tooltip` wraps a trigger element and a `.cz-tooltip__bubble` (toffee background, snow text, small radius). Appears on hover/focus.

### Figures and captions

`.cz-figure` wraps an image and a `<figcaption>`. Images get `--cz-radius-lg` corners. Optional `.cz-figure--bordered` adds a toffee border. Captions use muted text (`--cz-ink-soft`). On dark bands, captions inherit the band's text colour at reduced opacity.

### Divider rule

`.cz-divider-rule` is a centred ornament (such as mark-01) flanked by two horizontal rules. Width controlled via `--cz-divider-w`. The rules use `currentColor` at 45% opacity on dark bands.

### Ornament bullet list

`.cz-list--ornament` replaces standard bullets with the mark-01 tulip graphic via `::before` pseudo-element. Customise the colourway via `--cz-bullet`.

---

## 20. Icon sizing floors by category

Minimum legible sizes differ by category. Below these, the artwork degrades.

| Category | Floor | Notes |
|---|---|---|
| `mark` | 20px | Purpose-built for bullet glyphs, list markers, timeline dots |
| `ornament` sprays | 24px | Sprigs stay legible small |
| `ornament` garlands/dividers | 120px wide | They are wide and low; size by width |
| `corner` | 40px | Solid silhouettes, they hold up small |
| `badge` | 48px | Self-contained discs |
| `emblem` | 160px | Contains curved lettering — a hard floor, not a preference |
| `nature` (trees) | 32px | Plain silhouettes, they scale down well |
| `apparel`, `furniture` | 48px | Simple shapes, but surface motifs need the room |
| `vessel`, `book`, `machine`, `fire-light`, `building`, `animal` | 48px | Below this the floral detail turns to mush |

For anything smaller than 20px, use CSS shapes — no artwork in this set goes lower.

---

## 21. Frame safe areas

Each frame has a different usable content box. Set the four inset custom properties when using `.folk-frame`:

| Frame | Aspect | Content area | Inset properties |
|---|---|---|---|
| `frame-01` | 0.85 | 52.3% x 33.7% | `--fi-t:28.5%; --fi-r:23.7%; --fi-b:37.8%; --fi-l:24.0%` |
| `frame-02` | 0.81 | 40.7% x 37.4% | `--fi-t:30.3%; --fi-r:29.4%; --fi-b:32.3%; --fi-l:29.9%` |
| `frame-03` | 0.82 | 34.5% x 43.9% | `--fi-t:30.1%; --fi-r:32.7%; --fi-b:26.0%; --fi-l:32.8%` |
| `frame-04` | 0.77 | 47.0% x 27.0% | `--fi-t:27.7%; --fi-r:26.3%; --fi-b:45.4%; --fi-l:26.7%` |
| `frame-05` | 0.76 | 47.2% x 33.1% | `--fi-t:29.2%; --fi-r:26.2%; --fi-b:37.7%; --fi-l:26.6%` |

An 800px-wide frame gives roughly a 330px content box. Frames suit a pull quote, a short heading, or a small image — never body copy.

---

## 22. Icon-specific gotchas

These apply when choosing colourways and placing specific icons:

- **Candle:** in two-value colourways, reduces to a jar silhouette; the label motif largely merges. Use `full/candle.svg` where that detail matters.
- **Typewriter-01/02:** in light-bodied colourways (bread, flame, sunset, snow) both ornament colours are dark, so the paper sheet reads as dark. Graphically fine, semantically a stylisation.
- **Teacups and kettles read as families.** Grouping them is deliberate; mixing one teacup among unrelated objects breaks the pattern.
- **garland-02 and divider-01** use flame in `full/`; on a flame ground, use the `cream/` colourway instead.
- **tree-01/02/03** are single-colour silhouettes by design. `full/` gives one flat colour each (dusk, toffee, flame respectively).
- **Candle jar and wax** share the body colour in single-colour colourways; `full/` distinguishes them.
- **armchair-01/02 and stove-01** use bread for upholstery seams and flue where the source art used a second dusk. The palette has no second dusk, so these read as piping and contrast panels.

---

## 23. Toffee hex note

ICONS.md uses `#5B2226` for toffee (the original traced colour). The CSS design system uses `#5C3317` (a warmer brown chosen for the web implementation). These are different colours. The CSS value (`#5C3317`) is authoritative for all new production work. ICONS.md's value reflects the source artwork tracing; the SVGs themselves use the CSS-authoritative value.

---

## 24. AI tool-specific rules

These apply when an AI assistant is generating Cozendagen content:

1. **Never open files in `assets/icons/`.** They contain ~2 MB of path data that will exhaust a context window. Select graphics from the tables in ICONS.md or from `icons.json`.
2. **Never read SVG source code.** Choose a colourway folder and slug, write one `<img src>` line.
3. **Always apply the per-icon centering class** when placing an icon in a folk circle. Check cozendagen.css for `.cz-folk-circle--<slug>`.
4. **Always verify pattern URLs** resolve relative to the CSS file, not the HTML document (see §9 URL resolution gotcha).

---

## 25. CSS custom property reference

Key tokens another tool needs to generate valid markup:

**Palette:** `--cz-teal`, `--cz-camel`, `--cz-maroon`, `--cz-cream`, `--cz-magenta`, `--cz-orange`, `--cz-gold`

**Semantic:** `--cz-bg`, `--cz-ink`, `--cz-ink-soft`, `--cz-ink-invert`, `--cz-accent`, `--cz-accent-warm`, `--cz-line`, `--cz-line-soft`, `--cz-scrim`

**Type scale:** `--cz-text-xs`, `--cz-text-sm`, `--cz-text-base`, `--cz-text-md`, `--cz-text-lg`, `--cz-text-xl`, `--cz-text-2xl`, `--cz-text-3xl`, `--cz-text-4xl`

**Leading:** `--cz-leading-tight`, `--cz-leading-snug`, `--cz-leading-body`

**Tracking:** `--cz-tracking-wide`

**Font stacks:** `--cz-font-display` (Germania One), `--cz-font-body` (Futura/Jost)

**Spacing:** `--cz-1` through `--cz-10`

**Radius:** `--cz-radius-sm`, `--cz-radius`, `--cz-radius-lg`, `--cz-radius-pill`

**Borders:** `--cz-border`, `--cz-border-thick`

**Motion:** `--cz-ease`, `--cz-fast`, `--cz-slow`

**Layout:** `--cz-measure`, `--cz-container`, `--cz-gutter`, `--cz-stack-gap`, `--cz-grid-min`

**Band context:** `--cz-band-bg` (set by each band colour variant; consumed by pattern-ground panels)

**Components:** `--cfc-bg` and `--cfc-size` (folk circle), `--cpg-src` and `--cpg-opacity` (pattern ground), `--cpa-pattern` (photo accent), `--cz-corner-size`, `--cz-badge-size`, `--cz-bullet`, `--cz-marker`, `--cz-divider-w`, `--cz-tab-surface`

---

## 26. Mutual exclusions and "never do" rules

These are the hard constraints. Violating any of them breaks the visual system.

1. **No red, ever.** Not for errors, not for alerts, not for anything.
2. **No dark neutral.** No black, charcoal, slate, or near-black backgrounds. Scrim uses toffee at 82%.
3. **No bread or toffee as a band background.** They serve structural roles only.
4. **No font weights other than 400 and 700.** No light, no medium, no semibold.
5. **No drop shadows or elevation.** Outlines only (scherenschnitte).
6. **No emoji.** The icon library exists for this purpose.
7. **No inline SVG.** `<img src>` only.
8. **No editing SVGs to change colour.** Use a different colourway folder.
9. **Corners and patterns never appear on the same band.**
10. **No bare text on pattern backgrounds.** Always use the snow panel.
11. **No folk circles, icons, or corner ornaments on photo bands.**
12. **No body copy inside frames.** Pull quotes and short headings only.
13. **Emblem never below 160px and never recoloured.**
14. **Folk circles never below 100px.**
15. **One primary button per view.**
16. **One object illustration per section.** Ornaments are quieter and can repeat.
17. **`full/` colourway never on a saturated ground.**
18. **Campfire rule: logs and flames must never be the same colour.** Extend this to any icon with functionally distinct parts.
19. **Photo accent border: medium and large only.** No small.

---

## 27. Applying the system beyond web

### Email

Same palette, same typography hierarchy (fall back to Arial/Helvetica where Futura/Jost is unavailable). Bands become stacked table rows with inline background colours. Patterns and photo treatments may be used as background images where the email client supports them, with a solid-colour fallback. Corner ornaments are impractical in email — skip them. Folk circles work as inline images.

### PDF and print

Same palette (convert to CMYK for offset; the hex values are the screen reference). Germania One and Futura are the print fonts — no Jost substitution needed. All spacing, sizing, and typographic rules apply. Patterns tile at 600px at print resolution. Corner ornaments work well in print. Bleed photos get the same duotone treatments.

### Slide decks

One band per slide. Alternate snow and colour grounds. One object illustration per slide maximum. Emblem on the title slide and closing slide. Typography hierarchy applies: Germania One for titles, Futura bold for subtitles, Futura regular for body.

---

## 28. File inventory

| File | Purpose |
|---|---|
| `assets/cozendagen.css` | Full design system CSS. Load after Google Fonts link. |
| `assets/folk-icons.css` | Icon sizing helpers, folk-circle, folk-frame, folk-corners, folk-pattern utilities. |
| `assets/icons/<colourway>/<slug>.svg` | Pre-themed icon files. 8 colourways x 58 graphics. |
| `assets/patterns/<colourway>/pattern-01..04.png` | Seamless pattern tiles, 600px. `@2x` variants for retina. |
| `assets/photos/` | Sample event photos for demos. |
| `styleguide.html` | Visual demo page showing all components in context. |
| `ICONS.md` | Icon library reference: slugs, colourways, sizing, gotchas. |
| `COMPONENTS.md` | Component library: markup patterns, anatomy, composition recipes. |
| `DESIGN-SYSTEM.md` | This file — the canonical spec. |
