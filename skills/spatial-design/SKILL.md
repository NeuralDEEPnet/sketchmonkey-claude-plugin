---
name: spatial-design
description: Spatial and interior design with SketchMonkey, for retail stands, pop-up shops, showrooms, exhibition booths, shop-in-shops, cafes, kitchens, studios and the rooms a product lives in. Takes a space from a written space package (footprint, zones, fixtures, materials and light) to a consistent set of overview, eye-level, fixture detail and plan views, and on to walkthrough videos. Use for requests like 'design a pop-up shop for our candles', 'show me a trade fair stand for the launch', 'what could our showroom look like', 'a display wall for twelve mugs', 'concept for a small coffee bar' or 'design the room our speaker sits in'.
---

# Spatial design

Help people design a space the way an interior or exhibition designer does: the footprint and the route through it first, then fixtures and materials, then light. A space that works in plan almost always works in the photographs.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each image uses one render from the person's allowance; a full view set is four renders, so confirm before starting it. The full house rules are in the `studio` skill.

## Step 1: Write the space package (free)

Before any render, write a package of 80 to 140 words. It plays the role the product fingerprint plays in `product-shots`, and it goes into every prompt so every view shows the same space.

- **Type and purpose:** what it is, who visits and what they should do there ("3 by 3 metre pop-up shop where passers-by pick up, smell and buy candles").
- **Footprint and height:** width, depth and ceiling height in metres, which sides are open, where people enter.
- **Zones and route:** what a visitor meets first, second and last (attract, try, buy), and how many people fit.
- **Fixtures, with counts:** "one 2.4 m oak counter, three plinths at 90 cm, one back wall with four shelves". Counts and sizes stop the renders from inventing furniture.
- **What is on show:** the products, how many, and how they are grouped. Describe each product in a short phrase; use its saved fingerprint when one exists.
- **Materials and colours per surface:** floor, walls, fixtures and accents, each with a colour name and approximate hex.
- **Light:** daylight or none, warm or cool, and the one thing the light should pick out.
- **Must not change:** three to five traits that define the space.

Ask one question if the footprint or purpose is unclear; otherwise state what you assumed in one line. Sizes, sightline rules and plain-language terms are in `${CLAUDE_SKILL_DIR}/references/space-planning.md` (the `references` folder next to this file).

## Step 2: Explore directions (free)

For a new space, call `generate_directions` with the package as the `brief`, and present the five directions as a short board, the same way `explore-concepts` does. Read each lens for spaces:

| Lens | As a space |
|---|---|
| Ren | Precise and reduced; a clear grid, few materials, everything aligned |
| Maya | Welcoming and easy to use; soft edges, warm timber, things at hand height |
| Kai | Premium and polished; editorial styling, deep finishes, flagship-store presence |
| Zola | Dramatic and sculptural; strong shadows, monolithic forms, one bold gesture |
| Nova | Organic and experimental; flowing forms and natural textures |

The tool's materials and rationale are often written for gadgets. Use each direction's mood and form language, say so in one line, and keep the materials and colours from the space package or the ones the person chose.

Skip this step when the person already knows the look they want.

## Step 3: Render the view set

The standard set, in this order:

1. **Overview**, `16:9`: the whole space from a raised front corner. The layout check.
2. **Eye level**, `16:9`: what a visitor sees on the way in, camera at 1.6 m.
3. **Fixture detail**, `4:3`: the counter, a plinth or one shelf, with products at true scale.
4. **Plan**, `1:1`: straight down, like a furnished floor plan.

Start with the overview alone when the layout is still open, review it with the person, then render the rest. View recipes for stands, shops, hospitality and home rooms are in `${CLAUDE_SKILL_DIR}/references/space-views.md`.

Write each prompt yourself:

> **[view]** of **[full space package]**. **[direction's design language]**. **[light]**. **[camera and lens]**. Photorealistic spatial design render, no text, no logos, no signage lettering, no people.

Keep the closing words "spatial design render" in every prompt. SketchMonkey reads them to describe the image as a room, with architectural wording and light, even when the package names products on show; without them a stand full of lamps can be treated like a single gadget.

Call `render_concept` with:
- `prompt`: the prompt above.
- `preset`: `ren` for most work, `kai` for premium retail and editorial looks, `maya` for homes and hospitality. Avoid `nova` for buildable proposals. For the Zola look, use `zola` only for mood images, not for the plan or the overview.
- `autoEnhance: false`, because the prompt is complete.
- `aspectRatio` from the list above. For `1:1`, also write "square 1:1 format" in the prompt.

Start all renders in the set, then poll each `jobId` with `get_job` about every 15 seconds.

Leave signs and lettering out of the renders: image models garble text. If the person needs their name on the stand, say where it would go ("lightbox above the counter") and offer the `campaign` skill for real typography.

## Step 4: Keep it the same space

Once the person likes the overview, offer to save the space with `save_subject_model`: `kind: "space"`, a short `name`, the package as `identityLock`, the must-not-change traits as `immutableTraits`, and the render's `imageUrl` as `heroImageUrl`. Pass the returned ID as `subjectModelId` in later renders and videos so the studio conditions on that image. Say plainly that this improves consistency but doesn't guarantee identical results.

## Step 5: Review like a studio

Look at every render before replying. Check, view by view:
- **Counts and sizes:** the number of plinths, shelves and products matches the package; nothing doubled or missing.
- **Scale:** counters at about 90 cm, doors at about 2.1 m, products the right size on their fixtures.
- **Route:** the entrance is open, nothing blocks the way to the counter, at least 90 cm between fixtures.
- **Consistency:** floor, wall and fixture materials match across views.
- **Stray text:** garbled signs, labels or price tags.

Present the set as a contact sheet: view name, one line on what it shows, and `[Open full-size image](imageUrl)`. Then give a short crit: what works, and the one change that would improve the space most. For a deeper review use the `design-review` skill.

Keep the reply to one phone screen. Lead with the views; don't repeat the space package after rendering. One line on anything you assumed is enough, and the full package is there when the person asks for it.

## Step 6: Next steps

- A slow walkthrough or reveal (`turnaround-video`; a `push_in` toward the counter or a `crane_arc` over the stand works better than a full orbit in a room).
- Material and colour options for floor, walls and fixtures (`cmf-board`).
- Photographs of the products on show (`product-shots`), or packaging to match the stand (`packaging-design`).
- A build package for a shopfitter or stand builder: fixture list, sizes, materials and open questions (`engineering-handoff`).
- Opening posters and social posts (`campaign`).

## Boundaries

- Design original spaces. Don't copy a real brand's store design, logo or signage; describe the qualities the person likes instead.
- Renders are design proposals. They are not measured drawings, structural, fire, electrical or accessibility approval, and they don't confirm that the layout meets a venue's or a building's rules. Name those as topics to check with the venue, a shopfitter or an architect.
- Spaces only: no real people's faces or likeness in the renders.
