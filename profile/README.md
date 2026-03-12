# Veilio

**Make stolen data worthless.**

API-first data tokenization infrastructure. Replace plain-text sensitive data with secure tokens in your backend—if a database leaks, the data is unusable.

---

## What we do

Veilio provides a **tokenization API** that sits between your application and your database:

- **Tokenize** before storing: emails, phones, PII → opaque tokens in your DB  
- **Detokenize** when needed: with audit trail and access control  
- **Real data** stays in an isolated, encrypted vault—your DB only holds tokens  

No schema migration, no full-database rewrite. Integrate in hours, not months.

| | Your database | Attacker gets a copy |
|--|----------------|----------------------|
| Without Veilio | `john@company.com` | Exploitable |
| With Veilio | `tok_x7k2m9...` | Worthless |

---

## For technical teams

- **API-first** — REST API, official SDKs (JavaScript/TypeScript, Python)
- **Drop-in** — Works with any stack; tokenize in your backend before `INSERT`
- **Compliance-ready** — Audit logs, access control (RBAC), formats for GDPR/SOC 2/HDS/NIS 2
- **Zero refactoring** — Keep your schema; store tokens in the same columns

### Quick example

```javascript
import { VeilioClient } from '@veilio/sdk';

const veilio = new VeilioClient({ apiKey: process.env.VEILIO_API_KEY });

// Before storing
const { token } = await veilio.tokenize({ data: user.email, type: 'email' });
await db.users.insert({ email: token });

// When you need the value (e.g. support, export)
const { data } = await veilio.detokenize({ token, reason: 'support ticket #42' });
```

---

## Use cases

| Use case | Status |
|----------|--------|
| **Forms** (signup, contact) — tokenize on submit | ✅ Live |
| **IA / ML** — train on tokens, no PII in models | 🔜 Coming |
| **CRM & support** — detokenize on demand with audit | 🔜 Coming |
| **Data sharing** — analytics/partners see tokens only | 🔜 Coming |

---

## Who it's for

- **SaaS & AI startups** — Ship fast, protect PII, meet enterprise requirements  
- **Engineering teams** — API-first, DevOps-friendly; no dedicated security team required  
- **Technical founders** — Fix security architecture early; compliance (SOC 2, ISO, HDS) on the roadmap  

---

## We are onboarding testers! Join us for free at https://veilio.xyz

---

*France · Technology, Information and Media*
