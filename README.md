[![npm version](https://img.shields.io/npm/v/fscss.svg?style=flat-square)](https://www.npmjs.com/package/fscss)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Minified Size](https://img.shields.io/bundlephobia/min/fscss?style=flat-square)](https://bundlephobia.com/package/fscss)

FSCSS (Figured Shorthand CSS) is a lightweight, powerful CSS preprocessor that simplifies your styling workflow with intuitive shorthand syntax. Write cleaner, more maintainable stylesheets with 50% less code!

## Why FSCSS?

- ✨ **Concise syntax** - Write CSS with significantly less code
- ⚡️ **Lightweight** - Only 4KB minified (no dependencies)
- 🔄 **Reusable patterns** - Create style templates with variables and mixins
- 🚀 **Developer-friendly** - Features designed for modern workflows
- 💡 **Easy to learn** - Shorthand syntax that makes sense

## Installation

### Via npm
```bash
npm install fscss
```

### Via CDN
```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.6/e/exec.min.js"></script>
```

## Quick Start

### 1. Create an FSCSS file
```css
/* style.fscss */
$primary: #4361ee;
$secondary: #3a0ca3;

str(buttonStyle, "
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  font-weight: 600;
  transition: all 0.3s ease;
")

.button {
  buttonStyle
  background: $primary!;
  color: white;

  &:hover {
    background: $secondary!;
    transform: translateY(-2px);
  }
}
```

### 2. Include in your HTML
```html
<link type="text/fscss" href="style.fscss">
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.6/e/exec.min.js" async></script>
```

### 3. Use in your HTML
```html
<button class="button">Click Me</button>
```

## Core Features

### Variables
Define and reuse values throughout your stylesheets:
```fscss
$primary: #4361ee;
$spacing: 1rem;

.header {
  background: $primary!;
  padding: $spacing!;
}
```

### Style Stores (re(), str())
Create reusable style patterns:
```css
str(cardStyle, "
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  background: white;
")

.card {
  cardStyle
}
```

### Mixins (mx(), mxs())
Apply multiple properties with the same value:
```css
.container {
  mxs(width, height, max-width, min-width, "100%")
}
```

### Value Manipulation
```css
/* Repeat values */
.loading::after {
  content: "rpt(5, '• ')";
}

/* Extract parts of values */

.btn {
  size: 200px copy(6, size)!; /* 200px */
}
div{
width: $size!; /* 200px */
} 
```

### Vendor Prefixing
```css
.element {
  -*-transform: rotate(45deg);
}
```

### Keyframes Shorthand
```css
$(@keyframes slideIn, .slide-element, &[0.5s ease-out]) {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}
```

## Real-World Example

```css
/* Variables */
$primary: #4361ee;
$secondary: #3a0ca3;
$text-light: #f8f9fa;
$shadow: 0 4px 6px rgba(0,0,0,0.1);

/* Reusable styles */
str(navbarStyle, "
  display: flex;
  justify-content: space-between;
  padding: 1rem 2rem;
  background: $primary!;
  color: $text-light!;
  box-shadow: $shadow!;
")

str(navItemHover, "
  background: rgba(255,255,255,0.1);
  transform: translateY(-2px);
")

/* Component styles */
nav {
  navbarStyle
  
  .brand {
    font-size: 1.5rem;
    font-weight: 700;
  }
  
  ul {
    display: flex;
    gap: 1rem;
    list-style: none;
    
    li {
      a {
        padding: 0.5rem 1rem;
        border-radius: 4px;
        transition: all 0.3s ease;
        
        &:hover {
          navItemHover
        }
      }
    }
  }
}

/* Responsive utilities */
str(mobileHidden, "
  @media (max-width: 768px) {
    display: none;
  }
")

.desktop-only {
  mobileHidden
}
```

## Documentation

For complete documentation with examples, visit the [FSCSS Documentation](https://ekustack.github.io/fsdocs).

Documentation includes:
- 📚 Full syntax reference
- 🎮 Interactive examples
- 🧩 Feature deep dives
- 🚀 Performance best practices
- 🛠 Troubleshooting guide

## API Reference

### Compiler Options
When using the JavaScript API:
```js
import { exec } from "fscss";

new exec({
  type: "URL",      // Source type (URL, TEXT)
  content: "styles.fscss", // Source content
  onSuccess: "success massage",   
  onError: "error message" 
});
```

## Contributing

We welcome contributions! Here's how to get started:

1. Fork the repository
2. Install dependencies: `npm install`
3. Make your changes
4. Run tests: `npm test`
5. Submit a pull request

## License

FSCSS is MIT licensed. See [LICENSE](https://github.com/figsh/xfscss/blob/main/LICENSE) for details.

---

**FSCSS** © 2025 Figsh, David Hux, and Ekuyik Sam.  
Authored and maintained with ❤️ by developers for developers.
