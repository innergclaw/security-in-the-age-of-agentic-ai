# Security in the Age of Agentic AI
## A Community Framework for OpenClaw Deployments

**Version:** 1.0-draft  
**Date:** February 2026  
**Authors:** InnerGClaw, OpenClaw Community  
**Classification:** Public / Community Contribution

---

## Executive Summary

As AI agents gain access to real systems — files, browsers, APIs, and communication channels — the security model shifts from "trust the user" to "verify every action." This white paper presents a practical, tiered security framework for OpenClaw deployments that balances operational capability with risk mitigation.

The framework addresses:
- **Threat modeling** for agentic AI systems
- **Defense in depth** through six security tiers
- **Operational security** practices for daily use
- **Community standards** for collective defense

Our thesis: *Security is not a feature you add later. It's the foundation you build on.*

---

## 1. The Agentic Security Paradigm

### 1.1 What Changed?

Traditional software operates within defined boundaries. Agentic AI operates *across* boundaries:

| Traditional Software | Agentic AI |
|---------------------|------------|
| Fixed capabilities | Extensible via skills/tools |
| User-initiated actions | Autonomous decision loops |
| Single-context execution | Long-running, stateful sessions |
| Deterministic outputs | Probabilistic reasoning |
| Known attack surface | Expanding via tool access |

This shift requires rethinking security from first principles.

### 1.2 The Unique Risk Profile

AI agents introduce specific risks:

**Tool Misuse:** A compromised or confused agent can invoke powerful tools destructively. Shell access, file deletion, unauthorized messaging — each tool is a potential liability.

**Credential Exposure:** Agents often require API keys and tokens. These credentials exist in the agent's context window, logged to disk, and passed through multiple systems.

**Lateral Movement:** An agent with access to multiple services can pivot between them. A browser tool with access to a logged-in session becomes a gateway.

**Silent Execution:** Unlike human users, agents operate continuously. Malicious actions may happen while you're away, without the behavioral cues that trigger human suspicion.

**Prompt Injection:** External inputs (web content, messages, documents) can hijack agent behavior through carefully crafted prompts.

### 1.3 The Attacker's View

From an adversary's perspective, a compromised AI agent is:
- A persistent presence in your digital environment
- Access to all connected services and credentials
- The ability to act *as you* across platforms
- A trusted entity that bypasses normal suspicion

> **Case Study:** In 2025, researchers demonstrated that an AI coding assistant could be tricked into exfiltrating codebases by embedding malicious instructions in dependency documentation. The agent read the docs, followed the instructions, and emailed source code to an external address — all within normal operational parameters.

---

## 2. Threat Model

### 2.1 Assets to Protect

| Asset | Value | Exposure |
|-------|-------|----------|
| API Keys/Tokens | High | Stored in config, context window |
| Personal Files | High | Agent workspace access |
| Communications | High | Message tool, browser sessions |
| System Integrity | Critical | Exec tool, gateway control |
| Reputation | Critical | Posts sent as you |
| Financial Access | Critical | Browser with logged-in banks |

### 2.2 Threat Actors

| Actor | Motivation | Capability |
|-------|------------|------------|
| Opportunistic | Credential theft, spam | Low |
| Targeted | Data exfiltration, espionage | Medium |
| Supply Chain | Skill/tool poisoning | High |
| State/Advanced | Persistent access, surveillance | High |

### 2.3 Attack Vectors

1. **Skill Supply Chain:** Malicious or compromised skills/tools
2. **Prompt Injection:** Malicious content triggering unintended actions
3. **Credential Leakage:** Keys exposed in logs, context, or output
4. **Session Hijacking:** Interception of agent-gateway communication
5. **Insider Threat:** Legitimate user with excessive permissions
6. **Tool Misconfiguration:** Accidentally granted dangerous capabilities

---

## 3. The Six-Tier Security Framework

Our framework implements defense in depth through six complementary tiers. No single layer is sufficient; security emerges from the interactions between layers.

### Tier 1: Permission Model (Default Deny)

**Principle:** Start with everything blocked. Explicitly enable capabilities with justification.

**Implementation:**
- Tool allowlisting: Only explicitly approved tools function
- Block high-risk tools by default: exec, gateway, message
- Require confirmation for sensitive operations
- Time-bound permissions (session limits)

**Example Configuration:**
```yaml
securityProfile: strict
allowed_tools:
  - read
  - memory_search
  - web_search
blocked_tools:
  - exec
  - browser
  - message
  - gateway
require_confirmation:
  - edit
  - write
```

### Tier 2: Credential Hygiene

**Principle:** Minimize the blast radius of any single compromise.

**Practices:**
- Short-lived tokens (30-90 day rotation)
- Least-privilege scopes (read-only GitHub, limited Gmail)
- Segregated credentials (one key per service)
- Secure storage (OS keychain, not plaintext)
- Monitoring (alerts on unusual usage)

**The 5-Minute Rule:** If you wouldn't leave a key in a public GitHub repo for 5 minutes, don't give it to your agent.

### Tier 3: Network Isolation

**Principle:** Contain the agent to prevent lateral movement.

**Architecture:**

```
┌─────────────────────────────────────┐
│ TIER 1: Host Machine                │
│  Personal files, sensitive data     │
│  NO AGENT ACCESS                    │
├─────────────────────────────────────┤
│ TIER 2: Gateway/Controller          │
│  Localhost binding only             │
│  Firewall protected                 │
├─────────────────────────────────────┤
│ TIER 3: Agent Workspace             │
│  Isolated directory (chroot)        │
│  Ephemeral, wiped on restart        │
├─────────────────────────────────────┤
│ TIER 4: External Services           │
│  Allowlist egress only              │
│  DNS filtering, rate limits         │
└─────────────────────────────────────┘
```

### Tier 4: Audit & Transparency

**Principle:** You can't secure what you can't see.

**Requirements:**
- Log all tool invocations with timestamps
- Hash sensitive parameters (don't log raw tokens)
- 90-day retention minimum
- Append-only logs (tamper resistance)
- Human review triggers for anomalies

**Weekly Ritual:** 5-minute log review. Look for:
- Access outside workspace
- Unexpected external calls
- High-risk tool usage
- Failed authentication attempts

### Tier 5: Runtime Safeguards

**Principle:** Assume the agent will try something dangerous. Build guardrails.

**Pause Points:**
| Action | Required |
|--------|----------|
| Shell execution | Human confirmation |
| Outbound message | Human confirmation |
| File outside workspace | Human confirmation |
| System config change | Human confirmation |
| Credential file access | Human confirmation |

**Timeouts:**
- Maximum session duration: 2 hours
- Kill idle sessions after: 10 minutes
- Tool execution timeout: 30 seconds

### Tier 6: Incident Response

**Principle:** Assume breach. Plan for recovery.

**Compromise Playbook:**

```
1. ISOLATE (minutes 0-5)
   → Kill agent process
   → Revoke all active tokens
   → Disconnect from network

2. ASSESS (minutes 5-30)
   → Review logs (what was accessed?)
   → Check API dashboards (usage anomalies)
   → Verify file integrity

3. CONTAIN (minutes 30-60)
   → Rotate all exposed credentials
   → Audit connected systems
   → Enable enhanced monitoring

4. RECOVER (hours 1-24)
   → Restore from known-good backup
   → Re-deploy with hardened config
   → Document lessons learned

5. SHARE (days 1-7)
   → Report to community (anonymized)
   → Update framework with new learnings
   → Contribute indicators of compromise
```

---

## 4. Operational Security

### 4.1 Daily Practices

**Morning Security Check (2 minutes):**
```bash
~/.openclaw/security-check.sh
```

**Session Hygiene:**
- Start fresh sessions for sensitive work
- Kill idle sessions before walking away
- Review agent actions after each session

**Credential Rotation:**
- Set calendar reminders for 30/60/90 days
- Rotate immediately if any suspicious activity
- Never reuse rotated credentials

### 4.2 Configuration Templates

**Production Deployment (Strict):**
```yaml
profile: strict
allowed_tools: [read, memory_search, web_search]
blocked_tools: [exec, browser, message, gateway, nodes]
confirm_all_external: true
session_max_duration: 3600
auto_kill_idle: 300
audit_retention: 90_days
```

**Development Environment (Moderate):**
```yaml
profile: moderate
allowed_tools: [read, write, edit, memory_*, web_*]
blocked_tools: [exec, gateway]
require_confirmation: [browser, message, nodes]
session_max_duration: 7200
audit_retention: 30_days
```

### 4.3 Skill Security

**Before Installing a Skill:**
- [ ] Review source code
- [ ] Check author reputation
- [ ] Verify no unexpected network calls
- [ ] Test in isolated environment first
- [ ] Review permissions requested

**Skill Sandboxing:**
```yaml
skill_execution:
  network_access: deny_by_default
  allowed_hosts: [api.trusted-source.com]
  filesystem_access: workspace_only
  timeout: 30s
  allow_unsigned: false
```

---

## 5. Community Defense

### 5.1 Collective Security

Security in agentic AI is a collective problem. When one deployment is compromised:
- Attack patterns become known to adversaries
- Trust in the ecosystem erodes
- Other deployments face similar risks

**Our approach:** Share configurations, not just successes.

### 5.2 Contribution Model

**Share:**
- Sanitized security configurations
- Threat intelligence (attack patterns)
- Audit findings (anonymized)
- Framework improvements

**Document:**
- Your threat model
- Security decisions and tradeoffs
- Incident post-mortems
- Lessons learned

**Call Out:**
- Risky tutorials or shortcuts
- Skills with excessive permissions
- Configurations that bypass safeguards

### 5.3 Standards Evolution

This framework is a living document. As threats evolve and the ecosystem matures, we collectively update our standards.

**Version History:**
- v1.0 (Feb 2026): Initial framework, six-tier model

**Proposed v1.1 additions:**
- Automated threat intelligence sharing
- Skill signing and verification
- Formal audit checklists
- Insurance/risk transfer considerations

---

## 6. Recommendations

### For Individual Users

1. **Start with strict mode.** Open access gradually, not the reverse.
2. **Implement the daily security check.** 2 minutes prevents hours of cleanup.
3. **Use the 5-minute rule for credentials.** If it feels wrong, it is.
4. **Review logs weekly.** Patterns reveal compromises.
5. **Have a recovery plan.** Assume you'll need it.

### For Skill Developers

1. **Request minimum permissions.** Don't ask for exec if read suffices.
2. **Document your threat model.** Help users understand risks.
3. **Sign your skills.** Enable verification and trust.
4. **Accept bug reports.** Security issues are feature requests.

### For the Ecosystem

1. **Establish a security mailing list.** Coordinated disclosure for vulnerabilities.
2. **Create a skill registry.** Curated, audited, community-vetted tools.
3. **Fund security audits.** Independent review of core components.
4. **Build incident response capabilities.** Community support during breaches.

---

## 7. Conclusion

The promise of agentic AI — autonomous, capable, persistent assistants — comes with corresponding risks. The systems we build today will define the security boundaries for the decade ahead.

Our choice is not between security and capability. The most capable systems are those we can trust with important work. Security is what enables real deployment.

This framework is a starting point, not a destination. As the ecosystem evolves, so must our defenses. We invite the community to contribute, challenge, and improve these standards.

> **"Paranoia is a feature, not a bug."**

In an age of agentic AI, healthy skepticism is the foundation of trust.

---

## Appendices

### Appendix A: Security Checklist

**Pre-Deployment:**
- [ ] All tools default-deny, explicitly allowlisted
- [ ] Credentials scoped to minimum necessary
- [ ] Network egress filtered and monitored
- [ ] Audit logging enabled and immutable
- [ ] Sensitive actions require confirmation
- [ ] Incident response plan documented
- [ ] Recovery procedures tested
- [ ] Regular security reviews scheduled

**Daily Operation:**
- [ ] Security check script executed
- [ ] Sessions killed when not in use
- [ ] No credentials in logs or output
- [ ] Anomalies reviewed and explained

**Monthly Review:**
- [ ] Credential rotation calendar checked
- [ ] Log retention verified
- [ ] New skills audited
- [ ] Framework updates reviewed

### Appendix B: Glossary

| Term | Definition |
|------|------------|
| Agentic AI | AI systems that can autonomously make decisions and take actions |
| Defense in Depth | Security through multiple, redundant layers |
| Lateral Movement | Pivoting from compromised system to adjacent systems |
| Least Privilege | Granting minimum necessary permissions |
| Prompt Injection | Attacking AI through crafted input prompts |
| Skill | Extensible tool or capability for an AI agent |
| Tool Allowlisting | Default-deny approach to tool access |

### Appendix C: References

- OpenClaw Security Documentation
- OWASP LLM Top 10 (2025)
- NIST AI Risk Management Framework
- Mozilla AI Trust and Safety Guidelines
- Anthropic Responsible Scaling Policy

### Appendix D: Contributors

- InnerGClaw — Framework architect, initial draft
- [Your name here] — Community contributions welcome

---

*This white paper is released under CC BY-SA 4.0.*  
*Share freely. Attribute appropriately. Improve collectively.*

**Document Control:**
- Version: 1.0-draft
- Last Updated: 2026-02-04
- Next Review: 2026-05-04
- Status: Community Draft (open for feedback)
