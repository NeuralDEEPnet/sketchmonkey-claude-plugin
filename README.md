# SketchMonkey Design Studio for Claude

![SketchMonkey](assets/icon.png)

SketchMonkey Design Studio brings a product design studio into Claude. Describe a product, share a photo of it, or start from an idea, and Claude works with your SketchMonkey account to create studio-quality product shots, explore five design directions, build colour-material-finish boards, lay out launch campaigns and render 360° product videos. Everything is guided in plain language, so you don't need design software or design training.

## What you can do

| Ask for | Skill | What you get |
|---|---|---|
| "What can SketchMonkey do for my product?" | `/sketchmonkey:studio` | A friendly start that points you to the right workflow |
| "Make my product photos look professional" | `/sketchmonkey:product-shots` | Hero, white-background listing, lifestyle, detail and social shots that stay true to your product |
| "Show me five directions for a desk lamp" | `/sketchmonkey:explore-concepts` | Five design directions side by side, then concept renders of your favourites |
| "Give me three colourways for my headphones" | `/sketchmonkey:cmf-board` | Part-by-part colour, material and finish options, saved as an editable CMF sheet |
| "Make a launch campaign for my product" | `/sketchmonkey:campaign` | Poster, square, story and banner layouts with real copy, editable afterwards |
| "Set up our brand colours and voice" | `/sketchmonkey:brand-kit` | Saved brand rules, on-brand headline options and typography alternatives |
| "Make a 360° spin for Instagram Stories" | `/sketchmonkey:turnaround-video` | Short product videos with turntable, reveal, macro and other camera moves |

You don't have to type the commands. Ask in your own words and Claude picks the right workflow.

## Get started

1. **Install the plugin**
   - **Claude app (web, desktop, mobile):** open **Customize → Plugins**. Install SketchMonkey Design Studio from the directory once it's listed, or choose **Add → Add marketplace**, enter `NeuralDEEPnet/sketchmonkey-claude-plugin` and install it from there.
   - **Claude Code:** run `/plugin marketplace add NeuralDEEPnet/sketchmonkey-claude-plugin`, then `/plugin install sketchmonkey@neuraldeep`.
2. **Connect your SketchMonkey account**
   - **Claude app:** open the plugin's **Connectors** tab, select **Connect**, sign in to SketchMonkey and approve access.
   - **Claude Code:** run `/mcp`, choose the SketchMonkey server from this plugin and select **Authenticate**.
3. **Try a prompt**
   - "Make a white-background listing photo and a cosy kitchen scene of my ceramic pour-over dripper with a walnut base."
   - "Explore five design directions for a compact recycled-aluminium desk lamp."
   - "Turn that hero shot into a 6-second 360° spin for Stories."

You need a SketchMonkey account; sign up at [sketchmonkey.design](https://www.sketchmonkey.design). If you already added SketchMonkey as a custom connector in Claude, you can keep just one of the two connections to avoid duplicate tools.

## Good to know

- **Images are created, not retouched.** SketchMonkey renders new images from a detailed description of your product. When you share a photo, Claude describes your product to the studio in detail; it doesn't edit the photo's pixels.
- **Allowance.** Exploring directions, polishing prompts, CMF tables, layouts and text edits are free. Each image render and each video render counts toward your SketchMonkey plan's limits, and Claude checks before large batches. Plans and billing are managed only on the SketchMonkey website; this plugin never asks for payment details.
- **Exports.** Campaign and CMF layouts are saved in your SketchMonkey project. Asking for export details returns sizes and image links; the plugin doesn't produce finished PNG or PDF files.
- **Concepts, not engineering.** Concept renders and material suggestions are design proposals, not certified CAD, engineering analysis or manufacturing approval.

## What the plugin runs and sends

This plugin contains no executable code. It has two parts:

- **Skills:** written instructions that guide Claude through each workflow.
- **One remote connector:** the SketchMonkey MCP server at `https://sketchmonkey-neuraldeepnet.on.adaptive.ai/api/mcp`, operated by Neural Deep Network Ltd. Claude connects to it only after you sign in with OAuth 2.1 (PKCE), granting the scopes `account:read`, `creative:read`, `creative:write` and `renders:run`.

When you use the plugin, Claude sends SketchMonkey the design briefs, render prompts, project names, brand rules and layout edits needed for your request. SketchMonkey stores your projects, brand rules, saved product references and renders in your account and serves finished images and videos from its own content delivery network. Product photos you share with Claude are not uploaded to SketchMonkey; Claude only sends its written description. SketchMonkey rejects sensitive personal data such as identity documents, health records, payment card numbers, credentials and real-person biometric data. Operational connector logs keep only the tool name, status, duration, an error code and a pseudonymous network hash, and are deleted after 24 hours.

## Tools

| Tool | What it does | Changes data |
|---|---|---|
| `get_account_status` | Shows your plan and remaining image and video allowance | No |
| `enhance_prompt` | Suggests colour, material and finish language for a prompt | No |
| `generate_directions` | Compiles five design directions from a brief | No |
| `get_camera_presets` | Lists video camera moves and recipes | No |
| `list_subject_models` | Lists saved product references and samples | No |
| `inspect_artboard` | Reads a layout's text, style and layers | No |
| `generate_variants` | Suggests copy or typography alternatives for a layout | No |
| `get_artboard_export_metadata` | Returns layout sizes and background image links | No |
| `get_job`, `get_render_status` | Check a render and return the finished image or video | No |
| `render_concept` | Starts an image render (uses image allowance) | Creates a render |
| `render_video` | Starts a video render (uses video allowance) | Creates a render |
| `create_project` | Creates a design project | Creates |
| `create_campaign` | Creates campaign layouts in a project | Creates |
| `select_direction` | Sets a project's design direction | Overwrites |
| `apply_brand_dna` | Saves brand rules to a project and checks copy | Overwrites |
| `edit_artboard` | Edits a layout's text, font, alignment, accent or background | Overwrites |
| `save_subject_model` | Saves a reusable product reference | Creates or overwrites |

## Privacy policy

SketchMonkey's privacy policy is at [sketchmonkey.design/privacy](https://www.sketchmonkey.design/privacy) and its terms are at [sketchmonkey.design/terms](https://www.sketchmonkey.design/terms). It covers what SketchMonkey collects, how it's used and stored, sharing with third parties, retention and how to contact Neural Deep Network Ltd.

## Support

Visit [sketchmonkey.design/support](https://www.sketchmonkey.design/support) or email [3d@neuraldeep.net](mailto:3d@neuraldeep.net). You can disconnect Claude at any time from SketchMonkey's connections page or from the plugin's Connectors tab.

## License

The skills and files in this plugin are open source under the [MIT License](LICENSE); you're welcome to adapt them. Using the SketchMonkey service itself is governed by the [SketchMonkey Terms of Service](https://www.sketchmonkey.design/terms).

Contributions are welcome: open an issue or pull request on [GitHub](https://github.com/NeuralDEEPnet/sketchmonkey-claude-plugin). The `evals/` folder holds a `claude plugin eval` suite with mocked SketchMonkey tools, so changes to the skills can be tested without spending renders.
