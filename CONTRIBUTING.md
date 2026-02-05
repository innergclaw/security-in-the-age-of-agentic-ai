# Contributing to Security in the Age of Agentic AI

> Thank you for helping make agentic AI safer for everyone.

---

## 🎯 Why Contribute?

Security in agentic AI is a **collective problem**. When one deployment is compromised:
- Attack patterns become known to adversaries
- Trust in the ecosystem erodes
- Other deployments face similar risks

Your contribution — whether it's a configuration, a threat report, or a documentation fix — helps raise the bar for everyone.

---

## 🤝 How to Contribute

### 1. Share Configurations

**Sanitized security profiles, anonymized:**
```yaml
# Example contribution: Production hardened config
profile: production-hardened
contributor: @your-handle (optional)
tested_on: OpenClaw v1.x
notes: Used in production for 6 months, zero incidents
```

Submit via: Pull request to `configs/` directory

### 2. Report Threats

**Responsible disclosure process:**

1. **For active vulnerabilities:**
   - Email: security@innergintel.ai (placeholder)
   - Do NOT open public issues
   - Allow 30 days for remediation

2. **For general threat intelligence:**
   - Open a GitHub Discussion
   - Tag with `threat-intel`
   - Include: attack vector, impact, mitigation

### 3. Improve Documentation

**Spotted an error or unclear section?**
- Open an issue with label `documentation`
- Or submit a PR directly

**Want to translate?**
- We welcome translations
- Maintain in `translations/<lang>/` directory
- Follow original structure

### 4. Add Tools/Scripts

**Security automation contributions:**
- Place in `tools/` directory
- Include README with usage
- Add to main documentation index

### 5. Case Studies

**Real-world security stories (anonymized):**
- What went wrong
- How it was detected
- Lessons learned
- Submit as PR to `case-studies/`

---

## 📝 Contribution Guidelines

### Pull Request Process

1. **Fork** the repository
2. **Create a branch**: `git checkout -b feature/your-feature`
3. **Make your changes** with clear commit messages
4. **Test** your changes (if applicable)
5. **Submit PR** with detailed description

### Commit Message Format

```
type(scope): brief description

Longer explanation if needed

- bullet points for details
- reference issues with #123

Signed-off-by: Your Name <email@example.com>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation only
- `config`: Security configuration
- `tool`: Automation/script
- `case`: Case study

### Code/Config Standards

**YAML configs:**
- 2-space indentation
- Comments explaining non-obvious choices
- Tested before submission

**Scripts:**
- Include shebang (`#!/bin/bash` or `#!/usr/bin/env python3`)
- Add usage comments
- Handle errors gracefully
- No hardcoded credentials (use environment variables)

**Documentation:**
- Clear, concise language
- Examples where helpful
- Update table of contents if structure changes

---

## 🏷️ Issue Labels

| Label | Use For |
|-------|---------|
| `bug` | Errors in existing content |
| `docs` | Documentation improvements |
| `enhancement` | New features or sections |
| `config` | Security configuration contributions |
| `threat-intel` | Threat intelligence reports |
| `case-study` | Real-world security stories |
| `translation` | Non-English contributions |
| `good-first-issue` | Beginner-friendly tasks |

---

## 🛡️ Security Notes

### For Contributors

- **Never commit credentials** — Even "test" keys get scraped
- **Sanitize logs** — Before including in case studies
- **Anonymize** — Remove identifying details from real incidents
- **Verify** — Test configurations before submitting

### For Maintainers

- **Review carefully** — Malicious contributions could harm users
- **Verify attribution** — Ensure contributors are who they claim
- **Stay current** — Security advice ages quickly

---

## 🌟 Recognition

Contributors will be:
- Listed in [`README.md`](../README.md#acknowledgments)
- Mentioned in release notes
- (Optional) Listed by handle in commit history

**Hall of Fame** (significant contributions):
- Security framework co-authors
- Major tooling contributions
- Sustained maintenance efforts

---

## 📋 Checklist for PRs

Before submitting:

- [ ] I have read and agree to the license terms (CC BY-SA 4.0)
- [ ] My contribution is my own work or properly attributed
- [ ] No credentials or sensitive data included
- [ ] Documentation is clear and accurate
- [ ] (If code) Tested and working
- [ ] Commit messages are descriptive
- [ ] PR description explains the change

---

## 💬 Questions?

- **General:** Open a GitHub Discussion
- **Security sensitive:** Email security@innergintel.ai
- **Direct:** Reach out to @InnerGClaw

---

## 📄 License

By contributing, you agree that your contributions will be licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](../LICENSE).

---

> **"Share configurations, not just successes."**

Thank you for making the agentic AI ecosystem safer.

*— The InnerGClaw Team*
