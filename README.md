# SketchMonkey Design Studio for Claude

![SketchMonkey](assets/icon.png)

Install in Claude Code: `/plugin install sketchmonkey --marketplace NeuralDEEPnet/sketchmonkey-claude-plugin`

SketchMonkey Design Studio brings an industrial, transport, packaging and spatial design studio into Claude. Describe a product, vehicle, pack or space you are designing, share a sketch of it, or start from an idea, and Claude works with your SketchMonkey account to take the design from brief to launch layouts: explore five design directions, render concepts and full vehicle view sets, design the packaging and the stand or shop it is sold from, review designs like a studio lead, build colour-material-finish boards, prepare design-intent briefs for engineering, create design presentation renders for reviews and lay out campaign layouts with editable type. Everything is guided in plain language, so you don't need design software or design training.

## What you can do

| Ask for | Skill | What you get |
|---|---|---|
| "What can SketchMonkey do for my product design?" | `/sketchmonkey:studio` | A friendly start that points you to the right workflow |
| "Show me five directions for a desk lamp" | `/sketchmonkey:explore-concepts` | Five design directions side by side, then concept renders of your favourites |
| "Make presentation renders of my lamp concept for the design review" | `/sketchmonkey:presentation-renders` | A hero render, CMF variant renders and detail renders of the product you are designing, presented as a design-review board |
| "Give me three colourways for my headphones" | `/sketchmonkey:cmf-board` | Part-by-part colour, material and finish options, saved as an editable CMF sheet |
| "Make a launch campaign for my product" | `/sketchmonkey:campaign` | Poster, square, vertical and banner layouts with real copy and editable type |
| "Set up our brand colours and voice" | `/sketchmonkey:brand-kit` | Saved brand rules, copy checks and on-brand headline options |
| "Design a two-seat electric city car" | `/sketchmonkey:transport-design` | A vehicle specification, then side, three-quarter, interior and detail views of the same vehicle |
| "Design a gift box for my candle" | `/sketchmonkey:packaging-design` | A pack specification, then front, three-quarter, open and shelf views of the same pack |
| "Design a pop-up shop for our launch" | `/sketchmonkey:spatial-design` | A space specification, then overview, eye-level, fixture and plan views of the same space |
| "Take my kettle idea all the way to launch" | `/sketchmonkey:design-program` | A phased studio program with an allowance plan, checkpoints and a design log |
| "Review my SketchMonkey concept before the client sees it" | `/sketchmonkey:design-review` | A focused studio crit with the top three changes, and an optional corrected render |
| "Get this ready for a manufacturer" | `/sketchmonkey:engineering-handoff` | A design-intent brief: dimensions, parts, materials, processes and open questions |

You don't have to type the commands. Ask in your own words and Claude picks the right workflow.

## Get started

1. **Add the plugin**
   - **Claude app (web, desktop, mobile):** open **Customize → Plugins** and add SketchMonkey Design Studio from the plugin directory.
   - **Claude Code:** run the install command above, or open the plugin directory with Claude Code's plugin manager and add SketchMonkey Design Studio there. Claude Code's own [plugin guide](https://code.claude.com/docs/en/plugins/install) explains how.
2. **Connect your SketchMonkey account**
   - **Claude app:** open the plugin's **Connectors** tab, select **Connect**, sign in to SketchMonkey and approve access.
   - **Claude Code:** use `/mcp`, choose the SketchMonkey server from this plugin and select **Authenticate**.
3. **Try a prompt**
   - "Explore five design directions for a compact recycled-aluminium desk lamp."
   - "Make a hero render and a three-colourway comparison of that lamp concept for our design review."
   - "Review the hero render against the brief and tell me the top three changes."
   - "Design a cargo e-bike for city deliveries and show me the side view first."
   - "Design a rigid gift box for my candle and show it on a shelf."
   - "Design a 3 by 3 metre market stand for our ceramics."

You need a SketchMonkey account; sign up at [sketchmonkey.design](https://www.sketchmonkey.design). If you already added SketchMonkey as a custom connector in Claude, you can keep just one of the two connections to avoid duplicate tools.

## Good to know

- **Design work only.** Every render is a visual aid inside a design workflow: a concept, a view of a vehicle, pack or space, a colour-material-finish option or a presentation render of something you are designing. SketchMonkey renders them from a detailed written description of the design. The plugin is not a general-purpose image generator.
- **Allowance.** Exploring directions, polishing prompts, CMF tables, layouts and text edits are free. Each render counts toward your SketchMonkey plan's limits, and Claude checks before large batches. Plans and billing are managed only on the SketchMonkey website; this plugin never asks for payment details.
- **Exports.** Campaign and CMF layouts are saved in your SketchMonkey project. Asking for export details returns sizes and image links; the plugin doesn't produce finished PNG or PDF files.
- **Words in images.** Renders can't reliably letter a name on a box or a sign. Packs and stands are designed with blank zones, and the campaign layouts add real, editable type on top.
- **Concepts, not engineering.** Concept renders, material suggestions and design-intent briefs are design proposals, not certified CAD, engineering analysis, print-ready artwork, measured drawings, safety or type approval, or manufacturing approval.

## What the plugin runs and sends

This plugin contains no executable code. It has two parts:

- **Skills:** written instructions that guide Claude through each workflow.
- **One remote connector:** the SketchMonkey MCP server at `https://sketchmonkey-neuraldeepnet.on.adaptive.ai/api/mcp/directory`, operated by Neural Deep Network Ltd. Claude connects to it only after you sign in with OAuth 2.1 (PKCE), granting the scopes `account:read`, `creative:read`, `creative:write` and `renders:run`.

When you use the plugin, Claude sends SketchMonkey the design briefs, render prompts, project names, brand rules and layout edits needed for your request. SketchMonkey stores your projects, brand rules, saved design references and renders in your account. Finished renders are served from SketchMonkey's content delivery network at `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/`. For a render, Claude sends only its written description of your design. SketchMonkey rejects sensitive personal data such as identity documents, health records, payment card numbers, credentials and real-person biometric data. Operational connector logs keep only the tool name, status, duration, an error code and a pseudonymous network hash, and are deleted after 24 hours.

## Tools

These are the connector tools the skills use.

| Tool | What it does | Changes data |
|---|---|---|
| `get_account_status` | Shows your plan and remaining render allowance | No |
| `enhance_prompt` | Suggests colour, material and finish language for a prompt | No |
| `generate_directions` | Compiles five design directions from a brief | No |
| `list_subject_models` | Lists saved design references and samples | No |
| `inspect_artboard` | Reads a layout's text, style and layers | No |
| `generate_variants` | Suggests copy or typography alternatives for a layout | No |
| `get_artboard_export_metadata` | Returns layout sizes and background image links | No |
| `get_job`, `get_render_status` | Check a render and return the finished image | No |
| `render_concept` | Starts a design render (uses render allowance) | Creates a render |
| `create_project` | Creates a design project | Creates |
| `create_campaign` | Creates campaign layouts in a project | Creates |
| `select_direction` | Sets a project's design direction | Overwrites |
| `apply_brand_dna` | Saves brand rules to a project and checks copy | Overwrites |
| `edit_artboard` | Edits a layout's text, font, alignment, accent or background | Overwrites |
| `save_subject_model` | Saves a reusable design reference | Creates or overwrites |

## Privacy policy

SketchMonkey's privacy policy is at [sketchmonkey.design/privacy](https://www.sketchmonkey.design/privacy) and its terms are at [sketchmonkey.design/terms](https://www.sketchmonkey.design/terms). It covers what SketchMonkey collects, how it's used and stored, sharing with third parties, retention and how to contact Neural Deep Network Ltd.

## Support

Visit [sketchmonkey.design/support](https://www.sketchmonkey.design/support) or email [3d@neuraldeep.net](mailto:3d@neuraldeep.net). You can disconnect Claude at any time from SketchMonkey's connections page or from the plugin's Connectors tab.

## License

The skills and files in this plugin are open source under the [MIT License](LICENSE); you're welcome to adapt them. Using the SketchMonkey service itself is governed by the [SketchMonkey Terms of Service](https://www.sketchmonkey.design/terms).

Contributions are welcome: open an issue or pull request on [GitHub](https://github.com/NeuralDEEPnet/sketchmonkey-claude-plugin).
