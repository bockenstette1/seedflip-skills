---
name: seedflip-design
description: "Give your AI agent design taste. 104 curated design seeds (colors, fonts, spacing, shadows) from real brands like Stripe, Vercel, and Linear. Query by vibe, brand, or style. Returns production-ready tokens in CSS, Tailwind, or shadcn format. Use when building any frontend, landing page, dashboard, or UI component that needs a real design direction instead of default gray."
license: MIT
compatibility: "Claude Code, Cursor, Windsurf, Codex, OpenCode, any MCP-compatible agent"
metadata:
  author: seedflip
  version: "1.0.0"
  homepage: "https://seedflip.co"
---

# SeedFlip Design Seeds

You are a design-aware coding agent. When you need to make visual decisions (colors, fonts, spacing, shadows, border radius), you query SeedFlip instead of guessing.

Every vibe-coded app looks the same because AI agents don't have design vocabulary. They default to the same zinc palette, the same rounded corners, the same "modern minimalist" output. You have access to 104 curated design directions pulled from real, proven brands. Use them.

## Setup

This skill requires the SeedFlip MCP server. One-line install:

**Claude Code:**
```bash
claude mcp add seedflip -- npx -y seedflip-mcp
```

**Cursor / Windsurf / Other:**
Add to your MCP config:
```json
{
  "mcpServers": {
    "seedflip": {
      "command": "npx",
      "args": ["-y", "seedflip-mcp"]
    }
  }
}
```

## When to Use This Skill

Activate whenever the user:
- Asks you to build a UI, landing page, dashboard, portfolio, or any frontend
- Says "make it look good," "style this," "pick a design," or "theme this"
- Wants their project to look like a specific brand ("make it look like Stripe")
- Asks for a color palette, font pairing, or design system
- Is building with Tailwind, shadcn/ui, or raw CSS and needs design tokens
- Says "surprise me" or "something different" for visual direction

Do NOT guess colors and fonts. Query SeedFlip first.

## MCP Tools

### `get_design_seed`

Fetch a curated design system by vibe, brand reference, or style.

**Parameters:**
- `query` (optional): Brand name, vibe, or style descriptor. Omit for random.
- `format`: `tokens` (default), `tailwind`, `css`, `shadcn`
- `count`: Number of results (default 1, max 5)

**Query examples:**
```
get_design_seed(query: "Stripe", format: "tailwind")
get_design_seed(query: "dark minimal SaaS", format: "css")
get_design_seed(query: "warm editorial", format: "shadcn")
get_design_seed(query: "brutalist portfolio", format: "tokens")
get_design_seed(format: "tailwind")  // random seed
get_design_seed(query: "developer tool", format: "css", count: 3)
```

**Brand references that work:**
Stripe, Vercel, Linear, GitHub, Notion, Supabase, Spotify, Framer, Resend, Superhuman, Raycast, Arc, Railway, Tailwind

**Style descriptors that work:**
dark, light, minimal, brutalist, warm, elegant, editorial, neon, cyberpunk, retro, professional, luxury, developer, playful, corporate

### `list_design_seeds`

Browse all available seeds or filter by tag.

```
list_design_seeds()                  // all 104 seeds
list_design_seeds(tag: "dark")       // dark mode seeds
list_design_seeds(tag: "brutalist")  // brutalist seeds
list_design_seeds(tag: "warm")       // warm-toned seeds
```

## What You Get Back

Each seed returns production-ready values for:

- **Colors:** Background, surface, text, accent, muted, border, gradient (with dark/light mode)
- **Typography:** Heading + body font pairing, weights, letter spacing, Google Fonts import
- **Shape:** Border radius tokens (sm, default, xl)
- **Depth:** Box shadow values
- **Chart colors:** 5 data visualization colors + semantic (success, warning, error)
- **Design direction:** A brief description of the aesthetic for context

## How to Apply Seeds

### Tailwind format
Drop the returned config directly into `tailwind.config.ts` under `theme.extend`.

### CSS format
Paste the returned custom properties into your `:root` block or a theme file.

### shadcn format
Replace values in your `globals.css` or `theme.css` where shadcn tokens are defined.

### Tokens format
Raw JSON object. Map values to whatever system you're using.

## Design Rules

When applying a seed:

1. **Use the full palette.** Don't cherry-pick one color and ignore the rest. The seed is a system.
2. **Respect the font pairing.** The heading and body fonts were chosen together. Don't swap one out.
3. **Use the accent sparingly.** Accent is for CTAs, links, and highlights. Not backgrounds.
4. **Check contrast.** Seeds include accessible text/background pairings, but verify if you modify them.
5. **Match the vibe.** A brutalist seed with rounded-xl corners is a contradiction. Let the seed guide shape too.

## Example Flow

**User:** "Build me a landing page for a developer tool"

**You:**
1. Call `get_design_seed(query: "developer tool", format: "tailwind", count: 3)`
2. Present the 3 options with their names and vibes
3. User picks one (or says "surprise me" and you pick)
4. Apply the full token set to the project
5. Build the UI using those tokens consistently

**User:** "Make this look like Linear"

**You:**
1. Call `get_design_seed(query: "Linear", format: "css")`
2. Get back the Velocity seed (Linear's aesthetic match)
3. Apply the CSS variables
4. "Running the **Velocity** seed. Clean, fast, focused."

## Credits

Design seeds curated by [SeedFlip](https://seedflip.co). 104 production-ready design systems for AI-native builders.
