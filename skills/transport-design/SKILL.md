---
name: transport-design
description: Transport and vehicle design with SketchMonkey, for cars, motorcycles, e-bikes, scooters, trucks, buses, trains, aircraft cabins, eVTOLs, boats and mobility pods. Takes a vehicle from package and proportions to a consistent set of side, front three-quarter, rear three-quarter, interior and detail renders, and on to turntable videos. Use for requests like 'design an electric city car', 'sketch a cafe-racer motorcycle', 'show me a tram for our city', 'interior for a sleeper train', 'concept for a two-seat eVTOL' or 'what could our e-bike look like'.
---

# Transport design

Help people design vehicles the way a transport design studio does: proportions first, then surfaces, then details, always seen from the standard views. A vehicle that reads well in side view almost always reads well everywhere else.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. Each image uses one render from the person's allowance; a full view set is five renders, so confirm before starting it. The full house rules are in the `studio` skill.

## Step 1: Write the vehicle package (free)

Before any render, write a package of 80 to 140 words. It plays the role the product fingerprint plays in `product-shots`, and it goes into every prompt so every view shows the same vehicle.

- **Type and mission:** what it is, who rides in it, where and how far ("two-seat urban electric city car for 30 km daily commutes and tight parking").
- **Layout and drivetrain:** seats and layout (1+1, 2+2, 3 rows, cab-forward), drive (electric skateboard, mid-engine, hub motors, pantograph, sail), wheels or hull or rotors.
- **Proportions, as ratios:** length to height, wheelbase to overall length, front and rear overhangs, wheel diameter against body height, greenhouse (the glass area) against body side. "Wheelbase about 70% of length, very short overhangs, wheels about half the body-side height."
- **Stance:** wheels pushed to the corners, track width, ride height, rake.
- **Signature elements:** lamp graphic, shoulder line, beltline kick, roof shape, nose shape, wheel design.
- **Materials and colours per zone:** body paint, lower cladding, glazing, brightwork, wheels or trims, with a colour name and approximate hex.
- **Must not change:** three to five traits that define the vehicle.

Ask one question if the mission or size is unclear; otherwise state what you assumed in one line. Transport words and their plain meanings are in `${CLAUDE_SKILL_DIR}/references/transport-vocabulary.md` (the `references` folder next to this file). Use them in prompts; explain them in plain words when you talk to the person.

## Step 2: Explore directions (free)

For a new vehicle, call `generate_directions` with the package as the `brief`, and present the five directions as a short board, the same way `explore-concepts` does. Read each lens for vehicles:

| Lens | As a vehicle |
|---|---|
| Ren | Precise, reduced and engineered; clean surfaces, honest proportions |
| Maya | Friendly and easy to live with; generous glass, step-in height, soft radii |
| Kai | Premium and polished; deep paint, perfect reflections, launch-stage presence |
| Zola | Dramatic and sculptural; faceted surfaces, aggressive stance |
| Nova | Organic and experimental; flowing biomimetic surfaces |

The tool's materials, palettes and rationale are written for gadgets (CNC aluminium, moulded polymer, bronze, marble). Use only each direction's mood and form language, say so in one line, and keep the materials and colours from the vehicle package or the ones the person chose.

Skip this step when the person already knows the look they want.

## Step 3: Render the view set

The standard set, in this order:

1. **Side profile**, `16:9`: the proportion check. Pure side elevation, wheels at the same height, camera at mid-wheel height.
2. **Front three-quarter**, `16:9`: the hero.
3. **Rear three-quarter**, `16:9`: lamp graphic, tail shape and stance.
4. **Interior**, `16:9`: the driver's or passenger's view, or a cabin overview.
5. **Detail**, `4:3`: lamp signature, wheel, door handle or seat.

Start with the side profile alone when proportions are still open, review it with the person, then render the rest. View recipes for cars, two-wheelers, rail, aircraft, boats and pods are in `${CLAUDE_SKILL_DIR}/references/vehicle-views.md`.

Write each prompt yourself:

> **[view]** of **[full vehicle package]**. **[direction's design language]**. **[setting]**. **[lighting]**. **[camera and lens]**. Photorealistic transport design render, no text, no badges, no logos, no licence plate characters.

Keep the closing words "transport design render" in every prompt. SketchMonkey reads them to switch from product and room wording to transport wording, which is what keeps a car body from being described like a gadget or a cabin like a room.

Call `render_concept` with:
- `prompt`: the prompt above.
- `preset`: `ren` for most work and `kai` for premium launch looks. Avoid `nova` for production-intent views; it adds surreal effects. For the Maya, Zola or Nova look, use `ren` and write that look into the prompt.
- `autoEnhance: false`, because the prompt is complete.
- `aspectRatio` from the list above.

Start all renders in the set, then poll each `jobId` with `get_job` about every 15 seconds.

## Step 4: Keep it the same vehicle

Once the person likes a front three-quarter render, offer to save the vehicle with `save_subject_model`: `kind: "car"` (use it for any vehicle), a short `name`, the package as `identityLock`, the must-not-change traits as `immutableTraits`, and the render's `imageUrl` as `heroImageUrl`. Pass the returned ID as `subjectModelId` in later renders and videos so the studio conditions on that image. Say plainly that this improves consistency but doesn't guarantee identical results.

## Step 5: Review like a studio

Look at every render before replying. Check, view by view:
- **Proportions:** wheelbase, overhangs and wheel size match the package; nothing stretched.
- **Stance:** wheels fill the arches, sit on the ground, and match each other.
- **Consistency:** the lamp graphic, glass shape and feature lines match across views.
- **Stray text:** badges, plate characters or warped lettering.

Present the set as a contact sheet: view name, one line on what it shows, and `[Open full-size image](imageUrl)`. Then give a short crit: what works, and the one change that would improve the design most. For a deeper review use the `design-review` skill.

## Step 6: Next steps

- A 360° turntable or a smooth side-profile glide (`turnaround-video`; `cameraPreset` `industrial_turntable` or `lateral_profile`).
- Colour and trim options: paint, cladding, wheels and interior textiles (`cmf-board`).
- A design-intent package for engineering or a CAD model (`engineering-handoff`).
- Launch visuals and a reveal campaign (`campaign`).

## Boundaries

- Design original vehicles. Don't copy a real manufacturer's signature grille, lamp graphic, badge or name; describe the qualities the person likes instead ("a long-bonnet grand tourer feel"). Label studies of existing vehicles "unofficial concept".
- Renders are design proposals. They are not crash, aerodynamic, homologation or airworthiness evidence, and they don't confirm that the package fits real people, batteries or engines.
