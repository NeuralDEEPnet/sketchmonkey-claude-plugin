# Space view recipes

Each recipe gives the camera and light part of the prompt. Put the full space package and the design language in front of it, and end with "Photorealistic spatial design render, no text, no logos, no signage lettering, no people."

## Light that makes a space read

- **Even daylight:** "soft even daylight from the open side, gentle shadows, true-to-life colour." Honest and calm; best for the overview and the plan.
- **Retail spots:** "warm track spotlights on the products, softer ambient light on the walls, light pools on the floor." Makes products the brightest thing in the image.
- **Evening:** "dusk outside, warm interior glow, lit shelves and counter." For hospitality and shop fronts.
- **Exhibition hall:** "neutral overhead hall lighting, darker surroundings, the stand lit from its own spots." Shows how the stand stands out from its neighbours.

## The standard set

| View | Camera part of the prompt | Ratio |
|---|---|---|
| Overview | "Raised three-quarter view from the front corner, camera about 3 m high looking down at 30°, 24 mm lens, the whole footprint in frame" | `16:9` |
| Eye level | "Eye-level view from the entrance, camera at 1.6 m, 28 mm lens, straight verticals" | `16:9` |
| Fixture detail | "Close view of the [counter / plinth / shelf] with products at true scale, 50 mm lens, shallow depth of field" | `4:3` |
| Plan | "Top-down plan view looking straight down, orthographic feel, furniture and floor finish visible, no roof" | `1:1` |
| Elevation | "Straight-on front elevation of the back wall, long lens, no perspective distortion" | `16:9` |

## Trade fair stands and pop-ups

- Show the stand from the aisle, slightly off-centre, with a hint of neutral neighbouring stands so the scale is clear.
- Name the open sides in the prompt ("open to the aisle on the front and left").
- Add "raised floor with a flush edge" or "hall carpet" so the floor reads correctly.

## Shops and showrooms

- Eye level from the door is the hero. Add "straight verticals, architectural photography".
- A window view from outside at dusk makes a strong opening image: "seen from the street through the shop window at dusk".
- For a display wall, use the elevation recipe and give the shelf count and the number of products per shelf.

## Cafes, bars and small hospitality

- Lead with the counter. "Three-quarter view of the counter from the customer side, camera at 1.5 m."
- Name seat counts and table sizes; otherwise chairs multiply.
- Evening light suits them best.

## Rooms a product lives in

- For a room built around one product (a speaker, a lamp, a kettle), describe the room as the space package and the product as what is on show, with its position ("on the oak sideboard, left of centre").
- When the product must stay exactly true to a real photo, render the room here and place the product with the `photo-edit` skill instead.

## Social formats

- `9:16` for stories: use the eye-level recipe with "vertical framing, floor to ceiling".
- `3:4` for feeds: the fixture detail or a tight eye-level crop.
