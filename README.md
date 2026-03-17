# Sass Forever 🤘

**Sass Forever** is not a CSS framework.  
It's a simple, opinionated structure to organize your Sass projects so they stay readable and scalable over time.

No installation.  
No magic.  
Just structure.

---

## 📁 Architecture

Follow this structure and adapt it to your own projects.

```
styles/
  utilities/
    _variables.sass   # Colors, font families, breakpoints…
    _mixins.sass      # Mixins & responsive helpers (+tablet, +desktop…)

  base/
    _fonts.sass       # Font loading (@font-face, Google Fonts…)
    _reset.sass       # Generic reset (kept neutral)

  layout/
    _global.sass      # Global elements (body, h1, p…) + app shell
    _header.sass
    _footer.sass

  components/         # Reusable UI blocks
    _container.sass   # Max-width + horizontal padding wrapper
    _button.sass
    _card.sass
    _modal.sass

  pages/              # Page-specific context
    _home.sass
    _about.sass

  helpers/
    _spacing.sass     # Spacing helpers (margin, padding, gap…)
    _visibility.sass  # Visibility helpers (.hidden, .block…)
    _flex.sass        # Flex helpers (.flex, .items-center…)
    _grid.sass        # CSS Grid helpers (.grid, .grid-cols-2…)

  styles.sass         # Single compilation entry point
```

Each folder has one responsibility.  
Each file does one thing.

Every folder should contain a private `_index.sass` file that forwards its internal files,  
so the main entry point stays minimal and explicit.

---

## 🏁 Entry Point

Only one file is compiled:

```sass
// styles.sass

@use 'base'        // Reset + font loading
@use 'layout'      // App shell + global element styling
@use 'components'  // Reusable UI blocks
@use 'pages'       // Page-specific context
@use 'helpers'     // Global helper classes
```

All global element styling (body, h1, p, etc.) lives in `layout/_app.sass`.

---

## 🛠 Using Utilities (Variables & Mixins)

Utilities are not loaded globally in the entry point.  
They are imported only where needed.

```sass
@use '../utilities' as *

.card
  padding: 16px

  +tablet
    padding: 24px
```

Utilities provide design tokens and mixins,  
but do not generate CSS on their own.

---

## 📄 Page Naming Convention

Page styles should be scoped using body classes.

```sass
// pages/_dashboard.sass
body.dashboard
  ...
```

For nested pages:

```sass
// pages/dashboard/_settings.sass
body.dashboard
  &.dashboard-settings
    ...
```

The page defines the context.  
Components remain reusable.

---

## 🧩 Multiple Modules

If your project has multiple modules (for example `website` and `admin`),  
duplicate the structure inside each module:

```
styles/
  website/
    ...
    styles.sass   # Entry point
  admin/
    ...
    styles.sass   # Entry point
```

Each module owns its styles and its compilation entry point.

---

## 🧠 Philosophy

- One responsibility per folder
- One responsibility per file
- One compilation entry point
- No implicit magic

**Sass Forever** is not a framework.  
It's just a way. 🤘
