---
name: engineering-handoff
description: Turns an approved SketchMonkey concept into a design-intent package for engineers, CAD modellers and manufacturers, with overall dimensions, a part list, material and process per part, finishes, parting lines and draft, assembly notes, compliance topics to check and open questions, and hands it on to a CAD tool when one is connected. Use for requests like 'prepare this for engineering', 'what do I send to a manufacturer', 'make a spec for my factory', 'how would this be made', 'design handoff' or 'get this ready for CAD'.
---

# Engineering handoff

Close the gap between a beautiful concept and something an engineer or factory can quote. The package records design intent; engineers confirm the numbers.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Writing the package is free. The full house rules are in the `studio` skill.

## Step 1: Gather what's decided

Collect from the conversation, or ask for in one question:
- The approved concept image (its link, copied exactly) and the product fingerprint or vehicle package.
- The chosen direction and CMF, if made.
- Target size, quantity (a batch of 50 or 50,000 changes the process), price band and market.

If the work lives in a project, `get_artboard_export_metadata` returns the saved layouts' sizes and background image links for the package. It doesn't produce finished files.

## Step 2: Write the design-intent package

Use these sections. Keep numbers as targets and mark each as "target" or "to confirm".

1. **Overview:** what it is, who it's for, the approved image link, the three to five must-not-change traits.
2. **Overall dimensions:** length, width, height and key ratios, plus weight target if known.
3. **Part list:** one row per part with name, quantity, material, process, finish, colour (name and approximate hex; say Pantone or RAL references are nearest matches to confirm against physical swatches).
4. **Manufacturing notes per part:** likely process and why, wall thickness range, draft direction and parting line location, visible versus hidden surfaces. Use `${CLAUDE_SKILL_DIR}/references/process-guide.md` (the `references` folder next to this file) for typical values and the right questions.
5. **Assembly and service:** how parts join (snap fits, screws, adhesive, welds), the assembly order, and what a user or technician must be able to open, replace or recycle.
6. **Compliance topics to check:** the families of standards that usually apply in the target market (for example electrical safety, radio, food contact, toy safety, battery transport, vehicle type approval). Name them as topics for a specialist to confirm, never as passed or certified.
7. **Open questions and risks:** what must be decided or tested next, most important first.
8. **Views needed for CAD:** front, side, top and three-quarter. If only one view exists, offer the matching renders (each uses allowance): `16:9` side elevations for vehicles and long products, `4:3` front and rear elevations, `1:1` for compact products, with `autoEnhance: false` and the same `subjectModelId` if one was saved.

Show a short summary in the chat (overview, part table, top three open questions) and offer the full package as a document the person can keep or send.

## Step 3: Hand on to CAD, if available

If a CAD or 3D connector is connected in this conversation (for example 3DJ for parametric CAD, drawings and STEP or STL exports), offer to pass the package to it: overall dimensions, part list and the approved image link. Follow that connector's own instructions and present its results separately from SketchMonkey's. If none is connected, say the package is ready for any CAD modeller or engineering partner.

## Boundaries

- This package is design intent, not engineering drawings, tolerance analysis, structural or safety validation, certification or a factory quote.
- Don't claim a material, process, certification or price is confirmed. Say who should confirm it (engineer, supplier, test lab).
- Keep proprietary details the person shares inside this conversation and their own documents.
