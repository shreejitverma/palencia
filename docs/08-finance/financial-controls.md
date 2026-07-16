# Financial Controls

> The safeguards that protect a high-value-inventory, high-average-order-value business — segregation of duties, authorization limits, purchase-to-pay and inventory controls, payment/fraud controls, revenue recognition, insurance, cash-flow management, and month-end close.

| | |
|---|---|
| **Owner** | Finance & Compliance |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

> **Not accounting, tax, or legal advice.** This document describes an internal control framework. Revenue recognition, inventory valuation methods, tax treatment, insurance adequacy, and AML obligations must be validated with a qualified accountant, insurer, and legal counsel, and adapted to the jurisdictions where Palencia Diamonds operates. AML controls here summarize obligations for dealers in precious stones, metals, and jewels (e.g. FinCEN rules in the US) — treat the detailed program as owned by [AML/KYC](../05-compliance-ethics/aml-kyc.md).

## 1. Why controls matter here specifically

Palencia carries **small, portable, high-value inventory** (loose diamonds, finished fine jewelry) and sells **high-ticket items online**. That combination creates concentrated risk:

- A single stone can be worth more than a month of some businesses' revenue — **theft, loss, and shrinkage** are existential.
- High-AOV e-commerce is a magnet for **card fraud and chargebacks**.
- Dealing in precious stones and metals brings **AML/KYC obligations** most retailers never face.

Controls are how "honest prices" and "precision in everything" show up on the finance side: the numbers are trustworthy, the inventory is real, and every dollar is traceable.

## 2. Control environment principles

| # | Principle | Why |
|---|---|---|
| 1 | **No one person controls a transaction end-to-end** | Segregation of duties (§3) prevents both error and fraud |
| 2 | **Authority is defined by threshold** | Approval limits (§4) scale scrutiny with dollar risk |
| 3 | **Every movement of value leaves a record** | Audit trail (§13) — nothing off-book |
| 4 | **Physical reality reconciles to the books** | Inventory counts (§7) tie to the ledger |
| 5 | **Controls are tested, not assumed** | Month-end close (§14) and periodic review verify they work |

## 3. Segregation of duties (SoD)

The core rule: **the person who authorizes, the person who has custody, and the person who records must not be the same person.** In a 10+ person company this requires deliberate role design, not just headcount.

| Function | Authorize | Custody / Execute | Record / Reconcile |
|---|---|---|---|
| **Buying stones/metal** | Merchandising lead / approver by threshold (§4) | Receiving (vault custody) | Finance (AP entry) |
| **Receiving inventory** | — | Receiving inspector | Finance / inventory system |
| **Paying suppliers** | Approver by threshold | Payment executor (releases funds) | Finance (reconciles bank) |
| **Selling / refunds** | Sales + refund approver | Fulfillment (ships) | Finance (revenue, reconciliation) |
| **Physical counts** | Finance schedules | Counter (not the custodian) | Finance reconciles variance |

- **Small-team compensating controls:** where full separation isn't possible, require a **second reviewer**, mandatory approvals above thresholds, and independent reconciliation. Document any SoD exception and the compensating control. `TODO:` map real names/roles to each cell.
- **Vault access** is restricted, logged, and dual-control for high-value movements. See [Inventory Management](../03-operations/inventory-management.md).

## 4. Authorization & approval thresholds

Scrutiny scales with dollar amount. Every spend/refund above a threshold needs the stated approval.

| Transaction type | Tier 1 (auto/self) | Tier 2 (manager) | Tier 3 (Finance/CEO dual) |
|---|---|---|---|
| **Purchase orders (stones/metal)** | ≤ `TODO: [$X]` | `TODO: [$X–$Y]` | > `TODO: [$Y]` |
| **Supplier payments** | ≤ `TODO: [$X]` | `TODO: [$X–$Y]` | > `TODO: [$Y]` (dual sign-off) |
| **Customer refunds** | ≤ `TODO: [$X]` | `TODO: [$X–$Y]` | > `TODO: [$Y]` |
| **Write-offs / inventory adjustments** | none | `TODO: [$X]` | any material amount (dual) |
| **New supplier onboarding** | — | Merchandising + Finance | AML/KYC sign-off (§6) |
| **Bank/vendor detail changes** | — | — | Dual verification (callback) — anti-fraud (§8) |

- **Dual authorization** required for high-value payments and any change to supplier bank details (a classic business-email-compromise attack vector).
- Thresholds reviewed `TODO: [cadence]` and set by Finance.

## 5. Purchase-to-pay (P2P) controls

The buy-side lifecycle, controlled at each step. Ties to [Sourcing & Procurement](../03-operations/sourcing-and-procurement.md).

1. **Requisition** — need identified, tied to demand/plan.
2. **Approved PO** — authorized per §4; PO issued to a **vetted, AML-screened** supplier (§6).
3. **Receipt & inspection** — Receiving verifies goods against PO **and against the grading report** (lab, cert number, 4Cs, weight, inscription where present). Mismatches are quarantined, not shelved.
4. **Three-way match** — invoice matched to PO and receipt before payment. No match, no pay.
5. **Payment** — released by a separate person (§3), within terms, to bank details verified out-of-band.
6. **Recording** — Finance books the payable/payment; inventory system updated at cost.

| P2P risk | Control |
|---|---|
| Paying for goods not received | Three-way match |
| Overpaying / duplicate payment | Invoice-to-PO match; duplicate-invoice check |
| Fraudulent supplier / diverted funds | Supplier vetting + bank-detail callback verification |
| Conflict/illicit stones | Grading-report verification + responsible-sourcing checks |

## 6. Cash handling & the AML link

We are, in substance, a **dealer in precious stones, metals, and jewels** — which carries anti-money-laundering obligations that a normal e-tailer does not. Cash and value handling connect directly to that program.

- **Online-first, low cash:** most sales settle by card/financing, which reduces cash-laundering exposure — but does not eliminate obligations.
- **Structuring / large payments:** watch for attempts to split payments to stay under reporting thresholds, unusual third-party payments, or requests to overpay and refund the difference (a laundering/fraud pattern).
- **KYC on high-value orders:** identity verification and record-keeping per the AML program above defined thresholds.
- **Escalation:** suspicious activity is escalated to the AML/Compliance owner — never handled ad hoc. Full obligations, thresholds, and SAR/reporting mechanics live in [AML/KYC](../05-compliance-ethics/aml-kyc.md).

`TODO:` Confirm applicable AML regime(s) and reporting thresholds for the jurisdiction(s) served, validated with counsel.

## 7. Inventory valuation & reconciliation

Inventory is our largest asset and biggest risk. It must be **valued correctly** and **reconciled to physical reality**.

### Valuation

| Topic | Approach |
|---|---|
| **Cost basis** | Carried at cost (stone invoice + attributable costs). See [Pricing Strategy §Diamonds](pricing-strategy.md) — we do **not** write inventory *up* on price-sheet rises |
| **Costing method** | `TODO: [specific-identification for stones (recommended), FIFO/weighted-avg for melee/metal]` — confirm with accountant |
| **Lower of cost/market** | Write **down** aging or declining inventory (e.g. lab-grown price erosion) to the lower of cost or net realizable value |
| **Consignment / memo stock** | Track separately; memo goods are **not owned** — never count them as our inventory |

### Reconciliation & counts

| Count type | Frequency | Who |
|---|---|---|
| High-value item cycle count | `TODO: [e.g. weekly/daily for loose stones]` | Counter ≠ custodian (§3) |
| Full physical inventory | `TODO: [e.g. quarterly/annually]` | Finance-supervised |
| Perpetual system check | Continuous | Inventory system vs. ledger |

- **Every count reconciles to the perpetual records and the general ledger.** Variances are investigated, documented, and require §4 approval to adjust.
- **Shrinkage** is tracked as a KPI; unexplained variance triggers investigation (theft, mis-picks, mis-grading). See [Inventory Management](../03-operations/inventory-management.md).

## 8. Payment processing, chargeback & fraud controls (high-AOV e-commerce)

High-ticket online jewelry is heavily targeted by card fraud. Controls protect revenue and reputation.

| Risk | Control |
|---|---|
| **Stolen-card orders** | AVS/CVV checks, 3-D Secure (SCA), fraud-scoring, velocity rules, high-value manual review |
| **Chargebacks (fraud & "item not received")** | Signature-confirmation insured shipping (proof of delivery), full order records, timely dispute responses |
| **Friendly fraud** | Delivery evidence + KYC on high-value orders; retain communications |
| **Refund abuse / overpayment scams** | Refunds only to original payment method; §4 approval; no cash-out of overpayments (see §6) |
| **Account takeover** | Verify identity on shipping-address/bank-detail changes |
| **Processor fees** | Recovered via overhead in [Pricing Strategy §13](pricing-strategy.md), not surprise checkout fees |

- **PCI DSS:** card data is handled only via a compliant processor/gateway; we do not store raw card numbers. `TODO:` confirm processor and PCI scope/attestation.
- **Manual review queue** for orders above `TODO: [$X]` before shipment of non-returnable/high-value goods.

## 9. Revenue recognition basics

> Confirm the applicable framework (e.g. ASC 606 / IFRS 15) with a qualified accountant.

- **Recognize revenue when control transfers** to the customer — generally **on delivery** for shipped goods, not at order or payment.
- **Deposits on custom orders are a liability (deferred revenue)**, not revenue, until the piece is delivered. See [Pricing Strategy §11](pricing-strategy.md).
- **Returns & refunds:** maintain a returns reserve/allowance given our generous return policy; recognize net of expected returns.
- **Gift cards / store credit:** deferred revenue until redeemed; `TODO:` breakage policy.
- **Financing sales:** recognize the product revenue at delivery; provider fees are an expense — do not net them into revenue.

`TODO:` Document the chosen revenue-recognition policy with the accountant and note the framework.

## 10. Insurance coverage

A high-value-inventory business must be insured against the losses that would otherwise be catastrophic.

| Coverage | Protects against | Notes |
|---|---|---|
| **Jewelers block / stock (inventory)** | Theft, burglary, loss, damage to stock — on-site and off-site | Core policy for our risk; confirm limits ≥ peak inventory value |
| **Transit / shipping** | Loss/damage in transit (inbound and to customer) | Ties to insured shipping — see [Shipping & Insurance](../03-operations/shipping-and-insurance.md) |
| **General liability** | Third-party injury/property claims | Standard business cover |
| **Cyber / crime** | Data breach, funds-transfer fraud, BEC | Increasingly essential for online + wire payments |
| **Property / BOP** | Premises, equipment | Facilities |

- **Adequacy check:** limits must track **peak inventory** (e.g. seasonal build), not average. Review coverage at each physical count and when inventory grows. `TODO:` record insurer, policy numbers, limits, deductibles.
- Insurance premiums are an overhead cost recovered in pricing (§ overhead, Pricing Strategy §7).

## 11. Budgeting & cash-flow management

Inventory ties up cash — a growing jewelry business can be profitable and still cash-starved.

- **Working-capital focus:** cash is locked in stones and metal; monitor **inventory turnover** and **days inventory outstanding** so we don't over-buy slow movers.
- **Cash-flow forecast:** rolling `TODO: [13-week]` forecast covering supplier payments (large, lumpy), payroll, insurance, and seasonality (engagement season peaks).
- **Budget vs. actual:** monthly variance review by Finance; material variances explained.
- **Purchase discipline:** buying is demand-informed (ties to §5 and Sourcing) to avoid cash trapped in dead stock.
- **Deposits fund custom:** custom deposits (Pricing §11) reduce our cash outlay on made-to-order stones — but are a liability until delivery (§9), not free cash.

## 12. Controls matrix

A compact map of key risks to controls, owners, and frequency. `TODO:` assign real owners.

| Control area | Key risk | Control(s) | Owner | Frequency |
|---|---|---|---|---|
| Segregation of duties | Fraud / error concealment | Role separation; second-reviewer; documented exceptions | Finance | Ongoing / reviewed quarterly |
| Authorization | Unapproved/oversized spend | Threshold approvals; dual sign-off (§4) | Finance / Mgmt | Per transaction |
| Purchase-to-pay | Overpay, ghost goods | Three-way match; duplicate check | Finance (AP) | Per invoice |
| Supplier integrity | Fraud, illicit stones | Vetting; AML screen; bank-detail callback | Merch + Compliance | Onboarding + change |
| Inventory valuation | Mis-stated asset value | Cost basis; LCM write-downs | Finance | Monthly / count |
| Physical inventory | Theft / shrinkage | Cycle + full counts; count ≠ custody; vault dual-control | Ops + Finance | Per §7 |
| Cash & AML | Money laundering | KYC thresholds; structuring watch; escalation | Compliance | Per transaction |
| Payment/fraud | Card fraud, chargebacks | AVS/CVV/3DS, scoring, manual review, delivery proof | Finance + Ops | Per order |
| Revenue recognition | Mis-timed revenue | Recognize on delivery; deferred deposits | Finance | Monthly close |
| Insurance | Uninsured loss | Jewelers block, transit, cyber; limit reviews | Finance | Quarterly / on growth |
| Cash flow | Illiquidity | 13-week forecast; turnover monitoring | Finance | Weekly / monthly |
| Recordkeeping | No audit trail | Immutable logs; retention policy | Finance | Ongoing |

## 13. Audit trail & recordkeeping

- **Everything is documented:** POs, invoices, receipts, grading reports, payments, sales, refunds, adjustments, and count sheets — each traceable to a person and a timestamp.
- **Immutable/append-only** system logs where possible; adjustments are entries, not overwrites.
- **Retention:** keep financial, AML/KYC, and tax records for the period required by law — `TODO: [state retention periods per jurisdiction, validated with counsel/accountant]`.
- **Access control:** least-privilege access to financial systems; changes logged.
- **Supports:** external audit/review, tax filing, AML examination, and insurance claims.

## 14. Month-end close checklist

Run every month; sign-off by Finance. Tie exceptions to §4 approvals.

- [ ] All supplier invoices received, matched (three-way), and booked
- [ ] All sales/refunds recorded; deferred deposits reconciled (custom orders)
- [ ] Revenue recognized on delivery; returns reserve updated
- [ ] Bank accounts reconciled; unmatched items investigated
- [ ] Payment-processor settlement reconciled (fees, chargebacks, holds)
- [ ] Inventory perpetual reconciled to ledger; cycle-count variances resolved
- [ ] Inventory write-downs (aging/lab-grown/LCM) assessed and posted
- [ ] Metal/stone cost inputs current (link to Pricing §8 repricing)
- [ ] Accruals booked (insurance, payroll, overhead)
- [ ] Cash-flow forecast refreshed
- [ ] Budget-vs-actual variance reviewed and explained
- [ ] AML/KYC exceptions and any suspicious-activity escalations logged
- [ ] Journal entries reviewed by a second person (SoD)
- [ ] Close signed off and locked; audit trail archived

## 15. Governance & review

- **Owner:** Finance & Compliance owns this framework; department leads own the controls in their area.
- **Testing:** controls are periodically tested (walkthroughs, sample re-performance), not assumed effective.
- **Exceptions:** any control exception is documented with a compensating control and time-boxed.
- **Review:** quarterly, or after any incident (fraud, loss, material variance) or significant growth in inventory value.

---

## Related documents
- [Pricing Strategy](pricing-strategy.md)
- [Inventory Management](../03-operations/inventory-management.md)
- [AML/KYC](../05-compliance-ethics/aml-kyc.md)
- [Shipping & Insurance](../03-operations/shipping-and-insurance.md)
- [Sourcing & Procurement](../03-operations/sourcing-and-procurement.md)
- [Company Overview](../00-company/company-overview.md)
- [Documentation Home](../../README.md)
