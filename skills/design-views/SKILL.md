---
name: design-views
description: Presents a product design as a consistent set of design views with SketchMonkey, such as a three-quarter hero view, side and front views, detail close-ups, colourway line-ups and scale or in-context views, for design reviews, presentation boards and sign-off. Use whenever someone wants to see what a product design looks like from several angles, compare finishes side by side, check its size in context or prepare visuals for a design presentation, even if they don't mention SketchMonkey, for example 'show me this speaker design from the side', 'line up the three colourways' or 'I need views of my lamp concept for the review'.
---

# Design views

Show a product design as a small, consistent set of views, so it can be judged, compared and signed off.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each view uses one render from the person's allowance, so confirm before more than four. The full house rules are in the `studio` skill.

## How it works (tell people when it matters)

Each view is a new design visual, rendered from a precise written description of the design, so the better the description, the closer the views match each other. These are visuals of a design proposal for exploring and reviewing it. They are not photographs of a finished product, and this plugin does not edit photographs. When someone shares a photo or a sketch, read the design from it and describe it; the views are rendered from that description.

## Step 1: Write the design fingerprint

Before the first render, write a fingerprint of 60 to 120 words from what the person said, what you can see in an attached photo or sketch, or an earlier SketchMonkey render. Cover:

- **What it is** and how it's used.
- **Silhouette and proportions**, with ratios or rough sizes ("cone about 1.4× wider than it is tall", "30 cm slim arm").
- **Materials and finishes per part** ("matte sand-glazed ceramic cone, oiled walnut base, thin brushed-brass rim").
- **Colours per part**, as a name plus an approximate hex ("warm sand #D8C3A5").
- **Distinctive details**: controls, seams, stitching, vents, feet, cable.
- **Must not change**: three to five traits that define the design.

Leave brand names, logos and printed text out of renders; image models garble lettering. Add text later in a layout (`campaign`).

If a fact that matters is missing (usually colour or material), ask one question. Otherwise assume and say what you assumed. When working from a photo or sketch, show the fingerprint back in two or three lines so the person can correct it before you spend renders.

## Step 2: Choose the views

If the person didn't say which views, propose the **starter set** of three and go ahead unless they object:

1. **Hero:** three-quarter view in soft studio light, 4:3. The view people judge the design by.
2. **Side:** a true side view at the design's mid-height, 4:3. The proportion check.
3. **Detail:** a close-up of the most distinctive detail, 1:1. The material and finish check.

More views, each with a full recipe, are in `${CLAUDE_SKILL_DIR}/references/view-recipes.md` (the `references` folder next to this file): front view, top view, colourway line-up, scale in context, in-use context and presentation key visual. Read it when planning anything beyond the starter set.

Match the aspect ratio to where the view will be used:

| Where it's going | Aspect ratio |
|---|---|
| Design review board (the default) | `4:3` |
| Presentation slide or wide board | `16:9` |
| Detail tiles and CMF sheets | `1:1` |
| Portrait presentation board | `3:4` |
| Tall objects on a portrait board | `9:16` |

## Step 3: Write each render prompt

Build each prompt in this order:

> **[view]** of **[full fingerprint]**. **[angle]**. **[setting and surface]**. **[lighting]**. **[lens and focus]**. **[composition]**. Photorealistic design visualisation, true-to-material, no text, no logos, no watermark.

Then call `render_concept` with:

- `prompt`: the full prompt above. Repeat the whole fingerprint in every prompt so the set stays consistent.
- `autoEnhance: false`. Your prompt is already complete; automatic enhancement adds generic lens materials that can change the design.
- `preset`: each lens adds its own style words to the prompt at render time, even with `autoEnhance: false`, so choose deliberately:
  - `ren` adds precise, CAD-quality hard-surface rendering. Use it for technical products and for side, front and top views (the default).
  - `kai` adds polished, presentation-ready styling. Use it for hero views of premium goods and for presentation key visuals.
  - Leave `preset` out for in-use context views, so your prompt alone sets the look.
  - `zola` adds cinematic drama. Use it only for a moody key visual.
  - Avoid `maya` for these views: it asks for product UI/UX detail and can add screen-like artefacts such as QR codes. Avoid `nova` unless the person wants an experimental look: it adds deliberate glitch effects.
- `aspectRatio`: from the table above. For `1:1`, also write "square 1:1 format" in the prompt; the server only adds ratio wording for non-square images, so square requests can otherwise come back in another shape.
- `subjectModelId`: only if the design was saved as a reference (Step 5).

For a set of views, start all renders first, then poll each job; they run in parallel.

A prompt that produced a faithful hero view in testing:

> Design visualisation of a compact desk lamp for small apartments: slim bead-blasted recycled-aluminium arm and round head in warm silver, a soft oatmeal fabric-wrapped cable, and a discreet circular touch dimmer on the weighted base. Three-quarter front view at eye level, lamp switched on with a warm 2700K glow. Seamless warm-grey paper sweep, large soft key light from the left, gentle rim light, soft contact shadow. 85mm lens, f/8, crisp focus across the whole lamp, clear space on the right. Photorealistic design visualisation, true-to-material, no text, no logos.

(Sent with `preset: "ren"`, `aspectRatio: "4:3"`, `autoEnhance: false`.)

## Step 4: Review and present

1. Poll `get_job` with each exact `jobId`. Renders usually take 25 to 40 seconds; check about every 15 seconds and never start a duplicate render because a job is still running.
2. Look at every finished image and compare it with the fingerprint. Fix-ups for common problems are listed below.
3. Present the set as a contact sheet, results first:

   **1 · Hero (4:3)**: warm studio light, lamp glowing, clear space on the right. [Open full-size image](imageUrl)
   **2 · Side (4:3)**: true side view, arm and base in proportion. [Open full-size image](imageUrl)

   Copy each `imageUrl` into its link exactly as the tool returned it; never retype or rebuild a link. Links repeat the word "sketchmonkey", which makes copying mistakes easy, so before sending compare each whole link with the tool result character by character. Today every image link starts with exactly `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/` (hyphen in the host, plain `sketchmonkey` in the path).
4. Point out anything that drifted from the fingerprint, or that differs between views, and offer one corrected render. If you couldn't see an image, say so in one line and ask the person to check it.
5. Offer two or three next steps that fit, for example: "review this design the way a studio lead would" (`design-review`), "compare colours, materials and finishes" (`cmf-board`), "lay the hero view out on a presentation board" (`campaign`, using the hero as the background), or "save this design so later views match" (Step 5).

Keep the whole reply to about one phone screen: the contact sheet, at most two short lines of notes or assumptions, then the next steps.

## Step 5: Keep the design consistent (optional)

For a design the person will come back to, offer to save it as a reusable reference. Ask first, because it saves to their account. Call `save_subject_model` with:

- `kind: "object"`, a `name` and an optional short `handle`.
- `identityLock`: the fingerprint.
- `immutableTraits`: the must-not-change list.
- `heroImageUrl`: their best SketchMonkey render of it. It must be an image SketchMonkey returned for this account; an image hosted elsewhere can't be used. A saved reference with an image is used as a visual reference in later renders, not only as text.

Afterwards pass the returned ID or handle as `subjectModelId` on later `render_concept` calls. Say plainly that a saved reference improves consistency but doesn't guarantee identical results. `list_subject_models` shows their saved references and a few built-in samples.

## Fixing common problems

| Problem | Change in the next prompt |
|---|---|
| Colour drifted | Give the colour twice, name and hex, and add "exact colour match". |
| Proportions off | Add a measurable ratio or size comparison. |
| Extra or missing parts | Add "exactly one ..., no additional ...". |
| Garbled text or fake logos | Keep "no text, no logos"; add real lettering later in a layout. |
| Looks plastic or too CGI | Add "natural material texture, subtle imperfections, realistic contact shadow". |
| Busy background | Add "minimal styling, a single prop at most, clean background". |
| Design too small in the frame | Add "the design fills about 70% of the frame". |
| A side or front view came back in perspective | Add "true orthographic-style view, camera level with the centre, long lens, no perspective distortion". |
| QR codes, screens, interface panels or glitch debris | Use `ren`, `kai` or no `preset`, and add "no QR codes, no screens, no interface elements". |
| Wrong shape (for example a square request came back wide) | Write "square 1:1 format" (or the ratio you need) in the prompt as well as in `aspectRatio`. |

## Boundaries

- Products and objects only. No real people's faces or likeness.
- These views show a design proposal. Don't present them as photographs of a finished product, and don't show features, sizes, finishes or certifications the design doesn't have.
- Use only image links and IDs that SketchMonkey returned for this account. Report allowance or permission errors honestly.
