# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Project Is

**Sass Forever** is a reference architecture for organizing Sass projects — not a buildable application. It has no package.json, no build system, and no tests. The `styles/` directory is a working structural example meant to be copied and adapted into real projects.

## Branches

- `main` — the Sass reference architecture (this branch)
- `gh-pages` — the Jekyll website published at [sass-forever.com](https://sass-forever.com), with its own `_sass/` structure, `_layouts/`, and `index.html`

Work on the architecture stays on `main`. Work on the documentation website goes on `gh-pages`.

## Architecture

All styles live under `styles/`, compiled from a single entry point `styles/styles.sass`. Each layer has a dedicated folder with a `_index.sass` that uses `@forward` to expose its files:

| Layer | Responsibility |
|---|---|
| `utilities/` | Design tokens (variables) and responsive mixins — generates no CSS |
| `base/` | Browser reset and font loading |
| `layout/` | App shell and global element styling (body, headings, etc.) |
| `components/` | Reusable, context-free UI blocks |
| `pages/` | Page-specific styles scoped to body classes |
| `helpers/` | Global utility classes with `!important` |

The entry point uses `@use` with inline comments, never `@import`:

```sass
@use 'base'        // Reset + font loading
@use 'layout'      // App shell + global element styling
@use 'components'  // Reusable UI blocks
@use 'pages'       // Page-specific context
@use 'helpers'     // Global helper classes
```

## Module System

**Utilities are not loaded globally.** Import them only in files that need variables or mixins:

```sass
@use '../utilities' as *

.card
  padding: 16px

  +tablet
    padding: 24px
```

The `as *` namespace gives direct access to all variables (`$primary`, `$font-body`, breakpoints) and mixins (`+tablet`, `+desktop`, `+dark`) without a namespace prefix.

`_index.sass` files use `@forward` (not `@use`) to expose internal partials to consumers outside the folder.

## Conventions

**Syntax:** All files use indented Sass syntax (`.sass` extension — no braces or semicolons), not SCSS.

**Page scoping:** Page styles are scoped via body classes, not separate stylesheets. Nested pages add a second body class:

```sass
// pages/_home.sass
body.home
  // top-level home styles

// pages/home/_settings.sass
body.home
  &.home-settings
    // settings subpage styles
```

**Responsive mixins:** Mobile-first. Breakpoints defined in `utilities/_mixins.sass`:
- `+tablet` → 768px
- `+desktop` → 1024px
- `+widescreen` → 1216px
- `+fullhd` → 1408px
- `+dark` → applies when `html.dark` class is present

**Helper classes:** Spacing helpers (`_spacing.sass`) are generated with `@each` loops (`.m-1`–`.m-6`, `.p-1`–`.p-6`, directional and axis variants). Flex and grid helpers are hand-coded for readability. All helpers use `!important`.

**Multiple modules:** For projects with distinct sections (e.g. `website` + `admin`), duplicate the full folder structure under each module directory with its own `styles.sass` entry point.
