# Cozendagen Component Library

This is the copy-paste reference for every component in the Cozendagen design system. DESIGN-SYSTEM.md remains the canonical spec for rules and constraints. This file answers "how do I build it?" while DESIGN-SYSTEM.md answers "what are the rules?" Sections here are grouped by component type, not by DESIGN-SYSTEM.md section number — cross-references point to the relevant spec sections where needed.

Each component is described in medium-agnostic terms first (anatomy, variants, when to use it), then gives the web markup pattern. For slides, print, email, or other formats, follow the anatomy description and consult DESIGN-SYSTEM.md §27 for medium-specific adaptations.

**Conventions used below:**

- `{colour}` = a CSS class suffix: `cream`, `teal`, `magenta`, `gold`, `orange`
- `{colourway}` = an icon folder name: `full`, `maroon`, `teal`, `magenta`, `orange`, `camel`, `gold`, `cream`
- `{slug}` = an icon filename without extension (see ICONS.md for the full list)
- Token references like `--cz-teal` are CSS custom properties defined in `cozendagen.css`

---

## 1. Palette swatches

Not a runtime component. Reference only — use when building colour documentation or brand sheets.

| Name | Hex | Role | CSS token |
|---|---|---|---|
| Flame | #DBA80D | Primary accent | `--cz-gold` |
| Valentine | #CD3684 | Primary accent | `--cz-magenta` |
| Sunset | #DE8426 | Primary accent | `--cz-orange` |
| Dusk | #14607F | Primary accent / default ink | `--cz-teal` |
| Snow | #F3E6D8 | Tertiary / default ground | `--cz-cream` |
| Toffee | #5C3317 | Tertiary / borders & dark ground | `--cz-maroon` |
| Bread | #D9A66A | Tertiary / warm neutral | `--cz-camel` |

Semantic tokens: `--cz-ink` (dusk), `--cz-ink-soft` (dusk at 72%), `--cz-bg` (snow), `--cz-line` (toffee), `--cz-line-soft` (toffee at 28%), `--cz-accent` (dusk, flips to flame on dark bands), `--cz-accent-warm` (flame), `--cz-scrim` (toffee at 82%).

---

## 2. Typography

### Anatomy

Two typeface families, two weights (400, 700). Germania One for display headings (h1, h2). Futura / Jost for everything else.

### Heading classes

| Element | Class | Font | Weight | Case |
|---|---|---|---|---|
| Display hero | `.cz-hero-title` | Germania One | 400 | uppercase |
| h1 | `.cz-display` (or bare `<h1>`) | Germania One | 400 | uppercase |
| h2 | — | Germania One | 400 | sentence |
| h3 | — | Jost | 700 | uppercase, tracked |
| h4 | — | Jost | 700 | normal |
| h5 | — | Jost | 700 | normal |
| h6 | — | Jost | 700 | uppercase, tracked |

### Text utilities

| Class | Purpose |
|---|---|
| `.cz-eyebrow` | Small tracked label above a heading. Jost 700, uppercase, tracked. |
| `.cz-lead` | Opening paragraph. Larger size, tighter leading, max 60ch. |
| `.cz-meta` | Captions, timestamps, helper text. Small, muted. |
| `.cz-small` | Small text. |

### Web markup

```html
<span class="cz-eyebrow">Section label</span>
<h2>Heading</h2>
<p class="cz-lead">Opening paragraph — larger, tighter leading.</p>
<p>Body copy at 17px.</p>
<p class="cz-meta">Caption or timestamp.</p>
```

### Non-web notes

For slides: Germania One titles, Futura bold subtitles, Futura regular body. For print: same fonts (no Jost substitution needed). For email: fall back to Arial/Helvetica where Futura/Jost is unavailable.

---

## 3. Bands

### What it is

A full-width horizontal section that forms the basic building block of page layout. A page (or slide, or print sheet) is a vertical stack of bands.

### Anatomy

1. **Background fill** — a palette colour
2. **Container** — centred content area (max-width constrained)
3. **Optional:** eyebrow label, heading, body copy, illustration, buttons
4. **Optional decorations:** corner ornaments OR pattern texture (never both)

### Variants

| Variant | Class | Background | Text colour | Notes |
|---|---|---|---|---|
| Snow (default) | `.cz-band--cream` | Snow | Dusk | The base of the system |
| Snow / valentine ink | `.cz-band--cream--magenta` | Snow | Valentine | Large text only |
| Snow / sunset ink | `.cz-band--cream--orange` | Snow | Sunset | Display headings only |
| Dusk | `.cz-band--teal` | Dusk | Snow | Body copy passes AA |
| Valentine | `.cz-band--magenta` | Valentine | Snow | Large text; body in panel |
| Flame | `.cz-band--gold` | Flame | Snow | Accent ground |
| Sunset | `.cz-band--orange` | Sunset | Snow | Accent ground |

Padding modifiers: `.cz-band--tight` (less), `.cz-band--tall` (more).

Dark-context hook: `.cz-band--dark` — add this class to any custom dark surface that isn't dusk or valentine. It flips links, buttons, form labels, validation, captions, and other sub-components to their dark-band variants (snow outlines, flame accents, etc.).

### Web markup

```html
<section class="cz-band cz-band--{colour}">
  <div class="cz-container">
    <span class="cz-eyebrow">Section label</span>
    <h2>Heading</h2>
    <p>Body copy.</p>
  </div>
</section>
```

### Non-web notes

For slides: one band per slide. Alternate snow and colour grounds. For print: bands become horizontal sections with the same colour fills. For email: bands become stacked table rows with inline background colours.

---

## 4. Buttons

### Anatomy

1. **Container** — pill-shaped with border-radius
2. **Label** — Jost 700 text
3. **Optional:** icon (folk art mark, left of label)

### Variants

| Variant | Class | Fill | Text | Hover |
|---|---|---|---|---|
| Primary | `.cz-btn--primary` | Toffee | Snow | Inverts to snow/toffee |
| Secondary | `.cz-btn--secondary` | Transparent | Toffee | Fills toffee, text snow |
| Flame | `.cz-btn--gold` | Flame | Toffee | Fills toffee, text flame |
| Tertiary | `.cz-btn--tertiary` | None | Toffee | Underline thickens |

Sizes: `.cz-btn--sm`, default (medium), `.cz-btn--lg`, `.cz-btn--block` (full-width).

On dark bands (dusk, valentine): secondary and tertiary auto-flip to snow outlines/text.

### Web markup

```html
<!-- Basic -->
<button class="cz-btn cz-btn--primary">Label</button>

<!-- With icon -->
<button class="cz-btn cz-btn--primary">
  <img src="assets/icons/cream/mark-01.svg" alt="">Label
</button>

<!-- Button row (centres and wraps) -->
<div class="cz-btn-row">
  <button class="cz-btn cz-btn--primary">Primary</button>
  <button class="cz-btn cz-btn--secondary">Secondary</button>
</div>
```

### Non-web notes

For slides and print: render as a rounded rectangle with the same fill/text colour pairing. Maintain the one-primary-per-view rule.

---

## 5. Cards

### What it is

A bordered container for a unit of content — an "essential", a feature, or a linked item.

### Anatomy

1. **Border** — toffee, 2px
2. **Optional icon** — folk art illustration above the title
3. **Title** — h4
4. **Body** — paragraph(s)

### Variants

| Variant | Class | Fill | Border |
|---|---|---|---|
| Default | `.cz-card` | Transparent (takes band ground) | Toffee |
| Filled | `.cz-card--filled` | Snow | Toffee |
| Link card | `a.cz-card` | Same as default | Flame on hover |

### Web markup

```html
<div class="cz-grid cz-grid--3">
  <div class="cz-card">
    <img class="folk-icon" src="assets/icons/{colourway}/{slug}.svg" alt="">
    <h4 class="cz-card__title">Title</h4>
    <div class="cz-card__body"><p>Description.</p></div>
  </div>
</div>
```

### Badge cards

A variant with a circular badge image (from the badge set) centred above a heading. For "essentials" grids.

```html
<div class="cz-grid" style="--cz-grid-min:180px">
  <div class="cz-badge-card">
    <img src="assets/icons/full/badge-house.svg" alt="">
    <h4 class="cz-no-margin">Title</h4>
    <p class="cz-meta cz-mb-0">Subtitle</p>
  </div>
</div>
```

### Non-web notes

For slides: render as a bordered box with the icon centred above the title. For print: same — toffee border, snow fill. Cards in a row should be equal width. Always use the folk icon library, never emoji.

---

## 6. Folk icons

### What it is

58 flat folk-art SVG illustrations in eight pre-themed colourways. Loaded as `<img>` elements — never inline SVG.

### Integration

```html
<img src="assets/icons/{colourway}/{slug}.svg" alt="" class="folk-icon">
```

### Size classes

| Class | Width |
|---|---|
| `.folk-icon--sm` | 80px |
| `.folk-icon` (default) | 120px |
| `.folk-icon--md` | 120px |
| `.folk-icon--lg` | 200px |
| `.folk-icon--xl` | 320px |

### Non-web notes

For slides and print: place the SVG file at the needed size. Respect the minimum size floors from DESIGN-SYSTEM.md §20. Choose the colourway folder that matches the background the icon sits on (see the colourway/ground matrix in DESIGN-SYSTEM.md §6).

---

## 7. Folk circles

### What it is

An icon centred inside a filled palette-colour disc. The circle provides its own visual ground, so the icon colourway contrasts with the circle fill, not with the band behind it.

### Anatomy

1. **Disc** — a round filled shape (palette colour)
2. **Icon** — a folk art SVG sized at 44% of the disc diameter
3. **Per-icon centering class** — corrects for asymmetric SVG padding

### Pair guide

| Circle fill | Icon colourway folder |
|---|---|
| Dusk | `cream/` |
| Valentine | `cream/` |
| Toffee | `cream/` |
| Flame | `maroon/` |
| Snow | `teal/` |
| Sunset | `maroon/` |

### Web markup

```html
<div class="cz-folk-circle cz-folk-circle--{slug}"
     style="--cfc-bg:var(--cz-{colour})">
  <img src="assets/icons/{colourway}/{slug}.svg" alt="">
</div>
```

The `cz-folk-circle--{slug}` class applies the per-icon translate/scale correction. Always include it. If no correction class exists for your icon, visually verify placement and add one.

Default size: 160px. In-band size: 136px (automatic). Override with `--cfc-size`. Never below 100px.

### Non-web notes

For slides and print: draw a filled circle in the palette colour, centre the icon at 44% of the disc diameter. Manually nudge the icon to visual centre — geometric centering will look off for most icons.

---

## 8. Corner ornaments

### What it is

Botanical flourishes placed at the four corners of a band or container. Two designs: `corner-01` (simpler) and `corner-02` (more elaborate).

### Rules

- Only on snow bands (coloured to match headline ink), OR on colour bands (snow-coloured corners)
- Corners and patterns are **mutually exclusive** — never on the same band
- The source SVG is drawn for top-left; the other three are mirrored copies

### Web markup

```html
<section class="cz-band cz-band--cream cz-band--cornered">
  <img class="folk-corner folk-corner--tl" src="assets/icons/{colourway}/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--tr" src="assets/icons/{colourway}/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--br" src="assets/icons/{colourway}/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--bl" src="assets/icons/{colourway}/corner-02.svg" alt="">
  <div class="cz-container">
    <!-- content -->
  </div>
</section>
```

### Standalone corner wrapper

For wrapping smaller content (pull quotes, short headings) outside a band context:

```html
<div class="folk-corners folk-corners--mirror" style="--fc-size:88px">
  <img class="folk-corner folk-corner--tl" src="assets/icons/{colourway}/corner-01.svg" alt="">
  <img class="folk-corner folk-corner--tr" src="assets/icons/{colourway}/corner-01.svg" alt="">
  <img class="folk-corner folk-corner--br" src="assets/icons/{colourway}/corner-01.svg" alt="">
  <img class="folk-corner folk-corner--bl" src="assets/icons/{colourway}/corner-01.svg" alt="">
  <div class="folk-corners__content cz-center">
    <!-- content -->
  </div>
</div>
```

### Non-web notes

For print: corners work well — place at the four corners of the content area. For slides: same approach, scaled to the slide dimensions. For email: skip corners (impractical in most email clients).

---

## 9. Pattern textures

### What it is

A band with a seamless raster tile layered at low opacity (10–18%) as subtle background texture. Body copy always goes inside a snow panel to maintain contrast.

### Anatomy

1. **Band** — the base colour band
2. **Pattern tile** — a 600px seamless PNG, rendered as a `::before` pseudo-element
3. **Snow panel** — a bordered snow rectangle holding body copy

### Web markup

```html
<section class="cz-pattern-ground cz-band cz-band--{colour}"
         style="--cpg-src:url('patterns/{colourway}/pattern-01.png');--cpg-opacity:0.12">
  <div class="cz-container">
    <span class="cz-eyebrow">Label</span>
    <h3>Heading</h3>
    <div class="cz-pattern-ground__panel" style="margin-inline:auto;max-width:54ch">
      <h4 class="cz-no-margin">Panel heading</h4>
      <p class="cz-mb-0">Body copy inside the snow panel.</p>
    </div>
  </div>
</section>
```

**URL resolution:** the `url()` in `--cpg-src` resolves relative to the CSS file, not the HTML document. So use `patterns/...` not `assets/patterns/...`.

### Non-web notes

For print: tile the pattern at 600px at print resolution, at 10–18% opacity. Body copy sits on a snow-filled rectangle. For slides: use the pattern tile as a subtle background fill on the slide ground. Always overlay a snow panel for text.

---

## 10. Photography treatments

Five approved treatments. **No folk circles, icons, or corner ornaments on any photo band.**

### 10a. Showstopper (full-bleed hero)

Full-viewport photo background with a dark scrim for text legibility. Two scrim types: bottom gradient and centre vignette.

```html
<!-- Bottom scrim -->
<section class="cz-hero cz-hero--tall">
  <img src="assets/photos/{filename}" alt="Description">
  <div class="cz-hero__scrim cz-hero__scrim--bottom">
    <h2>Heading</h2>
    <p>Body copy.</p>
  </div>
</section>

<!-- Centre scrim -->
<section class="cz-hero cz-hero--mid">
  <img src="assets/photos/{filename}" alt="Description">
  <div class="cz-hero__scrim cz-hero__scrim--center">
    <h3>Heading</h3>
    <p>Body copy.</p>
  </div>
</section>
```

Heights: `.cz-hero--tall` (80vh, min 500px), `.cz-hero--mid` (50vh, min 360px).

### 10b. Duotone bands

Photo desaturated and tinted with a palette colour via multiply blend. Dark scrim (35% black) layered for text legibility. Three approved tints: toffee, bread, valentine.

```html
<section class="cz-band cz-band--photo cz-band--photo-chocolate">
  <img src="assets/photos/{filename}" alt="Description">
  <div class="cz-container">
    <h2>Heading</h2>
    <p>Body copy — snow text on the duotone.</p>
  </div>
</section>
```

Tint classes: `.cz-band--photo-chocolate` (toffee), `.cz-band--photo-camel` (bread), `.cz-band--photo-magenta` (valentine).

### 10c. Storyteller (arch trio)

Three arch-shaped photos side by side, each with a headline and one line of body copy. For apples-to-apples comparison of three items.

```html
<div class="cz-arch-trio">
  <div class="cz-arch-trio__item">
    <div class="cz-arch-trio__photo">
      <img src="assets/photos/{filename}" alt="Description">
    </div>
    <h3>Title</h3>
    <p>One line of body copy.</p>
  </div>
  <!-- repeat for items 2 and 3 -->
</div>
```

### 10d. Gallery — split

Half photo, half content side by side. Reversible. Content side takes a colour fill.

```html
<!-- Photo left, content right -->
<div class="cz-split cz-split--cream">
  <div class="cz-split__photo">
    <img src="assets/photos/{filename}" alt="Description">
  </div>
  <div class="cz-split__content">
    <h2>Heading</h2>
    <p>Body copy.</p>
  </div>
</div>

<!-- Content left, photo right -->
<div class="cz-split cz-split--teal cz-split--reverse">
  <div class="cz-split__photo">
    <img src="assets/photos/{filename}" alt="Description">
  </div>
  <div class="cz-split__content">
    <h2>Heading</h2>
    <p>Body copy.</p>
  </div>
</div>
```

Content side colours: `.cz-split--cream` (snow), `.cz-split--teal` (dusk), `.cz-split--chocolate` (toffee), `.cz-split--camel` (bread).

### 10e. Gallery — asymmetric editorial grid

Five photos in a CSS grid: one hero, one tall sidebar, one wide, two small.

```html
<div class="cz-photo-grid">
  <div class="cz-photo-grid__item cz-photo-grid__item--hero"><img src="..." alt=""></div>
  <div class="cz-photo-grid__item cz-photo-grid__item--tall"><img src="..." alt=""></div>
  <div class="cz-photo-grid__item cz-photo-grid__item--wide"><img src="..." alt=""></div>
  <div class="cz-photo-grid__item cz-photo-grid__item--small-a"><img src="..." alt=""></div>
  <div class="cz-photo-grid__item cz-photo-grid__item--small-b"><img src="..." alt=""></div>
</div>
```

### 10f. Accent (pattern-ink border)

A square photo framed by a band of pattern tile. Medium (280px) or large (360px) only.

```html
<div class="cz-photo-accent cz-photo-accent--lg"
     style="--cpa-pattern:url(patterns/{colourway}/pattern-02.png)">
  <img src="assets/photos/{filename}" alt="Description">
</div>
```

### Non-web notes

For slides: use showstopper as a title slide background. Duotone works as a full-slide photo treatment. Arch trio and split translate directly — three arched images in a row, or a half-and-half slide layout. For print: same treatments apply. Always include the dark scrim for text legibility on photo backgrounds.

---

## 11. Frames

### What it is

Five decorative portrait border compositions with an empty centre for wrapping content. Content box is small relative to the frame (27–52% of width).

### When to use

Pull quotes, short headings, or small images. **Never body copy.** One per page maximum. Best for social media graphics, posters, and print — not typical web layouts.

### Safe areas

| Frame | Aspect | Content box | Inset properties |
|---|---|---|---|
| `frame-01` | 0.85 | 52% × 34% | `--fi-t:28.5%; --fi-r:23.7%; --fi-b:37.8%; --fi-l:24.0%` |
| `frame-02` | 0.81 | 41% × 37% | `--fi-t:30.3%; --fi-r:29.4%; --fi-b:32.3%; --fi-l:29.9%` |
| `frame-03` | 0.82 | 35% × 44% | `--fi-t:30.1%; --fi-r:32.7%; --fi-b:26.0%; --fi-l:32.8%` |
| `frame-04` | 0.77 | 47% × 27% | `--fi-t:27.7%; --fi-r:26.3%; --fi-b:45.4%; --fi-l:26.7%` |
| `frame-05` | 0.76 | 47% × 33% | `--fi-t:29.2%; --fi-r:26.2%; --fi-b:37.7%; --fi-l:26.6%` |

### Web markup

```html
<div class="folk-frame" style="--fi-t:28.5%;--fi-r:23.7%;--fi-b:37.8%;--fi-l:24.0%">
  <img src="assets/icons/full/frame-01.svg" alt="">
  <div class="folk-frame__content">
    <p>Short quote or heading here.</p>
  </div>
</div>
```

### Non-web notes

For print and social graphics: place the frame SVG, position content within the safe area percentages above. An 800px-wide frame gives roughly a 330px content box. For slides: use as a decorative feature element, one per slide maximum.

---

## 12. Ornaments

### What it is

Eight decorative floral elements: dividers, garlands, sprays, and a tiny tulip mark.

### Usage guide

| Ornament | Role | Recommended size |
|---|---|---|
| `divider-01` | Section divider | 200–320px wide |
| `garland-01`, `garland-02`, `garland-03` | Heavy breaks, festoons | 320–520px wide |
| `garland-03` (arched) | Above a heading | 320–520px wide |
| `spray-01`, `spray-02`, `spray-03` | Corner flourishes, card headers | 48–120px |
| `mark-01` | Bullet glyphs, list markers, timeline dots | 20–24px |

### Web markup — divider

```html
<img class="cz-divider" src="assets/icons/{colourway}/divider-01.svg" alt=""
     style="--cz-divider-w:280px">
```

### Web markup — divider rule (mark flanked by lines)

```html
<div class="cz-divider-rule">
  <img src="assets/icons/{colourway}/mark-01.svg" alt="" style="width:26px">
</div>
```

### Non-web notes

Ornaments are quieter than object illustrations and can repeat freely. Use dividers between sections, garlands as festive separators, sprays as card decorations. The mark-01 tulip is specifically built for bullet-sized use (20px floor).

---

## 13. Forms and validation

### Anatomy

1. **Field wrapper** — `.cz-field`, vertical stack of label → input → help/error
2. **Label** — `.cz-label`, with optional `.cz-label__req` for required indicator
3. **Input** — `.cz-input`, `.cz-textarea`, or `.cz-select`
4. **Help text** — `.cz-help`, muted dusk
5. **Error message** — `.cz-error`, sunset text
6. **Success message** — `.cz-success`, dusk text

### Web markup

```html
<!-- Text input -->
<div class="cz-field">
  <label class="cz-label" for="name">Your name <span class="cz-label__req">*</span></label>
  <input class="cz-input" id="name" type="text" required>
  <p class="cz-help">Help text.</p>
</div>

<!-- Error state -->
<div class="cz-field cz-field--error">
  <label class="cz-label" for="email">Email</label>
  <input class="cz-input" id="email" aria-describedby="err" aria-invalid="true">
  <p class="cz-error" id="err">Error message.</p>
</div>

<!-- Select -->
<div class="cz-field">
  <label class="cz-label" for="city">City</label>
  <select class="cz-select" id="city">
    <option>Option one</option>
  </select>
</div>

<!-- Textarea -->
<div class="cz-field">
  <label class="cz-label" for="msg">Message</label>
  <textarea class="cz-textarea" id="msg"></textarea>
</div>

<!-- Checkbox group -->
<fieldset>
  <legend>What are you bringing?</legend>
  <div class="cz-stack" style="--cz-stack-gap:.75rem">
    <div class="cz-check">
      <input type="checkbox" id="c1">
      <label for="c1">Label</label>
    </div>
  </div>
</fieldset>

<!-- Radio group -->
<fieldset>
  <legend>Event type</legend>
  <div class="cz-stack" style="--cz-stack-gap:.75rem">
    <div class="cz-check">
      <input type="radio" name="kind" id="r1">
      <label for="r1">Option</label>
    </div>
  </div>
</fieldset>
```

### Non-web notes

For print forms: toffee border, snow fill, Futura/Jost labels. Error fields use sunset border. The visual styling (border colour, fill, type) translates directly to any medium.

---

## 14. Layout utilities

### Grid

```html
<!-- Auto-fit grid (responsive columns) -->
<div class="cz-grid">
  <!-- children -->
</div>

<!-- Fixed 2 or 3 columns -->
<div class="cz-grid cz-grid--2"> ... </div>
<div class="cz-grid cz-grid--3"> ... </div>

<!-- Custom minimum column width -->
<div class="cz-grid" style="--cz-grid-min:180px"> ... </div>
```

### Stack (vertical spacing)

```html
<div class="cz-stack">
  <!-- children get uniform vertical spacing -->
</div>

<!-- Custom gap -->
<div class="cz-stack" style="--cz-stack-gap:1.5rem"> ... </div>
```

### Container

```html
<div class="cz-container"> ... </div>
<div class="cz-container cz-container--narrow"> ... </div>  <!-- 760px max -->
<div class="cz-container cz-container--wide"> ... </div>    <!-- 1380px max -->
```

### Utility classes

| Class | Effect |
|---|---|
| `.cz-center` | Centres text and inline elements |
| `.cz-measure` | Max-width 55ch (body copy line length) |
| `.cz-no-margin` | Removes all margins |
| `.cz-mt-0` | Removes top margin |
| `.cz-mb-0` | Removes bottom margin |
| `.cz-visually-hidden` | Screen-reader-only text |
| `.cz-skip` | Skip-to-content link |

---

## 15. Callouts and pull quotes

### Callouts

Bordered asides with a coloured left rule and an optional icon.

| Variant | Class | Border colour | Semantic role |
|---|---|---|---|
| Information | `.cz-callout--info` | Dusk | Neutral notes and asides |
| Emphasis | `.cz-callout--emphasis` | Flame | Worth noticing |
| Important | `.cz-callout--important` | Toffee | Heaviest weight |
| Filled | add `.cz-callout--filled` | — | Snow fill behind content |

```html
<div class="cz-callout cz-callout--info">
  <img src="assets/icons/{colourway}/mark-01.svg" alt="">
  <div>
    <p class="cz-callout__title">Title</p>
    <p class="cz-mb-0">Body text.</p>
  </div>
</div>
```

### Pull quotes

Large italic text with a flame left border. Optional centred variant with a decorative quotation mark.

```html
<!-- Left-aligned -->
<div class="cz-pullquote">
  <blockquote>The quote.</blockquote>
  <cite>Attribution</cite>
</div>

<!-- Centred -->
<div class="cz-pullquote cz-pullquote--centred">
  <blockquote>The quote.</blockquote>
  <cite>Attribution</cite>
</div>
```

### Non-web notes

For slides and print: render callouts as a box with a thick left border in the appropriate colour, with the icon at the left edge. Pull quotes: large italic text with a flame vertical rule.

---

## 16. Tables

### Anatomy

1. **Caption** — optional, above the table
2. **Header row** — toffee text, bold, thick bottom border
3. **Body rows** — separated by soft (28% toffee) horizontal rules
4. **All text left-aligned by default**

```html
<div class="cz-table-wrap">
  <table class="cz-table">
    <caption>Caption</caption>
    <thead>
      <tr><th>Column A</th><th>Column B</th></tr>
    </thead>
    <tbody>
      <tr><td>Data</td><td>Data</td></tr>
    </tbody>
  </table>
</div>
```

### Non-web notes

For slides: simplify tables to essential rows. Header row uses toffee bold text. Body rows separated by fine lines. For print: same styling — toffee header, soft horizontal rules.

---

## 17. Modals

### Anatomy

1. **Backdrop** — toffee at 82% alpha (never black)
2. **Modal box** — snow fill, toffee border, rounded corners
3. **Header** — title + close button
4. **Body** — any content
5. **Footer** — action buttons

```html
<dialog class="cz-modal" id="my-modal">
  <div class="cz-modal__head">
    <h3 class="cz-no-margin">Title</h3>
    <button class="cz-modal__close" aria-label="Close"
            onclick="this.closest('dialog').close()">&times;</button>
  </div>
  <div class="cz-modal__body">
    <p>Content.</p>
  </div>
  <div class="cz-modal__foot">
    <button class="cz-btn cz-btn--tertiary" onclick="this.closest('dialog').close()">Cancel</button>
    <button class="cz-btn cz-btn--primary">Continue</button>
  </div>
</dialog>

<!-- Trigger -->
<button onclick="document.getElementById('my-modal').showModal()">Open</button>
```

---

## 18. Navigation and footer

### Header

```html
<header class="cz-header">
  <div class="cz-container cz-header__inner">
    <a href="/" aria-label="Cozendagen">
      <img class="folk-emblem cz-header__mark" src="assets/icons/full/emblem.svg" alt="Cozendagen">
    </a>
    <button class="cz-nav-toggle" aria-expanded="false" aria-controls="nav">Menu</button>
    <nav class="cz-nav" id="nav">
      <a href="#">Link</a>
      <a href="#" aria-current="page">Current</a>
    </nav>
  </div>
</header>
```

Snow background, dusk text, soft bottom border. Mobile: hamburger toggle reveals vertical menu.

### Footer

```html
<footer class="cz-footer">
  <div class="cz-container">
    <div class="cz-footer__grid">
      <div>
        <img src="assets/icons/full/emblem.svg" alt="Cozendagen" style="width:160px">
      </div>
      <div>
        <h3>Column title</h3>
        <ul>
          <li><a href="#">Link</a></li>
        </ul>
      </div>
    </div>
  </div>
</footer>
```

Toffee background, snow text. Flame links and accents.

### Non-web notes

For slides: the emblem goes on the title slide and closing slide. For print: place the emblem in the header/footer area. For email: simplified header with emblem centred.

---

## 19. Additional components

### Tabs

```html
<div class="cz-tabs" role="tablist">
  <button class="cz-tab" role="tab" aria-selected="true" aria-controls="panel1">Tab 1</button>
  <button class="cz-tab" role="tab" aria-selected="false" aria-controls="panel2">Tab 2</button>
</div>
<div class="cz-tabpanel" id="panel1" role="tabpanel">
  <p>Content for tab 1.</p>
</div>
<div class="cz-tabpanel" id="panel2" role="tabpanel" hidden>
  <p>Content for tab 2.</p>
</div>
```

Active tab gets a toffee border and snow fill, with dusk text.

### Accordion

```html
<div class="cz-accordion">
  <details>
    <summary>Question</summary>
    <p>Answer.</p>
  </details>
  <details>
    <summary>Another question</summary>
    <p>Another answer.</p>
  </details>
</div>
```

Native `<details>`/`<summary>`. Flame chevron marker.

### Timeline

```html
<ol class="cz-timeline">
  <li>
    <span class="cz-timeline__date">2019</span>
    <p class="cz-timeline__title">Event title</p>
    <p class="cz-mb-0">Description.</p>
  </li>
</ol>
```

Soft toffee left-hand rule connecting entries. Mark-01 tulip glyphs (toffee colourway) as dot markers.

### Pagination

```html
<ul class="cz-pagination">
  <li><a href="#">Prev</a></li>
  <li><a href="#" aria-current="page">1</a></li>
  <li><a href="#">2</a></li>
  <li><a href="#">Next</a></li>
</ul>
```

Active page: toffee fill, snow text.

### Breadcrumbs

```html
<ol class="cz-breadcrumbs">
  <li><a href="#">Home</a></li>
  <li><a href="#">Section</a></li>
  <li>Current page</li>
</ol>
```

Flame slash separators.

### Tooltips

```html
<span class="cz-tooltip">
  <span data-tip tabindex="0">Trigger text</span>
  <span class="cz-tooltip__bubble" role="tooltip">Tooltip content.</span>
</span>
```

Toffee fill, snow text, small radius. Appears on hover/focus.

### Figures and captions

```html
<figure class="cz-figure">
  <img src="..." alt="Description">
  <figcaption>Caption text.</figcaption>
</figure>

<!-- With border -->
<figure class="cz-figure cz-figure--bordered">
  <img src="..." alt="Description">
  <figcaption>Caption text.</figcaption>
</figure>
```

Images get large radius corners. Captions use muted text.

### Divider rule

```html
<div class="cz-divider-rule" style="--cz-divider-w:200px">
  <img src="assets/icons/{colourway}/mark-01.svg" alt="" style="width:26px">
</div>
```

### Ornament bullet list

```html
<ul class="cz-list--ornament">
  <li>Item one</li>
  <li>Item two</li>
</ul>

<!-- Custom colourway -->
<ul class="cz-list--ornament" style="--cz-bullet:url('assets/icons/teal/mark-01.svg')">
  <li>Teal bullets</li>
</ul>
```

---

## 20. The emblem

### What it is

The Cozendagen seal. Fixed colours — only the `full/` version exists. Never recoloured. Its snow disc carries its own ground, so it works on any palette colour.

### Rules

- **160px hard floor** — below that the curved wordmark is unreadable
- For header, footer, print, and title slides
- Not an inline icon — it's a brand mark

```html
<img class="folk-emblem" src="assets/icons/full/emblem.svg" alt="Cozendagen">
```

---

## 21. Additional folk-icons.css utilities

These classes live in `folk-icons.css`, not `cozendagen.css`. They are lower-level sizing/layout helpers for the icon library assets.

### `.folk-badge`

A fixed square grid slot (140px) that centres any icon inside it. Useful for aligning a row of icons with different aspect ratios.

```html
<div class="folk-badge">
  <img src="assets/icons/{colourway}/{slug}.svg" alt="">
</div>
```

### `.folk-disc`

Sizing class for the five circular badge graphics (badge-house, badge-moose, etc.). Sets a square box at `--fd-size` (default 120px). The circle is part of the artwork, so no backing shape is needed.

```html
<img class="folk-disc" src="assets/icons/full/badge-house.svg" alt=""
     style="--fd-size:132px">
```

### `.folk-pattern`

A generic background-pattern utility. Sets a 600px repeating tile from `--fp-src`, with an optional `--fp-src-2x` for retina. This is the folk-icons.css counterpart to the higher-level `.cz-pattern-ground` component in cozendagen.css.

```html
<div class="folk-pattern" style="--fp-src:url('assets/patterns/{colourway}/pattern-02.png')">
  <!-- content -->
</div>
```

### `.folk-corner--tall`

A modifier for corner-02, which has a 2:3 aspect ratio. Sets `width:auto; height:var(--fc-size)` so the vertical and horizontal runs look equal in length.

```html
<img class="folk-corner folk-corner--tl folk-corner--tall"
     src="assets/icons/{colourway}/corner-02.svg" alt="">
```

---

## 22. Panels

### What it is

A snow-filled bordered container. Reserved for textured or patterned backgrounds where bare text would lose contrast.

```html
<div class="cz-panel">
  <p>Content that needs a solid ground behind it.</p>
</div>

<!-- Flush (no radius) -->
<div class="cz-panel cz-panel--flush"> ... </div>

<!-- Soft border -->
<div class="cz-panel cz-panel--plain"> ... </div>
```

**Do not use panels on plain colour bands.** Snow text reads directly on dusk/valentine/flame/sunset at display size. Panels are for pattern-ground bands and accent-colour bands where body copy needs AA contrast.

---

## Page composition patterns

These are not individual components but recipes for combining components into layouts. Use DESIGN-SYSTEM.md §3 (band rule) and §26 (never-do rules) as constraints.

### Landing page

1. **Hero** — showstopper (full-bleed photo, bottom scrim) or snow band with cornered heading
2. **Introduction** — snow band, eyebrow + h2 + lead paragraph
3. **Features** — snow band with a 3-column card grid (folk icons)
4. **Photo break** — duotone band or split
5. **Essentials** — snow band with badge card grid
6. **Call to action** — dusk or flame band, single heading + primary button
7. **FAQ** — snow band with accordion
8. **Footer**

### Event page

1. **Hero** — showstopper with event photo
2. **Details** — snow band, eyebrow + heading + body + buttons
3. **Schedule** — snow band with timeline
4. **Gallery** — asymmetric editorial grid or arch trio
5. **Registration** — dusk band with form
6. **Footer**

### Story / about page

1. **Hero** — snow band with cornered heading and folk circle
2. **Timeline** — snow band with timeline component
3. **Photo section** — alternating splits (snow/dusk, reversing direction)
4. **Pull quote** — snow band with cornered pull quote
5. **Closing** — dusk band, heading + button
6. **Footer**

### Slide deck

1. **Title slide** — colour ground (dusk or flame), emblem, Germania One title
2. **Content slides** — alternate snow and colour grounds, one per band
3. **Photo slides** — duotone or split treatment
4. **Feature slide** — 3-column layout with folk circles
5. **Closing slide** — emblem on colour ground, call to action

### Print poster / flyer

1. **Frame** — one decorative frame (frames 01–05) around the headline
2. **Body** — snow ground with toffee text
3. **Ornaments** — garland above the heading, divider between sections
4. **Emblem** — bottom centre, at least 160px
5. **Details block** — Futura bold for event name/date, regular for description

---

## File inventory

| File | Purpose |
|---|---|
| `DESIGN-SYSTEM.md` | Rules, constraints, and the canonical spec |
| `COMPONENTS.md` | This file — markup patterns and composition recipes |
| `ICONS.md` | Icon library: slugs, colourways, sizing, gotchas |
| `assets/cozendagen.css` | Full design system CSS |
| `assets/folk-icons.css` | Icon sizing helpers, folk-circle, folk-frame, folk-corners, folk-pattern utilities |
| `assets/icons/{colourway}/{slug}.svg` | Pre-themed icon files (8 colourways × 58 graphics) |
| `assets/patterns/{colourway}/pattern-01..04.png` | Seamless pattern tiles, 600px (+@2x) |
| `assets/photos/` | Sample event photos |
| `styleguide.html` | Visual demo page — every component rendered |
