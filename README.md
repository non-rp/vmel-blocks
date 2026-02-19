# Plugin Vmel Blocks

A set of custom Gutenberg blocks built with a modern build pipeline (Tailwind CSS) and an OOP PHP architecture for WordPress.

> Status: Planning / MVP / WIP  
> Requires: WordPress X.Y+, PHP 8.1+ 
> License: GPL-3.0-or-later

---

## Table of Contents
- [Goals](#goals)
- [Non-Goals](#non-goals)
- [Features](#features)
- [Blocks](#blocks)
- [Global Settings](#global-settings)
- [Architecture](#architecture)
- [Folder Structure](#folder-structure)
- [Build & Tooling](#build--tooling)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Performance](#performance)
- [Security](#security)
- [Compatibility](#compatibility)
- [Roadmap](#roadmap)
- [Changelog](#changelog)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)

---

## Goals
- Build reusable Gutenberg blocks focused on real-world layouts.
- Use Tailwind CSS to speed up UI development while keeping output predictable.
- Keep PHP side strictly OOP (autoloading, DI-friendly services, clear responsibilities).
- Optimize for performance: minimal CSS/JS shipped per page.

## Non-Goals
- Becoming a full page builder/theme replacement.
- Shipping a huge design system with hundreds of presets.
- Supporting legacy WP/PHP versions beyond the defined minimums.

---

## Features
- Custom blocks with clean markup and predictable frontend output.
- Editor controls with sane defaults and responsive options.
- Tailwind-based styling with a controlled output (no bloat).
- Per-block asset loading (when possible).
- Global plugin settings (colors/spacing/typography presets) (optional).
- Import/export settings (optional).
- i18n-ready UI.

---

## Blocks

### Layout
- **Container**: width, padding, background, optional inner grid.
- **Row / Grid**: columns, gap, responsive behavior.
- **Section**: spacing presets, background, anchor, optional shape divider.

### Content
- **Heading**: advanced typography, highlight part, margin presets.
- **Text / Rich Text**: max width, typography presets.
- **Buttons**: variants, sizes, icons, full width on mobile.

### Media
- **Image**: aspect ratios, border radius, caption.
- **Icon**: icon library strategy + size/color controls.

### Advanced / Utility (later)
- **Tabs / Accordion**
- **Modal**
- **Testimonials**
- **Query Loop enhancements** (if you go there)

For each block (template):
#### Block: {Block Name}
- **Purpose**
- **Controls**: (list editor controls)
- **Frontend output**: (notes about markup/classes)
- **Supports**: align, spacing, color, typography (what you support)
- **Accessibility**: aria/keyboard notes
- **Assets**: what loads (editor/front)

---

## Global Settings
- Design tokens / presets:
  - Colors
  - Spacing scale
  - Typography scale
  - Border radius scale
- Defaults per block
- Reset / migration strategy for settings changes
- Import/export (JSON) (optional)

---

## Architecture
High-level description of how PHP/JS/CSS parts communicate.

### PHP (OOP)
- Plugin bootstrap (single entry point).
- Service container / service registry approach.
- Block registration layer:
  - register_block_type / metadata (`block.json`)
  - render callbacks for dynamic blocks (if any)
- Settings API layer (if you provide global settings).
- REST endpoints (optional), capability checks.

### JavaScript
- Block editor code organization
- Shared components (controls, panels)
- Data flow strategy (block attributes vs global settings)

### Tailwind strategy
- Tailwind in editor + frontend:
  - Option A: compile a plugin stylesheet and scope it
  - Option B: generate minimal CSS for used classes (recommended)
- Strategy to avoid conflicts with theme styles
- Class naming conventions (if you add plugin prefixes)

---

## Folder Structure
Explain the intended structure early (helps you stay consistent).

Example:
- `plugin.php`
- `src/` (PHP)
  - `Plugin.php`
  - `Container/`
  - `Blocks/`
  - `Admin/`
  - `Assets/`
- `blocks/`
  - `{block-name}/`
    - `block.json`
    - `edit.tsx`
    - `save.tsx` (or `render.php` for dynamic)
    - `style.css` (generated or minimal)
- `assets/`
  - `css/`
  - `js/`
- `build/` (compiled output)
- `languages/`

---

## Build & Tooling
- Node version
- Package manager (npm/pnpm/yarn)
- Commands:
  - `dev`
  - `build`
  - `lint`
  - `format`
- WordPress scripts / Vite / custom webpack approach
- Tailwind config notes:
  - content paths
  - safelist policy (if needed)

---

## Development Workflow
- Local setup (WP + plugin + build)
- How to add a new block step-by-step
- How to add a new shared control component
- How to add styles safely without bloating CSS
- Release checklist

---

## Coding Standards
### PHP
- PHP version, strict types (yes/no)
- PSR-12, namespaces, autoloading
- OOP rules: no globals, no fat singletons, SRP services

### JS/TS
- TypeScript or JS
- ESLint/Prettier rules
- No inline strings in controls (i18n)

---

## Performance
- Asset loading strategy
- CSS size control strategy (Tailwind build)
- Avoiding layout shift / expensive reflows
- Caching for dynamic blocks (if any)

---

## Security
- Capability checks
- Sanitization/escaping strategy for dynamic render
- REST endpoints security (nonces, permissions)

---

## Compatibility
- Supported WP versions
- Supported PHP versions
- Known theme conflicts / limitations
- Full Site Editing vs classic themes notes

---

## Roadmap
### MVP (v0.1)
- [ ] Container block
- [ ] Grid block
- [ ] Buttons block
- [ ] Tailwind build pipeline (editor + frontend)
- [ ] Basic settings (optional)

### v0.2
- [ ] Typography presets
- [ ] Responsive controls improvements
- [ ] Better per-block asset loading

### v1.0
- [ ] Documentation
- [ ] Backward compatibility guarantees
- [ ] Import/export settings

---

## Changelog
Follow Keep a Changelog format.

---

## FAQ
- Why Tailwind in a WP plugin?
- Will it conflict with my theme?
- Can I disable plugin styles?
- Does it work with FSE?

---

## Contributing
- How to run locally
- PR rules
- Branch naming
- Commit message convention

---

## License
GPL-3.0-or-later

