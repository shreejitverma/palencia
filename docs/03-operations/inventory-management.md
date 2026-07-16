# Inventory Management

> How Palencia Diamonds tracks, secures, counts, and reconciles a small-volume, high-value inventory — so that every stone is traceable to its certificate, every item is accounted for, and shrinkage has nowhere to hide.

| | |
|---|---|
| **Owner** | Operations & Fulfillment |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Purpose & scope

Fine-jewelry inventory is unusual: low unit count, extreme unit value, and every diamond is legally and commercially distinct because it carries its own certificate. A single misfiled stone is a five-figure problem. This SOP covers:

- **Identification & tracking** — SKUs, lots, and individual stone traceability.
- **Physical security** — safes, access control, and dual-control for high-value goods.
- **Counting & reconciliation** — cycle counts, full audits, and how discrepancies are resolved.
- **Consignment / memo goods** — inventory we hold but don't own.
- **Insurance & shrinkage prevention.**

It connects tightly to [Financial Controls](../08-finance/financial-controls.md) (the value side) and [Shipping & Insurance](shipping-and-insurance.md) (goods in transit).

## 2. Principles

1. **Every diamond is a serial number.** A certified stone is tracked individually, cert-number ↔ item, from receipt to sale. It is never pooled or averaged.
2. **Custody is always known.** At any moment we can say who holds each high-value item and where it is.
3. **Dual control on the high stuff.** Above a defined value threshold, no single person is ever alone with the ability to move or remove an item unobserved.
4. **The record equals the vault.** The inventory system and the physical count must reconcile. When they don't, we stop and find out why.
5. **Own vs. hold is never blurred.** Consignment/memo goods are flagged distinctly and never commingled with owned stock in a way that hides ownership.

## 3. Item identification & tracking

### 3.1 Identifier hierarchy

| Level | What it is | Example use |
|---|---|---|
| **SKU** | Catalog product identifier (design + metal + spec) | A ring model in 14k white gold |
| **Lot** | A received batch of like items (esp. melee, findings, metal) | A parcel of 1.3mm melee |
| **Item / stock number** | A unique record for one physical piece or loose stone | This exact solitaire ring |
| **Certificate number** | The GIA/IGI report number, bound to the specific center stone | Traceability anchor |

### 3.2 Individual stone traceability — the cert ↔ item link

For every certified center stone:

1. On receipt, the **verified report number** (see [Sourcing & Procurement](sourcing-and-procurement.md) §4) is recorded as a field on the stone's item record.
2. The link is **one-to-one and permanent**: report number ↔ item ↔ (once set) finished piece ↔ order ↔ customer.
3. The laser inscription (matching the report number) is the physical tie-back; re-read at final QC (see [Quality Control](quality-control.md) §6).
4. When a loose stone becomes a set piece, the item record is updated but the **cert number carries forward** — so the certificate that ships is provably the stone's own.

> Traceability is not bureaucracy here — it is the anti-swap control and the backbone of the "certified diamonds" promise. If we can't tie a stone to its report, we can't sell it.

### 3.3 Melee, findings & metal

Small stones (melee), findings, and casting metal are tracked by **lot and weight**, not individually. Record quantity/weight in and out; reconcile by weight during counts (see §5). `TODO: [Confirm melee reconciliation tolerance by weight.]`

### 3.4 Inventory states

Every item carries a status so its location and availability are unambiguous:

`Received → In QC/Quarantine → Available (loose) → Reserved/In production → Finished (in QC) → Awaiting ship → Shipped/Sold`; plus `Consignment/Memo`, `Returned`, `Repair`, `Scrap/Loss`.

`TODO: [Confirm the inventory/ERP system of record Palencia uses.]`

## 4. Physical security

### 4.1 Storage

- High-value stones and finished pieces are stored in a **rated safe or vault** when not being actively worked. `TODO: [Confirm safe rating/TL-class and any UL rating required by our insurer.]`
- **Segregation:** owned stock, consignment/memo goods, customer property (repairs/resizes), and quarantined items are stored in separate, labeled locations.
- **Overnight rule:** nothing high-value is left out of the safe overnight. End-of-day secure-down is a signed step.

### 4.2 Access control

| Control | Standard |
|---|---|
| Safe access | Restricted to authorized roles only; access list reviewed `TODO: [frequency]` |
| Keys/combinations | Changed on personnel change; combinations known on a need-to-know basis |
| Facility access | Badge/lock control; visitor log; alarm and monitored intrusion detection `TODO: [Confirm alarm/monitoring provider.]` |
| Video | CCTV covering safe, bench, packing, and receiving areas; retention `TODO: [days]` |
| Audit trail | System logs who moved each item between states/locations, with timestamp |

### 4.3 Dual control for high value

For any item at or above the high-value threshold `TODO: [$ threshold]`:

- **Two authorized people** are present for safe open/close counts, high-value moves, and outbound packing.
- **Sign-off:** both initial the movement log. No solo custody of high-value goods.
- **Separation of duties:** the person who buys/receives is not the sole person who counts and reconciles (ties to [Financial Controls](../08-finance/financial-controls.md)).

## 5. Cycle counts, full audits & reconciliation

### 5.1 Cycle counts (rolling)

- **Frequency:** high-value loose stones and finished pieces counted `TODO: [weekly]`; melee/findings lots `TODO: [monthly]`.
- **Method:** blind count where practical (counter isn't shown expected quantity), then compared to system.
- **Verification:** for certified stones, confirm the **cert number + inscription** match the record — not just that "a stone" is present. This catches swaps, not only losses.
- **Dual control** for high-value count sessions.

### 5.2 Full physical audit

- **Frequency:** at least `TODO: [quarterly/annually]`, and always before/after major events (year-end, insurance renewal, key-holder change).
- **Scope:** 100% of owned inventory, consignment/memo goods, customer property, and quarantine.
- **Independence:** conducted or observed by someone independent of day-to-day custody (e.g., Finance).
- **Valuation tie-out:** results reconciled to the general ledger inventory value with Finance.

### 5.3 Reconciliation & discrepancy handling — SOP

1. **Compare** counted quantities/cert-matches to the system of record.
2. **Recount** any discrepancy immediately (blind, second counter).
3. **Investigate** confirmed variances: trace last known movement, custody, and audit log.
4. **Classify:** paperwork error, misplacement, mis-set, or genuine loss/shrinkage.
5. **Escalate** genuine unexplained loss of a high-value item **immediately** to Operations lead and Finance/Compliance; preserve CCTV and logs.
6. **Adjust** the record only with sign-off (dual approval for high value). Never quietly "true up."
7. **Document** root cause and corrective action; feed patterns into shrinkage prevention (§8).

## 6. Consignment & memo goods

Memo/consignment stones are held by Palencia but owned by the supplier until sold or purchased.

### 6.1 Handling rules

- **Distinct flagging:** marked `Consignment/Memo` in the system with the owning supplier, memo number, agreed value, and return-by date.
- **Segregated storage:** physically separate from owned stock.
- **Same controls:** subject to the same security, counting, and cert-traceability as owned stock.
- **Return discipline:** track memo aging; return or purchase before the memo period lapses. Overdue memo is a liability, not free inventory.
- **On sale:** convert to a purchase (raise PO / SoW check per [Sourcing & Procurement](sourcing-and-procurement.md)) at the point of sale, then fulfill.
- **Reconciliation:** memo goods are counted in every cycle count and full audit and reconciled to the supplier's memo statement.

`TODO: [Confirm standard memo terms and approval authority for taking goods on memo.]`

## 7. Inventory insurance

- All inventory — owned, consignment/memo (per agreement), and customer property in our care — must be covered by an appropriate policy (e.g., a jewelers block policy). `TODO: [Confirm insurer, policy type, and coverage limits.]`
- **Valuation basis** for insured values kept current from cost + valuation records; reconciled at each full audit.
- **Location & transit:** confirm coverage terms for on-premises, off-premises, and in-transit goods; goods in transit also governed by [Shipping & Insurance](shipping-and-insurance.md).
- **Conditions of cover:** meet the insurer's required safe rating, alarm, and dual-control conditions — a claim can be denied if conditions weren't met, so §4 controls are also insurance compliance.
- **Renewal:** full audit and valuation update feed the annual renewal.

## 8. Shrinkage prevention

Shrinkage in fine jewelry is rarely volume theft; it's a single high-value item slipping through custody gaps. Controls:

- [ ] Cert-match counts (not just "a stone is present") to defeat swaps
- [ ] Dual control on high-value custody, counts, and packing
- [ ] Separation of duties: buy/receive vs. count/reconcile
- [ ] Blind cycle counts on a rolling schedule
- [ ] End-of-day secure-down, signed
- [ ] CCTV over vault, bench, receiving, and packing
- [ ] Immediate investigation of any variance — no "it'll turn up"
- [ ] Access list and combinations reviewed and updated on personnel change
- [ ] Quarantine and consignment segregated to prevent commingling errors
- [ ] Independent full audit reconciled to the ledger

## 9. Key controls summary

| Control | Owner | Frequency |
|---|---|---|
| Cert ↔ item link created | Receiving | Per receipt |
| End-of-day secure-down | Operations | Daily |
| Cycle count (high value) | Operations (dual control) | `TODO: [weekly]` |
| Melee/lot weight count | Operations | `TODO: [monthly]` |
| Full physical audit | Finance/independent | `TODO: [quarterly/annually]` |
| Ledger reconciliation | Finance | Per audit |
| Access list review | Operations | On change / `TODO` |
| Insurance valuation update | Finance | Annually + at audit |

---

## Related documents
- [Financial Controls](../08-finance/financial-controls.md)
- [Shipping & Insurance](shipping-and-insurance.md)
- [Sourcing & Procurement](sourcing-and-procurement.md)
- [Quality Control](quality-control.md)
- [Vendor Management](vendor-management.md)
- [Documentation Home](../../README.md)
