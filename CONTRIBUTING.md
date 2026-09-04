# Contributing to FSCSS

Thank you for your interest in contributing to **FSCSS** (Figured Shorthand Cascading Style Sheet).

| Role | Repository | Purpose |
|------|------------|---------|
| **Core engine** | [Figsh/xfscss](https://github.com/Figsh/xfscss) | Compiler, runtime, CLI, language features |
| **Libraries / registry** | [fscss-ttr/FSCSS](https://github.com/fscss-ttr/FSCSS) | Plugin discovery (`libs.json`), docs site assets, named-import integration |
| **Individual modules** | Various under [fscss-ttr](https://github.com/fscss-ttr) and community | Standalone `.fscss` packages |

**Support the project:** [github.com/sponsors/Figsh](https://github.com/sponsors/Figsh) · [opencollective.com/fscss](https://opencollective.com/fscss)

---

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Where to Contribute](#where-to-contribute)
- [Reporting Issues](#reporting-issues)
- [Suggesting Features](#suggesting-features)
- [Submitting Pull Requests](#submitting-pull-requests)
- [Development Setup](#development-setup)
- [Contributing Libraries / Plugins](#contributing-libraries--plugins)
- [Coding Guidelines](#coding-guidelines)
- [Documentation Contributions](#documentation-contributions)
- [FSCSS Philosophy](#fscss-philosophy)
- [Review Process](#review-process)

---

## Code of Conduct

By participating you agree to:

- Be respectful and constructive
- Avoid toxic or harmful behavior
- Give helpful, actionable feedback
- Support new contributors

We aim for a friendly, professional community.

---

## Where to Contribute

### Core (`Figsh/xfscss`)

- Bug fixes in the compiler or runtime
- Performance improvements
- New or refined language features
- CLI enhancements
- Examples, tests, and core documentation

> Modules and plugins do **not** belong here. Use the ecosystem process below.

### Libraries registry & docs (`fscss-ttr/FSCSS`)

- Adding a library to the public registry (`assets/scripts/libs.json`)
- Improving the Libraries / Modules / Submit Guide pages
- Documentation and examples for the ecosystem
- Integrating a library into the named-import path (`xf/styles/`) when requested by maintainers

### Individual library repositories

- Bug fixes, features, and docs for a specific module (e.g. `st-core.fscss`, `circle-progress.fscss`)

---

## Reporting Issues

Before opening an issue:

1. Search existing issues and discussions.
2. Use a clear, descriptive title.
3. Include:

   - FSCSS version (e.g. `1.1.25`)
   - Environment (Browser / Node / CLI)
   - Plugin name + version (if applicable)
   - Minimal steps to reproduce
   - Expected vs actual behavior
   - Relevant code snippets or a minimal `.fscss` file

Security issues must **not** be reported publicly. See [SECURITY.md](./SECURITY.md).

---

## Suggesting Features

- Explain the problem the feature solves
- Provide concrete usage examples
- Show how it fits the FSCSS philosophy (shorthand, lightweight, modular)
- Note whether it is runtime-only, CLI-compatible, or both
- For plugins: indicate whether it belongs in an existing library or needs a new one

---

## Submitting Pull Requests

1. Fork the target repository.
2. Create a focused branch:

   ```bash
   git checkout -b feature/short-description
   # or
   git checkout -b fix/issue-number-short-description
   ```

3. Make your changes.
4. Test thoroughly (runtime + CLI when relevant).
5. Commit with a clear message (conventional style preferred):

   ```bash
   git commit -m "feat: add pattern matching threshold option"
   git commit -m "fix: correct array shuffle edge case"
   git commit -m "docs: improve library submission steps"
   ```

6. Push and open a Pull Request against the default branch (`main`).

**PR expectations**

- Keep the change focused — one concern per PR
- Do not mix unrelated fixes
- Update documentation when behavior or public APIs change
- Prefer backward compatibility; document breaking changes clearly
- Reference related issues

Maintainers review all PRs before merge. Please allow reasonable time for feedback.

---

## Development Setup

### Runtime (browser)

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@latest/runtime.min.js" defer></script>
<!-- or the exec entry point used by many plugins -->
<script src="https://cdn.jsdelivr.net/npm/fscss@latest/exec.min.js" defer></script>
```

### CLI

```bash
npm install -g fscss
fscss input.fscss output.css
```

### Local core development

```bash
git clone https://github.com/Figsh/xfscss.git
cd xfscss
npm install
# follow any scripts in package.json for tests / build
```

---

## Contributing Libraries / Plugins

This is the recommended path for sharing a new `.fscss` module with the community.

### Requirements before submitting

- Public GitHub repository
- File extension `.fscss`
- A root `package.json` is **strongly recommended**. It should include at least:

  | Field | Required | Notes |
  |-------|----------|-------|
  | `name` | ✓ | Short identifier (no `.fscss` suffix) |
  | `version` | ✓ | Semantic version |
  | `description` | ✓ | One-line summary shown on the libraries page |
  | `extension` | ✓ | Must be `"fscss"` |
  | `fscss_version` | ✓ | Minimum compiler version (semver range) |
  | `blocked_methods` | ✓ | Array of disabled built-ins; use `[]` if none |
  | `repository` | ✓ | GitHub URL |
  | `file.usage.directive` | ✓ | Mixin prefix pattern (e.g. `st-*`) |
  | `file.usage.helpers` | ✓ | Explicit list of public mixins/helpers |
  | `file.modules` | ✓ | Relative paths to all `.fscss` source files |
  | `file.remote` | ✓ | Single entry-point file for remote `@import` |
  | `author` | recommended | Shown on discovery cards |
  | `license` | recommended | MIT strongly preferred |
  | `keywords` | recommended | Improves search on the libraries page |
  | `bugs` | recommended | Issues URL |

- Entry file (`index.fscss` or `your-lib-name.fscss`) must be self-contained or import all internal modules. The `file.remote` field must point to this file.
- `README.md` with at least one clear usage example.

### Step 1 — List in the registry (discovery)

1. Open the registry editor:  
   https://github.com/fscss-ttr/FSCSS/edit/main/assets/scripts/libs.json
2. Append your repository URL to the `"remotes"` array (add a comma after the previous entry; **no trailing comma** after the last item).
3. Propose the change and open a Pull Request.

This makes the library visible at https://fscss.devtem.org/libraries. Users can still import via full raw URL.

### Step 2 — Named import support (optional, maintainer-driven)

To enable short imports such as:

```fscss
@import((*) from your-lib)
```

the entry file must be added under the core folder `xf/styles/`. This step is performed by maintainers after review; open a discussion or issue if you would like named-import support.

Full walkthrough: https://fscss.devtem.org/submit-guide  
Package schema details: https://fscss.devtem.org/modules-guide

### Quick checklist

- [ ] `package.json` contains all required fields
- [ ] `file.remote` points to a publicly reachable `.fscss` entry file
- [ ] Entry file is self-contained or correctly imports internals
- [ ] `file.usage.helpers` lists every public mixin/directive
- [ ] Repository is public
- [ ] `README.md` explains usage with ≥ 1 example
- [ ] PR opened against `fscss-ttr/FSCSS` adding the URL to `libs.json`

---

## Coding Guidelines

**Core**

- Keep the engine lightweight
- Prefer features that serve both runtime and CLI
- Maintain the shorthand-first philosophy
- Add comments for non-obvious logic
- Avoid breaking changes without clear migration notes

**Plugins / libraries**

- Do one thing well
- No unsafe `eval` or unexpected side effects
- Consistent macro prefix (e.g. `@st-`, `@circle-`, `@flex-`)
- Sensible defaults / fallbacks for all public variables
- Test in both browser runtime and CLI compilation
- Keep the compiled output small

---

## Documentation Contributions

Documentation is as important as code. Help by:

- Clarifying wording or fixing typos
- Adding practical examples
- Improving the Modules Guide, Submit Guide, or library READMEs
- Writing short tutorials

Standards: clear, concise, beginner-friendly, and consistent with existing FSCSS terminology.

---

## FSCSS Philosophy

- **Shorthand-first** — write less, express more
- **Modular** — use only what you need
- **Runtime + build-time** — flexible deployment
- **Minimal overhead** — stay lightweight
- **Developer productivity** — make styling enjoyable

Contributions that align with these principles are most likely to be accepted.

---

## Review Process

- All pull requests are reviewed by maintainers before merge.
- Feedback may request changes; please respond or update the PR.
- Library registry additions are checked for a valid public repo and (when present) a sensible `package.json`.
- Security-related changes receive extra scrutiny; see [SECURITY.md](./SECURITY.md).
- Maintainers may decline contributions that conflict with project scope or philosophy; a brief explanation will be provided.

---

Thank you for helping FSCSS grow.

Questions? Open a [discussion](https://github.com/fscss-ttr/FSCSS/discussions) or an issue in the appropriate repository.
