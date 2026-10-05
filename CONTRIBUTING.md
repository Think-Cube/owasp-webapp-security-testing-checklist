# Contributing to OWASP WebApp Security Testing Checklist

Thank you for helping keep this checklist accurate and up to date!

## How to Contribute

### Reporting Issues

Use GitHub Issues to:
- Report a checklist item that is outdated or incorrect
- Suggest a new test case or category
- Report broken links

### Proposing Changes

1. Fork this repository
2. Create a feature branch: `git checkout -b add/section-name` or `fix/item-description`
3. Make your changes
4. Submit a Pull Request using the provided template

### Guidelines

- Align new items with [OWASP WSTG](https://owasp.org/www-project-web-security-testing-guide/), [OWASP API Security Top 10 (2023)](https://owasp.org/API-Security/), or [OWASP Top 10 for LLMs](https://genai.owasp.org/) where applicable
- Reference the WSTG test ID (e.g., `WSTG-AUTHN-01`) or OWASP category when adding new items
- Keep item descriptions concise and action-oriented — start with a verb (Test, Verify, Check, Confirm)
- Use an appropriate emoji at the start of each new checklist item to maintain visual consistency
- Do not include tool-specific commands or output — this is a checklist, not a tutorial

### What Makes a Good Checklist Item

- Testable — can be confirmed pass/fail during a security review
- Vendor-neutral — describes what to test, not how to use a specific tool
- Scoped — covers one specific risk or attack vector

## Code of Conduct

Please read and follow our [Code of Conduct](CODE_OF_CONDUCT.md).
