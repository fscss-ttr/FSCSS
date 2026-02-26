
# FSCSS Plugins

Reusable plugin modules for FSCSS that extend the core engine with additional utilities, UI components, themes, and experimental features.

## Installation

Some plugins are available using the built-in `_init` system.

### Built-in Plugin Usage

```css
@import(exec(_init name))
```

Example:

```css
@import(exec(_init isjs))
```

Available _init Plugins

isjs

Write CSS properties using JavaScript-style syntax.

Example:

```css
.box {
  backgroundColor: red;
  fontSize: 20px;
}
```

Instead of:

```css
background-color: red;
font-size: 20px;
```

themes

Provides theme-based utilities.

Example:

```css
background: @event.theme(forest);
```

events

Event-driven styling helpers.

Example:

```css
tr Shape: @event.shape(star);
```

array1to500 (Deprecated)

Previously used to generate numeric sequences. Now unnecessary since FSCSS includes the count() method.

```css
@arr index[count(500,1)]
```

External Plugins

Some plugins are not part of _init and must be imported directly.

simple_ui

Lightweight UI component pack for building modern layouts quickly.

Import:

```css
@import(exec(https://cdn.jsdelivr.net/gh/fscss-ttr/FSCSS@main/xf/styles/simple-ui.fscss))
```

Usage:
After importing, use the following to list all available components on console:

```css
s-div{
  simple_ui.list
}
```

Works on FSCSS v1.1.13+

Example: Simple Landing Page (CDN Runtime)

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.13/exec.min.js" defer></script>

<style>
@import(exec(https://cdn.jsdelivr.net/gh/fscss-ttr/FSCSS@main/xf/styles/simple-ui.fscss))

  

body{
  margin: 0;
  font-family: sans-serif;
  background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
  color: white;
}

/* ===== Layout ===== */

.hero{
  text-align: center;
  padding: 100px 20px;
}

.features{
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(250px,1fr));
  gap: 20px;
  padding: 60px 40px;
}

/* ===== Hero Title ===== */

.hero_title{
  $bg: linear-gradient(90deg,#0ff,#06f);
  $weight: 700;
  font-size: 48px;
  Text_gradient
}

/* ===== Hero Button ===== */

.hero_btn{
  margin-top: 30px;
  $bg: linear-gradient(45deg,#06f,#0ff);
  $padding: 14px 28px;
  $radius: 30px;
  Button_glass
}
.hero_btn:hover {
  transform: scale(110%);
}

/* ===== Feature Cards ===== */

.card{
  $bg: rgba(255,255,255,.08);
  $border: 1px solid rgba(255,255,255,.15);
  Card_soft
}

.card h3{
  margin-top: 0;
}

</style>

<section class="hero">
  <h1 class="hero_title">Build Faster with FSCSS</h1>
  <p>Modern styling. Plugin system.</p>
  <button class="hero_btn">Get Started</button>
</section>

<section class="features">
  <div class="card">
    <h3>⚡ No Build Step</h3>
    <p>Run directly in the browser using CDN.</p>
  </div>

  <div class="card">
    <h3>🎨 Fallback Operator</h3>
    <p>Use $/variable || fallback for safe styling.</p>
  </div>

  <div class="card">
    <h3>🔌 Plugin Ready</h3>
    <p>Create reusable UI modules easily.</p>
  </div>
</section>

```

Using FSCSS in a Real Project (Processed CSS)

For production environments, compile FSCSS into standard CSS.

1. Install FSCSS CLI

```bash
npm install -g fscss
```

2. Compile

If your source file is style.fscss:

```bash
fscss style.fscss style.css
```

Then include in your HTML:

```html
<link rel="stylesheet" href="style.css">
```

This avoids runtime processing in production.

Creating Reusable Plugins

Create your own plugin modules using str():

```css
str(Button_modern, "
  background: $/bg || #06f;
  color: $/color || #fff;
  padding: $/padding || 12px 20px;
  border-radius: $/radius || 12px;
")
```

Users can then override variables:

```css
.btn {
  $bg: red;
  Button_modern
}
```

Best Practices:

· Always provide fallback values
· Keep plugins modular
· Avoid strict required variables unless necessary
· Design plugins to work safely without configuration

Why FSCSS Plugins?

· No heavy frameworks required
· Runtime or compiled usage options
· Component-based styling approach
· Variable fallback operator support
· Easy CDN distribution
· CLI support for production builds

---

FSCSS Plugins extend the core engine into a modular styling ecosystem.

Built for flexibility. Designed for runtime and build-time usage.

