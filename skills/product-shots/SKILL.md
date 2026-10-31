---
name: product-shots
description: Creates studio-quality product images with SketchMonkey, including hero shots, clean white e-commerce packshots, lifestyle scenes, close-up detail shots, colourway line-ups and social-ready verticals. Use whenever someone wants product photos or product images for a shop, website, marketplace listing, pitch deck or social post, even if they don't mention SketchMonkey, or shares a product photo and asks to make it look professional, for example 'make my product look premium', 'I need listing photos for Etsy', 'put my lamp in a cosy living room' or 'enhance this product photo'.
---

# Product shots

Turn a product, described or photographed, into a small set of beautiful, consistent, true-to-product images.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each image uses one render from the person's allowance, so confirm before more than four. The full house rules are in the `studio` skill.

## How it works (tell people when it matters)

SketchMonkey renders brand-new images from a precise description of the product. It does not edit the pixels of an uploaded photo, so the better the description, the closer the match. When someone shares a photo, say this in one friendly line and explain that you'll describe their product to the studio in detail.

## Step 1: Write the product fingerprint

Before the first render, write a fingerprint of 60 to 120 words from what the person said, what you can see in an attached photo, or an earlier SketchMonkey render. Cover:

- **What it is** and how it's used.
- **Silhouette and proportions**, with ratios or rough sizes ("cone about 1.4× wider than it is tall", "30 cm slim arm").
- **Materials and finishes per part** ("matte sand-glazed ceramic cone, oiled walnut base, thin brushed-brass rim").
- **Colours per part**, as a name plus an approximate hex ("warm sand #D8C3A5").
- **Distinctive details**: controls, seams, stitching, vents, feet, cable.
- **Must not change**: three to five traits that define the product.

Leave brand names, logos and printed text out of renders; image models garble lettering. Add text later in a campaign layout.

If a fact that matters is missing (usually colour or material), ask one question. Otherwise assume and say what you assumed. When working from a photo, show the fingerprint back in two or three lines so the person can correct it before you spend renders.

## Step 2: Choose the shots

If the person didn't say which shots, propose the **starter set** of three images and go ahead unless they object:

1. **Hero:** three-quarter view in a soft-lit studio, 4:3.
2. **Clean packshot:** centred on pure white, ready for marketplaces, 1:1.
3. **Lifestyle:** in a real setting that suits the buyer, 3:2.

More shot types, each with a full recipe, are in `${CLAUDE_SKILL_DIR}/references/shot-recipes.md` (the `references` folder next to this file): detail close-up, colourway line-up, flat lay, scale-in-context, social vertical, dramatic key visual and seasonal scene. Read it when planning anything beyond the starter set.

Match the aspect ratio to where the image will live:

| Where it's going | Aspect ratio |
|---|---|
| Marketplace listings (Amazon, Etsy, Shopify) | `1:1` |
| Website hero or banner, slides | `16:9` |
| Product page gallery | `4:3` or `1:1` |
| Instagram or LinkedIn feed (portrait) | `3:4` |
| Stories, Reels, TikTok | `9:16` |
| Pinterest | `2:3` |
| Editorial or lookbook spreads | `3:2` |

## Step 3: Write each render prompt

Build each prompt in this order:

> **[shot type]** of **[full fingerprint]**. **[view and angle]**. **[setting and surface]**. **[lighting]**. **[lens and focus]**. **[composition and space for copy]**. **[mood]**. Photorealistic, true-to-material, no text, no logos, no watermark.

Then call `render_concept` with:

- `prompt`: the full prompt above. Repeat the whole fingerprint in every prompt so the set stays consistent.
- `autoEnhance: false`. Your prompt is already complete; automatic enhancement adds generic lens materials that can change the product.
- `preset`: each lens adds its own style words to the prompt at render time, even with `autoEnhance: false`, so choose deliberately:
  - `kai` adds polished, brand-ready commercial styling. Use it for e-commerce, hero shots and packshots (the default).
  - `ren` adds precise, CAD-quality hard-surface rendering. Use it for technical products.
  - Leave `preset` out for lifestyle scenes, so your prompt alone sets the look.
  - `zola` adds cinematic drama. Use it only for moody key visuals.
  - Avoid `maya` for photographs: it asks for product UI/UX detail and can add screen-like artefacts such as QR codes. Avoid `nova` unless the person wants experimental art: it adds deliberate glitch effects.
- `aspectRatio`: from the table above. For `1:1`, also write "square 1:1 format" in the prompt; the server only adds ratio wording for non-square images, so square requests can otherwise come back in another shape.
- `subjectModelId`: only if the product was saved as a reference (Step 5).

For a set of shots, start all renders first, then poll each job; they run in parallel.

A prompt that produced a faithful, studio-quality hero shot in testing:

> Studio product photograph of a compact desk lamp for small apartments: slim bead-blasted recycled-aluminium arm and round head in warm silver, a soft oatmeal fabric-wrapped cable, and a discreet circular touch dimmer on the weighted base. Three-quarter front view at eye level, lamp switched on with a warm 2700K glow. Seamless warm-grey paper sweep, large soft key light from the left, gentle rim light, soft contact shadow. 85mm lens, f/8, crisp focus across the product, generous negative space on the right for copy. Photorealistic, true-to-material, no text, no logos.

(Sent with `preset: "ren"`, `aspectRatio: "4:3"`, `autoEnhance: false`.)

## Step 4: Review and present

1. Poll `get_job` with each exact `jobId`. Renders usually take 25 to 40 seconds; check about every 15 seconds and never start a duplicate render because a job is still running.
2. Look at every finished image and compare it with the fingerprint. Fix-ups for common problems are listed below.
3. Present the set as a contact sheet, results first:

   **1 · Hero (4:3)**: warm studio light, lamp glowing, space on the right for a headline. [Open full-size image](imageUrl)
   **2 · White packshot (1:1)**: centred on pure white, listing-ready. [Open full-size image](imageUrl)

   Copy each `imageUrl` into its link exactly as the tool returned it; never retype or rebuild a link. Links repeat the word "sketchmonkey", which makes copying mistakes easy, so before sending compare each whole link with the tool result character by character. Today every image link starts with exactly `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/` (hyphen in the host, plain `sketchmonkey` in the path).
4. Point out anything that drifted from the real product and offer one corrected render. If you couldn't see an image, say so in one line and ask the person to check it.
5. Offer two or three next steps that fit, for example: "turn the hero into a 360° spin" (`turnaround-video`, using this image), "put these into launch posters and social layouts" (`campaign`, using the hero as the background), "try another setting or colourway", or "save this product so future shots match" (Step 5).

Keep the whole reply to about one phone screen: the contact sheet, at most two short lines of notes or assumptions, then the next steps.

## Step 5: Keep the product consistent (optional)

For a product the person will shoot again, offer to save it as a reusable reference. Ask first, because it saves to their account. Call `save_subject_model` with:

- `kind: "object"`, a `name` and an optional short `handle`.
- `identityLock`: the fingerprint.
- `immutableTraits`: the must-not-change list.
- `heroImageUrl`: their best SketchMonkey render of it (an image they uploaded elsewhere can't be used).

Afterwards pass the returned ID or handle as `subjectModelId` on later `render_concept` and `render_video` calls. Say plainly that a saved reference improves consistency but doesn't guarantee identical results. `list_subject_models` shows their saved references and a few built-in samples.

## Fixing common problems

| Problem | Change in the next prompt |
|---|---|
| Colour drifted | Give the colour twice, name and hex, and add "exact colour match". |
| Proportions off | Add a measurable ratio or size comparison. |
| Extra or missing parts | Add "exactly one ..., no additional ...". |
| Garbled text or fake logos | Keep "no text, no logos"; add real branding later in a campaign layout. |
| Looks plastic or too CGI | Add "photographed, natural material texture, subtle imperfections, realistic contact shadow". |
| Busy background | Add "minimal styling, a single prop at most, clean background". |
| Product too small | Add "product fills about 70% of the frame". |
| QR codes, screens, interface panels or glitch debris | Use `kai` or no `preset`, and add "no QR codes, no screens, no interface elements". |
| Wrong shape (for example a square request came back wide) | Write "square 1:1 format" (or the ratio you need) in the prompt as well as in `aspectRatio`. |

## Boundaries

- Products and objects only. No real people's faces or likeness.
- When images will sell a real product, keep them faithful: no features, sizes, finishes or certifications the product doesn't have.
- Use only image links and IDs that SketchMonkey returned for this account. Report allowance or permission errors honestly.
