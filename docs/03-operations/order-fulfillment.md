# Order Fulfillment

> The end-to-end standard operating procedure for turning an online order into a certified piece safely delivered to the customer's door — from checkout to post-delivery follow-up.

| | |
|---|---|
| **Owner** | Operations & Fulfillment |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Purpose & scope

This document is the single source of truth for how Palencia Diamonds fulfills an order. It covers every catalog and custom order from the moment a customer completes checkout on www.palenciadiamonds.com to the post-delivery follow-up.

It exists to guarantee three things on every order:

1. **Accuracy.** The customer receives exactly the piece they bought — correct stone, correct grade, correct metal, correct size, correct engraving.
2. **Safety.** A high-value, uninsured-risk product is never exposed. Every hand-off is tracked, and every shipment is insured and signature-confirmed.
3. **Care.** The customer is informed at every stage and treated as if theirs is the only order we have.

> This is an operational reference, **not legal advice.** Payment, fraud, and AML/KYC steps must be confirmed with Finance & Compliance and qualified counsel for the jurisdictions we serve.

## 2. Roles in fulfillment

| Role | Responsibility in this flow |
|---|---|
| **Order Coordinator** | Owns the order record end to end; verification, customer comms, exception handling |
| **Finance / Compliance** | Payment capture, fraud screening, AML/KYC on high-value orders |
| **Merchandising / Sourcing** | Allocates in-stock stones or sources certified stones from vetted suppliers |
| **Production / Bench** | Setting, sizing, engraving, finishing |
| **Quality Control (QC)** | Independent inspection gate before packaging — see [Quality Control](quality-control.md) |
| **Packaging & Dispatch** | Presentation packaging, insured labeling, carrier hand-off |
| **Customer Experience (CX)** | Proactive updates, delivery confirmation, follow-up — see [Customer Experience Standards](../04-sales-cx/customer-experience-standards.md) |

## 3. Order classification (do this first)

Every order is triaged at intake because the path differs by type and value.

| Type | Definition | Typical lead time |
|---|---|---|
| **In-stock catalog** | Piece or components on hand; set/size only | 3–7 business days to dispatch |
| **Made-to-order catalog** | Cataloged design, stone sourced/set to order | 10–15 business days to dispatch |
| **Custom / bespoke** | Customer-specified design — routes to [Custom Design Workflow](custom-design-workflow.md) | Per commission schedule |
| **High-value order** | Order value ≥ `[bracketed] TODO: high-value threshold, e.g. $10,000` | Adds enhanced screening (Stage 2) |

> **Rule:** A custom order follows the [Custom Design Workflow](custom-design-workflow.md) through final approval, then **re-enters this document at Stage 7 (QC gate)** for packaging and dispatch.

## 4. Stage map (owners & SLA targets)

SLA clock starts when the order reaches the stage's **ready** state (prior stage complete). Business days, excluding weekends and holidays.

| # | Stage | Owner | SLA target | Gate to advance |
|---|---|---|---|---|
| 1 | Order intake & verification | Order Coordinator | Within 4 business hours of order | Details confirmed, no data mismatch |
| 2 | Payment & fraud / AML screening | Finance / Compliance | Same business day; high-value ≤ 2 business days | Payment captured, screen cleared |
| 3 | Allocation / sourcing of stone | Merchandising / Sourcing | In-stock same day; sourced ≤ 5 business days | Certified stone matched to order |
| 4 | Production / setting hand-off | Production / Bench | Setting complete ≤ 5 business days | Piece set, sized, cleaned |
| 5 | Engraving / personalization | Production / Bench | ≤ 2 business days | Engraving verified against order |
| 6 | (Custom only) design build | See custom workflow | Per commission | Final customer approval |
| 7 | **QC gate** | Quality Control | ≤ 1 business day | Pass per [Quality Control](quality-control.md) |
| 8 | Packaging & presentation | Packaging & Dispatch | ≤ 1 business day | Complete package checklist |
| 9 | Insured labeling & dispatch | Packaging & Dispatch | Same day as packaging | Insured, signature-confirmed label |
| 10 | Tracking & customer comms | CX | Within 1 hour of dispatch | Tracking sent to customer |
| 11 | Delivery confirmation | CX | Day of delivery | Signature captured |
| 12 | Post-delivery follow-up | CX | 3–5 days after delivery | Follow-up sent, logged |

**Target end-to-end:** in-stock 3–7 business days; made-to-order 10–15 business days from cleared payment to dispatch. Communicate the specific promise date at Stage 1.

---

## 5. Stage 1 — Order intake & verification

**Goal:** Confirm we can fulfill exactly what was ordered before any money or material moves.

1. Order lands in the order management system; Order Coordinator opens the record.
2. Verify line items against the catalog: design, metal (yellow / white / rose gold or platinum), center-stone spec (carat, cut, color, clarity), and the **GIA / IGI report number** if a specific stone was selected.
3. Confirm **ring/chain/bracelet size**. If size is missing or ambiguous, hold and request it — never guess.
4. Verify engraving text and font exactly as submitted (see Stage 5). Confirm character count is within the design's limit.
5. Validate the shipping address (deliverable, complete) and flag PO boxes or freight-forwarders (not permitted for insured high-value shipping — see [Shipping & Insurance](shipping-and-insurance.md)).
6. Set and record the **customer promise date** based on order classification (Section 3).

**Intake checklist**

- [ ] Design and SKU confirmed
- [ ] Metal and finish confirmed
- [ ] Stone spec (4Cs) and certificate reference confirmed
- [ ] Size captured (or held pending customer)
- [ ] Engraving text/font confirmed and within limit
- [ ] Shipping address deliverable and eligible for insured carrier
- [ ] Promise date set and recorded

## 6. Stage 2 — Payment & fraud / AML screening

**Goal:** Capture funds cleanly and protect against fraud and money-laundering risk without adding friction for legitimate customers.

1. Confirm authorization and capture per Finance's payment SOP. Do not begin sourcing or production until payment has cleared.
2. Run the standard fraud screen: AVS/CVV match, billing-vs-shipping consistency, device/velocity signals, and any gateway risk score.
3. **High-value orders** (≥ threshold in Section 3) receive enhanced review:
   - Manual review by Finance / Compliance.
   - Identity and address verification proportionate to risk.
   - AML/KYC checks consistent with **FinCEN rules for dealers in precious stones, metals, and jewels** and applicable sanctions screening. `[bracketed] TODO: confirm current KYC thresholds and record-keeping requirements with counsel.`
4. On any red flag, place the order on **Fraud Hold**, notify the customer neutrally (do not disclose screening detail), and escalate to Finance / Compliance.
5. On clearance, timestamp the record; the SLA clock for Stage 3 starts here.

## 7. Stage 3 — Allocation / sourcing of the stone

**Goal:** Match a specific certified stone to the order.

1. **In-stock:** Allocate the reserved stone; confirm its GIA/IGI report matches the order spec exactly (report number, carat, cut, color, clarity). Update [Inventory Management](inventory-management.md) to reserved/allocated.
2. **Sourced:** Merchandising requests the stone from a vetted supplier against the order spec.
   - Require the independent grading report and the supplier's **conflict-free / Kimberley Process** and RJC warranties on receipt.
   - Inspect the stone against its certificate on arrival before accepting.
3. Reconcile the physical stone's laser inscription (where present) to the certificate number.
4. Record the allocated certificate number on the order — this is the number that will ship with the piece.

> **Precision gate:** If the received stone does not match its certificate, or the certificate does not match the order, stop. Do not set a mismatched stone.

## 8. Stage 4 — Production / setting hand-off

**Goal:** Hand-set the certified stone into the correct piece, correctly sized.

1. Production receives the allocated stone, mounting, and order spec.
2. Confirm metal, finish, and setting style against the order.
3. Hand-set the stone; size the piece to the captured size (Stage 1).
4. Confirm **hallmarking / metal stamp** is present and correct for the metal and jurisdiction.
5. Clean and prepare the piece for engraving (if any) and QC.

## 9. Stage 5 — Engraving & personalization

**Goal:** Apply personalization exactly as ordered — a common and unforgiving error point.

1. Pull the engraving text and font from the order record (never from memory or a verbal note).
2. Read the text back character-for-character, including spacing, punctuation, and case.
3. Confirm placement (inside band, back of pendant, etc.) matches the design.
4. Engrave, then verify the finished engraving against the order **twice** — once by the bench, once at QC (Stage 7).

> Engraved and personalized pieces are typically **final sale**; a personalization error is our cost and our re-make. Verify before you cut.

## 10. Stage 6 — Custom build (custom orders only)

Custom orders complete CAD, approval, casting, setting, and finishing under the [Custom Design Workflow](custom-design-workflow.md). On **final customer approval** there, the piece re-enters this document at Stage 7.

## 11. Stage 7 — Quality Control gate

**Goal:** An independent inspector confirms the piece is exactly right before it can be packaged. QC is a hard gate — nothing ships without a pass. See [Quality Control](quality-control.md) for the full inspection protocol.

**QC confirms, at minimum:**

- [ ] Stone matches its GIA/IGI certificate (carat, cut, color, clarity; inscription where present)
- [ ] Setting secure; no loose stones, sharp edges, or porosity
- [ ] Metal, finish, and hallmark correct
- [ ] Size correct to specification
- [ ] Engraving correct character-for-character and correctly placed
- [ ] Piece clean, polished, and free of bench marks
- [ ] Matches the order and any approved custom renders

On **fail**, QC routes back to Production with documented reasons; the order is not advanced and the customer is proactively updated if the promise date is at risk. On **pass**, QC signs off and the certificate + appraisal are prepared for packaging.

## 12. Stage 8 — Packaging & presentation

**Goal:** Present the piece beautifully and completely, and prepare it for secure transit.

**Every shipment includes:**

| Item | Notes |
|---|---|
| The piece | Secured in the presentation box |
| **Presentation box** | Branded ring/jewelry box, protected for transit |
| **GIA / IGI grading report** | The certificate matching the shipped stone |
| **Appraisal** | Insurance/valuation document | `[bracketed] TODO: confirm appraisal provider and standard format` |
| **Care card** | Cleaning, wear, and warranty guidance |
| **Warranty / returns insert** | Return window, resizing, and manufacturing-defect coverage — see [Returns, Warranty & Resizing](../04-sales-cx/returns-warranty-resizing.md) |
| **Packing slip** | No pricing on gift orders when requested |

**Packaging checklist**

- [ ] Correct piece placed and secured in presentation box
- [ ] Certificate number on paperwork matches the shipped stone
- [ ] Appraisal enclosed
- [ ] Care card + warranty/returns insert enclosed
- [ ] Gift/pricing preferences honored
- [ ] Inner box protected; no rattle or movement
- [ ] Discreet outer packaging (no brand or "jewelry" markings) — see [Shipping & Insurance](shipping-and-insurance.md)

## 13. Stage 9 — Insured labeling & dispatch

**Goal:** Ship on a jewelry-appropriate insured, signature-confirmed service with declared value covering the full order.

1. Select the carrier/service per [Shipping & Insurance](shipping-and-insurance.md).
2. Declare value for the **full replacement value** of the piece.
3. Require **signature confirmation** (adult signature for high-value orders).
4. Use **discreet packaging** — no branding or content hints on the exterior.
5. Record tracking number and insured value on the order.
6. Hand to carrier with scan/receipt; never leave a shipment unattended for pickup.

## 14. Stage 10–11 — Tracking, comms & delivery confirmation

1. Within 1 hour of dispatch, CX sends the customer the tracking number, carrier, expected delivery date, and the **signature-required** notice.
2. Set proactive checkpoints: dispatched, out for delivery, delivered.
3. Coordinate with the customer if they need to redirect to a hold-for-pickup or secure location (see [Shipping & Insurance](shipping-and-insurance.md)).
4. On delivery, confirm signature capture. File the delivery/signature record with the order.
5. If tracking stalls or a delivery exception occurs, CX opens a carrier trace **immediately** and begins the claims process if needed (see [Shipping & Insurance](shipping-and-insurance.md)).

## 15. Stage 12 — Post-delivery follow-up

1. 3–5 days after delivery, CX sends a warm follow-up: confirm it arrived safely, that they're delighted, and remind them of resizing, warranty, and care support.
2. Invite a review and offer help with anything (resizing, questions about the certificate, care).
3. Log the outcome. Route any issue to [Returns, Warranty & Resizing](../04-sales-cx/returns-warranty-resizing.md).
4. Close the order record once follow-up is complete and no issue is open.

---

## 16. Exceptions & holds

| Situation | Action |
|---|---|
| Missing/ambiguous size | Hold at Stage 1; request from customer; do not guess |
| Fraud / AML flag | Fraud Hold at Stage 2; escalate to Finance / Compliance |
| Stone ≠ certificate | Stop at Stage 3/7; do not set or ship; re-source |
| QC fail | Return to Production; update customer if promise date at risk |
| Engraving error | Re-make at our cost; notify customer with revised date |
| Delivery exception / lost | Immediate carrier trace; open insured claim per shipping doc |
| Promise date at risk | Proactive CX outreach **before** the date, never after |

## 17. Metrics we watch

- **On-time dispatch rate** (dispatched by promise date)
- **QC first-pass rate** (pass without rework)
- **Order accuracy rate** (no post-delivery corrections)
- **Delivery success rate** (delivered & signed, first attempt)
- **Claims rate** (lost/damaged/stolen per shipments)
- `[bracketed] TODO: confirm target thresholds for each metric with Operations leadership.`

---

## Related documents
- [Quality Control](quality-control.md)
- [Shipping & Insurance](shipping-and-insurance.md)
- [Custom Design Workflow](custom-design-workflow.md)
- [Customer Experience Standards](../04-sales-cx/customer-experience-standards.md)
- [Returns, Warranty & Resizing](../04-sales-cx/returns-warranty-resizing.md)
- [Inventory Management](inventory-management.md)
- [Documentation Home](../../README.md)
