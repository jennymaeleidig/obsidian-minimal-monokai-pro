## 1. Color Scheme File

- [x] 1.1 Create `src/scss/color-schemes/monokai-pro.scss` with the dark-only Monokai Pro palette, following the existing pattern (e.g., dracula.scss, nord.scss)
- [x] 1.2 Define the 8 base color variables (`--color-red` through `--color-pink`) with Monokai Pro hex values
- [x] 1.3 Define HSL base and accent values: `--base-h: 285; --base-s: 5%; --base-l: 17%` and `--accent-h: 20; --accent-s: 96%; --accent-l: 70%`
- [x] 1.4 Define explicit background tiers (`--bg1: #2d2a2e`, `--bg2: #221f22`, `--bg3` as semi-transparent)
- [x] 1.5 Define explicit UI border tiers (`--ui1`, `--ui2`, `--ui3`) from the Monokai Pro border palette
- [x] 1.6 Define explicit text contrast tiers (`--tx1`, `--tx2`, `--tx3`) from the Monokai Pro foreground palette
- [x] 1.7 Define explicit accent tiers (`--ax1`, `--ax2`, `--ax3`) derived from orange `#fc9867`
- [x] 1.8 Define highlight backgrounds (`--hl1`, `--hl2`) and on-accent text (`--sp1`)
- [x] 1.9 Set `--font-monospace: 'Commit Mono', monospace` in the scheme block

## 2. Register in Build

- [x] 2.1 Add `@use 'color-schemes/monokai-pro';` to `src/scss/index.scss` in the color schemes section (alphabetically with existing imports)

## 3. Code Typography

- [x] 3.1 Add Commit Mono font stack to `--font-monospace` in `src/scss/variables/root.scss` (or verify it's set sufficiently in the color scheme)
- [x] 3.2 Add `font-variant-ligatures: contextual` to code blocks in `src/scss/content/code.scss`, targeting both CM6 editor blocks (`.HyperMD-codeblock`, `.cm-hmd-codeblock`) and reading view (`pre`, `code`, `.markdown-preview-view code`)
- [x] 3.3 Set code font size to 14px via `--font-code` variable override

## 4. Build and Verify

- [x] 4.1 Run `npm run build` to compile theme.css, obsidian.css, and Minimal.css
- [x] 4.2 Verify `theme.css` contains the `.theme-dark.minimal-monokai-pro-dark` rule with all expected variables
- [x] 4.3 Verify the build completes without SCSS errors
