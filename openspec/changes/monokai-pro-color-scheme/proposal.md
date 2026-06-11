## Why

This fork of the Minimal theme needs a Monokai Pro color scheme to match the user's VS Code, terminal, and system-wide theme. The existing Minimal theme ships 14 preset color schemes but none use the Monokai Pro palette. A new color scheme gives a cohesive Monokai Pro look across the Obsidian editor, reading mode, code blocks, and the published Digital Garden site — without touching any Minimal layout or feature code.

## What Changes

- **New color scheme**: `monokai-pro` dark-only color scheme added to the theme
- **Monokai Pro palette**: Background `#2d2a2e`, foreground `#fcfcfa`, orange accent `#fc9867`, plus red/green/yellow/cyan/purple sourced from the user's VS Code tmTheme (the authoritative source of truth)
- **Code block typography**: Commit Mono at 14px with contextual ligatures for code blocks and inline code — applies to both the CM6 editor and the rendered reading view
- **No structural changes**: All Minimal theme features (focus mode, colorful headings, tab styles, image grid, cards, etc.) remain untouched — only CSS variables change
- **Digital Garden compatibility**: The new color scheme's variables (`--background-primary`, `--text-normal`, `--text-accent`, etc.) are automatically consumed by the Digital Garden published site

## Capabilities

### New Capabilities
- `monokai-pro-color-scheme`: A dark-only Monokai Pro color scheme for the Minimal theme, using the authoritative Monokai Pro palette from the VS Code tmTheme, with Commit Mono code typography and contextual ligatures.

### Modified Capabilities
<!-- None — this is a pure addition, no existing specs change -->

## Impact

- **New file**: `src/scss/color-schemes/monokai-pro.scss` (~60 lines)
- **Modified file**: `src/scss/index.scss` (add one `@use` import line)
- **Modified file**: `src/scss/content/code.scss` (add Commit Mono font and ligature rules)
- **Build output**: `theme.css`, `Minimal.css`, and `obsidian.css` all regenerate with the new scheme included
- **No API changes, no dependency changes, no breaking changes**
