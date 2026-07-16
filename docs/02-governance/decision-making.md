# Decision-Making

> How decisions get made, who gets to make them, and how they're communicated — so Palencia Diamonds moves fast without breaking trust.

| | |
|---|---|
| **Owner** | Office of the Founder / CEO |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Annually |
| **Status** | Active |

---

## 1. Principles

- **Push decisions to the person closest to the customer and the facts.** Escalate for judgment, not for permission you already have.
- **One accountable owner per decision.** Advice can come from many; the call belongs to one (see the RACI in [Roles & Responsibilities](roles-and-responsibilities.md#raci-matrix)).
- **Values break ties.** When a decision is genuinely close, honesty and the customer's moment win over short-term margin. See [Mission, Vision & Values](../00-company/mission-vision-values.md).
- **Reversible and cheap? Decide fast.** Irreversible or expensive? Slow down, consult, and record.
- **Write down the decisions that matter** so we can learn from them.

---

## 2. Decision rights framework

Two things determine who decides: **how much it costs** and **how much is at stake if it's wrong** (impact/reversibility). A cheap, reversible decision is made locally; an expensive or irreversible one rises.

### 2.4 Financial authority thresholds

`TODO:` Confirm every dollar threshold below with Finance & the CEO; these are placeholders to be ratified.

| Decision type | Approver | Threshold `TODO` |
|---|---|---|
| Routine operating spend | Department Lead | up to `[$X]` |
| Stone / inventory purchase | Head of Merchandising | up to `[$X]` per stone/lot |
| Stone / inventory purchase (large) | CEO + Finance | above `[$X]` |
| Customer refund / goodwill credit | CX Specialist | up to `[$X]` |
| Customer refund / goodwill credit (large) | Head of Sales & CX | up to `[$X]`; above → CEO |
| Custom-commission quote & terms | Head of Sales & CX | standard terms; non-standard → CEO |
| Supplier onboarding | Head of Merchandising + Finance/Compliance | all (due diligence required) |
| Pricing / discount policy change | CEO + Finance | any |
| Marketing campaign budget | Head of Marketing | up to `[$X]`; above → CEO |
| Capital expenditure | CEO | above `[$X]` → Owners/Board `TODO` |
| Hiring (budgeted role) | Department Lead + HR | all |
| Hiring (new/unbudgeted role) | CEO | all |
| Compensation changes | HR + CEO | all |

### 2.5 Impact / reversibility ladder

| Decision class | Description | Who decides | Record? |
|---|---|---|---|
| **Type 1 — one-way door** | Costly or hard to reverse (new supplier program, pricing policy, brand direction, key hire) | CEO with relevant leads | Yes — decision record |
| **Type 2 — two-way door** | Reversible, low cost (a campaign test, a service gesture, a process tweak) | Owning role, no escalation | Only if useful |
| **Values-sensitive** | Any decision touching honesty, sourcing ethics, customer trust, or safety | Owning role **plus** Finance & Compliance; CEO if unresolved | Yes |

**Hard stops that no threshold overrides:**

- **QC hold** — the QC Lead can stop any shipment; no one overrides it for a deadline. See [Quality Control](../03-operations/quality-control.md).
- **Compliance pause** — Finance & Compliance can pause any transaction failing due diligence/AML until resolved. See [Code of Conduct §9](code-of-conduct.md).

---

## 3. Who decides what (quick reference)

| Domain | Accountable role |
|---|---|
| Strategy, annual plan, budget | CEO |
| Assortment & sourcing | Head of Merchandising |
| Stone verification & valuation | Gemologist |
| Craftsmanship & production schedule | Master Jeweler |
| Ship / hold quality gate | QC Lead |
| Customer service standards & resolutions | Head of Sales & CX |
| Brand, campaigns, claims | Head of Marketing |
| Fulfillment, inventory, logistics | Operations Manager |
| Pricing governance, controls, compliance | Finance & Compliance Officer |
| People, comp, policy | People / HR Lead |

Full detail in [Roles & Responsibilities](roles-and-responsibilities.md).

---

## 4. Decision-record (DR) template

Use a lightweight decision record for every **Type 1** and **values-sensitive** decision. Keep it to one screen. Store in `TODO: [decision log location — e.g., /docs/02-governance/decisions/ or shared drive]`.

```markdown
# DR-[YYYY]-[NNN]: [Short title]

- **Date:** YYYY-MM-DD
- **Owner (accountable):** [role / name]
- **Consulted:** [roles]
- **Class:** Type 1 / Values-sensitive
- **Status:** Proposed / Decided / Superseded by DR-___

## Context
What situation forced a decision? What's at stake?

## Options considered
1. Option A — pros / cons
2. Option B — pros / cons

## Decision
What we chose, and the one-line reason (tie-broken by which value, if applicable).

## Consequences
What changes, what we'll watch, and when we'll review it.

## Communication
Who was informed, where, and by when.
```

`TODO:` Confirm the decision-log location and numbering owner (suggest: Operations/Knowledge Management).

---

## 5. Meeting cadence

Meetings exist to make and communicate decisions — not to replace them. Every recurring meeting has an owner, a purpose, and a default output.

| Cadence | Meeting | Owner | Who | Purpose & output |
|---|---|---|---|---|
| **Daily** | Standup (15 min) | Rotating / Ops | Whole team or per-team | Today's priorities, blockers, orders needing attention. Output: unblocked day. |
| **Weekly** | Operations review | Operations Manager | Dept leads | Orders, production queue, QC holds, fulfillment, service issues. Output: this week's commitments. |
| **Monthly** | Business review (MBR) | CEO + Finance | Leadership | KPIs vs. plan, financials, sourcing/compliance status, escalations. Output: course corrections, ratified Type 1 decisions. |
| **Quarterly** | Strategy review | CEO | Leadership (+ Owners `TODO`) | Strategy, roadmap, budget, org changes, values check-in. Output: quarterly priorities, decision records. |
| **As needed** | Decision / incident huddle | Decision owner | Only those needed | Resolve a specific Type 1 or urgent issue. Output: a decision record. |

`TODO:` Confirm meeting days/times and the standup format (async vs. live) for a distributed, online-first team.

---

## 6. Escalation paths

Escalate when a decision is above your authority, blocked, values-sensitive, or genuinely close.

| Trigger | Escalate to | Timeframe |
|---|---|---|
| Above your financial threshold | The next approver in §2.4 | Before committing |
| QC hold vs. a promised deadline | Master Jeweler → CEO (QC hold stands until resolved) | Same day |
| Compliance/sourcing red flag | Finance & Compliance Officer → CEO | Immediately |
| Customer issue beyond service policy | Head of Sales & CX → CEO | Within 1 business day |
| Ethics / Code of Conduct concern | HR or Finance & Compliance → CEO; or confidential channel | Immediately — see [Code of Conduct §11](code-of-conduct.md) |
| Cross-department deadlock | Shared manager; if none, CEO | Within 1 business day |
| Security / loss / suspected theft | Operations + Finance & Compliance → CEO | Immediately |

**Rule of thumb:** if a decision could damage customer trust or the Palencia name, escalate early. We would always rather be asked.

---

## 7. Communication norms

How decisions travel once they're made:

- **Close the loop.** Whoever makes a decision tells everyone it affects — including those who raised the concern.
- **Right channel for the message:**
  - `TODO: [chat tool]` — quick, reversible, day-to-day.
  - Email / decision log — Type 1 and values-sensitive decisions, and anything needing a durable record.
  - Meetings — when discussion or alignment is genuinely needed, not for one-way updates.
- **Default to transparency.** Share the *why*, not just the *what*. Exceptions: confidential HR, customer data, and sensitive commercial terms.
- **Disagree and commit.** Voice dissent before the decision; once it's made and recorded, we move together. If new facts appear, reopen it with a decision record.
- **No decision by silence.** If a decision needs a call and no one owns it, name an owner — don't let it drift.
- **Write it down once, link to it many times.** Decisions of record live in the decision log; other docs link to them.

---

## 8. Keeping this current

- Owned by the CEO; reviewed annually and whenever thresholds, cadence, or the org materially change (see [Organizational Structure](organizational-structure.md)).
- Threshold and cadence `TODO`s must be ratified with Finance before this document is treated as binding.

---

## Related documents
- [Organizational Structure](organizational-structure.md)
- [Roles & Responsibilities](roles-and-responsibilities.md)
- [Code of Conduct](code-of-conduct.md)
- [Mission, Vision & Values](../00-company/mission-vision-values.md)
- [Company Overview](../00-company/company-overview.md)
- [Quality Control](../03-operations/quality-control.md)
- [Pricing Strategy](../08-finance/pricing-strategy.md)
- [Documentation Home](../../README.md)
