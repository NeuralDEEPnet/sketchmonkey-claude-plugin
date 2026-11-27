---
name: campaign
description: Turns a design or brief into editable multi-format SketchMonkey layouts (A4 poster or board, square tile, 9:16 portrait board, 16:9 slide and CMF sheet) with clear copy, for design presentations and product launches, and edits existing SketchMonkey layouts and artboards precisely without touching the artwork. Use for 'make a presentation board of my design', 'a poster for our launch', 'a title slide for the design review', and for any change to a saved layout or artboard such as 'change the headline on my square artboard', 'update the tagline on the poster' or 'try a serif font on the slide'.
---

# Layouts: boards, posters and CMF sheets

Turn one design and one message into a consistent set of layouts the person can keep editing.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Layouts and text edits use no render allowance; a new background render uses one image render. The full house rules are in the `studio` skill.

## Formats

| Format | Size | Use it for |
|---|---|---|
| `poster_a4` | 1240×1754 | Printed boards and posters, one-page PDFs |
| `square_1x1` | 1400×1400 | Square tiles for boards and feeds |
| `story_9x16` | 1080×1920 | Portrait boards and phone-height posters |
| `banner_16x9` | 1920×1080 | Presentation slides, wide boards and page headers |
| `cmf_sheet` | 1920×1200 | Colour, material and finish presentations |

If the person doesn't say which formats, make `banner_16x9` and `poster_a4` and say so.

## Step 1: Gather the essentials

You need the design, the one message to land, who will read it and, for a launch layout, a call to action ("Pre-order now", "Available 1 March"). Ask one question at most.

## Step 2: Line up the artwork

Layouts look best with a design visual as the background. The background must be a SketchMonkey render from the person's own account:
- Use a render from earlier in the conversation if there is one.
- Otherwise offer to make one with the `design-views` "presentation key visual" or "hero" recipe, framed with space for text (one image render).
- Images from elsewhere can't be used as backgrounds.

## Step 3: Set up the project and direction

1. Use the `projectId` from earlier, or call `create_project` with a short `name` and the `brief`.
2. Call `generate_directions` with the `brief` and `projectId`, summarise the five looks in a line each, and let the person choose. If they already picked a lens earlier, reuse it.
3. Call `select_direction` with the `projectId` and `directionId`. This replaces any earlier choice on the project.

## Step 4: Create the layouts

Call `create_campaign` with:
- `projectId`, a `name` for the set and the `brief`.
- `directionId`: **the same lens as Step 3**. Without it the campaign falls back to the Ren style.
- `formats`: the chosen formats.
- `backgroundUrl`: the render's image link from Step 2, if there is one.

## Step 5: Write the copy, then apply it

Every new layout starts with automatic placeholder text that must not reach a customer: the headline repeats the brief in capitals, the body text is a truncated design rationale ("Grounds … in Dieter Rams / Braun functionalism…"), and the tagline reads "NEURAL DEEP · REN SERIES", SketchMonkey's own studio name. Write proper copy for all four text fields (guidance in `${CLAUDE_SKILL_DIR}/references/copy-and-formats.md`, the `references` folder next to this file):
- **Headline:** seven words or fewer, one idea.
- **Subheadline:** one line with the key benefit or detail.
- **Body text:** one or two plain sentences about the product, or the person's own details such as price or availability if they gave them.
- **Tagline:** the brand or product name, or the call to action. Never leave the "NEURAL DEEP" placeholder.

Show the copy, then for each artboard: `inspect_artboard`, `edit_artboard` with `headline`, `subheadline`, `bodyText` and `tagline`, then `inspect_artboard` again to confirm the four fields changed and the artwork, font and colours didn't. Shorten the headline for the portrait format if needed.

## Step 6: Present

List each layout with its format, size and headline, and say it's saved in their SketchMonkey project. Offer next steps: try another font or accent colour, write alternative headlines (`brand-kit` keeps them on-brand), or add a format.

## Editing an existing layout

People can ask for precise changes at any time. Editable fields:
- Text: `headline`, `subheadline`, `bodyText`, `tagline`.
- Style: `fontFamily` (`sans`, `serif`, `mono` or `grotesk`), `textAlignment` (`left`, `center` or `right`), `accentColor` (a hex value).
- Artwork: `backgroundUrl` (a SketchMonkey render from their account).

Always `inspect_artboard` first, send `edit_artboard` with only the requested fields, then `inspect_artboard` again and confirm the change and that everything else was preserved. Only edit artboards whose IDs SketchMonkey returned for this account.

## Exports

`get_artboard_export_metadata` returns each layout's size and background image link. It does not produce finished PNG or PDF files; say so plainly if someone asks for a download.

## Boundaries

Keep claims truthful: no invented awards, certifications, prices, reviews or specifications. Don't put real people's names or likeness in layouts.
