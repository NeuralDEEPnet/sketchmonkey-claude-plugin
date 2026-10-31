# Camera controls

Use a `cameraPreset` for most clips. For a custom move, leave the preset out and combine one option from each table below. If a preset is set, it overrides the individual controls.

## Motion (`cameraMotion`)

| Value | What the camera does | Use it to |
|---|---|---|
| `orbit_360` | Full circle around the product at a steady distance | Show every side |
| `push_in` | Slow move toward the product | Draw attention to a detail or material |
| `pull_out` | Starts close and moves back to reveal the whole product | Make a dramatic reveal |
| `pan_horizontal` | Slides sideways along the product | Show a long or sleek profile |
| `tilt_vertical` | Travels up from base to top | Emphasise height and proportions |
| `crane_arc` | Sweeps down from above to eye level in a curve | Add scale and drama |
| `static_tripod` | Camera stays still while light moves across the surfaces | Show reflections and finishes calmly |
| `drone_spiral` | Rises in a corkscrew around the product | Showpieces and trade-show energy |

## Angle (`cameraAngle`)

| Value | Viewpoint | Feels |
|---|---|---|
| `eye_level` | Straight on | Honest, natural proportions |
| `low_angle` | Looking up | Powerful, heroic |
| `high_angle` | Looking down at about 35° | Shows top surfaces and controls |
| `top_down` | Straight down | Graphic, flat-lay style |
| `isometric` | Technical three-sided view | Engineering and catalogue |
| `macro_detail` | Extreme close-up | Texture and craftsmanship |

## Pacing (`cameraPacing`)

| Value | Feel |
|---|---|
| `smooth_cinematic` | Gentle ease in and out, filmic |
| `studio_precision` | Constant speed, catalogue-like |
| `dramatic_reveal` | Lingers, then sweeps |

## Lens (`lensFraming`)

| Value | Framing |
|---|---|
| `tight_hero` | 85mm, product fills the frame, flattering perspective |
| `wide_context` | 35mm, shows the product in its surroundings |
| `macro_focus` | 100mm macro, ultra-close on materials |

## Recipes by product type

| Product | Suggested setup |
|---|---|
| Headphones, speakers, gadgets | `industrial_turntable`, 16:9, 6 s |
| Shoes, bags, fashion accessories | `hero_reveal`, 9:16, 6 s |
| Watches, jewellery, knives | `cmf_macro`, 1:1, 6 s |
| Perfume, cosmetics | `locked_studio`, 9:16, 6 s |
| Furniture, lamps | `lateral_profile` or custom `crane_arc` + `high_angle` + `smooth_cinematic` + `wide_context`, 16:9, 8 s |
| Drones, robots, modular kits | `cad_isometric`, 16:9, 8 s |

## Fixing common problems

| Problem | Try |
|---|---|
| Product warps or changes shape | Animate an existing render with `referenceImageUrl`, use `static_tripod` or `orbit_360` with `studio_precision`, and add "rigid, no morphing" to the prompt |
| Motion too fast or jerky | `smooth_cinematic` pacing and an 8-second clip |
| Too much background | `tight_hero` lens and "seamless studio background" |
| Details not visible | `cmf_macro` preset, or `push_in` with `macro_detail` and `macro_focus` |
| Feels flat | `low_angle` with `dramatic_reveal`, plus "strong rim light" in the prompt |
