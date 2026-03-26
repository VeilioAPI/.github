# Veilio

## Make stolen data worthless.

API-first data tokenization infrastructure.  
Replace plain-text sensitive data with secure tokens in your backend—if a database leaks, the data is unusable.

---

## What we do

Veilio provides a tokenization API that sits between your application and your database:

- **Tokenize before storing**: emails, phones, and PII become opaque tokens in your DB
- **Detokenize when needed**: with access control and audit trail
- **Keep real data isolated** in an encrypted vault while your application database stores tokens
- **Integrate fast**: no full schema migration, no full-database rewrite

| Your database | Attacker gets a copy |
| --- | --- |
| **Without Veilio**: `john@company.com` | **Exploitable** |
| **With Veilio**: `tok_x7k2m9...` | **Worthless** |

---

## For technical teams

- **API-first**: REST API + official SDKs (JavaScript/TypeScript, Python)
- **Drop-in integration**: works with any stack; tokenize in your backend before `INSERT`
- **Compliance-ready**: audit logs, RBAC, and controls aligned with GDPR / SOC 2 / HDS / NIS 2
- **Zero-refactor mindset**: keep your schema and store tokens in the same columns

---

## Quick example

```ts
import { VeilioClient } from '@veilio/sdk';

const veilio = new VeilioClient({
  apiKey: process.env.VEILIO_API_KEY
});

// Before storing
const { token } = await veilio.tokenize({
  data: user.email,
  type: 'email'
});
await db.users.insert({ email: token });

// When needed (support, export, operations)
const { data } = await veilio.detokenize({
  token,
  reason: 'support ticket #42'
});
```

---

## Use cases

| Use case | Status |
| --- | --- |
| Profile/account pages: tokenize PII fields on save | ✅ Live |
| Contact and lead forms: tokenize on submit | ✅ Live |
| Marketing campaigns and landing pages: protect collected personal data | ✅ Live |
| Newsletter/emailing databases: controlled detokenization for approved workflows | ✅ Live |
| Legacy CSV datasets: batch tokenization for historical data | ✅ Live |
| CRM native read flows with transparent detokenization | 🔜 Phase 2 |

---

## Who it’s for

- **SaaS & AI startups**: ship fast, protect PII, and meet enterprise requirements
- **Engineering teams**: API-first, DevOps-friendly; no dedicated security team required to start
- **Technical founders**: fix data security architecture early and prepare for compliance milestones

---

## We are onboarding testers

Join us for free: [https://veilio.xyz](https://veilio.xyz)

Docs available here : [https://docs.veilio.xyz](https://docs.veilio.xyz)

