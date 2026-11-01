---
name: turnaround-video
description: Creates short product videos with SketchMonkey, including 360° turntable spins, hero reveals, macro material close-ups and other cinematic camera moves, from a description or an existing SketchMonkey render. Use whenever someone wants a product video, spin or animation, even if they don't mention SketchMonkey, for example 'make a 360 video of my product', 'animate this render', 'a turnaround for Instagram stories', 'a product reveal clip' or 'show the texture up close in motion'.
---

# Product videos

Bring a product to life in a short clip with a deliberate camera move.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each clip uses one video render, and video allowances are much smaller than image allowances, so confirm before more than two. The full house rules are in the `studio` skill.

## Step 1: Choose the source

Best to worst for faithfulness:
1. **Animate an existing render.** Pass the render's image link as `referenceImageUrl`. It must be a SketchMonkey render from the person's account, usually one from earlier in the conversation.
2. **A saved product reference.** Pass its ID or handle as `subjectModelId`.
3. **A description only.** Write the product fingerprint into the prompt (see the `product-shots` skill).

If the person has no render yet and cares about accuracy, offer to make a hero shot first (one image render), then animate it.

## Step 2: Pick a camera recipe

Offer these in plain words and recommend one:

| Recipe (`cameraPreset`) | Looks like | Best for |
|---|---|---|
| `industrial_turntable` | A smooth 360° spin from a slightly raised angle | Catalogues, electronics, packaging, any "show me all sides" |
| `hero_reveal` | Starts close on a detail, pulls back to reveal the whole product from low down | Launches, flagship products, cars, footwear |
| `cmf_macro` | Slow push-in on textures and finishes | Materials, watches, wearables, craftsmanship |
| `cad_isometric` | Technical sweep showing top, front and side | Modular hardware, drones, mechanical products |
| `lateral_profile` | Glides along the side profile | Sleek shapes, appliances, furniture, vehicles |
| `locked_studio` | Still camera while light sweeps across the surfaces | Perfume, jewellery, sculptural objects |

A recipe sets motion, angle, pacing and lens together and overrides individual controls. For a custom move, leave `cameraPreset` out and set `cameraMotion`, `cameraAngle`, `cameraPacing` and `lensFraming` instead; `${CLAUDE_SKILL_DIR}/references/camera-recipes.md` (the `references` folder next to this file) explains every option and how to fix common problems. `get_camera_presets` (free) returns the live list.

## Step 3: Format and length

| Where it's going | `aspectRatio` | `durationSeconds` |
|---|---|---|
| Stories, Reels, TikTok | `9:16` | `6` |
| Website, YouTube, slides | `16:9` | `6` or `8` |
| Feed posts | `1:1` | `4` or `6` |

Default to `16:9` and `6` seconds if nothing is said, and say so.

## Step 4: Write the prompt and render

Prompt: the product fingerprint, the setting and the lighting, then: "single continuous shot, the product stays rigid and keeps its exact shape and colours, no morphing, no text, no logos."

Call `get_account_status` first if you haven't this conversation and check `videoQuota.effectiveRemaining`. Then call `render_video` with `prompt`, the camera recipe or controls, `aspectRatio`, `durationSeconds`, and `referenceImageUrl` or `subjectModelId` if you have one.

If `render_video` refuses the request, quote its reason in plain words, don't retry more than once, and suggest making the video on [sketchmonkey.design](https://www.sketchmonkey.design) or trying again later. Never describe a refused video as started.

## Step 5: Deliver

Poll `get_job` with the exact `jobId` about every 20 seconds; clips usually take 30 to 90 seconds. Then present:

> **360° turntable · 6 s · 9:16**: smooth spin from a slightly raised angle. [▶ Watch the video](videoUrl)

Copy the `videoUrl` exactly as returned and compare the whole link with the tool result before sending; today links start with exactly `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/`.

You can't watch the video yourself, so ask whether the speed, angle or framing should change, and offer a specific alternative ("a slower `cmf_macro` push-in on the knurled dial"). Other next steps: a vertical version for Stories, or using the clip alongside campaign layouts (`campaign`).

## Boundaries

Products, objects, vehicles and spaces only; no real people's faces or likeness. Use only image links and IDs that SketchMonkey returned for this account, and report allowance limits honestly.
