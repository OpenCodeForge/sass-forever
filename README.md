# Sass Forever 🤘

**Sass Forever** is not a CSS framework.  
It’s a **simple, pragmatic way** to organize your styles so they stay readable, scalable, and sane over time.

It focuses on:
- 🧠 a **shared mental model** for teams
- 🗂 a **clear separation of responsibilities**
- 🔧 Sass used as a **compiler**, not a framework
- 📦 compatibility with any stack (Rails, Laravel, JS frameworks, or none)

No magic. No heavy abstractions.  
Just structure and clarity.

---

## 📁 File & Folder Architecture

```text
styles/
  utilities/
    _index.sass        # Public Sass API (forwards)
    _variables.sass    # Design tokens, constants
    _mixins.sass       # Responsive helpers, abstractions

  helpers/
    _index.sass        # Helpers entry point
    _spacing.sass      # Margin, padding helpers
    _visibility.sass   # Visibility, display helpers

  layouts/
    _index.sass        # Layouts public API
    _container.sass    # Page container
    _grid.sass         # Grid layouts

  base/
    _fonts.sass        # Local & external fonts
    _reset.sass        # CSS reset / normalization
    _typography.sass   # Global text styles

  components/
    _button.sass       # Buttons
    _card.sass         # Cards
    _modal.sass        # Modals

  pages/
    _home.sass         # Home page styles
    _about.sass        # About page styles

  application.sass    # Single compilation entry point
```

This structure is intentionally explicit:
- folders describe **responsibilities**
- file names describe **intent**
- nothing is implicit or magical

---

## 🏁 application.sass

There is **one and only one** file that gets compiled.

```sass
@use 'base/fonts'
@use 'base/reset'
@use 'base/typography'

@use 'layouts'
@use 'helpers'

@use 'components/button'
@use 'components/card'

@use 'pages/home'
@use 'pages/about'
```

Everything else is imported explicitly.  
This keeps the CSS output predictable and easy to reason about.

---

## 🧩 Example usage

### Using variables and mixins

```sass
@use '../utilities' as *

.title
  color: $primary-color
  font-size: 1.2rem

  +tablet
    font-size: 1.5rem
```

### Responsive mixins (mobile-first)

```sass
@use '../utilities' as *

.card
  padding: 16px

  +tablet
    padding: 24px

  +desktop
    padding: 32px
```

Mixins centralize breakpoints and keep responsive rules consistent across the project.

---

### Using helpers in HTML

```html
<div class="container my-2">
  <p class="hidden">This text is visually hidden</p>
</div>
```

Helpers are global, simple, and designed to be obvious at a glance.

---

## 🧠 How to read this structure

- 🛠 **utilities/** → Sass logic only, no CSS output  
- 🧩 **helpers/** → small, global utility classes  
- 🧱 **layouts/** → structural building blocks (space & flow)  
- 🎨 **base/** → global foundations (fonts, reset, typography)  
- 🧩 **components/** → visual UI elements  
- 📄 **pages/** → page-specific context  

Each layer has a clear role.  
Each file does one thing.

---

## 🏁 Final Words

There are many ways to write CSS.

**Sass Forever** is one that stays:
- readable
- maintainable
- adaptable over time

Just a way. 🤘
