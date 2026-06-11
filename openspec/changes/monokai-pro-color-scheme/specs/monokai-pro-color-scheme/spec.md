## ADDED Requirements

### Requirement: Monokai Pro dark color scheme

The theme SHALL provide a dark-only Monokai Pro color scheme activated by the CSS class `.theme-dark.minimal-monokai-pro-dark`.

#### Scenario: Dark scheme applies Monokai Pro background and text colors
- **WHEN** the Obsidian vault uses dark mode and the Monokai Pro color scheme is active
- **THEN** the primary background SHALL be `#2d2a2e`
- **AND** the secondary background (sidebar, panels) SHALL be `#221f22`
- **AND** the primary text color SHALL be `#fcfcfa`
- **AND** muted text SHALL be `#939293`
- **AND** faint text SHALL be `#727072`

#### Scenario: Dark scheme uses the Monokai Pro accent palette
- **WHEN** the Monokai Pro dark color scheme is active
- **THEN** the 8 base colors SHALL match the Monokai Pro palette:
  - `--color-red`: `#ff6188`
  - `--color-orange`: `#fc9867`
  - `--color-yellow`: `#ffd866`
  - `--color-green`: `#a9dc76`
  - `--color-cyan`: `#78dce8`
  - `--color-blue`: `#78dce8`
  - `--color-purple`: `#ab9df2`
  - `--color-pink`: `#ab9df2`

#### Scenario: Dark scheme uses orange as the interactive accent
- **WHEN** the Monokai Pro dark color scheme is active
- **THEN** the accent color for links and interactive elements SHALL be `#fc9867` (orange)
- **AND** the accent hover state SHALL be a lighter shade of the same orange

#### Scenario: Dark scheme defines all required Minimal UI variables
- **WHEN** the Monokai Pro dark color scheme is active
- **THEN** the following CSS custom properties SHALL be explicitly defined:
  - `--base-h`, `--base-s`, `--base-l` (background HSL basis)
  - `--accent-h`, `--accent-s`, `--accent-l` (accent HSL basis)
  - `--bg1`, `--bg2`, `--bg3` (background tiers)
  - `--ui1`, `--ui2`, `--ui3` (border/divider tiers)
  - `--tx1`, `--tx2`, `--tx3` (text contrast tiers)
  - `--ax1`, `--ax2`, `--ax3` (accent contrast tiers)
  - `--hl1`, `--hl2` (highlight/selection backgrounds)
  - `--sp1` (text on accent background)

### Requirement: Monokai Pro scheme is registered in the theme build

The new color scheme partial SHALL be imported in `src/scss/index.scss` so it compiles into the output CSS.

#### Scenario: Build includes Monokai Pro scheme
- **WHEN** the theme is built via `node build.js`
- **THEN** `theme.css` and `obsidian.css` SHALL contain the Monokai Pro color scheme CSS
- **AND** the scheme SHALL be scoped to `.theme-dark.minimal-monokai-pro-dark`

### Requirement: Commit Mono code typography

Code blocks and inline code SHALL use Commit Mono at 14px with contextual ligatures.

#### Scenario: Code blocks use Commit Mono with ligatures
- **WHEN** the theme is active
- **THEN** the monospace font family SHALL include `'Commit Mono'` as the first choice
- **AND** code blocks in both the CM6 editor and reading view SHALL use a 14px font size
- **AND** code blocks SHALL have `font-variant-ligatures: contextual` applied

#### Scenario: Ligature fallback is safe
- **WHEN** Commit Mono is not installed on the system
- **THEN** the font stack SHALL fall back to system `monospace`
- **AND** the ligature property SHALL not cause rendering errors
