[![npm version](https://img.shields.io/npm/v/fscss.svg?style=flat-square)](https://www.npmjs.com/package/fscss)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Minified Size](https://img.shields.io/bundlephobia/min/fscss?style=flat-square)](https://bundlephobia.com/package/fscss)

## FSCSS (Figured Shorthand CSS)

FSCSS is a shorthand CSS preprocessor that reduces boilerplate and adds powerful new syntax for rapid styling.
Think of it as CSS with superpowers — arrays, functions, variables, randomness, shorthand repetition, and more.


---

### Example
```css
/* CSS */
.box, .card {
  animation: trans 3s ease-in infinite;
} 

@keyframes trans {
  from {
    width: 0;
    height: 0;
    background: red;
  } 
  to {
    width: 200px;
    height: 200px;
    background: blue;
  } 
}
```
```css
/* FSCSS */
$(@keyframes trans, .box, .card &[3s ease-in infinite]) {
  from {
    %2(width, height [: 0;]) 
    background: red;
  } 
  to {
    %2(width, height [: 200px;])
    background: blue;
  }
}
```
**Quick try**

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.13/exec.min.js" defer>
</script>

<style>
div{
  margin: 10px;
}
$(@keyframes trans, .box, .card &[3s ease-in infinite alternate]){
  from {
    %2(width, height [: 0;]) 
    background: red;
  } 
  to {
    %2(width, height [: 200px;])
    background: blue;
  }
}
</style>

<div class="box">
</div>

<div class="card">
</div>
```

---

## Core Features

- Variables ($var, str()) → define reusable values

- Style Replacement (%n()) → shorthand repeated properties
- Repeat Function (rpt()) → repeat values quickly

- Copy Function (copy()) → copy parts of values

- String Extractor (@ext()) → extract substrings from values

- Drops / Shared Properties → reuse style groups

- Attribute Selectors → dynamic selectors

- Keyframes ($(@keyframes …)) → generate animations easily

- Vendor Prefixing (-*) → auto add prefixes

- Function-based (@fun) → reusable function-like blocks

- Array Methods (@arr) → define & loop arrays

- Random Function (@random()) → random values at runtime

- Number Calculation (num()) → evaluate math expressions

- Import (@import) → include external FSCSS files

- @event → event-based styling logic

- exec() → debugging and runtime helpers

### Installation

**NPM**
```bash
npm install fscss
```
**CDN**
```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.11/exec.min.js" defer></script>
```
Usage

Link FSCSS files directly:
```html
<link type="text/fscss" href="style.fscss">
```
Or import inside a style block:
```html
<style>
@import(exec(style.fscss))
</style>
```
**Async is required for script loading.**


---

### Live Demo

- CodePen Example https://codepen.io/David-Hux/pen/Kwdbyga


---

### Why FSCSS?

- FSCSS takes a shorthand approach:

- Less boilerplate → shorter files

- Array + function logic → more expressive

- Built-in randomness & numeric ops → great for dynamic UIs

- Vendor prefixing → no need for autoprefixer

- Designed for dynamic content, 3D animations, and complex prototypes



---

## Feedback Wanted

FSCSS is experimental — I’d love to hear from developers:

Does this shorthand-first style improve readability?

Would you try this for prototyping or animation-heavy projects?

What features would make it production-ready?

---


## Documentation

For complete documentation with examples, visit the [FSCSS Documentation](https://fscss.devtem.org/).

Documentation includes:
- Full syntax reference
- Interactive examples
- Feature deep dives
- Performance best practices
- Troubleshooting guide

## API Reference

### Compiler Options
When using the JavaScript API:
```js
import { exec } from "https://cdn.jsdelivr.net/npm/fscss@1.1.6/e/xfscss.min.js";

new exec({
  type: "URL",      // Source type (URL, TEXT)
  content: "styles.fscss", // Source content
  onSuccess: "success massage",   
  onError: "error message" 
});
```



## License

FSCSS is MIT licensed. See [LICENSE](https://github.com/figsh/xfscss/blob/main/LICENSE) for details.

---

Figsh—**FSCSS**.
Authored and maintained with ❤️ by developers for developers.
