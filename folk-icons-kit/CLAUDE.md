# Cozendagen — project rules

Cozendagen is Cliff Lewis's winter cultural tradition, based in Lancaster PA. This repo is
its marketing site: 8 static pages, vanilla HTML/CSS/JS, no framework, no build step.

**Read `PROJECT-BRIEF.md` before doing anything.** It carries the brand system, the page
inventory, the illustration library, and the decisions already settled — including several
that were reached the hard way and should not be relitigated.

---

## Non-negotiables

**No red, ever.** Cozendagen is deliberately not-Christmas-coded. Maroon `#5B2226` is the
warm limit of the palette; nothing may drift brighter or warmer than it. This applies to
every colour that enters the site, not just the illustrations.

**Seven colours, no others.** Any new colour needs Cliff's sign-off, not an inference from
what looks nice.

```css
--folk-teal:    #14607F;   --folk-magenta: #CD3684;
--folk-camel:   #D9A66A;   --folk-orange:  #DE8426;
--folk-maroon:  #5B2226;   --folk-gold:    #DBA80D;
--folk-cream:   #F3E6D8;
```

**There is no dark/near-black ground colour, and you must not introduce one.** Teal is the
darkest colour in active use and it is mid-tone. If a design seems to need a deep anchor,
raise it rather than inventing one.

**Typography:** Germania One for display, Jost for body and utility (both Google Fonts; Jost
stands in for Futura pending licensing).

---

## The illustration library

`assets/icons/` holds 58 graphics — 57 in 8 colourways plus the fixed-colour emblem — and 64
seamless pattern tiles in `assets/patterns/`. Full documentation is in `ICONS.md`.

Four rules, all load-bearing:

1. **Never use an emoji as an icon, anywhere, for any reason.** Cozendagen has its own
   visual identity and this library exists precisely so you never need one. If nothing in the
   library fits, leave a placeholder and flag it — an emoji is never the fallback. This also
   rules out emoji in headings, list markers, buttons and callouts.
2. **Never open the files in `assets/icons/` or `assets/patterns/`.** ~2 MB of path data;
   reading them will exhaust the context window for no benefit. Select graphics from
   `ICONS.md` or `assets/icons.json`, both of which are small and complete.
3. **Never write inline `<svg>`, `<symbol>`, `<use>` or `<path>` markup into a page.** A
   sprite-based approach was evaluated and deliberately rejected — injecting path data into
   HTML made every later edit to that page cost 60k–180k tokens to read. See PROJECT-BRIEF
   §6 for the full reasoning.
4. **Never edit an SVG to change its colour.** Colour comes from choosing a different
   colourway folder. If the combination you want doesn't exist, say so rather than
   improvising.

The only integration point is:

```html
<img src="assets/icons/<colourway>/<slug>.svg" alt="" class="folk-icon">
```

The **emblem** is the exception to the colourway system: `assets/icons/full/emblem.svg` only,
fixed colours, never recoloured, never below 160px. It is the header brand seal.

Match the colourway to the section background — every colourway has a `best_on` list in
`assets/icons.json`. Link `assets/folk-icons.css` for the sizing, badge, frame, corner and
pattern helpers.

---

## Working conventions

- Keep it vanilla. No framework, no bundler, no package.json unless Cliff asks.
- Every image on the site is currently a labelled placeholder — a dashed box reading
  `[ PHOTO — description ]`. Replacing those with real illustrations is the main task.
- **Don't substitute an unrelated graphic for a missing subject.** Leave the placeholder and
  flag it. The known gaps are listed in PROJECT-BRIEF §8.
- Illustrations are visually loud. One object illustration per section is usually plenty;
  ornaments and corners are quieter and can repeat.
- Ask before inventing brand content — taglines, event names, dates, testimonials. Cliff
  writes the voice.
