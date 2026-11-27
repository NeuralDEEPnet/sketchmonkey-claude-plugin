---
name: presentation-renders
description: Creates design presentation renders with SketchMonkey for a product the person is designing, as part of the design process, including a hero render of the concept, CMF variant renders, detail renders and a design-review board that brings the views together. Use when someone working on a product design in SketchMonkey wants to present it or prepare a design review, for example 'make presentation renders of my SketchMonkey concept', 'render the hero view for our design review', 'show the three colourways side by side for the review' or 'put together a design-review board for the kettle concept'.
---

# Presentation renders

Turn a product design in progress into a small set of consistent, true-to-design renders that a team can review and decide from.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each image uses one render from the person's allowance, so confirm before more than four. The full house rules are in the `studio` skill.

## How it works (tell people when it matters)

This skill renders visualisations of a design from a precise written description of it, so the better the description, the closer the match. Every render here is a visual aid for the design process: it shows the concept, a colour-material-finish option or a detail so the person and their team can judge the design and decide what to change. The design usually comes from `explore-concepts` or an earlier SketchMonkey render; it can also be described in words or shown in a sketch.

## Step 1: Write the product fingerprint

Before the first render, write a fingerprint of 60 to 120 words from what the person said, a sketch they shared, or an earlier SketchMonkey render. Cover:

- **What it is** and how it's used.
- **Silhouette and proportions**, with ratios or rough sizes ("cone about 1.4× wider than it is tall", "30 cm slim arm").
- **Materials and finishes per part** ("matte sand-glazed ceramic cone, oiled walnut base, thin brushed-brass rim").
- **Colours per part**, as a name plus an approximate hex ("warm sand #D8C3A5").
- **Distinctive details**: controls, seams, stitching, vents, feet, cable.
- **Must not change**: three to five traits that define the design.

Leave brand names, logos and printed text out of renders; image models garble lettering. Add text later in a campaign layout.

If a fact that matters is missing (usually colour or material), ask one question. Otherwise assume and say what you assumed. When working from a sketch, show the fingerprint back in two or three lines so the person can correct it before you spend renders.

## Step 2: Choose the renders

If the person didn't say which renders, propose the **review set** of three images and go ahead unless they object:

1. **Hero render:** three-quarter view of the concept in a soft-lit neutral studio, 4:3.
2. **CMF variant render:** the same design in the colourways under discussion, side by side, 16:9. If only one colourway exists, render a second view (side or rear) instead.
3. **Detail render:** a close view of the detail that most needs a decision, 4:3.

Full recipes for these, and for the scale check and the alternative-view render, are in `${CLAUDE_SKILL_DIR}/references/shot-recipes.md` (the `references` folder next to this file). Read it when planning anything beyond the review set.

Match the aspect ratio to how the design will be reviewed:

| Where it's reviewed | Aspect ratio |
|---|---|
| Design-review slides, screen presentations | `16:9` |
| Printed boards, general review | `4:3` |
| Compact products, detail grids | `1:1` |
| Tall products | `3:4` |
| Colourway line-ups | `16:9` or `3:2` |

## Step 3: Write each render prompt

Build each prompt in this order:

> **[render type]** of **[full fingerprint]**. **[view and angle]**. **[neutral studio setting and surface]**. **[lighting]**. **[lens and focus]**. **[composition]**. Photorealistic design presentation render, true-to-material, no text, no logos, no watermark.

Then call `render_concept` with:

- `prompt`: the full prompt above. Repeat the whole fingerprint in every prompt so the set stays consistent.
- `autoEnhance: false`. Your prompt is already complete; automatic enhancement adds generic lens materials that can change the design.
- `preset`: each lens adds its own style words to the prompt at render time, even with `autoEnhance: false`, so choose deliberately:
  - `kai` adds polished, presentation-ready styling. Use it for hero and CMF variant renders (the default).
  - `ren` adds precise, CAD-quality hard-surface rendering. Use it for technical products.
  - Leave `preset` out when your prompt alone should set the look.
  - `zola` adds cinematic drama. Use it only when the person asks for a moody presentation image.
  - Avoid `maya` here: it asks for product UI/UX detail and can add screen-like artefacts such as QR codes. Avoid `nova` unless the person wants an experimental look: it adds deliberate glitch effects.
- `aspectRatio`: from the table above. For `1:1`, also write "square 1:1 format" in the prompt; the server only adds ratio wording for non-square images, so square requests can otherwise come back in another shape.
- `subjectModelId`: only if the design was saved as a reference (Step 5).

For a set of renders, start all renders first, then poll each job; they run in parallel.

An example hero render prompt:

> Design presentation render of a compact desk lamp for small apartments: slim bead-blasted recycled-aluminium arm and round head in warm silver, a soft oatmeal fabric-wrapped cable, and a discreet circular touch dimmer on the weighted base. Three-quarter front view at eye level, lamp switched on with a warm 2700K glow. Seamless warm-grey studio sweep, large soft key light from the left, gentle rim light, soft contact shadow. 85mm lens, f/8, crisp focus across the product, product slightly off-centre. Photorealistic design presentation render, true-to-material, no text, no logos.

(Sent with `preset: "ren"`, `aspectRatio: "4:3"`, `autoEnhance: false`.)

## Step 4: Review and present the board

1. Poll `get_job` with each exact `jobId`. Renders usually take 25 to 40 seconds; check about every 15 seconds and never start a duplicate render because a job is still running.
2. Look at every finished image and compare it with the fingerprint. Fix-ups for common problems are listed below.
3. Present the set as a **design-review board**, results first: each render with a label, what it shows and the decision it supports.

   **1 · Hero (4:3)**: the overall form in warm studio light, lamp glowing. *Decide:* is the head too large for the arm? [Open full-size image](imageUrl)
   **2 · CMF variants (16:9)**: warm silver, graphite and sage side by side. *Decide:* which colourway leads. [Open full-size image](imageUrl)

   Copy each `imageUrl` into its link exactly as the tool returned it; never retype or rebuild a link. Links repeat the word "sketchmonkey", which makes copying mistakes easy, so before sending compare each whole link with the tool result character by character. Today every image link starts with exactly `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/` (hyphen in the host, plain `sketchmonkey` in the path).
4. Point out anything that drifted from the design and offer one corrected render. If you couldn't see an image, say so in one line and ask the person to check it.
5. Offer two or three next steps that fit, for example: "run a design review on the hero" (`design-review`), "build the full colour, material and finish board" (`cmf-board`), "prepare the design-intent brief for engineering" (`engineering-handoff`), "set the hero into launch layouts with editable type" (`campaign`), or "save this design so later renders match" (Step 5).

Keep the whole reply to about one phone screen: the board, at most two short lines of notes or assumptions, then the next steps.

## Step 5: Keep the design consistent (optional)

For a design the person will render again, offer to save it as a reusable reference. Ask first, because it saves to their account. Call `save_subject_model` with:

- `kind: "object"`, a `name` and an optional short `handle`.
- `identityLock`: the fingerprint.
- `immutableTraits`: the must-not-change list.
- `heroImageUrl`: their best SketchMonkey render of it. A saved reference with an image is used as a visual reference in later renders, not only as text.

Afterwards pass the returned ID or handle as `subjectModelId` on later `render_concept` calls. Say plainly that a saved reference improves consistency but doesn't guarantee identical results. `list_subject_models` shows their saved references and a few built-in samples.

## Fixing common problems

| Problem | Change in the next prompt |
|---|---|
| Colour drifted | Give the colour twice, name and hex, and add "exact colour match". |
| Proportions off | Add a measurable ratio or size comparison. |
| Extra or missing parts | Add "exactly one ..., no additional ...". |
| Garbled text or fake logos | Keep "no text, no logos"; add real branding later in a campaign layout. |
| Looks plastic or too CGI | Add "natural material texture, subtle imperfections, realistic contact shadow". |
| Busy background | Add "plain neutral studio background, no props". |
| Product too small | Add "product fills about 70% of the frame". |
| QR codes, screens, interface panels or glitch debris | Use `kai` or no `preset`, and add "no QR codes, no screens, no interface elements". |
| Wrong shape (for example a square request came back wide) | Write "square 1:1 format" (or the ratio you need) in the prompt as well as in `aspectRatio`. |

## Boundaries

- Design presentation only: renders of a product the person is designing, for concept and design-review use. This skill doesn't make general-purpose or stock-style pictures.
- Products and objects only. No real people's faces or likeness.
- Keep renders faithful to the design: no features, sizes, finishes or certifications it doesn't have. Renders are design proposals, not certified CAD, engineering analysis or manufacturing approval.
- Use only image links and IDs that SketchMonkey returned for this account. Report allowance or permission errors honestly.
