# Veilio

Make stolen data worthless.

Veilio replaces plaintext personal data with tokens. The email, phone number, IBAN, or name no longer sits in your database. It sits in an encrypted vault. Your application stores only a token. If the database, the backup, or the export leaks, there is nothing left to resell, nothing left to spam, and nobody left to call.

Site: [veilio.fr](https://veilio.fr) · Docs: [docs.veilio.xyz](https://docs.veilio.xyz)

---

## Encryption is not enough

Encrypting the disk or the database protects a file at rest. The moment an application is allowed to read, it decrypts. A SQL injection, a copied backup, an export, a replica, an admin laptop: the plaintext is right there.

Veilio does not replace that encryption. It sits in front of it. The row itself no longer holds the value. Encryption protects the vault. The token protects everything else: your database, your backups, your SQL logs, the file someone sent "just to take a look."

| | Plaintext database, even encrypted at rest | Tokenized database |
|---|---|---|
| Dump, backup, replica | A usable customer list | Worthless tokens |
| Export or table copy | An address book | Nothing to phish |
| A flaw that reads the rows | The jackpot | The flaw is still there. The jackpot is not. |

Veilio does not stop the intrusion. Veilio makes sure an intrusion no longer hands over your customers.

## Two reasons to adopt Veilio

**Fear, on the executive side.** A leak is no longer just an outage. It is a list of real people: fines, notifications, lost trust, weeks of incident response. The usual scenario is not a movie attacker. It is a backup left open, an access right too wide, a file that gets forwarded. As long as the value sits in the database, that scenario is enough.

**Advantage, on the commercial side.** Your customers trust you with their users, their employees, their files. A competitor that still stores emails in plaintext does not have the same argument. You can say it, and show it: your users' data is not readable in your database. Detokenization happens only for an authorized action, with a trail. Trust becomes a buying criterion, not a line on a security page.

---

## Use cases

- **Accounts and profiles.** Email, phone, address: a token on save, the real value only when you need to write to the person or open the record.
- **Forms.** Contact, signup, lead: the data is tokenized at collection. The spreadsheet or the marketing database does not become a plaintext prospecting file.
- **Business application.** Case files, billing, a CRM your team built: identity fields go to the vault. Amounts, document numbers, and reconciliation keys stay in plaintext. The business keeps running.
- **Files and history.** A CSV, an export, an old database: import, batch tokenization, and a working file that no longer holds the plaintext.
- **Sharing a dataset.** You hand a dataset to another team or to a vendor. They receive tokens, access limited in time, and only the columns you allowed. Not a full copy of the customer file.
- **Data that leaves.** Export, send, connector to another system: what leaves your perimeter is already tokenized. The authorized recipient detokenizes. Everyone else sees a token.
- **Data-entry software you do not own, database you do.** The gateway sits in front of the database. The screen still shows the real values. The database stores only tokens.
- **Software and database both hosted by the vendor.** You do not get into their database. Either the vendor calls Veilio on save and on display, or you protect only the flow that lands on a server you own.

You do not tokenize the whole database. You tokenize identity. An amount, an account number, or a reconciliation key stays business data.

---

## How it connects

### You own the code: SDK

A homegrown application, a backend your team ships, a form, an API. You call Veilio before you write, and again when the screen needs the plaintext.

JavaScript SDK, Python SDK, or HTTP. The existing column stores the token instead of the email. You do not run a second database on your side: the plaintext lives in the Veilio vault, encrypted with AES.

```javascript
import { VeilioClient } from '@veilio/sdk';

const veilio = new VeilioClient({
  apiKey: process.env.VEILIO_API_KEY
});

const { token } = await veilio.tokenize({
  data: user.email,
  type: 'email'
});
await db.users.insert({ email: token });

const { data } = await veilio.detokenize({
  token,
  reason: 'customer email'
});
```

Several fields on the same record go through one bulk call. Each new value counts as a token. The call counts as one request.

### You have files: datasets

Import a CSV or a JSON, tokenize the columns you choose, then work and share the dataset.

Sharing does not hand over the plaintext file. Access is limited to that dataset, to a duration, and to the columns allowed for the role. Useful for a vendor, another team, or an exchange where the copy must not become a usable list.

### You do not own the code, the database is yours: Gateway

A vendor's data-entry product, the database server on your premises, a connection string you can change. Veilio Gateway sits between the software and the database.

On save, it sends the value to the vault and lets the token be written. On display, it detokenizes so the screen shows the real value. The business software never talks to Veilio. Your team does not rewrite every screen.

This mode does not cover software whose vendor also hosts the database. In that case the gateway has nowhere to sit. The vendor has to call the API, or you protect the flow that leaves toward your own server.

### The three situations

| Situation | How it connects |
|---|---|
| Your own tool or backend | SDK or API, in your code |
| Files, history, a handoff to a third party | Datasets, then bounded sharing |
| Third-party software, database on your side | Gateway in front of the database |
| Software and database both at the vendor | The vendor calls the API. Otherwise, SDK on the flow that arrives on your side |

The API, the SDKs, and datasets are available. The gateway is the connection for software you do not own, as soon as the database is yours.

---

## Our other products

Same house. Four different jobs. None of them replaces the others.

**Exposure.** A free exposure scan, in one minute: surface, leaks, hygiene. No account. The point is to see what is already outside, before talking about protection.

**Alyren.** Pseudonymization of the prompt. Your teams keep talking to an AI. The model receives a linked twin, the same person for the name and the email, not your customer. The plaintext stays in Alyren. It is reversible. It is not anonymization. Veilio protects systems. Alyren protects what people paste into an AI, outside the connector you control.

**Exchange.** Data sharing between organizations, with governance and a trail, when a file has to move from one entity to another without becoming a wild copy.

---

## Who it is for

Teams building a product that stores their users' data. CISOs and CIOs who want a database copy to stop being an incident. Vendors and integrators who need to tell their customers: your data is not in plaintext on our side.

Start: [veilio.fr](https://veilio.fr) · Docs: [docs.veilio.xyz](https://docs.veilio.xyz)
