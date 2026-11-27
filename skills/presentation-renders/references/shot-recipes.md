# Presentation render recipes

Each recipe gives the parts of a render prompt that follow the product fingerprint. Always end prompts with: "Photorealistic design presentation render, true-to-material, no text, no logos, no watermark." Send them with `autoEnhance: false`.

Every recipe serves a design decision. If a render wouldn't help the person or their team judge the design, leave it out.

## Review set

### Hero render
- **Use for:** the lead image of a design review or concept presentation; shows the overall form.
- **View:** three-quarter front, camera at product height or slightly above.
- **Set:** seamless studio sweep in a soft neutral (warm grey, sand, pale sage) chosen so the design's colours read truthfully.
- **Light:** large soft key light from one side, gentle rim light to separate the silhouette, soft contact shadow.
- **Lens:** 85mm, f/8, crisp focus across the product.
- **Composition:** product slightly off-centre, filling about 70% of the frame.
- **Ratio:** `4:3`, or `16:9` for review slides.
- **Lens preset:** `kai` for premium goods, `ren` for technical products.

### CMF variant render
- **Use for:** comparing colour, material and finish options of the same design before choosing one.
- **View:** two to five identical units in a neat row or gentle arc, same angle.
- **Set:** seamless neutral sweep, the same for every variant.
- **Light:** even soft light, so differences come from the finishes, not the lighting.
- **Prompt tip:** list each unit's colour, material and finish in order with name and hex, and add "identical shape and size, only the colour and finish differ".
- **Ratio:** `16:9` or `3:2`.
- **Alternative:** one variant per render, with the hero recipe unchanged and only the CMF words swapped, when the finishes need a closer look.

### Detail render
- **Use for:** judging a detail, material junction, control or texture.
- **View:** close on the detail under discussion (a knurled dial, stitching, glaze texture, a hinge, a parting line).
- **Light:** low raking light that reveals surface texture.
- **Lens:** 100mm macro, shallow depth of field, focus on the detail.
- **Ratio:** `1:1` or `4:3`.

## More review renders

### Alternative view
- **Use for:** checking the design from the side, rear or top once the hero is approved.
- **View:** straight side, rear three-quarter or top-down, named exactly.
- **Set and light:** the same as the hero, so the views compare fairly.
- **Prompt tip:** add "same product as described, no design changes".
- **Ratio:** the same as the hero.

### Scale check
- **Use for:** answering "how big is it?" in a review.
- **Set:** on a plain neutral surface next to one or two familiar objects of known size (a coffee cup, a paperback, a smartphone, a pen).
- **Prompt tip:** state the real size ("about 30 cm tall") and the reference objects.
- **Ratio:** `4:3`.

## Assembling the design-review board

Present the renders together in the reply, most important decision first:

1. Hero render: the overall form and proportion.
2. CMF variant render: the options still open.
3. Detail render: the detail that needs a decision.
4. Alternative view or scale check, if made.

Give each a one-line label, what it shows and the decision it supports. Keep set, light and angle consistent across the board so differences come from the design.

## Lighting cheat sheet

| Purpose | Lighting words |
|---|---|
| Clean and premium | Large softbox key, white bounce fill, crisp rim light |
| Honest colour check | Overcast daylight, soft shadows, neutral white balance |
| Form and surface reading | Even top light, gradient reflections, precise specular highlights |
| Texture and detail | Low raking side light, soft fill |
