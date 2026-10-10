---
name: tapewatch-design
description: Tapewatch's house style for the public site - palette, type, layout, components, data-honesty rules, and the checks every visual change must pass. Use before any change to index.html or any new page, section, component, color, font, or illustration on the site.
---

# Tapewatch design guide

The site looks like a credit research printout: warm paper, black ink, and
one red pencil for whatever we flag. A reader should come away thinking "these
people read loan tapes for a living", not "this is a crypto startup".

Every change has to pass three tests:

1. **Would a rating agency print this?** If it needs a gradient, a glow, an
   icon grid, or an exclamation mark to work, it doesn't belong here.
2. **Does red mean something?** Red marks a finding, a flag, or the one thing
   we want the reader to act on. If you add red, you've added a finding.
3. **Is it true?** Every number is real and sourced, or it's labeled as an
   illustrative example.

All styles live in the `<style>` block of `index.html`. The values below match
that file. If they ever disagree, the file is what ships, so fix whichever one
is wrong in the same PR.

## Never do this

These are the patterns that made the old site read as AI-generated. Don't
bring them back in any form.

- A centered hero, or a pill or badge above the headline.
- Rows of identical cards, especially with an icon on top of each one.
- Three pricing cards with the middle one glowing or scaled up.
- Gradients, glows, glassmorphism, blurred blobs, 3D coins, or stock crypto
  art. The only blur on the site is the paywalled sample row.
- Rounded corners. Everything is square. The one exception is the hollow
  circle in the CLEAN flag.
- Dark mode as the default, grey text on near-black, or neon accents.
- Inter, Space Grotesk, Geist, Instrument Serif, Playfair, Fraunces, or
  Georgia as a display face.
- Emoji, decorative icons, or illustrations that don't show data.
- Made-up social proof: "most popular", "trusted by", logo walls,
  testimonials, user counts, or anything else we can't back up.
- Colored left borders on cards as decoration. The red bar is reserved for
  flagged rows and the one recommended rate.

## Color

Use the tokens in `:root` and never write a hex value inline. If you need a
new color, add a token, explain why in the PR, and get Kai's OK.

| Token | Value | Use | Contrast |
|---|---|---|---|
| `--paper` | `#F2EFE8` | Page background | |
| `--card` | `#FBFAF6` | Inside exhibits: figures, tables, the form box | |
| `--ink` | `#141413` | Text, rules, primary buttons, dark bands | 16.1 on paper |
| `--ink-2` | `#4A4844` | Secondary text: ledes, captions, labels | 7.9 on paper |
| `--hair` | `#CBC6BA` | Hairlines inside a block. Never text. | 1.5 (decorative) |
| `--pen` | `#C23B22` | Findings, DRIFT, focus rings, the key word in h1 | 4.6 on paper, 5.1 on card |
| `--pen-tint` | pen at 8% | Background of flagged rows and DRIFT flags | |
| `--amber` | `#8A5A00` | WATCH only | 5.7 on card |
| `--amber-tint` | amber at 12% | Background of WATCH flags | |

On dark surfaces (the ticker and footer) use the `-on-ink` variants:
`--pen-on-ink` `#FF7A5C` (7.2), `--amber-on-ink` `#E9B949` (10.1),
`--ok-on-ink` `#B9C7BD` (10.5), and `--ink-muted` `#B8B4AA` (8.9) for body
text.

Rules:

- About 95% of any screen is paper and ink. Red is for marks, not
  decoration, so keep it rare.
- Signals have fixed colors. DRIFT is pen, WATCH is amber, and CLEAN is
  `--ink-2` with a hollow circle. CLEAN stays neutral: no bright green
  anywhere on the site.
- Dark surfaces are bands (ticker, table header, footer), never whole
  sections.
- Any text color must reach 4.5:1 on its background. Check new pairs before
  shipping.

## Type

Three families, all loaded from Google Fonts in one `<link>` that doesn't
block render (`media="print"` plus `onload`, with a `<noscript>` fallback).
If you need a new weight, add it to that same URL. The browser fakes any
weight that isn't loaded, and it looks bad.

| Role | Family | Loaded | Used for |
|---|---|---|---|
| Argument | Newsreader | 400, 500, italic 400 | h1, h2, rate names |
| Reading | IBM Plex Sans | 400, 500, 600 | Body text, buttons, h3, nav |
| Data | IBM Plex Mono | 400, 500 | Every number, ID, price, label, flag, axis, and the ticker |

Scale:

| Element | Size | Weight | Notes |
|---|---|---|---|
| h1 | `clamp(40px, 5.6vw, 76px)` | 400 | Line height 1.02, letter spacing -0.025em. One per page. |
| h2 | `clamp(30px, 3.6vw, 46px)` | 400 | Line height 1.08 |
| h3 (sans) | 17px | 600 | Inside text columns |
| h3 (serif) | 24px | 500 | Rate card names only |
| Lede | 18px | 400 | `--ink-2`, max 560px wide |
| Section sub | 17px | 400 | `--ink-2`, max 640px wide |
| Body | 15 to 16px | 400 | Line height 1.55 |
| Mono label | 11 to 12px | 400 to 500 | Uppercase, letter spacing 0.04 to 0.06em |

Rules:

- If it's a number, set it in mono. Use `font-variant-numeric: tabular-nums`
  and right-align numeric columns.
- Headings use sentence case. Only short mono labels are uppercase.
- The italic word in h1 is the page's only italic: one word, underlined in
  pen. Don't add italics anywhere else.
- Don't bold whole sentences. Bold marks a name: a pool name, a figure, or
  the start of a note.

## Layout

- Content width: max `1200px`, with a `clamp(16px, 4vw, 48px)` gutter.
- The hero is two columns, argument on the left and an exhibit on the right.
  Text is left-aligned. Nothing is centered.
- Every section after the hero uses the report grid: a `220px` label column
  and the content beside it. The label is a mono two-digit number and a name
  (`01 Method`, `02 Sample`). Number sections in order, and renumber them all
  if you insert one.
- Rules:
  - A 2px ink rule starts a major block (section labels, the key figures
    row, the rate card).
  - A 1px ink rule separates sections and rows.
  - A `--hair` rule separates items inside a block.
  - Use dotted hairlines only inside tape-style tables.
- Exhibits (figures, tables, the timeline, the form) get a 1px ink border on
  `--card`. Only the hero figure gets the hard `6px 6px 0` ink shadow, so
  there's one per page.
- Vertical rhythm: sections use `clamp(56px, 7vw, 96px)` padding. Don't add
  one-off margins. Reuse `.sub` and the existing spacing.
- Breakpoints:
  - At 1180px the rate card stacks.
  - At 960px the hero, the section grid, and the signup collapse to one
    column, and the nav links hide.
  - At 640px tables stack into records, and the figure columns go vertical.

## Components

Reuse these before you invent anything. The class names are the ones in
`index.html`.

- **Masthead** (`.mast`). Logo, three anchor links, and one small primary
  button. Keep it to that.
- **Logo** (`#mark` symbol). Three tape rows with the short middle row in
  pen. Reference it with `<svg><use href="#mark"/></svg>` and set colors
  with `--mark-a` and `--mark-p`. The favicon is the same drawing as a data
  URI. Don't redraw, recolor, or animate it.
- **Ticker** (`.ticker`). The script builds it from the sample table, so
  edit the table, not the ticker. It's the only animation on the site, and
  it stops under `prefers-reduced-motion`.
- **Dateline** (`.dateline`). One mono line above h1 with the positioning
  statement. It's not a badge, so don't box it.
- **Buttons** (`.btn.primary`, `.btn.secondary`, `.btn.small`). Square, 1px
  ink border. Primary is ink and turns pen on hover. Secondary is outlined
  and fills ink on hover. Use at most one primary per row of actions.
  Labels are verbs naming what happens ("Request surveillance"), never
  "Learn more" or "Get started".
- **Figure** (`figure.tape`). A mono head line, the content, and a
  `figcaption` starting "Fig. N." The caption is required. Number figures in
  page order.
- **Annotation** (`.tape .note`). A pen box with a mono label (`Σ OBL-0217`)
  and one sentence stating the finding with numbers. Use it in any exhibit
  that shows a flag.
- **Flagged row** (`tr.hit`). Pen text on pen tint, with a 3px pen bar on
  the first cell.
- **Signal flag** (`.flag.alert`, `.flag.warn`, `.flag.ok`). The only labels
  are DRIFT, WATCH, and CLEAN. Adding a fourth changes the methodology, so
  that's Kai's call.
- **Data table** (`.sheet`). An ink header row with mono uppercase column
  names, `--card` rows, and hairlines. Give each cell a role class: `.pool`,
  `.num`, `.mand`, `.find`, or `.sig`. Keep the explicit `role` attributes,
  and give each stacked cell a `data-k` label, so it still reads as a table
  on phones. End it with a `.sheet-foot` line saying what's shown.
- **Key figures** (`.figures`). Big mono numbers with a one-line sans
  description. Every figure needs a source before it ships (see below).
- **Numbered columns** (`.cols`). An ink rule, a pen mono number, an h3, and
  a paragraph. These are text columns, not cards, so no boxes and no icons.
- **Timeline** (`.timeline`). Shows cadence. Ticks are ink, flags are pen,
  axis labels are mono. Put flags on exact positions (`calc(100% * week /
  52)`), never eyeballed percentages.
- **Contents list** (`.contents`). Roman numerals in mono, with hairline
  rows.
- **Rate card** (`.rate`). One row per product: serif name, mono price with
  a mono sub-label, a dash list, and an action. `.rate.feature` gets the pen
  bar. Use it on at most one row, and only for the product we actually
  recommend.
- **Footer**. An ink band with the logo, the disclaimer, and contact details
  in mono.

### Adding a section

```html
<section class="sec" id="slug">
  <div class="label"><b>05</b>Name</div>
  <div>
    <h2>Sentence-case claim the section proves</h2>
    <p class="sub">One or two sentences of context.</p>
    <!-- exhibit: .sheet, figure.tape, .timeline, .cols, or .rates -->
  </div>
</section>
```

Every section makes one claim in its h2 and backs it with one exhibit. If
there's nothing to show, the section probably doesn't need to exist.

## Data and copy

Tapewatch is a research publisher. The design only works if the content
holds up.

- **Illustrative data says so.** Any exhibit that isn't real data carries
  "Illustrative" in its caption. Its numbers must not match a real finding
  (Fig. 1's cluster deliberately doesn't add up to Pool A's 11.8%). Use
  placeholder IDs in the `L-0000` and `OBL-0000` pattern. Never use
  realistic-looking contract addresses or real names.
- **Every new number needs a source.** A footnote, a link, or a methodology
  note. The current key figures ($12B+, ~25%, 0) don't have sources yet, so
  don't add more like them.
- **Facts and method, no advice, no motive.** Findings describe what the
  tape shows ("top borrower reached 11.8% via affiliated entities"), never
  intent ("the manager hid…") or advice ("sell").
- **Positioning, pricing, signal labels, and the methodology are Kai's
  call.** Flag any change to them in the PR. Don't just ship it.
- **Writing.** Apply the `unslop` skill to new copy: plain words, sentence
  case, no em dashes, and no "unlock", "seamless", or "revolutionize".

## Motion and interaction

- Only the ticker moves, and it stops under reduced motion. No scroll
  animations, parallax, counters, or hover lifts.
- Hover changes color only, over 150ms.
- Focus is a 2px pen outline offset by 3px. Never remove it.
- Decorative duplicates (the ticker) get `aria-hidden="true"`. Exhibits that
  carry meaning get a text alternative (the timeline has `role="img"` and an
  `aria-label`).

## Technical

- Buildless: one `index.html`, inline CSS and JS, and no framework. Any
  library comes from a CDN with an exact pinned version, and it needs a
  reason the PR states.
- New values go in `:root` as tokens. Keep the three-line comment at the
  top of the `<style>` block accurate.
- Inline scripts stay small. Build DOM with `textContent` and
  `createElement`, not `innerHTML` from data.

## Before opening a PR

Render the page in Playwright (see AGENTS.md) and check:

- [ ] Screenshots at 390px and 1440px, before and after.
- [ ] Zero horizontal overflow at 390, 980, 1024, 1200, 1440, and 2560px
      (`document.documentElement.scrollWidth - innerWidth === 0`).
- [ ] No console errors except third-party embeds blocked by the sandbox.
- [ ] Ticker is still with reduced motion (`reducedMotion: 'reduce'`).
- [ ] Every `data-event` attribute and Tally link is still there, and UTM
      params still reach Tally links.
- [ ] No new hex values outside `:root`, no new fonts or weights missing
      from the font URL, and no rounded corners.
- [ ] Any new exhibit has a caption, and illustrative data is labeled.
- [ ] Copy changes to positioning, pricing, or methodology are listed for
      Kai in the PR body.

## Changing the system

The guide can change, but on purpose. A new token, component, font, or
breakpoint gets added to this file in the same PR that uses it, with a line
in the PR body saying why. Changes to the palette, typefaces, logo, or
signal labels need Kai's approval before they merge.
