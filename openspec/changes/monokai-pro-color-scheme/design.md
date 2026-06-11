## Context

This is a fork of the [obsidian-minimal](https://github.com/kepano/obsidian-minimal) theme (v8.2.1) by @kepano. The Minimal theme uses SCSS compiled into `theme.css` and `obsidian.css` via a Node.js build script (`build.js` using the `sass` package). Color schemes live in `src/scss/color-schemes/` as partial SCSS files, each defining CSS custom properties scoped to a theme class like `.theme-dark.minimal-nord-dark`.

The user's entire development environment uses the Monokai Pro color palette: VS Code (source of truth via `MonokaiPro.tmTheme`), terminal (Ghostty), Neovim, pi agent, glow, and bat. This theme fork brings that same palette to Obsidian. The published Digital Garden site consumes the same CSS variables, so the colors apply automatically there too.

The authoritative Monokai Pro palette comes from two chezmoi-managed sources:
- `~/.local/share/chezmoi/dot_config/bat/themes/MonokaiPro.tmTheme` — the VS Code TextMate theme with full syntax scopes
- `~/.local/share/chezmoi/dot_pi/agent/themes/monokai-pro.json` — a simplified JSON palette

## Goals / Non-Goals

**Goals:**
- Add a dark-only Monokai Pro color scheme as a new SCSS partial in the Minimal theme's existing color-scheme system
- Use the exact Monokai Pro hex values from the VS Code tmTheme as the authoritative source
- Set Commit Mono 14px with contextual ligatures as the code block font
- Register the new scheme in `index.scss` so it compiles into the output CSS
- Keep all existing color schemes, features, and layout code untouched

**Non-Goals:**
- No light mode variant (Monokai Pro is dark-only by design)
- No structural changes to Minimal's layout, components, or feature flags
- No changes to the Minimal Theme Settings companion plugin (the scheme is available via the built `theme.css` / `obsidian.css`; users apply it via Style Settings plugin or CSS snippet)
- No deep syntax highlighting overrides — the 8 `--color-*` CSS variables suffice; Obsidian's built-in CodeMirror-to-color-var mapping handles token-level highlighting
- No true-black variant (`minimal-dark-black`) — Monokai Pro's warm `#2d2a2e` background is part of its identity

## Decisions

### Decision 1: Use Minimal's existing color scheme pattern (not a standalone theme)

**Rationale:** Minimal already has 14 color schemes following a well-defined pattern. Creating a new SCSS partial in the same structure means zero risk of breaking other features, automatic compatibility with all Minimal theme features, and trivial maintenance. A standalone full-theme CSS file would duplicate thousands of lines and diverge over time.

**Alternative considered:** Fork the FaintWhisper obsidian-monokai-pro repo. Rejected — it's a standalone theme (not Minimal-based), incomplete (only ~12KB of CSS, minimal feature support), and hasn't been updated since 2022.

### Decision 2: Compute HSL base/accent values from the hex palette, not from dynamic-color.scss formulas

**Rationale:** Minimal's `dynamic-color.scss` derives `--bg1`, `--bg2`, `--ui1`, etc. from `--base-h/s/l` using formulas. However, most mature color schemes (Nord, Catppuccin, Dracula) override these with explicit hex values for precise color control. We follow the same pattern: define `--base-h: 285; --base-s: 5%; --base-l: 17%` for auto-derived fallbacks, then explicitly set `--bg1: #2d2a2e`, `--bg2: #221f22`, etc. to ensure exact palette fidelity.

**Derivation for `--base-h/s/l` (dark mode):**
- Background `#2d2a2e` → HSL(285°, 5%, 17%) — a near-gray with subtle purple warmth
- Accent orange `#fc9867` → HSL(20°, 96%, 70%)

### Decision 3: Orange (#fc9867) as the accent color

**Rationale:** The user's pi theme uses `"accent": "#fc9867"`. The tmTheme uses orange for function arguments, decorators, and namespaces. In VS Code, the Monokai Pro theme uses warm orange as its primary interactive accent. Purple (`#ab9df2`) is used for numbers and constants — a secondary role.

**Alternative considered:** Purple as accent. Rejected — purple is semantically reserved for constants/numbers in the Monokai Pro grammar; orange is the active/interactive color.

### Decision 4: Map Monokai Pro cyan (#78dce8) to both `--color-blue` and `--color-cyan`

**Rationale:** Monokai Pro has no distinct blue in its palette — `#78dce8` (a teal-cyan) serves as both the "cool" accent for types, library functions, and storage types. Obsidian expects separate `--color-blue` and `--color-cyan` variables. Mapping the same teal to both ensures consistent rendering regardless of which variable Obsidian's token engine queries.

### Decision 5: Commit Mono with ligatures via `--font-monospace` and `font-variant-ligatures`

**Rationale:** The user wants Commit Mono at 14px with contextual ligatures specifically for code blocks. Minimal uses `--font-monospace` for the editor and `--font-code` for rendered code. We set `--font-monospace: 'Commit Mono', monospace` at the color-scheme level and add explicit `font-variant-ligatures: contextual` rules in `code.scss` for code blocks. The ligature rule targets both CM6 editor code blocks (`.HyperMD-codeblock`) and reading view code blocks (`.markdown-preview-view code`, `pre`).

## Risks / Trade-offs

- **[Risk] Commit Mono font not installed** → Mitigation: The `font-family` stack falls back to system `monospace`. The ligature rule is purely additive — no ligature fallback behavior is harmed.
- **[Risk] Obsidian's CodeMirror token mapping may color some tokens unexpectedly** → Mitigation: The 8 `--color-*` vars are intentionally simple. If a specific token looks wrong, explicit `.cm-*` overrides can be added later in a follow-up change without touching the color scheme file.
- **[Risk] Obsidian updates its CSS variable naming** → Mitigation: Minimal theme itself breaks under such changes; our scheme uses the same variables Minimal uses, so it inherits the same resilience (or breakage).
- **[Trade-off] No light mode** → The scheme only activates under `.theme-dark`. Users in light mode see Minimal's default light colors. This is by design — Monokai Pro is fundamentally a dark theme.
