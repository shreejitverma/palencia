# Data Privacy & Security

> How Palencia Diamonds collects, protects, and honors the rights attached to customer and employee data — for an online-first business where trust is the product.

| | |
|---|---|
| **Owner** | Compliance Officer / IT & Operations |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Annually (and upon material regulatory or system change) |
| **Status** | Active |

---

> [!IMPORTANT]
> **This document is operational guidance, not legal advice.** Privacy and data-security obligations (GDPR, CCPA/CPRA, PCI-DSS, breach-notification laws, and others) depend on where our customers reside, where we operate, our data volumes, and our processors. **Qualified counsel and, where appropriate, a QSA (for PCI) must review this program for every jurisdiction in which Palencia operates before it is treated as binding.** Where law and this policy conflict, the law governs.

## 1. Purpose & scope

This policy governs all personal data Palencia processes — from prospective and current customers, website visitors, and employees — across our website, CRM, payment flows, marketing tools, and vendors. It applies to every employee and processor that touches that data.

**Principle:** We collect the minimum we need, protect it rigorously, use it honestly, and honor the rights people have over it.

## 2. Data we collect and why

| Data category | Examples | Purpose | Lawful basis (GDPR framing) | Notes |
|---|---|---|---|---|
| Identity & contact | Name, email, phone, shipping/billing address | Fulfill orders, deliver, support | Contract / legitimate interest | Core to every order |
| Order & product | Items, sizes, engravings, custom specs | Fulfillment, warranty, resizing | Contract | Ties to [CRM](../04-sales-cx/crm-and-clienteling.md) |
| Payment | Card data, transaction records | Process payment | Contract | **Tokenized via PCI-compliant processor — raw card data never stored by us** (§6) |
| Account | Login credentials, preferences | Account services | Contract | Passwords hashed, never plaintext |
| Marketing & consent | Email opt-in, campaign engagement | Marketing with consent | Consent | Opt-out honored (§10) |
| Website/behavioral | Cookies, device, IP, analytics | Site function, analytics, ads | Consent / legitimate interest | Cookie consent (§10) |
| KYC/AML (as applicable) | ID, screening results | Legal compliance | Legal obligation | See [AML & KYC](aml-kyc.md); restricted access |
| Employee/HR | Employment records | Employment | Contract / legal obligation | Out of primary scope; `[TODO: cross-ref HR retention policy]` |

`[TODO: Confirm the full data inventory against the live website, CRM, and marketing stack; keep this table as the maintained record of processing.]`

## 3. Privacy principles

1. **Lawfulness, fairness, transparency** — a clear, current privacy notice tells people what we do.
2. **Purpose limitation** — data collected for one purpose isn't repurposed without a basis.
3. **Data minimization** — we don't collect "just in case."
4. **Accuracy** — people can correct their data.
5. **Storage limitation** — we retain only as long as needed (§7).
6. **Integrity & confidentiality** — security by design and default (§5–6).
7. **Accountability** — we can demonstrate compliance.

## 4. Data-subject / consumer rights (GDPR & CCPA/CPRA)

We honor applicable rights regardless of a customer's location where feasible, and always where legally required.

| Right | GDPR | CCPA/CPRA | How we handle it |
|---|---|---|---|
| Access / know | ✔ | ✔ | Provide categories and copies on verified request |
| Deletion / erasure | ✔ | ✔ | Delete unless a legal retention basis applies (e.g., AML, tax) |
| Correction / rectification | ✔ | ✔ | Update on verified request |
| Portability | ✔ | ✔ (limited) | Provide in a portable format |
| Opt out of "sale"/"sharing" | — | ✔ | Honor "Do Not Sell or Share My Personal Information"; respect opt-out preference signals `[TODO: confirm GPC handling]` |
| Object / restrict processing | ✔ | Limited | Stop or restrict where required |
| Withdraw consent | ✔ | ✔ | Easy unsubscribe / consent withdrawal |
| Non-discrimination | — | ✔ | No penalty for exercising rights |

- **Request intake:** `[TODO: publish a privacy request channel, e.g., privacy@palenciadiamonds.com and/or a web form.]`
- **Identity verification** before fulfilling requests; **response deadlines** per applicable law. `[TODO: confirm SLAs — e.g., GDPR ~1 month, CCPA ~45 days.]`
- **We do not sell personal data for money.** `[TODO: confirm no "sharing" for cross-context behavioral advertising under CPRA; adjust disclosures if ad pixels constitute "sharing."]`

## 5. Security controls

| Control | Standard |
|---|---|
| **Encryption in transit** | TLS/HTTPS across the site and admin |
| **Encryption at rest** | Encrypt databases and backups containing personal data |
| **Access control** | Role-based, least-privilege; unique accounts; no shared logins |
| **Authentication** | Strong passwords + MFA on admin, CRM, email, and payment dashboards |
| **Password storage** | Salted hashing; never plaintext |
| **Logging & monitoring** | Access and change logs; alerting on anomalies `[TODO: confirm tooling]` |
| **Patching** | Timely updates to platform, plugins, and dependencies |
| **Backups** | Regular, encrypted, tested restores |
| **Device security** | Company devices encrypted, screen-locked, endpoint-protected |
| **Offboarding** | Access revoked promptly when roles change or staff leave |

## 6. Payment data & PCI-DSS

> [!IMPORTANT]
> **We never store, process, or transmit raw cardholder data on our own systems.** Payment is handled by a PCI-DSS-compliant processor/gateway; card entry is tokenized/hosted by the processor so sensitive card data does not touch Palencia's servers.

- Maintain **PCI-DSS** compliance appropriate to our merchant level via our processor. `[TODO: confirm merchant level, SAQ type (likely SAQ A for a hosted/tokenized flow), and QSA/ASV needs with the payment provider.]`
- Never record full card numbers, CVV, or full track data anywhere (email, notes, CRM, tickets).
- Refunds go only to the original payment method (also an AML control — see [AML & KYC](aml-kyc.md)).

## 7. Data minimization & retention

| Data | Retention target | Basis |
|---|---|---|
| Order & fulfillment records | `[TODO: confirm — often tied to tax/warranty period]` | Contract / legal |
| Marketing contacts | Until opt-out + `[TODO]` | Consent |
| Website analytics | `[TODO: confirm]` | Consent / legitimate interest |
| KYC/AML records | Per [AML & KYC](aml-kyc.md) retention | Legal obligation |
| Support tickets | `[TODO: confirm]` | Legitimate interest |
| Backups | `[TODO: confirm rotation]` | Security |

- We delete or anonymize data when its purpose and legal-retention window end.
- Retention that conflicts with a deletion request is documented and explained to the requester.

## 8. Vendors & processors

- Any vendor handling personal data (CRM, email/marketing, hosting, analytics, shipping, payment) is a **processor** and must be governed by a **Data Processing Agreement (DPA)**.
- DPAs must require: processing only on our instructions, adequate security, sub-processor controls, breach notification to us, deletion/return on termination, and (for cross-border transfers) a valid transfer mechanism. `[TODO: confirm SCCs/adequacy for any non-EU/US transfers with counsel.]`
- Vendors are risk-assessed and inventoried; see [Vendor Management](../03-operations/vendor-management.md).

### Vendor privacy checklist

- [ ] DPA signed and on file
- [ ] Security posture reviewed (certifications, SOC 2 / ISO 27001 if available)
- [ ] Sub-processors disclosed
- [ ] Cross-border transfer mechanism valid
- [ ] Breach-notification obligation in contract
- [ ] Data deletion/return terms on offboarding

## 9. Breach response

A personal-data breach is any unauthorized access, loss, or disclosure. Speed and documentation are critical.

| Step | Action | Owner |
|---|---|---|
| 1. Detect & report | Anyone who suspects a breach notifies the Compliance Officer **immediately** | All staff |
| 2. Contain | Isolate affected systems; revoke compromised access | IT / Ops |
| 3. Assess | Scope, data types, individuals, and risk of harm | Compliance / IT |
| 4. Notify | Regulators and individuals **within legal deadlines** where required | Compliance Officer + counsel |
| 5. Remediate | Fix root cause; strengthen controls | IT / Ops |
| 6. Document | Full incident record and lessons learned | Compliance |

> [!IMPORTANT]
> Notification deadlines are strict and jurisdiction-specific (e.g., **GDPR: without undue delay and, where feasible, within 72 hours** to the supervisory authority; various US state deadlines). **Involve counsel immediately** — do not self-assess notification duty. `[TODO: confirm the notification matrix for our markets.]`

## 10. Cookies & marketing consent

- **Cookie consent:** Non-essential cookies (analytics, advertising) require consent via a compliant banner with granular controls and easy withdrawal. `[TODO: confirm CMP tool and default-off for non-essential in required regions.]`
- **Marketing consent:** Email/SMS marketing is opt-in where required; every message has a working unsubscribe; opt-outs are honored promptly and suppress across the stack.
- **Preference signals:** Honor recognized opt-out signals where legally required. `[TODO: confirm Global Privacy Control (GPC) handling.]`
- Marketing practices also follow the honesty standard in the [Ethics Policy](ethics-policy.md).

## 11. Handling a data-subject / consumer request (DSAR)

A consistent workflow keeps us within legal deadlines and avoids over- or under-disclosing.

| Step | Action | Owner |
|---|---|---|
| 1. Receive | Log the request with date and channel | Compliance |
| 2. Verify | Confirm the requester's identity | Compliance |
| 3. Scope | Identify systems holding the person's data (use §2 inventory) | Compliance / IT |
| 4. Assess | Check for legal holds (AML, tax, litigation) that limit deletion | Compliance + counsel |
| 5. Fulfill | Provide, correct, delete, or opt-out as required | Compliance / IT |
| 6. Respond | Reply within the legal deadline; explain any exceptions | Compliance |
| 7. Record | Retain proof of handling | Compliance |

> When a deletion request collides with a legal retention duty (e.g., AML/tax records), we retain only what the law requires and delete the rest, and we tell the requester.

## 12. International data transfers

- Cross-border transfers of personal data (e.g., EU/UK to US, or to a processor abroad) require a valid transfer mechanism — adequacy, Standard Contractual Clauses (SCCs), the UK IDTA/Addendum, or another lawful basis. `[TODO: confirm which mechanisms apply to our processor map with counsel.]`
- Transfers are inventoried alongside vendors (§8).

## 13. Roles & training

| Role | Responsibility |
|---|---|
| **Compliance Officer** | Owns this policy, rights requests, breach response, DPA oversight |
| **IT & Operations** | Implements and maintains security controls |
| **Marketing** | Owns consent, cookies, and unsubscribe hygiene |
| **CX / Sales** | Handles data respectfully; routes rights requests; never records card data |
| **All employees** | Complete privacy/security training; report incidents immediately |

Privacy & security training is delivered at onboarding and at least annually.

---

## Related documents
- [CRM & Clienteling](../04-sales-cx/crm-and-clienteling.md)
- [Ethics & Anti-Corruption Policy](ethics-policy.md)
- [AML & KYC](aml-kyc.md)
- [Vendor Management](../03-operations/vendor-management.md)
- [Financial Controls](../08-finance/financial-controls.md)
- [Documentation Home](../../README.md)
