# Security Policy

## Supported Versions

Security updates are provided for the following releases of the **fscss** npm package (core engine):

| Version | Supported          |
| ------- | ------------------ |
| 1.2.x   | :white_check_mark: |
| 1.1.x   | :white_check_mark: |
| < 1.1   | :x:                |

Only the latest two minor lines receive active security patches. Older versions should upgrade.

Individual community libraries (`.fscss` modules) are maintained by their respective authors. Security concerns specific to a library should be reported to that repository’s maintainers; the core team can assist with coordination when needed.

---

## Reporting a Vulnerability

**Do not** open a public GitHub issue, discussion, or pull request for security vulnerabilities.

Report privately using one of these channels:

1. **GitHub private vulnerability reporting** (preferred for the core repo)  
   → https://github.com/Figsh/xfscss/security/advisories/new

2. **Email**  
   → safetyunion5550@gmail.com

Please include as much of the following as possible:

- Description of the vulnerability and its potential impact
- Affected version(s) of `fscss` (and any related library if applicable)
- Step-by-step reproduction instructions or a minimal proof-of-concept
- Location of the affected code (file, line, commit, or URL) if known
- Any suggested mitigations

### What to expect

- Acknowledgement of the report
- Status updates while the issue is investigated (accepted / needs more information / declined)
- If accepted: a fix will be prioritized and a patched release issued. You will be credited in the release notes unless you request anonymity.
- If declined: a brief explanation will be provided (not a security issue, expected behavior, already known/fixed, etc.)

Please allow a reasonable coordinated-disclosure window before any public discussion so that users have time to update.

---

## Scope

In-scope examples:

- Remote code execution or arbitrary code evaluation through the compiler/runtime
- Injection of malicious CSS/JS that escapes the intended sandbox of the runtime
- Supply-chain issues in published npm packages under the `fscss` name
- Privilege escalation or data leakage caused by the FSCSS tooling itself

Out of scope (report as regular issues when appropriate):

- Bugs that only produce incorrect CSS output with no security impact
- Issues in third-party or community libraries that do not affect the core engine
- Denial-of-service via extremely large or pathological input (unless it indicates a deeper flaw)
- Social-engineering or phishing attacks against project maintainers

---

## Security Best Practices for Contributors & Library Authors

- Never introduce `eval`, dynamic `Function` constructors, or equivalent on untrusted input.
- Prefer pure data transformations; keep side effects explicit and minimal.
- Validate and sanitize any user-controlled values that influence generated CSS or runtime behavior.
- Keep dependencies minimal and regularly audited.
- For libraries submitted to the registry: ensure the entry file and any remote resources are served over HTTPS and do not execute unexpected scripts.

---

## Contact

- Core security reports: safetyunion5550@gmail.com or GitHub private advisory on [Figsh/xfscss](https://github.com/Figsh/xfscss)
- General questions: [GitHub Discussions](https://github.com/fscss-ttr/FSCSS/discussions)

Thank you for helping keep FSCSS and its ecosystem safe.