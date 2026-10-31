---
name: brand-kit
description: Saves a brand's colours, tone of voice and banned styles to a SketchMonkey project, checks copy against those rules, and creates on-brand headline and typography alternatives for campaign layouts. Use for 'set up our brand colours', 'apply our brand guidelines', 'is this tagline on-brand', 'give me three headline options' or 'try different fonts on the poster'.
---

# Brand kit

Capture a brand once so every direction and layout stays on-brand, then help people pick the best words and type.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Nothing here uses render allowance. The full house rules are in the `studio` skill.

## Step 1: Gather the brand

Collect, in the person's words:
- **Brand name.**
- **Colours:** three to six, each with a name, a hex value and a role (`primary`, `secondary`, `accent`, `background` or `text`). Use only values the person gives or that appear in material they share. Never guess a brand's hex codes from memory.
- **Tone:** one sentence ("warm, plain-spoken and a little playful").
- **Rules to avoid:** words, claims or styles that are off-limits ("never say cheap", "no neon", "no exclamation marks").

If they have guidelines or a website, ask them to paste the key parts.

## Step 2: Save it to a project

1. Use the `projectId` from earlier, or call `create_project` with a short `name` and `brief`.
2. Call `apply_brand_dna` with the `projectId` and `brandDna`: `name`, `palette` (a list of `hex`, `name` and `role`), `tone` and `forbiddenRules`. This replaces any brand rules already saved on that project, so confirm before overwriting existing rules.
3. To check some text at the same time, include it as `validateContent`. Report the result exactly: which rules it broke, or that it passed.

From then on, `generate_directions` with this `projectId` takes the saved brand into account.

## Step 3: Headline and copy options

Write three alternatives yourself in the brand's tone, each a different angle (benefit, emotion, curiosity), and check each against the rules to avoid before showing them. `generate_variants` with `variantType: "copy"` also returns quick mechanical variations of the current headline; use them only as raw material.

To check new copy against the saved rules with the tool, call `apply_brand_dna` again with exactly the same saved rules plus `validateContent`. That re-saves identical rules, so nothing changes. Otherwise check the copy yourself and say that you did.

## Step 4: Typography options

Call `generate_variants` with the `artboardId`, `variantType: "typography"` and a `count` up to 5. Describe each option in plain words ("editorial serif, centred") and recommend one that suits the brand's tone.

## Step 5: Apply the choice

When the person picks an option: `inspect_artboard`, then `edit_artboard` with only the chosen fields (`headline`, `subheadline`, `tagline`, `fontFamily`, `textAlignment` or `accentColor`), then `inspect_artboard` again and confirm that only those fields changed. Use only artboard IDs SketchMonkey returned for this account.

## Boundaries

Saved brand rules guide directions and help check copy; they don't guarantee every generated image follows them. Don't invent brand assets, trademarks or claims.
