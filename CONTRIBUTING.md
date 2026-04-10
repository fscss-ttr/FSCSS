# Contributing to FSCSS

Thank you for your interest in contributing to [FSCSS](https://www.npmjs.com/package/fscss) (Figured Shorthand Cascading Style Sheet).

**Core repository:** [https://github.com/Figsh/xfscss](https://github.com/Figsh/xfscss)  
**Plugin ecosystem:** [https://github.com/fscss-ttr](https://github.com/fscss-ttr)  
**Support the project:** [https://opencollective.com/fscss](https://opencollective.com/fscss)

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Reporting Issues](#reporting-issues)
- [Suggesting Features](#suggesting-features)
- [Submitting Pull Requests](#submitting-pull-requests)
- [Development Setup](#-development-setup)
- [Plugin Guidelines](#plugin-guidelines)
- [Coding Guidelines](#coding-guidelines)
- [Documentation Contributions](#documentation-contributions)
- [FSCSS Philosophy](#fscss-philosophy)

---

## Code of Conduct

By participating in this project, you agree to:

- Be respectful and constructive
- Avoid toxic or harmful behavior
- Provide helpful feedback
- Support new contributors

We aim to maintain a friendly and professional community.

---

## How to Contribute

The **fscss-ttr** org is the home of the FSCSS plugin ecosystem. Contributions here include:

- Building new plugins
- Fixing bugs in existing plugins
- Improving plugin performance
- Adding or refining plugin-specific features
- Writing examples, demos, and tutorials
- Enhancing documentation

> Looking to contribute to the **core FSCSS engine**? Head over to [Figsh/xfscss](https://github.com/Figsh/xfscss) instead.

---

## Reporting Issues

Before creating an issue:

1. **Check** if it already exists.
2. **Use** a clear and descriptive title.
3. **Provide:**
   - FSCSS version
   - Plugin name and version
   - Environment (Browser / Node / CLI)
   - Steps to reproduce
   - Expected behavior
   - Actual behavior
   - Code snippets if applicable

---

## Suggesting Features

When suggesting a feature:

- Explain the problem it solves
- Provide example usage
- Describe how it fits into FSCSS philosophy
- Mention if it's runtime-only, CLI-compatible, or both
- Note whether it belongs in an existing plugin or warrants a new one

---

## Submitting Pull Requests

1. **Fork** the repository
2. **Create** a new branch
```bash
git checkout -b feature/your-feature-name
```
3. Make your changes
4. Test thoroughly
5. Commit clearly
```bash
git commit -m "feat: add new chart utility"
```
6. Push your branch
```bash
git push origin feature/your-feature-name
```
7. Open a Pull Request

**PR Guidelines**

- Keep changes focused and modular
- Do not mix unrelated fixes
- Write clear commit messages
- Update documentation when needed
- Ensure backward compatibility when possible

---

## Development Setup

**Runtime Testing (CDN)**

Include the FSCSS runtime in your HTML:

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@latest/exec.min.js" defer></script>
```

Then load your plugin stylesheet as you would any `.fscss` file.

**CLI Development**

Install globally:

```bash
npm install -g fscss
```

Compile FSCSS to standard CSS:

```bash
fscss input.fscss output.css
```

---

## Plugin Guidelines

All plugins in the `fscss-ttr` ecosystem should follow these conventions:

- **Lightweight** — Do one thing well, avoid bloat
- **Safe** — No unsafe eval or side effects
- **Documented** — Include a clear `README.md` with usage examples
- **Prefixed** — Use a consistent macro prefix (e.g. `@st-`, `@icon-`, `@flex-`)
- **Fallback-friendly** — Provide sensible defaults for all variables
- **Compatible** — Test across both runtime (browser) and CLI environments

Browse existing plugins in the [fscss-ttr](https://github.com/fscss-ttr) org for conventions and structure before starting a new one.

---

## Coding Guidelines

- Keep plugins lightweight and focused
- Avoid bloating with unnecessary features
- Maintain the shorthand philosophy
- Follow consistent naming patterns
- Ensure compatibility with both runtime and CLI modes
- Write clean, readable code
- Add comments for complex logic

---

## Documentation Contributions

Documentation is as important as code. You can help by:

- Fixing grammar or clarity issues
- Adding usage examples
- Writing tutorials or demo guides
- Improving plugin READMEs

**Documentation Standards**

All documentation should be:

- **Clear** — Easy to understand
- **Concise** — No unnecessary fluff
- **Beginner-friendly** — Accessible to new users
- **Consistent** — Follows FSCSS style and terminology

---

## FSCSS Philosophy

- **Shorthand-first styling** — Write less, do more
- **Modular architecture** — Use what you need
- **Runtime + build-time support** — Flexible deployment options
- **Minimal overhead** — Lightweight and fast
- **Developer productivity focused** — Make styling enjoyable

If your contribution aligns with this philosophy, you're on the right track.

---

❤️ Thank You

Your contributions help FSCSS grow into a powerful modular styling ecosystem.

Let's build something great together.

