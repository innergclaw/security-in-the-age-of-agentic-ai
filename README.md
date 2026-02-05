# Security in the Age of Agentic AI

> A Community Framework for OpenClaw Deployments

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![Status: Community Draft](https://img.shields.io/badge/Status-Community%20Draft-yellow.svg)]()

---

## Overview

As AI agents gain access to real systems — files, browsers, APIs, and communication channels — the security model shifts from "trust the user" to "verify every action."

This repository contains a practical, tiered security framework for OpenClaw deployments that balances operational capability with risk mitigation.

**Thesis:** *Security is not a feature you add later. It's the foundation you build on.*

---

## 📚 Contents

| File | Description |
|------|-------------|
| [`SAFETY_WHITEPAPER.md`](SAFETY_WHITEPAPER.md) | Complete framework with threat model, six-tier architecture, and recommendations |
| [`SECURITY.md`](SECURITY.md) | Quick-start security guide and operational checklist |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to contribute to this framework |
| [`LICENSE`](LICENSE) | CC BY-SA 4.0 — Share freely, improve collectively |

---

## 🎯 Quick Start

**For New Deployments:**
1. Read [`SECURITY.md`](SECURITY.md) first
2. Implement the [Security Checklist](SECURITY.md#security-checklist)
3. Review [`SAFETY_WHITEPAPER.md`](SAFETY_WHITEPAPER.md) for deep understanding

**For Existing Deployments:**
1. Run the [Security Check](SECURITY.md#operational-security)
2. Compare your setup against the [Six-Tier Framework](SAFETY_WHITEPAPER.md#3-the-six-tier-security-framework)
3. Identify gaps and prioritize fixes

---

## 🛡️ The Six-Tier Framework

| Tier | Focus | Key Principle |
|------|-------|---------------|
| 1 | Permission Model | Default deny, explicit allow |
| 2 | Credential Hygiene | Least privilege, short-lived tokens |
| 3 | Network Isolation | Contain lateral movement |
| 4 | Audit & Transparency | Log everything, review weekly |
| 5 | Runtime Safeguards | Human confirmation for risk |
| 6 | Incident Response | Assume breach, plan recovery |

---

## 🤝 Community Defense

Security in agentic AI is a collective problem. When one deployment is compromised:
- Attack patterns become known to adversaries
- Trust in the ecosystem erodes
- Other deployments face similar risks

**Our approach:** *Share configurations, not just successes.*

See [`CONTRIBUTING.md`](CONTRIBUTING.md) to join the effort.

---

## 📖 Key Principles

> **"Paranoia is a feature, not a bug."**

- **Start strict, open gradually** — Don't learn security after a breach
- **The 5-minute rule** — If you wouldn't leave a key in a public repo for 5 minutes, don't give it to your agent
- **Defense in depth** — No single layer is sufficient
- **Collective security** — We rise or fall together

---

## 🙏 Acknowledgments

- **InnerGClaw** — Framework architect, initial draft
- **OpenClaw Community** — Feedback, testing, contributions
- **Security researchers** — Who responsibly disclosed vulnerabilities

---

## 📄 License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](LICENSE).

**You are free to:**
- **Share** — Copy and redistribute
- **Adapt** — Remix and build upon

**Under these terms:**
- **Attribution** — Give appropriate credit
- **ShareAlike** — Distribute contributions under same license

---

*"In an age of agentic AI, healthy skepticism is the foundation of trust."*
