---
name: cmf-board
description: Builds colour, material and finish (CMF) directions for a product and saves them as an editable SketchMonkey CMF sheet. Use for requests like 'make a CMF board', 'what finishes would suit my headphones', 'give me three colourways for this bottle', 'material options for a kettle' or 'CMF sheet for this concept'.
---

# CMF board

Help people choose how their product looks and feels: colours, materials and finishes, part by part. Start with a clear table in the chat, then save it as an editable CMF sheet if they want to keep it.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. The table and saved sheet use no render allowance; optional swatch renders use one image render each. The full house rules are in the `studio` skill.

## Step 1: Understand the product's parts

List the visible parts (for example body, lid, base, button, cable). Note anything that's fixed (material, budget, sustainability, a brand colour). Ask one question at most.

## Step 2: Propose colourways in the chat (free)

Give two to four colourways. Each one gets a short name, a one-line mood and a part-by-part table:

**Colourway A · "Studio Sand"**: warm and calm, made for the kitchen.

| Part | Material | Finish | Colour |
|---|---|---|---|
| Body | Recycled aluminium | Bead-blasted, clear anodised | Warm Silver #C9C5BE |
| Base | Oiled walnut | Matte oil | Walnut #5C4033 |
| Dial | Zinc alloy | Fine knurl, satin | Champagne #CBB892 |

Then add one line on why it works and one practical note (wear, fingerprints, cleaning, cost tier). `${CLAUDE_SKILL_DIR}/references/cmf-vocabulary.md` (the `references` folder next to this file) has precise material, finish and colour-role vocabulary. `enhance_prompt` (free) can also suggest CMF language for a product; use its ideas, not its text verbatim.

## Step 3: Save as an editable CMF sheet (when they want to keep it)

1. Use the `projectId` from earlier in the conversation, or call `create_project` with a short `name` and the `brief`.
2. Call `generate_directions` with the `brief` and `projectId`, and let the person pick the lens that matches their favourite colourway (Step 2's styles map naturally: precise → Ren, soft → Maya, premium → Kai, dramatic → Zola, futuristic → Nova).
3. Call `select_direction` with the `projectId` and the chosen `directionId`. This replaces any earlier choice on the project; mention that if one existed.
4. Call `create_campaign` with the `projectId`, a `name` (for example "CMF · Studio Sand"), the `brief`, `formats: ["cmf_sheet"]` and the **same `directionId`**. Without `directionId` the sheet falls back to the Ren style. If the person has a SketchMonkey render of the product, pass its image link as `backgroundUrl`.
5. The sheet starts with placeholder text: the headline repeats the brief, the body text is a truncated design rationale and the tagline reads "NEURAL DEEP · … SERIES". Call `inspect_artboard`, then `edit_artboard` with a proper `headline` (the colourway name), `subheadline` (materials in a few words), `bodyText` (one or two sentences on the colourway, from your table), `tagline` (the product or brand name) and `accentColor` (the colourway's accent hex). Call `inspect_artboard` again and confirm that only those fields changed.
6. Tell the person the sheet is saved in their SketchMonkey project, with its size (1920×1200).

## Step 4: Show the materials (optional, uses renders)

Offer a visual: a detail close-up of the hero material or a colourway line-up of the product (see the `product-shots` recipes). One render each; confirm first.

## Exports

`get_artboard_export_metadata` returns the sheet's size and any background image link. It does not produce a finished PNG or PDF; say so plainly if someone asks for a file.

## Boundaries

CMF directions are conceptual design proposals, not tested material specifications, supplier quotes or compliance approvals. Suggest that people confirm finishes with their manufacturer. Use only IDs and image links that SketchMonkey returned for this account.
