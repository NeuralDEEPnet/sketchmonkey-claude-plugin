# View recipes

Each recipe gives the parts of a render prompt that follow the design fingerprint. Always end prompts with: "Photorealistic design visualisation, true-to-material, no text, no logos, no watermark." Send them with `autoEnhance: false`.

## Core views

### Hero
- **Use for:** the lead image of a design review or presentation.
- **View:** three-quarter front, camera at the design's height or slightly above.
- **Set:** seamless paper sweep in a soft neutral (warm grey, sand, pale sage) chosen to flatter the design's colours.
- **Light:** large soft key light from one side, gentle rim light to separate the silhouette, soft contact shadow.
- **Lens:** 85mm, f/8, crisp focus across the whole design.
- **Composition:** design slightly off-centre, clear space on one side for a title.
- **Ratio:** `4:3`, or `16:9` for slides.
- **Lens preset:** `ren` for technical products, `kai` for premium goods.

### Side
- **Use for:** checking proportion, stance and the main line of the design.
- **View:** true side view, camera level with the design's mid-height.
- **Set:** plain light-grey background with a faint ground line.
- **Light:** even, soft light from above and the front, a light contact shadow.
- **Lens:** 135mm, f/11, everything sharp, no perspective distortion.
- **Composition:** design centred, filling about 80% of the width.
- **Ratio:** `4:3`, or `16:9` for long objects.
- **Lens preset:** `ren`.

### Detail close-up
- **Use for:** judging material, finish, joins and controls.
- **View:** macro on the most distinctive detail (a knurled dial, stitching, glaze texture, a hinge).
- **Light:** low raking light that reveals surface texture.
- **Lens:** 100mm macro, shallow depth of field, focus on the detail.
- **Ratio:** `1:1` or `4:3`.

## More views

### Front
- **Use for:** symmetry, the face of the design and control layout.
- **View:** straight-on front view, camera level with the centre.
- **Set and light:** as the side view.
- **Lens:** 135mm, f/11, no perspective distortion.
- **Ratio:** `4:3` or `1:1`.
- **Lens preset:** `ren`.

### Top
- **Use for:** footprint, plan shape and anything used from above.
- **View:** straight top-down, 90 degrees.
- **Set:** plain light-grey surface.
- **Light:** soft, even light with a light shadow on one side to show height.
- **Ratio:** `1:1` or `4:3`.
- **Lens preset:** `ren`.

### Colourway line-up
- **Use for:** choosing between finishes on a CMF board.
- **View:** three to five identical units in a neat row or gentle arc, same angle.
- **Set:** seamless neutral sweep.
- **Prompt tip:** list each unit's colour in order with name and hex, and add "identical shape and size, only the colour differs".
- **Ratio:** `16:9`.

### Scale in context
- **Use for:** answering "how big is it?".
- **Set:** next to familiar everyday objects of known size (a coffee cup, a paperback, a smartphone, a pen) on a desk or counter.
- **Prompt tip:** state the real size ("about 30 cm tall") and the reference objects.
- **Ratio:** `4:3`.

### In-use context
- **Use for:** checking that the design suits the place it is meant for.
- **View:** natural eye level, as someone would see it in use.
- **Set:** the intended setting, described with two or three props at most (see the setting ideas below).
- **Light:** natural window light, soft shadows.
- **Lens:** 50mm, f/2.8, the design sharp, background gently soft.
- **Composition:** the design clearly the subject, filling about a third of the frame.
- **Ratio:** `4:3` or `16:9`.
- **Lens preset:** none, so the scene description sets the look. Avoid `maya` and `nova`.

### Presentation key visual
- **Use for:** the title slide or cover of a design presentation.
- **Set:** dark backdrop (charcoal, deep navy) or a sculptural plinth.
- **Light:** single strong key light with crisp rim highlights and deep shadows.
- **Composition:** generous clear space for a title.
- **Ratio:** `16:9` for slides, `3:4` for a portrait board.
- **Lens preset:** `kai`, or `zola` for a moodier look.

## Setting ideas by product type

| Product type | Settings that fit an in-use context view |
|---|---|
| Kitchen and tableware | Sunlit kitchen counter in light stone, breakfast table with linen, open shelving |
| Lighting and decor | Calm living room at dusk, bedside table, reading nook with a lounge chair |
| Tech and audio | Minimal desk with a laptop and plant, studio shelf, bedside at night |
| Personal care | Marble bathroom shelf, vanity with soft morning light |
| Outdoor and sport | Trailhead at golden hour, wooden deck, gym bench with a towel |
| Accessories | Concrete plinth, dressing table, café table by a window |
| Kids and pets | Bright playroom floor with soft rugs, sunny garden lawn |
| Furniture | Airy room with white walls and an oak floor, gallery-like space |

## Lighting cheat sheet

| Mood | Lighting words |
|---|---|
| Clean and precise | Large softbox key, white bounce fill, crisp rim light |
| Warm and homely | Low golden-hour window light, warm 2700K practical lamps |
| Fresh and natural | Overcast daylight, soft shadows, airy |
| Dramatic | Single hard key from the side, deep shadows |
| Technical | Even top light, gradient reflections, precise specular highlights |
