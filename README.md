# Kerning class assistant

Review kerning classes in the browser. Drop in a `.glyphs` file, sort the classes
out, download the finished font. Nothing is installed and the font never leaves
your machine — it is read and written in the page itself.

**https://nnedashkovsky.github.io/kerning-assistant/**

## What it does

* **Case** — pick a glyph and the assistant gathers its companions by gap profile,
  laid out in bands of closeness
* **Review** — the classes already in the font, ranked by spread: the ones where
  somebody stands out come first
* **Twin classes** — capitals against small caps, `@Y` against `@Y.alt01`. Their
  memberships should mirror; the gaps are shown and fixed with one button
* **Similar classes** — pairs that are nearly one class already
* **All classes** — the whole font, unassigned glyphs included, with reassignment

A running list of findings sits below: glyphs drawn alike but filed apart, and —
separately — glyphs drawn alike whose sidebearings disagree. The second is a
spacing bug rather than a grouping one, and the app says so.

## How closeness is measured

Each glyph gets a gap profile: at every scanline, the distance from the outline to
the edge of its advance. The distance between two glyphs is the weighted mean
relative difference between those profiles, in percent. Zones carry different
weight — body 1.0, above x-height 0.75, below the baseline 0.30, accents above cap
height 0.12 — so a difference in the body splits a class while one under the
baseline usually does not. Marks are skipped when profiling, which is why `Aacute`
always lands wherever `A` does.

## Writing back

Only the `kernLeft` and `kernRight` lines of the glyphs you changed are rewritten.
The file is not re-serialised, so outlines, components, anchors, kerning and
features are untouched by construction.

## Locally

`index.html` is self-contained: open it from disk, no server needed.
