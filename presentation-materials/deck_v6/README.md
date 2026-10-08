# Fifteen-slide conference deck

A separate, compressed version of the current Google presentation, built from the route proposed in [Capex2.md](../../presentation-review/Capex2.md). The original Google deck and earlier local decks are unchanged.

| File | Purpose |
|---|---|
| [main_deck.pdf](main_deck.pdf) | Ready-to-present, 16:9 PDF with exactly **15 slides**. |
| [main_deck.pptx](main_deck.pptx) | Editable PowerPoint for importing into Google Slides. Text, tables, diagrams, and curves use native editable shapes; all 15 slides include speaker notes. |
| [main_deck.md](main_deck.md) | Editable source containing all visible slide text, table values, and chart labels. |
| [speaker-notes.md](speaker-notes.md) | Speaking notes, timing, source links, and optional answers for discussion. |
| [preview.png](preview.png) | Overview of all 15 slides. Full-size page previews are in `previews/`. |

The speaking allocations total **18 minutes**, leaving two minutes of buffer within the 20-minute speaking limit and at least five minutes for questions in the 25-minute slot. This is a planning estimate; rehearse the actual delivery. Slide 11, the settling-depth comparison, is the first optional cut if needed. No backup pages are appended to the main PDF or PPTX; supporting reports are linked in the notes.

The closing QR code encodes **https://earthland.ai/ccs/**, which leads to charlie’s canonical Google presentation. This local alternative has not been published or substituted at that address.

## Editing

For a direct Google Slides workflow, import `main_deck.pptx` as a **new presentation**. It was opened and rendered successfully in LibreOffice; its Google Slides import has not been tested. Inspect the imported fonts and spacing before using that version for a talk.

For reproducible local changes, edit `main_deck.md` and/or `speaker-notes.md`, then rebuild from `pc_cap`:

```bash
PYTHONDONTWRITEBYTECODE=1 OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 \
../assets/envs/status-paper-20260911/bin/python -m aw.conference_deck_v6
```

That command regenerates the PDF and PPTX. PowerPoint or Google edits do not automatically update the Markdown. Preserve `---` slide separators and layout comments in the Markdown. Numerical table values are checked against saved experimental reports; changes to those numbers require a corresponding scientific source change. The layout check reports overlapping or off-page text.

To refresh the page previews after a rebuild, run from this directory:

```bash
pdftoppm -scale-to 1600 -png main_deck.pdf previews/slide
```

The existing overview `preview.png` is the visually reviewed build supplied with this edition; the command above refreshes the individual images.

## Provenance and checks

The source Google export had 30 pages and SHA-256 `79f7ff54fc4e4a1bd0e5789cee4e9e2406dfbe7cff89e0d1ead85d5a420f9112`. The source is the [canonical Google deck](https://docs.google.com/presentation/d/1ofdKlNOS3n_cKVoS4Ga_81xDDU7Rt0_j8sSf2aVuPLg/edit), fetched October 8, 2026. Later edits to that deck are not automatically incorporated here.

The presentation tables were checked against completed project reports. The survival curves were redrawn from the saved, hash-checked loss vectors and saved exponential fits; no new model calls, tail fits, or GPU jobs were run. The 15 PDF pages and the independently rendered PPTX pages match the Markdown text. All PDF pages were visually inspected, and the builder detected no text overlap or clipping.

Build code: [conference_deck_v6.py](../../../pc_cap/aw/conference_deck_v6.py). Numerical, layout, text-parity, and PowerPoint-render checks: [build records](../../../pc_cap/logs/presentation/deck_v6/).

Scientific scope remains explicit: the main learned reader is BP-trained; the two PC interventions are separate; legacy settling uses a different base checkpoint; observed tail shapes do not prove a power-law family; and the mixture guarantees a per-token likelihood bound rather than unchanged greedy answers or general semantic safety.
