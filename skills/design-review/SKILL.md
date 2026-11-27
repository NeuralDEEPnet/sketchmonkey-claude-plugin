---
name: design-review
description: Gives a structured, studio-style design review of a design being made with SketchMonkey (a product, vehicle, pack or space), from a SketchMonkey render or from the sketch or description the SketchMonkey work is based on, covering proportion, form, surfaces, details, colour-material-finish, ergonomics, early manufacturability flags and fit to the brief, and keeps it to the three changes that matter most. Use only for reviews of designs in a SketchMonkey workflow, for example 'review my SketchMonkey concept', 'what would a senior designer change in this SketchMonkey render', 'crit our SketchMonkey concept before we show the client' or 'why does the car we rendered in SketchMonkey look off'. Not for general critiques of designs made elsewhere.
---

# Design review

Review a design the way a good studio lead would: specific, kind, and focused on the few changes that matter most. Reviews are free; only the optional corrected render uses allowance.

This skill is for designs being made with SketchMonkey. If someone wants a critique of something that isn't part of their SketchMonkey work, this skill doesn't apply.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. The full house rules are in the `studio` skill.

## Step 1: Know what you're reviewing

You need the design (a SketchMonkey render from this conversation or the person's account, or the sketch or written description their SketchMonkey work starts from; say a description-only review can't judge surfaces or exact proportions) and the intent (the brief, or one sentence on who it's for). If the intent is missing, ask for it in one question; a review without a brief is only taste.

## Step 2: Look properly

Look at the image itself, not only its description. Work through the lenses in `${CLAUDE_SKILL_DIR}/references/review-checklist.md` (the `references` folder next to this file) and note what you actually see. For vehicles, also use the proportion and stance checks in the `transport-design` skill.

## Step 3: Write the review

Keep it to about one phone screen:

> **Verdict:** one sentence on how well it meets the brief.
>
> **Working well:** two or three specific strengths ("the single shoulder line ties the front and rear lamps together").
>
> **Top three changes,** most important first. For each: what you see, why it matters for this brief, and the change ("the base looks heavy at 40% of the height; drop it to about 25% so the shade leads").
>
> **Early manufacturing flags** (only if any): for example sharp internal corners on a moulded part, an undercut, a very thin wall, or a seam across a visible surface. Say these are things to check with an engineer, not findings.

Score only if the person asks; then use 1 to 5 per lens with one line of evidence each.

## Step 4: Turn fixes into images (optional, uses allowance)

Offer to apply the top change, or all three: rewrite the design's prompt with the changes (or write one from the sketch or description, the way the matching design skill does) and render once with `render_concept` (`autoEnhance: false`, same `preset` and `aspectRatio` as before). If the product is saved and the change leaves its saved traits alone, also pass `subjectModelId`. If the change touches a saved trait (for example a proportion or the stance), the saved model would hold the old design in place, so render without `subjectModelId`, say so, and offer to save the corrected render as a new reference afterwards. Show before and after side by side.

Look at the new image and say honestly whether each change landed.

## Boundaries

- Critique the design, never the person. Be direct about problems and generous about what works.
- Manufacturing and ergonomics notes are early flags from an image, not engineering analysis, testing or approval.
- If the image shows a real brand's product, review it as a design exercise and don't suggest copying another brand's signature features.
