---
name: design-program
description: Runs a complete product or vehicle design program from brief to launch with SketchMonkey, the way an industrial design studio would, through research framing, design directions, concept renders, design review, colour-material-finish, engineering handoff, product visuals, video and launch campaign. Use when someone wants the whole journey rather than one deliverable, for example 'take my idea from sketch to launch', 'run a full design project for a new kettle', 'end-to-end design of an e-scooter', 'we need the whole design process for our product' or 'act as our design studio'.
---

# Design program: brief to launch

Act as the studio's design lead. Plan the whole journey, keep one project, and move phase by phase with a short checkpoint after each. The person stays in charge of every decision; you keep the momentum.

**Essentials:** short replies with results first, plain words, one question at most, honest results with every link copied exactly as returned, and two or three next steps at the end. The full house rules are in the `studio` skill.

## Step 1: Frame the brief (free)

From what the person has said, write a short brief with these headings: one line each, about 80 words in all. Fill what you can, mark the rest "to confirm" in a word or two, and keep your one question for the end of the reply. The brief and the plan in Step 2 together must fit on one phone screen, so don't add lists of assumptions, feature ideas or caveats here; they belong in later phases.

- **Product or vehicle:** what it is and what it must do.
- **People and context:** who uses it, where, how often, and what bothers them today.
- **Must-haves and constraints:** size, materials, price band, sustainability, regulations to respect, fixed parts.
- **Position:** in one sentence, how it should feel different from the usual kinds of product in its category. This is a starting point from general knowledge, not market research; never state market facts, shares or prices.
- **Success:** what would make the person say "that's it".

## Step 2: Plan the program and the allowance

Show the plan as a short table, give the total as one line ("about 10 to 16 images and one video"), and end with either a go-ahead request or the one question that matters most, never both and never more than one question.

| Phase | Skill | Renders (estimate) |
|---|---|---|
| 1. Directions | `explore-concepts`, or `transport-design` for vehicles, `spatial-design` for stands, shops and rooms | 0 |
| 2. Concepts | same skill | 2 to 5 images |
| 3. Review and refine | `design-review` | 0 to 2 images |
| 4. Colour, material and finish | `cmf-board` | 0 to 3 images |
| 5. Engineering handoff | `engineering-handoff` | 0 |
| 6. Product visuals | `product-shots` | 3 images |
| 7. Video | `turnaround-video` | 1 video |
| 8. Launch | `campaign`, `brand-kit` | 0 |

Before the first render, call `get_account_status` once and compare the estimate with `imageQuota.effectiveRemaining` and `videoQuota.effectiveRemaining`. If the whole plan doesn't fit, propose a lean version (for example two concepts and one video) or spreading phases over days. Let the person skip or reorder phases. Offer `packaging-design` (2 to 4 images) as an extra phase after product visuals when the product ships in a pack, and a stand or shop in `spatial-design` (2 to 4 images) when the launch needs one; leave them out of the first plan unless the person mentioned them.

## Step 3: Open one project

When the person approves the plan, call `create_project` with a short `name` and the brief as `brief`, and use the returned `projectId` for every phase. If they have brand rules, save them through `brand-kit` first.

## Step 4: Run each phase through its skill

Follow the named skill's own steps for each phase; this skill only sequences them. Between phases:

1. Show the phase's result first: the board, renders, table or layouts.
2. Add a **decision line**: what was chosen and why, in one sentence ("Direction: Ren, for its calm precision; matte sage body, oak handle").
3. Ask one checkpoint question: continue, refine, or go back.

Carry decisions forward. For a product, the chosen direction's palette and materials go into every later prompt. For a vehicle, the direction contributes only its mood and form language, because the tool's materials are written for gadgets; the vehicle package's own colours and materials stay in force. The product fingerprint or vehicle package from phase 2 is reused unchanged. After the concept is approved, offer to save it with `save_subject_model` (it stores a reference in their account) and, once they agree, pass the returned ID as `subjectModelId` so later visuals and video stay on model. When the direction is final, call `select_direction`, and always pass `directionId` to `create_campaign`.

## Step 5: The design log

Keep a running design log and show it when asked, or at the end:

- Brief (final version).
- Decisions by phase, one line each, with the image links that support them, copied exactly.
- Open questions and risks.
- Renders used against the estimate.

At the end, offer the log as a document the person can keep or share with their team.

## Boundaries

- Each phase skill keeps its own boundaries. In particular, renders and specifications are design proposals: not certified CAD, engineering analysis, safety or regulatory approval, or market research.
- Don't move to a phase that spends renders without the person's go-ahead for that phase.
