# SketchMonkey Design Studio for Claude

![SketchMonkey](assets/icon.png)

SketchMonkey Design Studio is a design guide and studio for physical products, vehicles, packaging and spaces, inside Claude. Describe a product, vehicle, pack or space, share a sketch or photo of it, or start from an idea, and Claude works with your SketchMonkey account the way an industrial design studio would: frame the brief, explore five design directions, see concept visuals and consistent view sets, build colour-material-finish boards, review designs like a studio lead, prepare design-intent briefs for engineering and lay the result out on presentation boards. Everything is guided in plain language, so you don't need design software or design training.

It is a design tool. It makes design visuals of a proposal; it does not edit photographs and does not generate video.

## What you can do

| Ask for | Skill | What you get |
|---|---|---|
| "What can SketchMonkey do for my product?" | `/sketchmonkey:studio` | A friendly start that points you to the right workflow |
| "Show me five directions for a desk lamp" | `/sketchmonkey:explore-concepts` | Five design directions side by side, then concept visuals of your favourites |
| "Show my speaker design from the side and up close" | `/sketchmonkey:design-views` | A consistent set of views of one design: hero, side, detail, colourway line-up or in context |
| "Give me three colourways for my headphones" | `/sketchmonkey:cmf-board` | Part-by-part colour, material and finish options, saved as an editable CMF sheet |
| "Critique this concept before the client sees it" | `/sketchmonkey:design-review` | A focused studio crit with the top three changes, and an optional corrected visual |
| "Design a two-seat electric city car" | `/sketchmonkey:transport-design` | A vehicle specification, then side, three-quarter, interior and detail views of the same vehicle |
| "Design a gift box for my candle" | `/sketchmonkey:packaging-design` | A pack specification, then front, three-quarter, open and shelf views of the same pack |
| "Design a pop-up shop for our launch" | `/sketchmonkey:spatial-design` | A space specification, then overview, eye-level, fixture and plan views of the same space |
| "Take my kettle idea from brief to sign-off" | `/sketchmonkey:design-program` | A phased studio program with an allowance plan, checkpoints and a design log |
| "Get this ready for a manufacturer" | `/sketchmonkey:engineering-handoff` | A design-intent brief: dimensions, parts, materials, processes and open questions |
| "Make a presentation board of the final design" | `/sketchmonkey:campaign` | Board, poster, slide and CMF sheet layouts with real copy, editable afterwards |
| "Set up our brand colours and voice" | `/sketchmonkey:brand-kit` | Saved brand rules, on-brand headline options and typography alternatives |

You don't have to type the commands. Ask in your own words and Claude picks the right workflow.

## Get started

1. **Add the plugin**
   - **Claude app (web, desktop, mobile):** open **Customize → Plugins** and add SketchMonkey Design Studio from the plugin directory.
   - **Claude Code:** open the plugin directory with Claude Code's plugin manager and add SketchMonkey Design Studio there. Claude Code's own [plugin guide](https://code.claude.com/docs/en/plugins/install) explains how.
2. **Connect your SketchMonkey account**
   - **Claude app:** open the plugin's **Connectors** tab, select **Connect**, sign in to SketchMonkey and approve access.
   - **Claude Code:** use `/mcp`, choose the SketchMonkey server from this plugin and select **Authenticate**.
3. **Try a prompt**
   - "Explore five design directions for a compact recycled-aluminium desk lamp."
   - "Show my ceramic pour-over dripper with a walnut base as a hero view, a side view and a detail."
   - "Give me three colourways for a pair of over-ear headphones."
   - "Design a cargo e-bike for city deliveries and show me the side view first."
   - "Design a rigid gift box for my candle and show it on a shelf."
   - "Design a 3 by 3 metre market stand for our ceramics."

You need a SketchMonkey account; sign up at [sketchmonkey.design](https://www.sketchmonkey.design).

## Good to know

- **Design visuals of a proposal.** Every image is rendered fresh from a detailed description of the design. When you share a photo or sketch, Claude reads the design from it and describes it; the photo itself is not uploaded or edited.
- **Allowance.** Exploring directions, polishing prompts, reviews, handoff briefs, CMF tables, layouts and text edits are free. Each image render counts toward your SketchMonkey plan's limits, and Claude checks before large batches. Plans and billing are managed only on the SketchMonkey website; this plugin never asks for payment details.
- **Exports.** Layouts and CMF sheets are saved in your SketchMonkey project. Asking for export details returns sizes and image links; the plugin doesn't produce finished PNG or PDF files.
- **Words in images.** Renders can't reliably letter a name on a box or a sign. Packs and stands are designed with blank zones, and the layouts add real, editable type on top.
- **Concepts, not engineering.** Concept visuals, material suggestions and design-intent briefs are design proposals, not photographs of a finished product, certified CAD, engineering analysis, print-ready artwork, measured drawings, safety or type approval, or manufacturing approval.

## What the plugin runs and sends

This plugin contains no executable code. It has two parts:

- **Skills:** written instructions that guide Claude through each workflow.
- **One remote connector:** the SketchMonkey Design Studio MCP server at `https://www.sketchmonkey.design/api/mcp/design`, operated by Neural Deep Network Ltd. It offers design tools only. Claude connects to it after you sign in with OAuth 2.1 (PKCE), granting the scopes `account:read`, `creative:read`, `creative:write` and `renders:run`.

Two more addresses belong to the same SketchMonkey service, and nothing else is contacted:

- **Sign-in:** the sign-in and consent pages are served by SketchMonkey's account service at `https://sketchmonkey-neuraldeepnet.on.adaptive.ai`.
- **Finished images:** image links point to SketchMonkey's own content delivery network at `https://sketchmonkey-neuraldeepnet.adaptive.ai/cdn/sketchmonkey/`.

When you use the plugin, Claude sends SketchMonkey the design briefs, render prompts, project names, brand rules and layout edits needed for your request. SketchMonkey stores your projects, brand rules, saved design references and renders in your account. Claude sends only its written description of your design; your own photos and files are not uploaded. SketchMonkey rejects sensitive personal data such as identity documents, health records, payment card numbers, credentials and real-person biometric data. Operational connector logs keep only the tool name, status, duration, an error code and a pseudonymous network hash, and are deleted after 24 hours.

## Tools

| Tool | What it does | Changes data |
|---|---|---|
| `get_account_status` | Shows your plan and remaining design-render allowance | No |
| `enhance_prompt` | Suggests colour, material and finish language for a brief | No |
| `generate_directions` | Compiles five design directions from a brief | No |
| `list_subject_models` | Lists saved design references and samples | No |
| `inspect_artboard` | Reads a layout's text, style and layers | No |
| `generate_variants` | Suggests copy or typography alternatives for a layout | No |
| `get_artboard_export_metadata` | Returns layout sizes and background image links | No |
| `get_job` | Checks a render and returns the finished image | No |
| `render_concept` | Starts a design concept visual (uses image allowance) | Creates a render |
| `create_project` | Creates a design project | Creates |
| `create_campaign` | Creates board, poster, slide and CMF sheet layouts in a project | Creates |
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
