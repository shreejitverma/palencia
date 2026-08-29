# Lifecycle Marketing, Retention & High-Touch Clienteling Playbook

> The retention engine and lifetime value (LTV) framework for fine jewelry — turning single engagement ring buyers into lifelong repeat clients and vocal brand advocates across wedding bands, anniversaries, and milestones.

| | |
|---|---|
| **Owner** | Lifecycle Marketing & CRM Clienteling |
| **Last reviewed** | 2026-08-29 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. The High-AOV Lifetime Value (LTV) Math

In traditional e-commerce, LTV is built on 30-day consumable repeat purchases. In certified fine jewelry, LTV follows a **multi-year milestone trajectory**:

```
                       THE 10-YEAR FINE JEWELRY REVENUE CURVE
                       
  Year 0               Year 1               Year 3             Year 5             Year 10
 ───┼────────────────────┼────────────────────┼──────────────────┼──────────────────┼───►
    │                    │                    │                  │                  │
    ▼                    ▼                    ▼                  ▼                  ▼
 [ ENGAGEMENT RING ]  [ WEDDING BANDS ]    [ 1ST ANNIVERSARY] [ 5-YEAR UPGRADE ] [ 10-YEAR TENNIS
   AOV: $4,500          AOV: $1,800          Diamond Earrings   Center Stone       BRACELET ]
   (Initial Acq.)       (40% Attach Rate)    AOV: $1,200        AOV: $3,500        AOV: $5,500
```

### Cumulative Customer Lifetime Value Progression:
- **Day 0 (Initial Ring Purchase)**: $\$4,500$ Revenue ($\text{CAC} = \$450$, $\text{ROAS} = 10\times$).
- **Day 180 (Matching Wedding Bands)**: $+\$1,800$ ($\text{Zero Paid CAC} \to \text{Blended ROAS} = 14\times$).
- **Year 3–5 (Milestones & Upgrades)**: $+\$4,700$ ($\text{Lifetime LTV} = \$11,000$, $\text{LTV:CAC} > 24:1$).

---

## 2. The 6 Automated Lifecycle Revenue Flows

```
┌──────────────────────────────┬──────────────────────────────┬──────────────────────────────┐
│ Flow Name                    │ Trigger & Timing             │ Core Psychological Angle     │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **1. Welcome & 4Cs           │ User subscribes or completes │ Removes buying anxiety;      │
│ Education Series**           │ ring quiz (Days 0–14)        │ teaches 4Cs & honesty story. │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **2. High-Intent Abandoned   │ Added ring to cart / viewed  │ Reverses risk; offers        │
│ Checkout Concierge**         │ high-value diamond (1h & 24h)│ live gemologist chat / CAD.  │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **3. Post-Delivery Care &    │ 3 days after insured package │ Builds delight; prompts ring │
│ Review Solicitation**        │ delivery confirmation        │ sizing check & honest review.│
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **4. Wedding Band Bridge     │ 90 to 180 days post-delivery │ Introduces matching bands    │
│ (The Couple Transition)**    │ of engagement ring           │ designed for their setting.  │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **5. Annual Anniversary &    │ 30 days prior to recorded    │ Timely, curated milestone    │
│ Milestone Countdown**        │ anniversary / birthday date  │ gifts (earrings, pendants).  │
├──────────────────────────────┼──────────────────────────────┼──────────────────────────────┤
│ **6. Diamond Trade-Up &      │ 3 years post-purchase of     │ Offers 100% credit toward a  │
│ Upgrade Equity Invitation**  │ certified center diamond     │ larger diamond upgrade.      │
└──────────────────────────────┴──────────────────────────────┴──────────────────────────────┘
```

---

## 3. High-Touch Clienteling: The 1-on-1 VIP Concierge

For transactions over **$5,000**, automated email is supplemented by **personalized human clienteling** via private SMS and WhatsApp Business:

```
                      HIGH-TOUCH CLIENTELING WORKFLOW
                      
 [ Lead: Quiz Score > $5k OR Cart Value > $5k ]
                        │
                        ▼
 ┌─────────────────────────────────────────────────────────────┐
 │ DEDICATED GEMOLOGIST OUTREACH (Within 15 Minutes)           │
 │ • Sends personalized 15-second video loupe inspection of    │
 │   the 2 diamonds the customer was comparing online.         │
 │ • "Hi Alex, here is stone A vs stone B under 40x zoom..."   │
 └──────────────────────────────┬──────────────────────────────┘
                                │
                                ▼
 ┌─────────────────────────────────────────────────────────────┐
 │ 3D CAD RENDERING & VIRTUAL CONSULTATION                     │
 │ • Customer receives private link to view custom setting CAD │
 │ • Option to book 15-minute Google Meet screen-share.        │
 └─────────────────────────────────────────────────────────────┘
```

---

## 4. Email & SMS Deliverability Engineering

To ensure 99%+ inbox placement across Gmail, Apple Mail, and Yahoo:

```
┌──────────────────────────────────────┬────────────────────────────────────────────────────────┐
│ Technical Infrastructure Standard    │ Specification & Configuration                          │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **DMARC Policy Enforcement**         │ `v=DMARC1; p=reject; rua=mailto:dmarc@palencia.com`     │
│                                      │ Prevents brand spoofing and phishing.                  │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **BIMI (Brand Indicators)**          │ Verified Mark Certificate (VMC) rendering official     │
│                                      │ Palencia logo badge in mobile inboxes.                 │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **Algorithmic Sunset Policy**        │ Automatically suppress marketing emails to users who   │
│                                      │ have not engaged in 60 days to protect sender score.   │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **SMS Quiet Hours & TCPA Guard**     │ Enforce zero marketing texts between 8:00 PM and       │
│                                      │ 9:00 AM recipient local time. Explicit double opt-in.  │
└──────────────────────────────────────┴────────────────────────────────────────────────────────┘
```

---

## Related documents

- [Ad Tech & Paid Media Pipeline](ad-tech-and-paid-media-pipeline.md)
- [Creative Strategy & Briefing](creative-strategy-and-briefing.md)
- [Landing Page & CRO Playbook](landing-page-and-cro-playbook.md)
- [Marketing Strategy](marketing-strategy.md)
- [CRM & Clienteling](../04-sales-cx/crm-and-clienteling.md)
- [Documentation Home](../../README.md)
