---
name: campaign
description: Turns a product or brief into an editable multi-format SketchMonkey launch campaign (A4 poster, square post, 9:16 story, 16:9 banner and CMF sheet) with strong copy, and edits existing SketchMonkey layouts and artboards precisely without touching the artwork. Use for 'make a launch campaign', 'poster and Instagram versions of my product', 'a banner for my website', and for any change to a saved layout or artboard such as 'change the headline on my square artboard', 'update the tagline on the story' or 'try a serif font on the poster'.
---

# Launch campaign

Turn one product and one message into a consistent set of campaign layouts the person can keep editing.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Campaign layouts and text edits use no render allowance; a new background render uses one image render. The full house rules are in the `studio` skill.

## Formats

| Format | Size | Use it for |
|---|---|---|
| `poster_a4` | 1240×1754 | Print posters, flyers, PDF one-pagers |
| `square_1x1` | 1400×1400 | Instagram and LinkedIn feed posts, marketplace banners |
| `story_9x16` | 1080×1920 | Instagram and Facebook Stories, Reels and TikTok covers |
| `banner_16x9` | 1920×1080 | Website heroes, YouTube, slides, email headers |
| `cmf_sheet` | 1920×1200 | Colour, material and finish presentations |

If the person doesn't say which formats, make `square_1x1` and `story_9x16` and say so.

## Step 1: Gather the essentials

You need the product, the one message to land, the audience and, ideally, a call to action ("Pre-order now", "Available 1 March"). Ask one question at most.

## Step 2: Line up the artwork

Layouts look best with a product image as the background. The background must be a SketchMonkey render from the person's own account:
- Use a render from earlier in the conversation if there is one.
- Otherwise offer to make one with the `product-shots` "dramatic key visual" or "hero" recipe, framed with space for text (one image render).
- Images from elsewhere can't be used as backgrounds.

## Step 3: Set up the project and direction

1. Use the `projectId` from earlier, or call `create_project` with a short `name` and the `brief`.
2. Call `generate_directions` with the `brief` and `projectId`, summarise the five looks in a line each, and let the person choose. If they already picked a lens earlier, reuse it.
3. Call `select_direction` with the `projectId` and `directionId`. This replaces any earlier choice on the project.

## Step 4: Create the layouts

Call `create_campaign` with:
- `projectId`, a campaign `name` and the `brief`.
- `directionId`: **the same lens as Step 3**. Without it the campaign falls back to the Ren style.
- `formats`: the chosen formats.
- `backgroundUrl`: the render's image link from Step 2, if there is one.

## Step 5: Write the copy, then apply it

Every new layout starts with automatic placeholder text that must not reach a customer: the headline repeats the brief in capitals, the body text is a truncated design rationale ("Grounds … in Dieter Rams / Braun functionalism…"), and the tagline reads "NEURAL DEEP · REN SERIES", SketchMonkey's own studio name. Write proper copy for all four text fields (guidance in `${CLAUDE_SKILL_DIR}/references/copy-and-formats.md`, the `references` folder next to this file):
- **Headline:** seven words or fewer, one idea.
- **Subheadline:** one line with the key benefit or detail.
- **Body text:** one or two plain sentences about the product, or the person's own details such as price or availability if they gave them.
- **Tagline:** the brand or product name, or the call to action. Never leave the "NEURAL DEEP" placeholder.

Show the copy, then for each artboard: `inspect_artboard`, `edit_artboard` with `headline`, `subheadline`, `bodyText` and `tagline`, then `inspect_artboard` again to confirm the four fields changed and the artwork, font and colours didn't. Shorten the headline for the story format if needed.

## Step 6: Present

List each layout with its format, size and headline, and say it's saved in their SketchMonkey project. Offer next steps: try another font or accent colour, write alternative headlines (`brand-kit` keeps them on-brand), add a format, or make a 360° video for the story (`turnaround-video`).

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
