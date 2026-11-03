---
name: photo-edit
description: Edits a real product photo with SketchMonkey while keeping the product itself unchanged, for one precise change such as a new background or scene, an added accessory, a wider tray, a different colourway, or removed clutter, and reports a fidelity score that shows the product was kept. Use whenever someone wants to change, fix, extend or restage an existing photo of their product rather than get new shots, for example 'put my bottle on a marble counter', 'make the drip tray wider, keep everything else', 'remove the cable from this photo' or 'show this lamp in black'.
---

# Product photo edit

Change one thing in a real photo and keep everything else: the product's shape, proportions, colours, buttons, materials and the camera angle. This is what generic image tools get wrong, because they redraw the product. SketchMonkey edits the photo itself, then measures how much of the rest stayed the same.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each edit uses one image render from the person's allowance. The full house rules are in the `studio` skill.

## When to use this skill and when to use `product-shots`

- Use **this skill** when the person has a photo and wants that photo changed: a new background, an added or bigger part, a colour change, something removed.
- Use **`product-shots`** when they want new images from scratch, such as a set of listing shots from a description, or when the photo is too poor to keep (blurry, cut off, very dark).

## Step 1: Get the photo onto SketchMonkey

The edit tool only works on photos stored in the person's SketchMonkey account. Call `upload_reference_image` once per photo:

- If they gave a **public link** to the image (their shop page, a CDN, a cloud link that opens the image itself), pass it as `imageUrl`. It must be `https://` and point straight at the image.
- If you can **read the file** (in Claude Code, or a file in your working folder), pass its bytes as `imageBase64`. PNG, JPEG and WebP up to 10 MB work.
- If you can only **see** an image in the chat, you can't pass its pixels. Ask in one line for a direct link to the image, or for the file itself in Claude Code. Don't describe the photo and render a new one instead without saying so; that would be a new image, not an edit.
- If the photo is already a **SketchMonkey render** from this account (its link starts with `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/`), skip the upload and use that link.

Give it a short `label` ("ceramic dripper, front"). Keep the returned image URL for the next step; don't show it to the person unless they ask.

## Step 2: Write the instruction

One change per edit. Say what changes, where, and what must stay. Name the part the way it looks in the photo:

> Make the white drip tray wider and longer, extending forward by about a third; keep the machine, its buttons, colours and the camera angle exactly as they are.

> Replace the background with a light travertine kitchen counter in soft morning light; keep the bottle, its label, colour and reflections exactly as they are.

Then call `edit_product_photo` with:

- `sourceImageUrl`: the URL from Step 1.
- `instruction`: as above.
- `regionHint`: where the change happens, in plain words ("under the base", "bottom", "background", "left side") or as normalised `x,y,w,h`. Leave it out for whole-scene changes such as a new setting.
- `preserveStrength`: leave the default (0.88) for most edits. Use about `0.95` for a small change to one part. Use about `0.7` for a new scene or background, where more of the picture has to change.
- `maskImageUrl`: only if the person supplied a mask (white = change, black = keep); upload it first like the photo.
- `aspectRatio`: leave the default, which matches the source photo, unless they asked for another shape.

For several changes, do them one after another, using each finished image as the next `sourceImageUrl`. Tell the person you're going step by step so each change stays precise.

## Step 3: Check the result and report the fidelity

1. Poll `get_job` with the exact `jobId` about every 15 seconds; edits usually take 20 to 40 seconds. Never start a duplicate edit because one is still running.
2. Look at the edited image next to the original. Did the requested change happen? Did anything else move, recolour or disappear?
3. Read the fidelity score `get_job` reports (`similarityScore`, measured outside the edited area, from 0 to 1):
   - **0.9 or higher:** the rest of the photo is essentially unchanged. Say so in plain words ("everything outside the tray is unchanged, 99.7% match").
   - **Below 0.9, or a `warning`:** tell the person what drifted and offer one retry, with a narrower instruction, a `regionHint`, or a higher `preserveStrength`.
4. Present the result first: the first line of the reply is the edited image. Keep any caveat to one short line after it, and don't mention tool settings.

   **Edited · wider drip tray**: tray extended forward; machine, buttons and angle unchanged (99.7% match). [Open full-size image](imageUrl)

   Copy every link exactly as the tool returned it, character for character. Image links start with exactly `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/`.
5. Offer two or three next steps, for example: "try the tray in black", "put it on a white background for your listing", "make a 360° spin of it" (`turnaround-video`, with this image), or "save this product so new shots match it" (`save_subject_model` with this image as `heroImageUrl`, see `product-shots` Step 5).

## Boundaries

- Products, objects and spaces only. Don't edit photos showing people's faces or other personal details; ask for a product-only photo instead.
- Only photos the person owns or has the right to use. Don't upload images from other brands' sites to pass off as theirs.
- When an edited photo will sell a real product, it must show the real product: no features, sizes, colours or finishes it doesn't have. A concept edit ("what would it look like in black") is fine; say it's a concept when it goes into a listing.
- Report upload errors (size, format, an unreachable link) and allowance errors honestly, and never route around a refusal with another tool.
