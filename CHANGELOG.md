# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres
to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.3.0](https://github.com/metreeca/skin/compare/v0.2.0...HEAD)

### Added

- `presets/roboto.css` and `presets/inter.css` - alternative entries, included in place of `index.css`, that set the
  interface in bundled variable faces: Roboto, Roboto Condensed and Roboto Mono for the Metreeca brand, or Inter,
  Inter Tight and Geist Mono. Each preset scales its mono face to the text around it, so code spans and mono labels
  need no size of their own. Each also follows every face with a metric-matched platform face, so content-sized
  tables, grids and labels keep their width when the bundled faces arrive, so the layout holds still as they load
- `colorFlag`, `colorFlagStroke`, `backgroundColorFlag` - a fifth step of the meaning scale, between `pass` and
  `warn`, which singles a thing out for attention although nothing has gone wrong; the important Markdown alert
  takes it in place of the note blue, so it no longer reads as a plain note beside the notes around it
- Editor colours - colours an author picks for content, as text or as fill: a neutral column of `colorBlack`,
  `colorGray` and `colorWhite`, plus red, yellow, green, blue and purple in three steps each, as `colorRedStrong`,
  `colorRed` and `colorRedSubtle`. Only the plain step carries a contrast guarantee, legible as large text
- Token additions for components to read in place of literals, so an app retuning one reaches the whole interface:
  - `borderColorField` - the edge of a field, held to the contrast a control boundary needs
  - `colorStrongOver` - legible text over a fill painted in the strong accent, whatever accent an app supplies
  - `backgroundColorHoverNeutral`, `backgroundColorPressedNeutral` - states for a control that answers to no accent,
    visible on whatever surface it stands on except an overlay, where controls take the accent states
  - `lineHeightDisplay`, `letterSpacingCaps`, `inlineSizeProse` - display leading, caps tracking and prose measure
  - `textTransformHeading`, `textTransformCaps` - the casing of headings and of labels in capitals, which a subtree
    recases by restating one token, so a section can title itself in capitals without rules of its own
  - `strokeWidthStrong` - a stroke matching `fontWeightStrong`, for glyphs set beside strong text
  - `backdropFilterGlass` - the blur behind `backgroundColorGlass`, typed by the new `Filter` ladder
  - `durationSpin` - the period of a busy mark, which keeps turning under `prefers-reduced-motion` so that it never
    signals finished work while it is still under way, as a stopped spinner would
- Base styles for the markup the reset used to leave bare, so plain documents need no classes:
  - Forms - fields share one height and edge; disabled fields recede, read-only fields keep their value legible;
    checkboxes and radios match the text size; labels, fieldsets, legends, meters, colour wells, file buttons and
    search clear buttons follow the design system; date and time pickers show their button only on hover or focus,
    and never on a field that takes no input; an unanswered required menu reads as an empty field
  - Text - `h4` to `h6`, `b`, `i`, `cite`, `dfn`, `var`, `kbd`, `samp`, `mark`, `sub`, `sup` and titled `abbr`
  - Blocks - media held inside their column, `figure` captions, `details` disclosures with a chevron, `dialog` as an
    overlay surface over the blanket, table captions, and images floated by `align` that stretch across narrow screens
  - Navigation - nested lists in a `nav` read as a compact table of contents, with collapsible top-level groups and
    the `aria-current` link marked out in the strong accent, so readers see where they stand
  - Heading groups - an `hgroup` sets a page or section title as display type, with an eyebrow above and a lead below
  - Text wrapping - running text avoids a lone last word and multi-line headings are balanced, while text areas and
    editable content keep the platform wrapping, so words being typed never jump between lines
- `data-offscreen` - hides an element from sight while keeping it in the accessibility tree, for a status region or
  the name of an icon control, which the `hidden` attribute would remove for every reader

### Changed

- **Breaking**: `index.css` no longer bundles the Roboto faces, and the font tokens default to the platform faces.
  To keep the Metreeca brand faces, import `@metreeca/skin/presets/roboto.css` in place of `@metreeca/skin/index.css`
- **Breaking**: `data-theme` is renamed `data-scheme`. Replace `data-theme="dark"` with `data-scheme="dark"`; an
  element still carrying the old name silently falls back to the platform scheme, so search for it before upgrading
- **Breaking**: `colorInfo`, `colorInfoStroke` and `backgroundColorInfo` are renamed `colorNote`, `colorNoteStroke`
  and `backgroundColorNote`, and their custom properties `--skin--color-info*` and `--skin--background-color-info`
  become `--skin--color-note*` and `--skin--background-color-note`; the old names are gone, with no alias
- **Breaking**: the `Flag` type naming the viewport tokens is renamed `Breakpoint`
- **Breaking**: the base size is set on `body`, leaving the root at the size the reader chose, so `fontSize` means
  one length at every depth. A measure written in `rem` to follow the base text size has to move to `em` or a token.
  On the widest screens the base size now grows to `1.25rem`, as text read from further away looked small
- **Breaking**: table cells no longer collapse their borders, so a sticky header keeps its rule while rows scroll. A
  border set on a row or row group no longer draws, and a `hidden` cell border no longer suppresses its neighbour's
- **Breaking**: `colorOver` is the text colour over the caution fill only. A fill painted in `colorFail` takes
  `colorStrongOver` for its text instead, since black over the light failure red falls short of AA
- Colours - every anchor and derived role is retuned so that it holds its WCAG budget on the surfaces it is painted
  on, in both schemes, and stays inside the sRGB gamut so every browser paints the same colour:
  - the meaning scale anchors are text grade in both schemes, so each serves as text or as a mark, and each stroke
    role is now its anchor; caution text is never set on the caution tint, where `colorWarn` falls short of AA
  - the caution step is one dark gold in the light scheme and a gold in the dark one, serving as text, mark and fill
    alike, in place of a yellow fill beside a separate orange stroke that read as brown
  - dark state fills, status tints and raised surfaces now read as distinct from the page and from each other
  - hover and pressed colours step away from the page in either scheme, enabled controls are told apart from links,
    and a link under the pointer stays clearly apart from the body text, rather than fading into it
  - `colorPlaceholder`, `colorLabel` and `colorFocus` hold their budgets on every surface they are set on, the
    placeholder no longer sharing the disabled colour; `borderColor` follows `colorDisabled`
  - the light table stripe is fainter, every status tint takes the same share of its anchor, and
    `backgroundColorGlass` is a pale, nearly opaque tray in place of a mid-grey slab
- Markdown alerts - drawn on the page behind a bar in the stroke of their step, in place of a tinted box
- Form fields - an invalid value is marked once the reader has edited it (`:user-invalid`), or at once where the app
  sets `aria-invalid="true"`; selects are marked too, and the focus ring follows `:focus-visible`. Values read in
  the text colour whatever colour their label takes, so an entered value never reads as part of the label
- `code`, `kbd`, `samp` - set at the size of the surrounding text, a preset scaling its mono face itself
- `small` - set in the placeholder colour; `dt` terms - set at the size of the surrounding text
- Headings - `h2` stands out from `h3` at a glance, `h4` to `h6` take the label colour, and a heading adds no room
  where its container, a heading group or another heading already sets it apart from what precedes it
- Enlarged images - an image carrying `active` sits on an overlay card at its own size within a narrow margin, in
  place of stretching over the viewport, so pictures with transparent areas stand on a surface
- Quotations and preformatted blocks - more room at either side; a focusable preformatted block shows the focus mark
- Focus marks - links, `details` summaries and preformatted blocks are ringed with the corners of a control

### Fixed

- Date fields, menus and text fields stood at different heights
- `progress` was painted as a flat green bar in Blink-based browsers
- The invalid mark doubled the edge of a field rather than replacing it
- `button:active` painted its text in the focus grey rather than in `colorPressed`
- Focus and invalid rings around links, preformatted blocks, `details` summaries, checkboxes and radios were hidden
  under the background of the content following them, so the keyboard position was partly lost
- The focus ring of a checkbox or radio squared off around the platform's rounded corners

### Removed

- **Breaking**: `look`, its `--skin--look` custom property and the `look` option of `css()` are removed: one value
  could not quieten the buttons of a toolbar without its fields. A binding package now sets a default look per kind
  of widget, and a widget stating `look` itself is unaffected, so only area-wide settings need replacing

## [0.2.0](https://github.com/metreeca/skin/compare/v0.1.0...v0.2.0) - 2026-11-05

### Added

- `@metreeca/skin` - the design system moved over from `@metreeca/tile`: the `skin` token map naming every
  `--skin--*` custom property, covering typography, spacings, scalings, colours, borders, elevations, palettes,
  layers, motions, opacities, viewports and visuals, so components and apps address every token by name
- `@metreeca/skin/index.css` - the stylesheet stating the token values in both colour schemes and styling plain
  document markup, Markdown alerts and highlight.js code inside the `skin` cascade layer, so that an app or component
  overrides any of it with an ordinary unlayered rule, needing no `!important` and no control over load order
- Metreeca brand defaults: slate and orange accent anchors and the bundled variable Roboto faces, which an app
  replaces with its own brand by redefining the anchor and face tokens alone, with no change to a component
- Specimen page, built with the docs, showing every token live in both colour schemes with contrast readouts and a
  brand tuner previewing, in both schemes at once, the `:root` override an app would state for its own accents

## [0.1.0](https://github.com/metreeca/skin/releases/tag/v0.1.0) - 2026-11-05

Initial release, claiming the package name ahead of the design system moving over from `@metreeca/tile`.

- `@metreeca/skin` - root module, empty pending the design system sources
