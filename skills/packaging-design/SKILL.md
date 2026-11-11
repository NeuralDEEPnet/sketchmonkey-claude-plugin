---
name: packaging-design
description: Packaging design with SketchMonkey, for boxes, cartons, sleeves, labels, bottles and jars, pouches, tins, gift sets, mailer boxes and the unboxing moment. Takes packaging from a written pack specification (format, size, material, print finishes and what goes on each face) to a consistent set of front, three-quarter, open and shelf views, and on to unboxing videos and a brief for a packaging supplier. Use for requests like 'design a box for my candle', 'what could our tea tin look like', 'make a gift set for the launch', 'design a label for my hot sauce', 'show the unboxing' or 'how would this look on a shelf'.
---

# Packaging design

Help people design packaging the way a packaging designer does: the format and size first, then material and finish, then what each face says. The pack has two jobs, to protect the product and to be chosen, and every decision should serve one of them.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each image uses one render from the person's allowance; a full view set is four renders, so confirm before starting it. The full house rules are in the `studio` skill.

## Step 1: Write the pack specification (free)

Before any render, write a specification of 70 to 130 words. It plays the role the product fingerprint plays in `product-shots`, and it goes into every prompt so every view shows the same pack.

- **Product and channel:** what goes inside, its size and weight, and where the pack is seen first (shelf, online listing, gift, delivery).
- **Format:** the structure in plain words ("rigid two-piece box with a lift-off lid", "tuck-end folding carton", "kraft mailer with a printed sleeve"). Formats and when to use them are in `${CLAUDE_SKILL_DIR}/references/pack-formats.md` (the `references` folder next to this file).
- **Outer size:** width, depth and height in millimetres, from the product size plus protection.
- **Material and finish:** board or substrate, colour, and print finishes ("uncoated 350 gsm cream board, one-colour print, blind-embossed mark on the lid").
- **Faces:** what sits on the front, top, sides and back, as shapes and zones rather than words ("small centred mark in the upper third, one line of small text below, a coloured band around the base").
- **Inside:** insert or tray, tissue, how the product sits, and the first thing seen when it opens.
- **Must not change:** three to five traits that define the pack.

Ask one question if the product size or the channel is unclear; otherwise state what you assumed in one line. If the person has brand rules saved, use those colours and say so.

## Step 2: Explore directions (free)

For new packaging, call `generate_directions` with the specification as the `brief`, and present the five directions as a short board, the same way `explore-concepts` does. Read each lens for packaging:

| Lens | As packaging |
|---|---|
| Ren | Precise and reduced; a strict grid, one or two colours, technical clarity |
| Maya | Friendly and tactile; soft colours, rounded shapes, easy to open |
| Kai | Premium and polished; rigid board, foil or emboss, gift-ready |
| Zola | Bold and editorial; strong contrast, unusual structure, a statement on the shelf |
| Nova | Organic and experimental; moulded fibre, natural textures, flowing pattern |

The tool's materials are often written for gadgets (CNC aluminium, moulded polymer). Use each direction's mood, palette and form language, say so in one line, and keep the board, print and finishes from the pack specification.

Skip this step when the person already knows the look they want.

## Step 3: Render the view set

The standard set, in this order:

1. **Front**, `4:3`: straight-on packshot of the main face. The design check.
2. **Three-quarter**, `4:3`: the hero, showing front, side and top.
3. **Open**, `4:3`: lid off or flaps open, the product in its insert.
4. **In context**, `16:9`: on a shelf among neutral neighbours, or on a doorstep or desk for delivery packs.

Start with the front alone when the design is still open, review it with the person, then render the rest. Camera, light and wording for each view and format are in `${CLAUDE_SKILL_DIR}/references/pack-views.md`.

Write each prompt yourself:

> **[view]** of **[full pack specification]**. **[direction's design language]**. **[setting and surface]**. **[lighting]**. **[camera and lens]**. Photorealistic packaging photograph, true-to-material, blank label areas, no readable text, no logos, no barcodes.

Call `render_concept` with:
- `prompt`: the prompt above.
- `preset`: `kai` for most packaging; it adds polished, retail-ready styling. Leave `preset` out for uncoated, kraft and moulded-fibre packs, so your prompt alone sets the look. `zola` only for moody key visuals. Avoid `ren`, `maya` and `nova` here: they add hard-surface, screen-like or glitch effects that don't suit board and paper.
- `autoEnhance: false`, because the prompt is complete.
- `aspectRatio` from the list above. For a `1:1` listing image, also write "square 1:1 format" in the prompt.

Start all renders in the set, then poll each `jobId` with `get_job` about every 15 seconds.

**Words on the pack.** Image renders garble lettering, so design the pack with blank zones and shapes, and describe the type as "a small line of fine text" rather than quoting it. For the real name and copy, offer the `campaign` skill, which sets true, editable typography over the render. Say this once, plainly, the first time you show a pack.

## Step 4: Keep it the same pack

Once the person likes the three-quarter render, offer to save the pack with `save_subject_model`: `kind: "object"`, a short `name`, the specification as `identityLock`, the must-not-change traits as `immutableTraits`, and the render's `imageUrl` as `heroImageUrl`. Pass the returned ID as `subjectModelId` in later renders and videos. Say plainly that this improves consistency but doesn't guarantee identical results.

## Step 5: Review like a studio

Look at every render before replying. Check:
- **Structure:** the format matches the specification (a lift-off lid is not a hinged lid), edges and folds are where real board would fold.
- **Proportion:** the pack is the right size for the product; no oversized box for a small item.
- **Faces:** zones, bands and marks are where the specification puts them, and the same on every view.
- **Stray text:** garbled lettering, invented logos, barcodes or certification marks. Recycling symbols and certification marks must never appear unless the person holds them.
- **Inside:** the product sits in the insert the specification describes.

Present the set as a contact sheet: view name, one line on what it shows, and `[Open full-size image](imageUrl)`. Then give a short crit: what works, and the one change that would improve the pack most.

Keep the reply to one phone screen. Lead with the views; don't repeat the pack specification after rendering. One line on anything you assumed ("I assumed a 105 mm cube with a 35 mm lid") is enough, and the full specification is there when the person asks for it. If you couldn't see an image, say so in one short sentence rather than listing checks for the person to do.

## Step 6: Next steps

- An unboxing or reveal video (`turnaround-video`; a `static_tripod` lid lift or a slow `push_in` on the open box).
- Colour and finish options for a range: three flavours, sizes or tiers (`cmf-board`).
- The real name and copy on a poster, post or listing image (`campaign`).
- A shop shelf or a pop-up stand to show it on (`spatial-design`).
- A brief for a packaging supplier: sizes, board, print and finish per part, quantities and open questions (`engineering-handoff`).

## Boundaries

- Design original packaging. Don't copy a real brand's pack, logo or trade dress; describe the qualities the person likes instead.
- Renders are design proposals. They are not dielines, print-ready artwork, colour proofs or transit-test results, and they don't confirm food-contact safety, child resistance, or legal labelling such as ingredients, weights, warnings or recycling marks. Name those as topics to check with the packaging supplier and the relevant regulator.
- When the pack is shown to sell a real product, keep claims honest: no "recyclable", "compostable", "organic" or similar unless the person confirms it is true for the real pack.
