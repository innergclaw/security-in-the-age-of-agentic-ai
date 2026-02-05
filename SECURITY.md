# Security Guidelines

> Quick-start security for OpenClaw deployments

---

## 🚨 Before You Start

**The 5-Minute Rule:**  
If you wouldn't leave an API key in a public GitHub repo for 5 minutes, don't give it to your agent.

---

## ✅ Security Checklist

### Pre-Deployment

- [ ] **Tool Permissions:** Default deny, explicitly allowlist
- [ ] **Block high-risk tools:** exec, gateway, message (unless required)
- [ ] **Credential scope:** Read-only tokens, minimal permissions
- [ ] **Token rotation:** Set calendar reminders (30/60/90 days)
- [ ] **Network isolation:** Agent workspace separated from host
- [ ] **Audit logging:** Enabled, immutable, 90-day retention
- [ ] **Confirmation gates:** Sensitive actions require approval
- [ ] **Incident response plan:** Documented and tested

### Daily Operation

- [ ] **Security check script executed** (2 minutes)
- [ ] **Sessions killed when idle**
- [ ] **No credentials in logs/output**
- [ ] **Anomalies reviewed**

### Weekly Review

- [ ] **Log review** (5 minutes) — Look for unusual patterns
- [ ] **Failed authentications**
- [ ] **Unexpected external calls**
- [ ] **Access outside workspace**

### Monthly Maintenance

- [ ] **Credential rotation calendar checked**
- [ ] **Log retention verified**
- [ ] **New skills audited**
- [ ] **Framework updates reviewed**

---

## 🔒 Security Profiles

### Strict Mode (Recommended for Production)

```yaml
profile: strict
allowed_tools:
  - read
  - memory_search
  - web_search
blocked_tools:
  - exec
  - browser
  - message
  - gateway
  - nodes
require_confirmation:
  - edit
  - write
session_max_duration: 3600
auto_kill_idle: 300
```

### Moderate Mode (Balanced)

```yaml
profile: moderate
allowed_tools:
  - read
  - write
  - edit
  - memory_search
  - memory_get
  - web_search
  - web_fetch
blocked_tools:
  - exec
  - gateway
require_confirmation:
  - browser
  - message
  - nodes
session_max_duration: 7200
```

### Minimal Mode (Development Only)

```yaml
profile: minimal
allowed_tools: [all]
blocked_tools: []
require_confirmation:
  - exec
  - gateway
  - message
```

---

## 🔑 Credential Hygiene

### Best Practices

| Practice | Implementation |
|----------|----------------|
| Short-lived | Rotate every 30-90 days |
| Scoped | Read-only GitHub, limited Gmail |
| Segregated | One key per service |
| Secure storage | OS keychain, never plaintext |
| Monitoring | Alerts on unusual usage |

### What NOT to Do

❌ Store credentials in workspace files  
❌ Share tokens across services  
❌ Use admin/root tokens  
❌ Commit keys to version control  
❌ Ignore rotation reminders  

---

## 🏰 Network Isolation

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
│  Isolated directory                 │
│  Ephemeral, wiped on restart        │
├─────────────────────────────────────┤
│ TIER 4: External Services           │
│  Allowlist egress only              │
└─────────────────────────────────────┘
```

---

## 📊 Audit Requirements

### Log Everything

```yaml
audit:
  log_all_tool_calls: true
  log_level: info
  hash_sensitive_params: true
  retention_days: 90
  immutable_logs: true
```

### Review Triggers

Alert when agent:
- Accesses files outside workspace
- Makes unexpected external calls
- Uses high-risk tools (exec, browser, message)
- Accesses credential files
- Exhibits unusual request patterns

---

## 🚨 Incident Response

### Compromise Playbook

**1. ISOLATE (0-5 minutes)**
```bash
# Kill agent process
pkill -f openclaw

# Revoke tokens immediately
# Disconnect from network
```

**2. ASSESS (5-30 minutes)**
- Review logs (what was accessed?)
- Check API dashboards
- Verify file integrity

**3. CONTAIN (30-60 minutes)**
- Rotate all exposed credentials
- Audit connected systems
- Enable enhanced monitoring

**4. RECOVER (1-24 hours)**
- Restore from known-good backup
- Re-deploy with hardened config
- Document lessons learned

**5. SHARE (1-7 days)**
- Report to community (anonymized)
- Update framework
- Contribute IOCs

---

## 🛠️ Security Check Script

```bash
#!/bin/bash
# Daily security check (~2 minutes)

echo "🔍 OpenClaw Security Check"
echo "=========================="

# Check active profile
echo "Profile: $(cat ~/.openclaw/security/active.json | grep securityProfile)"

# Check for exposed credentials
echo "Scanning for credential files..."
find ~/.openclaw -name "*.env" -o -name "*credential*" 2>/dev/null

# Check log status
echo "Audit logs: $(ls ~/.openclaw/logs/*.log 2>/dev/null | wc -l) files"

# Check gateway
curl -s http://localhost:3000/status >/dev/null && echo "Gateway: Running" || echo "Gateway: Down"

echo ""
echo "✓ Security check complete"
```

---

## 📚 Additional Resources

- [Full Whitepaper](SAFETY_WHITEPAPER.md) — Deep dive into threat model and framework
- [Contributing Guide](CONTRIBUTING.md) — How to improve these guidelines
- [OpenClaw Security Docs](https://docs.openclaw.ai/security)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)

---

> **"Paranoia is a feature, not a bug."**  
> In an age of agentic AI, healthy skepticism is the foundation of trust.
