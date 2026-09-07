# Folk Home Icon Set — instructions for Claude

58 flat folk-art graphics for the Cozendagen site, each in four pre-finished colourways,
plus 4 seamless background patterns, also in every palette colour.
Style is paper-cut / scherenschnitte: flat colour, no gradients, no strokes, no shading.

---

## The only integration point

```html
<img src="assets/icons/<colourway>/<slug>.svg" alt="" class="folk-icon">
```

That is the entire mechanism. Pick a slug, pick a colourway, write one line.

**Three rules, all load-bearing:**

0. **Never use an emoji as an icon, anywhere, for any reason.** Cozendagen has its own
   visual identity and this library exists so you never have to reach for one. If no graphic
   fits, leave a placeholder and flag it — an emoji is never the fallback.
1. **Never open the files in `assets/icons/`.** ~2 MB of path data; reading them will exhaust
   the context window. Select graphics from the tables below or from `icons.json`.
2. **Never write inline `<svg>`, `<symbol>`, `<use>`, or `<path>` markup into a page.** A
   sprite-based approach was evaluated and deliberately rejected: injecting path data into
   HTML made every later edit to that page cost 60k–180k tokens to read. `<img src>` is the
   only integration point.
3. **Never edit the SVGs to change colour.** Colour comes from choosing a different
   colourway folder. If a needed combination doesn't exist, say so rather than improvising.

No build step, no sprite, no script to run, no local server requirement.

---

## Colourways — one per palette colour

Eight folders. `full/` is the original seven-colour artwork; the other seven are named for
the **body** colour and use three values each.

| folder | body | ornament (light) | ornament (dark) | reads best on | soft but usable on |
|---|---|---|---|---|---|
| `full/` | seven-colour artwork | — | — | cream, camel, white | — |
| `maroon/` | #5B2226 | cream | camel | camel, cream, orange, gold, white | teal |
| `teal/` | #14607F | cream | camel | camel, cream, gold, white | maroon, magenta |
| `magenta/` | #CD3684 | cream | camel | cream, white | teal, orange |
| `orange/` | #DE8426 | teal | maroon | maroon | magenta |
| `camel/` | #D9A66A | teal | maroon | teal, maroon | cream |
| `gold/` | #DBA80D | teal | maroon | teal, maroon | cream |
| `cream/` | #F3E6D8 | teal | maroon | teal, maroon, magenta | camel, gold |

**Picking one:** match the body colour to the section background using the two right-hand
columns. Anything in "reads best on" is a safe choice. "Soft but usable" means the silhouette
edge goes quiet against that ground — fine for a large decorative piece whose interior
ornament carries the shape, risky for a small badge.

Note that `camel/` and `gold/` are nearly identical in luminance, so neither works on the
other's ground, and both go soft on cream — they want a teal, maroon or magenta section.
Conversely `cream/` needs a saturated ground and will vanish on cream or white.

Never place a `full/` graphic on a saturated ground — the artwork contains gold, orange,
magenta and teal and will collide with the background. The `palette` column in the tables
below says what each graphic actually contains.

### How the colours get assigned

Not by hand, and not by flattening everything that isn't the outline into one colour.

**Objects** (vessels, machines, apparel, buildings, animals, books) are tiered. Each layer's
colour comes from its **nesting depth**, measured geometrically while tracing: the outline,
then what sits inside it, then what sits inside that. Depth 0 takes the body colour; odd
depths take an ornament colour; even depths return to the body, which is how a paper-cut
behaves — the deepest marks read as holes back to the ground.

Two ornament colours rather than one, because same-depth siblings all sit on the body: for a
dark body every ornament has to be light, so a single ornament colour would collapse the
source art's light and mid tiers together. Where a depth level spans a wide range of
lightness in the original, its siblings are split — lighter ones take the light ornament,
darker ones the dark. That is what keeps a candle's label distinct from its wax, or a
typewriter's keys distinct from its paper.

One more correction on top of that: an ornament colour is picked to contrast with the *body*,
which is the wrong reference for an element that forms part of the outer contour — there it
borders the page instead. In six of the seven colourways one ornament colour is the same as
the ground the colourway is rated for, so such an element would read as a hole punched in the
silhouette. Those elements take the body colour instead.

**Decorative compositions** are handled differently, because they have no enclosing body —
every element borders the page directly, so an ornament colour chosen to contrast with a body
is the wrong colour there.

- The `ornament` and `corner` categories are a flat single colour per colourway. Pure
  foliage reads best as one clean silhouette, and it can never collide with the ground.
- The `frame` category gets two tones: the body plus a **companion** colour chosen to
  contrast with both the body and the ground the colourway is rated for, so both tones read
  against the page. Frames contain recognisable objects — a stove, a teacup, a cat — that
  need to separate from the foliage. The split follows the artwork's own tonal division,
  found at the widest gap in source lightness weighted by how evenly it divides the ink, and
  the body goes to whichever group forms the outer contour. That lands between 56% and 83%
  body across the five frames.

Three audits run over the built files, not over a re-implementation of the rules, so they
cannot drift from what actually ships. Across all 364 graphic-colourway combinations: nothing
falls below 1.70:1 against whatever it sits on, and no element that borders the page falls
below 1.45:1 against the ground its colourway is rated for. The only graphics rendered as a
single tone are the ornaments, by design.

---

## Palette

```
teal    #14607F      magenta #CD3684
camel   #D9A66A      orange  #DE8426
maroon  #5B2226      gold    #DBA80D
cream   #F3E6D8
```

**No red, ever.** Maroon is the warm limit of the system; nothing may drift brighter or
warmer than it. There is deliberately no dark/near-black ground colour — do not introduce one.

---

## Sizing

Link `assets/folk-icons.css` for `.folk-icon` with `--sm` (80px), `--md` (120px), `--lg`
(200px), `--xl` (320px), plus `.folk-badge` for a fixed square slot that aligns graphics of
differing aspect ratios in a row.

Aspect ratios range 0.74–3.46. Set width **or** height, never both.

**Minimum legible size differs by category — this matters:**

| category | floor | notes |
|---|---|---|
| `mark` | **20px** | purpose-built for bullet glyphs, list markers, timeline dots |
| `ornament` sprays | **24px** | sprigs stay legible small |
| `ornament` garlands / dividers | **120px wide** | they are wide and low; size by width |
| `corner` | **40px** | solid silhouettes, they hold up small |
| `badge` | **48px** | self-contained discs |
| `emblem` | **160px** | contains curved lettering; a hard floor, not a preference |
| `nature` (trees) | **32px** | plain silhouettes, they scale down well |
| `apparel`, `furniture` | **48px** | simple shapes, but the surface motifs need the room |
| `vessel`, `book`, `machine`, `fire-light`, `building`, `animal` | **48px** | below this the floral detail turns to mush |

For anything smaller than 20px, use CSS shapes — no artwork in this set goes lower.

Other notes: `alt=""` for decoration, real alt text only when the graphic carries meaning.
One object illustration per section is usually plenty; they are visually loud. Ornaments are
quieter and can repeat.

---

## The emblem — 1 graphic, fixed colours

`assets/icons/full/emblem.svg` is the Cozendagen seal: a cream disc with the wordmark curved
top and bottom, a dotted teal ring, and a kettle, cottage, socks and teacup inside.

**It has no colourway variants and must not be recoloured.** Only `full/` exists. Its cream
disc carries its own ground, so it sits on any palette colour without adjustment — verified
on cream, white, teal and magenta.

```html
<img src="assets/icons/full/emblem.svg" alt="Cozendagen" class="folk-emblem">
```

**160px is the floor**, and that is a hard limit rather than a preference — it contains
curved lettering, and below 160px the wordmark stops being readable. Use it for the header,
the footer, and print. Do not use it as an inline icon; reach for a badge or an object
instead.

This is the header brand seal. It replaces the placeholder star that currently appears
site-wide.

## Circular badges — 5 graphics

Self-contained discs: the circle is part of the artwork, so a badge needs no backing shape
and reads on any ground. Each has a top flourish, a centred object and a bottom spray.

| slug | subject |
|---|---|
| `badge-house` | cottage |
| `badge-moose` | moose |
| `badge-socks` | socks |
| `badge-sweater` | sweater |
| `badge-teacup` | teacup |

Available in all eight colourways. **In `full/` the five discs are five different palette
colours** — orange, gold, magenta, camel and teal — which makes them work as a set on one
page without any further choices. That is the intended use for a row of badges; the single-
colour colourways are for when a set needs to sit inside one section's palette.

```html
<img src="assets/icons/full/badge-house.svg" alt="" class="folk-disc" style="--fd-size:132px">
```

They are square, so a row aligns without `.folk-badge`. Floor is 48px.

These came in off-palette — a cyan disc, a peach disc, grey florals, and gradients on the
teacup — and were corrected to the seven colours with the gradients flattened to two tones.

## Objects — 37 graphics

| slug | subject | aspect | palette (`full/`) |
|---|---|---|---|
| `coffee-pot-01` | gooseneck pour-over pot | 1.04 | gold maroon teal magenta |
| `coffee-pot-02` | gooseneck pour-over pot | 1.04 | maroon camel gold magenta cream |
| `kettle-01` | stovetop kettle, floral spray | 0.82 | camel maroon teal magenta |
| `kettle-02` | stovetop kettle, lotus medallion | 0.82 | magenta camel cream maroon gold |
| `kettle-03` | stovetop kettle, four fan medallions | 0.82 | teal gold maroon cream camel |
| `kettle-04` | stovetop kettle, single flowering branch | 0.82 | teal camel gold maroon cream |
| `moka-pot` | stovetop espresso maker | 0.81 | magenta maroon cream gold |
| `teacup-01` | teacup, tulip spray | 1.28 | teal cream camel gold |
| `teacup-02` | teacup, tulip spray | 1.28 | maroon cream camel gold magenta |
| `teacup-03` | teacup, wildflower spray | 1.28 | camel maroon teal magenta |
| `teacup-04` | teacup, tulip + petal border | 1.28 | teal cream gold camel |
| `campfire` | campfire with logs | 0.87 | maroon orange gold camel magenta |
| `candle` | lit candle in a glass jar | 0.82 | maroon teal cream camel gold orange |
| `stove-01` | wood stove with lit firebox and flue | 0.5 | teal maroon cream orange camel |
| `closed-book-01` | closed book, standing | 0.74 | maroon orange camel cream magenta |
| `closed-book-02` | closed book, standing | 0.74 | teal camel cream magenta |
| `open-book` | open book, sprig-decorated cover | 1.11 | maroon camel gold |
| `radio-01` | cabinet radio, floral pilasters | 0.78 | orange maroon cream gold |
| `radio-02` | cabinet radio, blossom panel | 0.78 | teal maroon cream orange camel |
| `sewing-machine-01` | hand-crank sewing machine | 1.63 | teal gold cream magenta |
| `sewing-machine-02` | hand-crank sewing machine | 1.63 | maroon orange camel |
| `typewriter-01` | typewriter with paper | 1.14 | teal camel maroon orange cream |
| `typewriter-02` | typewriter with paper | 1.14 | magenta camel gold cream teal |
| `armchair-01` | upholstered armchair, blossom on the headrest | 0.85 | teal camel maroon cream |
| `armchair-02` | wingback armchair, petal skirt | 0.99 | teal camel maroon |
| `slippers-01` | pair of house slippers | 1.01 | cream maroon |
| `socks-01` | pair of dotted wool socks | 0.76 | teal camel maroon |
| `sweater-01` | turtleneck sweater, tulip motif | 1.44 | camel maroon teal |
| `sweater-02` | turtleneck sweater, sprig field | 1.44 | teal cream camel |
| `house-01` | tall gabled house, lotus over a plank door | 0.55 | teal cream camel |
| `house-02` | tall gabled house, tulip motif and door-side sprigs | 0.55 | maroon cream camel orange |
| `house-03` | cottage with chimney, window and flower beds | 0.85 | teal cream camel |
| `tree-01` | pine, notched tiers | 0.53 | teal |
| `tree-02` | pine, scalloped tiers | 0.6 | maroon |
| `tree-03` | pine, plain triangular tiers | 0.62 | gold |
| `moose-01` | moose with striped saddle blanket | 1.03 | camel maroon teal |
| `moose-02` | moose with floral flank | 1.03 | teal cream maroon |

Categories: `vessel` (11), `fire-light` (3), `book` (3), `machine` (6), `furniture` (2),
`apparel` (4), `building` (3), `nature` (3), `animal` (2).

## Ornaments — 8 graphics

Decorative florals with no object in them — section dividers, corner flourishes, and small
marks. Because they are scattered arrangements rather than single objects, the two-value
colourways render them as clean single-colour ornaments, which is usually what a divider
wants.

| slug | subject | aspect | palette (`full/`) |
|---|---|---|---|
| `divider-01` | slim horizontal divider, blossom + two wings | 3.46 | teal gold maroon |
| `garland-01` | wide horizontal swag, lotus at centre | 1.91 | maroon camel teal cream |
| `garland-02` | wide low garland, blossoms | 2.0 | gold teal maroon |
| `garland-03` | wide arched crown garland | 2.44 | teal maroon cream camel |
| `mark-01` | single tulip with leaves &mdash; smallest piece, holds at 20px | 1.26 | camel teal |
| `spray-01` | upright symmetrical spray, tulip at centre | 0.96 | maroon camel teal cream |
| `spray-02` | upright wheat-stem sprig | 0.97 | maroon teal camel |
| `spray-03` | symmetrical lotus spray, wide | 1.38 | teal camel cream maroon |

## Corners — 2 graphics

Single-colour flourishes for the corners of a content area — a lighter-weight alternative to
the frames, and the piece you reach for most often. Both are drawn for the **top-left**
corner; place four rotated copies to surround a block.

Use the `.folk-corners` helper in `folk-icons.css`:

```html
<div class="folk-corners" style="--fc-size:110px">
  <img class="folk-corner folk-corner--tl" src="assets/icons/toffee/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--tr" src="assets/icons/toffee/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--br" src="assets/icons/toffee/corner-02.svg" alt="">
  <img class="folk-corner folk-corner--bl" src="assets/icons/toffee/corner-02.svg" alt="">
  <div class="folk-corners__content">
    <h2>Heading</h2>
    <p>Body copy sits here, with no size limit &mdash; unlike the frames.</p>
  </div>
</div>
```

Rotation makes the flourish chase around the frame. Add `.folk-corners--mirror` to the
wrapper for bilateral symmetry instead, which reads more classical. You can also use just
two (top-left and bottom-right) for a lighter touch.

| slug | subject | aspect |
|---|---|---|
| `corner-01` | snowflake, blossoms and swirls &mdash; top-left reference | 1.0 |
| `corner-02` | sprigs, tulip and snowflakes &mdash; top-left reference | 0.67 |

`corner-01` is square; `corner-02` is 2:3, so its vertical run is longer than its horizontal
one — add `.folk-corner--tall` if you'd rather the two runs looked equal. Both are one solid
colour, so every colourway is a flat silhouette and they work at any size down to about 40px.

**These came in as vector artwork rather than raster, so they were recoloured without
tracing** — the paths are the originals, not approximations. Like the other decorative
compositions they are a flat single colour in each colourway.

## Frames — 5 graphics

Portrait border compositions with an empty centre, for wrapping content. Same four
colourways as everything else.

Use the `.folk-frame` helper in `folk-icons.css`. Set the four inset custom properties from
the table below — they come from each frame's `safe_area` in `icons.json`:

```html
<div class="folk-frame" style="--fi-t:30.3%;--fi-r:29.4%;--fi-b:32.3%;--fi-l:29.9%">
  <img src="assets/icons/full/frame-02.svg" alt="">
  <div class="folk-frame__content">
    <p>Short pull quote goes here.</p>
  </div>
</div>
```

**The content box is small relative to the frame** — 27–52% of the width. An 800px-wide
frame gives roughly a 330px content box. Frames suit a pull quote, a short heading, or a
small image. They will not hold body copy; don't try.

| slug | subject | aspect | safe area | inset properties |
|---|---|---|---|---|
| `frame-01` | cats, wing chair, woman and teacups | 0.85 | 52.3% x 33.7% | `--fi-t:28.5%;--fi-r:23.7%;--fi-b:37.8%;--fi-l:24.0%` |
| `frame-02` | wood stove, typewriter and butterflies | 0.81 | 40.7% x 37.4% | `--fi-t:30.3%;--fi-r:29.4%;--fi-b:32.3%;--fi-l:29.9%` |
| `frame-03` | sewing machine, birds, candles and coffee pots | 0.82 | 34.5% x 43.9% | `--fi-t:30.1%;--fi-r:32.7%;--fi-b:26.0%;--fi-l:32.8%` |
| `frame-04` | wing chairs, moka pots and teacups | 0.77 | 47.0% x 27.0% | `--fi-t:27.7%;--fi-r:26.3%;--fi-b:45.4%;--fi-l:26.7%` |
| `frame-05` | cat, birds, kettles and coffee pots | 0.76 | 47.2% x 33.1% | `--fi-t:29.2%;--fi-r:26.2%;--fi-b:37.7%;--fi-l:26.6%` |

Frames are the largest files in the kit (300–440 KB each, ~105 KB gzipped). One per page at
most.

## Patterns — 4 seamless tiles

Raster tiles, not SVG: a traced pattern runs ~1,900 shapes and would be slow repeated across
a viewport. 600px tiles with `@2x` versions for retina.

**Pattern colourways work differently from the icons** — the ground colour is baked into
the file, and the folder is named for the *ink*:

| folder | ground | ink |
|---|---|---|
| `full/` | cream `#F3E6D8` | full palette — busy, for a feature band |
| `maroon/` `teal/` `magenta/` `orange/` | cream `#F3E6D8` | that colour |
| `camel/` `gold/` | cream `#F3E6D8` | that colour — very quiet, reads as texture |
| `cream/` | teal `#14607F` | cream — the inverted one, for a saturated band |

```css
.story-band {
  background-image: url("assets/patterns/toffee/pattern-02.png");
  background-repeat: repeat;
  background-size: 600px 600px;
  background-color: #F3E6D8;   /* match the tile's ground for the pre-paint flash */
}
@media (-webkit-min-device-pixel-ratio:2), (min-resolution:192dpi) {
  .story-band { background-image: url("assets/patterns/toffee/pattern-02@2x.png"); }
}
```

Or use the `.folk-pattern` helper with `--fp-src` / `--fp-src-2x`.

| slug | subject |
|---|---|
| `pattern-01` | vertical floral columns with teacups |
| `pattern-02` | kettles and teacups, tossed |
| `pattern-03` | cats, wing chairs, typewriters and books |
| `pattern-04` | sweaters, socks, moka pots and candles |

**Don't set body copy directly over `full/`** — it's too busy. Use `maroon/` or `teal/`
behind text, reduce `background-size` to 300–400px to make the motif read as texture rather
than illustration, or keep text off the pattern entirely. Tile files are 56–129 KB (600px)
and 122–327 KB (`@2x`); `pattern-01` is the densest and heaviest.

`icons.json` carries all of the above — icons, frames with safe areas, and patterns — plus
the resolved path for every colourway.

### How to use the ornaments

- **Section dividers** — `divider-01` centred at 200–320px wide between bands of content.
  `garland-01`/`-02`/`-03` at 320–520px for a heavier break.
- **Bullet glyphs and list markers** — `mark-01` at 20–24px.
- **Timeline dot markers** — `mark-01` at 24px, or `divider-01` rotated if you want a rule.
- **Corner flourishes / card headers** — `spray-01`, `spray-02`, `spray-03` at 48–120px.
- **Above a heading** — `garland-03` (arched) sits well over centred display type.

---

## Coverage against the site's needs

**Available**, mapped to the nine `how-to-celebrate` essentials:

| essential | graphic |
|---|---|
| home | `house-01/02/03` |
| hearth | `stove-01` |
| bonfire | `campfire` |
| socks | `socks-01` |
| drinks | 11 vessels — teacups, kettles, coffee pots, moka pot |
| sweaters | `sweater-01/02` |
| crafts | `sewing-machine-01/02` |
| books | `open-book`, `closed-book-01/02` |
| candlelight | `candle` |

Also available: corner flourishes (`corner-01/02`), seating (`armchair-01/02`), slippers (`slippers-01`), radios
(`radio-01/02`), winter landscape (`tree-01/02/03`), animals (`moose-01/02`), five frames,
four patterns, and the full ornament set.

**Still missing:** gloves and hats (needed for the `clothing-drive` donation badges
alongside `socks-01`) and small animals (bird, fish, squirrel, cat). The circular badge
format and the header brand seal are both **done** — see the emblem and badge sections above. Do not substitute an unrelated graphic for a missing subject —
leave the placeholder and flag it.

---

## Gotchas

- `candle` in the two-value colourways reduces to a jar silhouette with a solid interior; its
  label motif largely merges. Use `full/candle.svg` where that detail matters.
- `typewriter-01/02`: the sheet of paper is camel in `full/`. In the light-bodied colourways
  (`camel/`, `gold/`, `orange/`, `cream/`) both ornament colours are dark, so the paper reads
  as a dark sheet — there is no lighter value available than the body. Graphically fine,
  semantically a stylisation.
- The four teacups, and separately the four kettles, read as a family. Grouping them is a
  deliberate effect; mixing one teacup in among unrelated objects is not.
- `garland-02` and `divider-01` use gold in `full/`; on a gold ground use `cream/`.
- `tree-01/02/03` are single-colour silhouettes by design, so `full/` gives one flat colour
  each (teal, maroon, gold respectively) and the colourway folders give the rest.
- `candle` keeps its jar and wax at the same nesting level, so they share the body colour in
  the seven single-colour colourways; `full/` distinguishes them.
- `armchair-01/02` and `stove-01` use camel for upholstery seams, cushions and flue where
  the source art used a second, darker teal. The palette has no second teal, so these
  read as piping and contrast panels rather than as shading. Intentional.
