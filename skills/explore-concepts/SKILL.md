---
name: explore-concepts
description: Explores new product ideas through SketchMonkey's five design lenses (Ren, Maya, Kai, Zola, Nova) and renders the favourite directions as concept images. Use whenever someone asks for design directions, concepts or ideas for a physical product, even if they don't mention SketchMonkey, for example 'design a desk lamp', 'explore five design directions for a smart speaker', 'what could my water bottle look like', 'concept sketches for a kettle' or 'render it in the Nova style'.
---

# Explore concepts

Help people see what their product idea could become, compare directions side by side, and render the ones they love.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Exploring directions is free; each concept render uses one image render, so confirm before more than four. The full house rules are in the `studio` skill.

## Step 1: Sharpen the brief

A good brief covers what the product does, rough size, materials or constraints that are fixed, who it's for and the feeling it should give. If one of these is missing and matters, ask one question; otherwise assume and say so. Treat anything the person stated as fixed (for example "recycled aluminium") as a constraint for every direction.

## Step 2: Show five directions (free)

Call `generate_directions` with the `brief`. Nothing is saved and no allowance is used. If the work already lives in a project, also pass its `projectId`; any saved brand rules then shape the directions.

Present a compact board, one block per lens, in plain words:

> **🧑‍🔧 Ren · precise and engineered**
> Bead-blasted aluminium, crisp chamfers, a single signal-orange accent.
> Palette: Matte Anthracite #18181B · Warm Off-White #F4F4F5 · Signal Orange #EA580C
> Best if you want it to feel trustworthy and timeless.

Guidelines:
- Describe each lens by its look and feeling; keep its name as a label.
- Rewrite the tool's titles and headlines in your own words. They are generated mechanically and often repeat the brief.
- If a lens suggests materials that contradict the brief (for example bronze or titanium for an aluminium product), present it as an alternative take and keep the person's materials in the render unless they choose otherwise.
- End by asking which to render: one favourite, a shortlist, or all five (five renders).

The lens profiles in `${CLAUDE_SKILL_DIR}/references/lenses.md` (the `references` folder next to this file) help you describe, mix and render each lens well.

## Step 3: Render the chosen directions

For each chosen lens, write the prompt yourself:

> Concept render of **[product and purpose]**, **[fixed constraints]**. Design language: **[the lens's form language]**. Materials and finish: **[the person's materials, plus the lens's materials as accents where they fit]**. Colour palette: **[the direction's palette names and hex values]**. **[the direction's lighting]**. Three-quarter view, product fills about 60% of the frame, clean studio background. Photorealistic concept render, no text, no logos.

Call `render_concept` with:
- `prompt`: the prompt above.
- `preset`: the lens ID (`ren`, `maya`, `kai`, `zola` or `nova`).
- `autoEnhance: false`, because the prompt is complete.
- `aspectRatio`: `1:1` for most objects, `16:9` for vehicles and wide products, `3:4` for tall products.

Quick alternative when the person just wants a fast look: send their plain brief with the lens `preset` and leave `autoEnhance` on. Never send text from `enhance_prompt` with `autoEnhance` on; that enhances it twice.

Start all chosen renders first, then poll each `jobId` with `get_job`, about every 15 seconds.

## Step 4: Review and present

Look at every finished image. Present them side by side as a contact sheet with the lens, a one-line description and `[Open full-size image](imageUrl)`. Then give a short design critique for each: what works in the form, materials and details, and one thing to refine. Keep it concept-level; don't claim manufacturability or engineering validation.

## Step 5: Keep going

Offer the next steps that fit:
- Refine the favourite: a different colourway, a material swap, another angle or a detail close-up.
- Mix lenses ("Ren's precision with Maya's soft grip"), written into a new prompt.
- Build a colour, material and finish board (`cmf-board`).
- Make polished product shots of the chosen concept (`product-shots`).
- Launch posters and social layouts (`campaign`), or a 360° spin (`turnaround-video`).

Save work only when the person wants to keep it or continue into a board or campaign. Then call `create_project` with a short `name` and the `brief`, and use the returned `projectId` from then on.

## Boundaries

Concepts are design proposals, not certified CAD, engineering analysis or manufacturing approval. Use only IDs and image links that SketchMonkey returned for this account.
