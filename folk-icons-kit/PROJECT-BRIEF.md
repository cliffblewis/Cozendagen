# Cozendagen — project brief

Everything established so far, for the chat taking over the website design overhaul. Written
to be read once, in full, before touching code. Roughly 15 minutes of reading that will save
you several wrong turns.

Companion files: `CLAUDE.md` (the short rules), `ICONS.md` (the asset consumption contract),
`assets/icons.json` (machine-readable manifest).

---

## 1. What Cozendagen is

Cliff Lewis's winter cultural tradition, based in Lancaster, Pennsylvania. A season of
deliberate coziness — hearth, hot drinks, wool, crafts, books, candlelight, bonfires,
community gatherings and a clothing drive.

**It is deliberately not Christmas.** That distinction drives the entire visual system: no
red, no evergreen-and-crimson, no Santa iconography. The register is Pennsylvania Dutch /
Scandinavian folk art — flat colour, confident shapes, tulips and sprigs, closer to
paper-cut (scherenschnitte) than to soft vector illustration.

---

## 2. The site as it stands

Eight static pages, vanilla HTML/CSS/JS, no framework and no build step. The pages are
already built and the visual system is finalised. **Real illustrations were the missing
piece, and that is what has just been produced.**

Every image on the site is currently a labelled placeholder — a dashed box reading
`[ PHOTO — description ]`. There is no existing SVG markup to conflict with; you are filling
empty slots.

| page | illustration slots |
|---|---|
| `index.html` | hero illustration, 3 "what it is" badges, flagship photo placeholder |
| `the-story.html` | timeline dot markers, one supporting illustration |
| `how-to-celebrate.html` | **9 "essentials" badges** — the densest page |
| `events.html` | event-type icons (flagship vs. community-hosted) |
| `host-an-event.html` | 2 criteria icons, a city/map graphic |
| `clothing-drive.html` | 3 donation-item badges (gloves, hats, socks) |
| `community.html` | gallery frame treatments, quote/testimonial dividers |
| `about.html` | press/media icons, FAQ dividers |
| site-wide | header brand seal (currently a placeholder star), footer wordmark, section dividers |

---

## 3. Brand system

### Palette — seven colours, and only these

| role | name | hex |
|---|---|---|
| core | teal-blue | `#14607F` |
| core | camel / tan | `#D9A66A` |
| core | maroon / burgundy | `#5B2226` |
| core | cream / ivory | `#F3E6D8` |
| accent | magenta / pink | `#CD3684` |
| accent | orange | `#DE8426` |
| accent | gold | `#DBA80D` |

**Hard rule: no red, ever.** Maroon is the warm limit; nothing may drift brighter or warmer.

**Background frequency** (confirmed by Cliff, after an earlier message had it backwards):
gold, orange, magenta and teal are the high-frequency section backgrounds. Camel and cream
are occasional. **Maroon is never a background.**

**There is no dark/near-black ground colour in the system, and one should not be introduced.**
Teal is the darkest colour in active use and it is mid-tone. An earlier draft of the asset
work invented `#2B1416` as a dark ground; that was withdrawn precisely because inventing a
system colour to serve the icons would be backwards. If a design appears to need a deep
anchor, raise it with Cliff.

### Typography

- Display: **Germania One** (Google Fonts)
- Body / utility: **Jost** (Google Fonts, standing in for Futura pending licensing)

### Style conventions carried over from Cliff's existing licensed library

- Flat colour, thick confident outlines, minimal shading.
- **Inverse-colour surface decoration**: the same shape appears in several official
  colourways with its surface ornament rendered in a contrasting colour. The illustration
  library below implements exactly this.
- Circular badge / seal format recurs and reinforces a "stamped tradition" feel over a
  "startup logo" feel. Worth preserving for the header seal.

---

## 4. The illustration library

58 graphics — 57 of them in 8 colourways, plus the fixed-colour emblem — and 4 seamless
patterns in 8 inks at 2 resolutions (**64 tiles**). Only what a page references is served.

All of it was produced by tracing Cliff's **licensed** stock illustrations, which he has full
rights to reproduce, and remapping them onto the seven-colour palette. The two corner
ornaments arrived as vector and were recoloured without tracing, so their paths are the
originals.

### Categories

| category | count | slugs |
|---|---|---|
| vessel | 11 | teacups, kettles, coffee pots, moka pot |
| fire-light | 3 | `campfire` `candle` `stove-01` |
| book | 3 | `open-book` `closed-book-01` `closed-book-02` |
| machine | 6 | typewriters, sewing machines, radios |
| furniture | 2 | `armchair-01` `armchair-02` |
| apparel | 4 | `sweater-01/02` `socks-01` `slippers-01` |
| building | 3 | `house-01/02/03` |
| nature | 3 | `tree-01/02/03` |
| animal | 2 | `moose-01` `moose-02` |
| ornament | 8 | sprays, garlands, `divider-01`, `mark-01` |
| corner | 2 | `corner-01` `corner-02` |
| frame | 5 | `frame-01`…`frame-05` |
| badge | 5 | `badge-moose` `badge-house` `badge-teacup` `badge-socks` `badge-sweater` |
| emblem | 1 | `emblem` — fixed colours, no variants |

### Colourways

`full/` is the original seven-colour artwork, for light grounds only. The other seven are
named for the **body** colour.

| folder | body | ornament (light / dark) | reads best on | soft but usable on |
|---|---|---|---|---|
| `maroon/` | #5B2226 | cream / camel | camel, cream, orange, gold, white | teal |
| `teal/` | #14607F | cream / camel | camel, cream, gold, white | maroon, magenta |
| `magenta/` | #CD3684 | cream / camel | cream, white | teal, orange |
| `orange/` | #DE8426 | teal / maroon | maroon | magenta |
| `camel/` | #D9A66A | teal / maroon | teal, maroon | cream |
| `gold/` | #DBA80D | teal / maroon | teal, maroon | cream |
| `cream/` | #F3E6D8 | teal / maroon | teal, maroon, magenta | camel, gold |

`assets/icons.json` carries `best_on` / `use_on` / `soft_on` for each. **Match the colourway
to the section background** — that is the single most important decision when placing a
graphic. Note that camel and gold are near-identical in luminance, so neither works on the
other's ground and both go soft on cream; and `cream/` needs a saturated ground.

### Patterns

Seamless raster tiles, not SVG — a traced pattern runs ~1,900 shapes and would be slow
repeated across a viewport. 600px tiles with `@2x` versions. The **ground colour is baked
into the file** and the folder is named for the *ink*, so `cream/` means cream ink on teal.

| slug | subject |
|---|---|
| `pattern-01` | vertical floral columns with teacups |
| `pattern-02` | kettles and teacups, tossed |
| `pattern-03` | cats, wing chairs, typewriters and books |
| `pattern-04` | sweaters, socks, moka pots and candles |

`camel/` and `gold/` patterns are deliberately very low contrast — texture rather than
illustration, which is usually what you want behind text. Don't set body copy over `full/`.

---

## 5. Every graphic

| slug | category | subject | aspect (w/h) |
|---|---|---|---|
| `coffee-pot-01` | vessel | gooseneck pour-over pot | 1.04 |
| `coffee-pot-02` | vessel | gooseneck pour-over pot | 1.04 |
| `kettle-01` | vessel | stovetop kettle, floral spray | 0.82 |
| `kettle-02` | vessel | stovetop kettle, lotus medallion | 0.82 |
| `kettle-03` | vessel | stovetop kettle, four fan medallions | 0.82 |
| `kettle-04` | vessel | stovetop kettle, single flowering branch | 0.82 |
| `moka-pot` | vessel | stovetop espresso maker | 0.81 |
| `teacup-01` | vessel | teacup, tulip spray | 1.28 |
| `teacup-02` | vessel | teacup, tulip spray | 1.28 |
| `teacup-03` | vessel | teacup, wildflower spray | 1.28 |
| `teacup-04` | vessel | teacup, tulip + petal border | 1.28 |
| `campfire` | fire-light | campfire with logs | 0.87 |
| `candle` | fire-light | lit candle in a glass jar | 0.82 |
| `stove-01` | fire-light | wood stove with lit firebox and flue | 0.5 |
| `closed-book-01` | book | closed book, standing | 0.74 |
| `closed-book-02` | book | closed book, standing | 0.74 |
| `open-book` | book | open book, sprig-decorated cover | 1.11 |
| `radio-01` | machine | cabinet radio, floral pilasters | 0.78 |
| `radio-02` | machine | cabinet radio, blossom panel | 0.78 |
| `sewing-machine-01` | machine | hand-crank sewing machine | 1.63 |
| `sewing-machine-02` | machine | hand-crank sewing machine | 1.63 |
| `typewriter-01` | machine | typewriter with paper | 1.14 |
| `typewriter-02` | machine | typewriter with paper | 1.14 |
| `armchair-01` | furniture | upholstered armchair, blossom on the headrest | 0.85 |
| `armchair-02` | furniture | wingback armchair, petal skirt | 0.99 |
| `slippers-01` | apparel | pair of house slippers | 1.01 |
| `socks-01` | apparel | pair of dotted wool socks | 0.76 |
| `sweater-01` | apparel | turtleneck sweater, tulip motif | 1.44 |
| `sweater-02` | apparel | turtleneck sweater, sprig field | 1.44 |
| `house-01` | building | tall gabled house, lotus over a plank door | 0.55 |
| `house-02` | building | tall gabled house, tulip motif and door-side sprigs | 0.55 |
| `house-03` | building | cottage with chimney, window and flower beds | 0.85 |
| `tree-01` | nature | pine, notched tiers | 0.53 |
| `tree-02` | nature | pine, scalloped tiers | 0.6 |
| `tree-03` | nature | pine, plain triangular tiers | 0.62 |
| `moose-01` | animal | moose with striped saddle blanket | 1.03 |
| `moose-02` | animal | moose with floral flank | 1.03 |
| `divider-01` | ornament | slim horizontal divider, blossom + two wings | 3.46 |
| `garland-01` | ornament | wide horizontal swag, lotus at centre | 1.91 |
| `garland-02` | ornament | wide low garland, blossoms | 2.0 |
| `garland-03` | ornament | wide arched crown garland | 2.44 |
| `mark-01` | ornament | single tulip with leaves &mdash; smallest piece, holds at 20px | 1.26 |
| `spray-01` | ornament | upright symmetrical spray, tulip at centre | 0.96 |
| `spray-02` | ornament | upright wheat-stem sprig | 0.97 |
| `spray-03` | ornament | symmetrical lotus spray, wide | 1.38 |
| `corner-01` | corner | snowflake, blossoms and swirls &mdash; top-left reference | 1.0 |
| `corner-02` | corner | sprigs, tulip and snowflakes &mdash; top-left reference | 0.67 |
| `frame-01` | frame | cats, wing chair, woman and teacups — safe area 52.3%×33.7%, insets T28.5 R23.7 B37.8 L24.0 | 0.85 |
| `frame-02` | frame | wood stove, typewriter and butterflies — safe area 40.7%×37.4%, insets T30.3 R29.4 B32.3 L29.9 | 0.81 |
| `frame-03` | frame | sewing machine, birds, candles and coffee pots — safe area 34.5%×43.9%, insets T30.1 R32.7 B26.0 L32.8 | 0.82 |
| `frame-04` | frame | wing chairs, moka pots and teacups — safe area 47.0%×27.0%, insets T27.7 R26.3 B45.4 L26.7 | 0.77 |
| `frame-05` | frame | cat, birds, kettles and coffee pots — safe area 47.2%×33.1%, insets T29.2 R26.2 B37.7 L26.6 | 0.76 |

---

## 6. How to use the assets — and why it works this way

### Two special cases

**The emblem** (`assets/icons/full/emblem.svg`) is the Cozendagen seal and the **header brand
seal** — it replaces the placeholder star that appears site-wide. One file, fixed colours,
never recoloured. Its cream disc carries its own ground so it works on any palette colour.
**160px floor**, hard: it contains curved lettering that stops being readable below that.
Class `.folk-emblem`.

**The badges** are self-contained circular discs — circle included in the artwork, so no
backing shape needed and they read on any ground. In `full/` the five discs are five
different palette colours, which makes them work as a set on one page. Class `.folk-disc`
with `--fd-size`. Floor 48px.

### The integration point

```html
<link rel="stylesheet" href="assets/folk-icons.css">
...
<img src="assets/icons/toffee/kettle-02.svg" alt="" class="folk-icon folk-icon--md">
```

That's it. No sprite, no build step, no script, no local server. Works when you open the
file straight off disk.

### Four rules, all load-bearing

1. **Never use an emoji as an icon, anywhere.** Cliff was explicit about this: stay inside the
   Cozendagen visual identity at all times. The library exists so an emoji is never needed. If
   nothing fits, leave a placeholder and flag it — an emoji is not the fallback, and that
   includes headings, list markers, buttons and callouts.
2. **Never open the files in `assets/icons/` or `assets/patterns/`.** ~2 MB of path data.
   `ICONS.md` and `assets/icons.json` contain everything needed to select and place a
   graphic, at about 2,000 tokens instead of 400,000.
3. **Never write inline `<svg>`, `<symbol>`, `<use>` or `<path>` markup into a page.**
4. **Never edit an SVG to change colour.** Colour = a different colourway folder.

### Why rule 2 exists

A sprite-based approach was designed, costed, and rejected. Injecting subset sprite markup
into each page would have put the path data inside the files that get edited most: a nine-
badge page would carry ~700 KB of path data, about 180k tokens to read. Changing a headline
on that page would cost more context than the entire library's documentation. `<img src>`
keeps pages a few KB, so editing them stays cheap forever.

The trade-off accepted in exchange: `<img>` renders in an isolated context, so CSS custom
properties don't reach inside it and the icons are not recolourable at runtime. That is why
there are eight pre-finished colourways instead of a theming layer. Hover-state colour
changes and a runtime dark-mode toggle are not available for icons. If a specific component
genuinely needs that, raise it — a token-driven variant of the whole set exists in history
and could be regenerated for that one component.

### CSS helpers in `assets/folk-icons.css`

- `.folk-icon` with `--sm` 80px, `--md` 120px, `--lg` 200px, `--xl` 320px. Aspect ratios
  range 0.67–3.46, so set width **or** height, never both.
- `.folk-badge` — a fixed square slot that centres graphics of differing aspect ratios so a
  row of badges aligns.
- `.folk-frame` — a frame with content absolutely positioned in its empty centre. Set the
  four inset custom properties from that frame's `safe_area`.
- `.folk-corners` + `.folk-corner--tl/tr/br/bl` — four rotated copies of a corner ornament
  around a content block. `--fc-size` controls scale. `.folk-corners--mirror` reflects
  instead of rotating, which reads more classical.
- `.folk-pattern` with `--fp-src` / `--fp-src-2x`.

### Minimum legible sizes — these differ by category

| category | floor |
|---|---|
| `mark-01` | 20px — purpose-built for bullet glyphs, list markers, timeline dots |
| `ornament` sprays | 24px |
| `nature` (trees) | 32px |
| `corner` | 40px |
| `ornament` garlands / dividers | 120px **wide** (they are wide and low; size by width) |
| `badge` | 48px |
| `emblem` | **160px** — hard floor; contains curved lettering |
| everything else | 48px |

Below 20px, use CSS shapes. No artwork in the set goes lower.

### Frames vs corners — pick corners more often

Frames have a small content box: 27–52% of the frame's width, so an 800px frame yields
roughly a 330px content area. They suit a pull quote, a short heading, or a small image, and
will not hold body copy. Frames are also the heaviest files (300–440 KB).

Corners have no content-size limit — they just pad a block. Cliff uses them heavily in social
posts and they're the better default for most sections.

---

## 7. How colour is assigned inside a graphic (background, not instructions)

You don't need this to use the library, but it explains why things look the way they do and
why certain requests are hard.

Each layer's colour comes from its **nesting depth**, measured geometrically during tracing:
the outline, then what sits inside it, then what sits inside that. Odd depths take an
ornament colour; even depths return to the body, which is how a paper-cut behaves.

Two ornament colours rather than one, because same-depth siblings all sit on the body — for a
dark body every ornament must be light, so one ornament colour would collapse the source
art's light and mid tiers together.

Decorative compositions are handled differently because they have no enclosing body:
`ornament` and `corner` are a flat single colour per colourway; `frame` gets the body plus a
companion colour chosen to contrast with both the body and the rated ground.

Three audits run over the built files (not over a re-implementation, so they can't drift):
across all 364 graphic-colourway combinations, nothing falls below 1.70:1 against whatever it
sits on, and nothing bordering the page falls below 1.45:1 against its rated ground.

**Practical consequence:** if you ask for a colour combination the palette can't support —
a light ornament on a light body, or a dark ornament that also has to read on a dark ground —
it genuinely cannot be done with seven colours and no dark neutral. That's a palette
constraint, not an oversight.

---

## 8. Known gaps — do not paper over these

**Missing subjects.** No source art exists and Cliff has said the last batch was final:

- **gloves and hats** — needed for `clothing-drive.html`, which wants three donation badges
  and currently only has `socks-01`. Cliff has an open offer from the asset thread to
  hand-author these two in-style; they're simple enough shapes to do convincingly.
- **small animals** — bird, fish, squirrel, cat. Note that `frame-01`, `frame-03` and
  `frame-05` contain a cat and birds; extracting them was offered and declined, but the
  option stands.
**Resolved since the earlier gap list:** the circular badge format and the header brand seal
are both **done**. Cliff supplied the emblem and five badges; they are in the library. The
header seal work is now simply swapping the placeholder star for
`assets/icons/full/emblem.svg` on all eight pages.

**Coverage against the 9 `how-to-celebrate` essentials** — 8 of 9 are covered:

| essential | graphic |
|---|---|
| home | `house-01/02/03` |
| hearth | `stove-01` |
| bonfire | `campfire` |
| socks | `socks-01` |
| drinks | 11 vessels |
| sweaters | `sweater-01/02` |
| crafts | `sewing-machine-01/02` |
| books | `open-book`, `closed-book-01/02` |
| candlelight | `candle` |

**Don't substitute an unrelated graphic for a missing subject.** Leave the placeholder and
flag it.

---

## 9. Open questions worth resolving early

1. **Section inventory with background colours.** Nobody has written down which sections use
   which of the seven backgrounds. With that list, colourway choices become mechanical
   instead of case-by-case, and collisions can be checked up front.
2. **Design tokens.** `folk-icons.css` declares the seven colours under `:root`. If a broader
   token system emerges, these should become aliases into it rather than a second source of
   truth.
3. **Gloves and hats.** Blocks `clothing-drive.html` — it needs three donation badges and
   only `socks-01` exists.
4. **Repo weight.** 44 MB of assets. Fine for git, but if it becomes an issue the unused
   colourways can be pruned — `assets/icons.json` makes it easy to see what a page actually
   references.

---

## 10. Working with Cliff

Established preferences from the asset thread:

- **He reviews visually.** Render what you build and show it to him — contact sheets, a demo
  page, screenshots. He catches contrast and detail problems immediately from an image and
  will not catch them from a description.
- **He will push back on quality, and he's usually right.** Several rounds of the asset work
  were spent on contrast failures he spotted that automated checks had missed. When he says
  something looks wrong, measure it rather than explaining why it's fine.
- **Ask before deciding things that are his to decide.** Brand voice, what the seal depicts,
  whether to introduce a colour, scope. He explicitly objected once to work proceeding while
  a decision addressed to him sat unanswered — surface those first, prominently, rather than
  burying them after finished work.
- Be concise and direct. Skip preamble.
