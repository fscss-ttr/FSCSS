# FSCSS @define 

*For version 1.1.15+*

> Reusable style definitions for generating CSS blocks and property groups.

---

## Overview

`@define` allows developers to create reusable style definitions in FSCSS. These definitions can represent either property groups or full CSS blocks, enabling modular and maintainable stylesheets.

FSCSS defines operate as direct string generators, injecting final CSS output during compilation.

---

### Key Characteristics

- Reusable – Define once, use anywhere
- Parameter support – Accept inputs with default values
- Direct output – Expands into final CSS during compilation
- Two modes – Property Defines and Block Defines

---

### Define Declaration

```fscss
@define name(param:default) { ... }
```

Example

```fscss
@define center() {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Usage

```fscss
.box {
  @center()
}
```

Output

```css
.box {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

### Parameters

Defines can accept parameters with optional default values.

```fscss
@define card(bg: black, color: white, pad: 20px, bd-r: 10px) {
  background: @use(bg);
  border-radius: @use(bd-r);
  padding: @use(pad);
  color: @use(color);
}
```

Usage

```fscss
.box {
  @card(#007999)
}
```

Output

```css
.box {
  background: #007999;
  border-radius: 10px;
  padding: 20px;
  color: white;
}
```

If a parameter is not provided, the default value (para: default) is used.

---

### Parameter Access

Parameters must be accessed using @use().

```css
@use(parameter)
```

**Example:**

```css
background: @use(bg);
padding: @use(pad);
```

This ensures the compiler correctly resolves parameter values.

**✅ Correct:** background: @use(bg);
**❌ Invalid**: background: bg;

---

### Property Defines

Property Defines generate reusable groups of CSS properties.

```fscss
@define center() {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

**Ideal for:**

- Layout utilities
- Flex/Grid helpers
- Common styling patterns

---

### Block Defines

Block Defines generate full CSS structures such as media queries or nested rules.
They use string blocks (enclosed in quotes).

```fscss
@define screen(size) {
  "
  @media (max-width: @use(size)) {
    .box {
      padding: 10px;
    }
  }
  "
}
```

Usage

```css
@screen(750px)
```

**Useful for:**

- Media queries
- Animation blocks
- Reusable layout wrappers
- Complex CSS generators

---

**Multiple Defines**

Multiple defines can be combined within a single rule.

```fscss
@define center() {
  display: flex;
  justify-content: center;
  align-items: center;
}

@define card(bg) {
  background: @use(bg);
  padding: 20px;
  border-radius: 10px;
}

.box {
  @card(#007999)
  @center()
}
```

Output

```css
.box {
  background: #007999;
  padding: 20px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

### Importing Define Libraries

Defines can be shared through external files.

```css
@import(exec(./your_ui_components.fscss)) /*or plugins*/
```

This enables reusable libraries such as:

- Layout utilities
- Component systems
- Animation presets
- Theme packs

---

### Important Notes

- Parameters must be referenced with @use() inside define bodies.
- Defines expand inline – they inject CSS directly where used, allowing multiple defines to compose styles within a single rule.

---

### Design Philosophy

FSCSS defines are designed to provide reusable styling primitives without introducing full programming complexity.

**They focus on:**

- Reusable CSS patterns
- Readable syntax
- Predictable compilation

Rather than acting as full scripting constructs, defines serve as modular CSS generators.

---

### Practical Examples

Flex Center Utility

```css
@define center() {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @center()
}
```

Card Component

```css
@define card(bg: #111, color: white, pad: 20px) {
  background: @use(bg);
  color: @use(color);
  padding: @use(pad);
  border-radius: 10px;
}

.box {
  @card(#007999)
}
```

Responsive Helper

```fscss
@define mobile(size) {
  "
  @media (max-width: @use(size)) {
    .box {
      padding: 10px;
    }
  }
  "
}

@mobile(768px)
```

---

### Best Practices

- Use Property Defines for reusable utilities
- Use Block Defines for complex CSS structures
- Provide default values for flexible usage
- Keep defines focused and single‑purpose
- Organise large define collections into importable files

---

### Why FSCSS Defines?

Feature Benefit
Reusable styles Reduce repetition
Parameter support Flexible components
Direct expansion Predictable output
Plugin‑friendly Share define libraries

---

### Summary

FSCSS defines provide a lightweight mechanism for creating reusable styling patterns.
They enable developers to build modular CSS systems while maintaining simple and readable syntax.

**Use them to:**

- Create layout utilities
- Build reusable UI components
- Generate responsive helpers
- Organise style systems

> FSCSS Defines: Modular styling through reusable definitions.

---

Additional Note: **@use()**

`@use()` is the dedicated function to access parameter values inside a define. It guarantees that the compiler correctly substitutes the provided (or default) value. Always prefix parameter names with `@use()` in the define body.
