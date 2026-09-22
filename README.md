[![npm version](https://img.shields.io/npm/v/fscss.svg?style=flat-square)](https://www.npmjs.com/package/fscss)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)
[![Minified Size](https://img.shields.io/bundlephobia/min/fscss?style=flat-square)](https://bundlephobia.com/package/fscss)

## FSCSS (Figured Shorthand CSS)

FSCSS is a lightweight, modern CSS preprocessor that reduces boilerplate and adds powerful new syntax for rapid styling.
Think of it as CSS with superpowers — arrays, functions, variables, randomness, shorthand repetition, and more.

## FSCSS NPM repository: https://github.com/Figsh/xfscss

![FSCSS repo stats](https://raw.githubusercontent.com/Figsh/xfscss/refs/heads/main/docs/charts/languages.svg) 

---

## FSCSS Modern Remote Module Protocol

The Modern Remote Module Protocol is a core design choice built directly into the FSCSS compiler. Instead of forcing developers to download package archives via node modules just to write a styling prototype, the FSCSS engine resolves imports over the air on-demand.

**Files:** [xf/styles](/xf/styles)

**Repositories:** [/assets/scripts/libs.json](/assets/scripts/libs.json)

---

### Why FSCSS?

- FSCSS takes a shorthand approach:

- Less boilerplate: shorter files

- Array + function logic: more expressive

- Built-in randomness & numeric ops: great for dynamic UIs

- Vendor prefixing: no need for autoprefixer

- Designed for dynamic content, 3D animations, and complex prototypes



---

## Get started 

Start with our templates and remote library's https://fscss.devtem.org/libraries 

**version 1.2.4+ pattern**
<br/>Define:
```css
pattern(0.6: "rounded primary button with color: white, bg: red", `
background: @match(background:?\s([#\w\d-_]+)) @match(bg:?\s([#\w\d-_]+));
color: @match(color:?\s([#\w\d-_]+)) @match(text:?\s([#\w\d-_]+));
border-radius: 25px;
padding: 10px 20px;
border: 2px solid;
font-weight: 700;
`)
```
<br/>Then use:
```css
.primary {
  rounded primary button with color: #0BCEAE, background: midnightblue
}
```
https://fscss.devtem.org/pattern

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

https://fscss.devtem.org/api

## License

FSCSS is MIT licensed.

---

**FSCSS**.
Authored and maintained with ❤️ by developers for developers.
