# Facebook & Meta Ads Playbook

> The end-to-end Facebook strategy for Palencia Diamonds - the organic trust layer plus the full Meta Ads architecture (pixel/CAPI, catalog, campaign structure, audiences, creative, budgets, and measurement) that powers paid across both Facebook and Instagram.

| | |
|---|---|
| **Owner** | Marketing & Brand (Growth / Performance) |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Role in the funnel

Facebook plays two distinct roles:

| Role | What it does | Funnel stage |
|---|---|---|
| **Organic page = trust ledger** | The page validates legitimacy: reviews/recommendations, history, responsiveness, real business details. Older gift buyers and the parents/friends a ring buyer consults still check Facebook | Consideration |
| **Meta Ads = the paid engine** | Ads Manager runs prospecting and retargeting across Facebook, Instagram, and Audience Network from one account. This is our primary paid-social system for demand creation and long-cycle retargeting | Awareness → Purchase |

This document owns the **Meta Ads architecture** for the whole company; the [Instagram Playbook](instagram.md) references it for Instagram placements.

## 2. Why Facebook matters for a diamond brand

- **Gift buyers and older self-purchasers** (anniversary, milestone) index heavily on Facebook - segments underserved by TikTok.
- A ring purchase is often a **family-consulted decision**; the people consulted frequently vet the jeweler on Facebook.
- Meta's ad system remains the strongest **demand-creation and retargeting machine** for e-commerce: a months-long consideration cycle needs persistent, sequenced re-engagement, and Meta delivers it efficiently.
- Facebook Reviews/Recommendations are a free trust surface that feeds our social-proof engine.

## 3. Organic page standards

The page's job is to pass a legitimacy check, not to win reach.

| Element | Standard |
|---|---|
| Completeness | Full business info, hours/response expectations, website, brand promise in the About section |
| Reviews / Recommendations | Enabled; every review answered (especially critical ones) within `[2 business days] TODO:`; never gate or suppress - see [Channels & Social §7](../channels-and-social.md#7-reviews--ugc--the-trust-engine) |
| Content cadence | `[2-3 posts/week] TODO:` - cross-post the best Instagram content plus Facebook-native proof (customer stories, milestones, education) |
| Messenger | Same concierge SLA as Instagram DMs (see [Instagram Playbook §5](instagram.md#5-dm-concierge--lead-handling)); enable FAQ auto-greetings that stay honest |
| Groups (optional) | `TODO:` evaluate a "getting engaged" community play only if we can staff it authentically |

## 4. Meta Ads foundations (do these before spending)

| Foundation | Standard |
|---|---|
| **Business Manager hygiene** | Verified business; two-factor on all users; least-privilege roles; backup admin |
| **Pixel + Conversions API (CAPI)** | Both installed and deduplicated. CAPI is mandatory - browser-only tracking undercounts a long, multi-device cycle. Server events for ViewContent, AddToCart, InitiateCheckout, Purchase, Lead |
| **Event match quality** | Pass hashed customer data (email, phone) where consented; target EMQ `[>= 6.0] TODO:` verify |
| **Domain verification & event priority** | Domain verified; Purchase and Lead prioritized |
| **Consent** | Events fire only per our consent framework - see [Data Privacy & Security](../../05-compliance-ethics/data-privacy-and-security.md) |
| **UTM discipline** | Every ad URL carries structured UTMs (source/medium/campaign/content) so GA4 and CRM can stitch the journey |

## 5. Catalog & feed

One product catalog powers Facebook/Instagram Shops, product tags, and dynamic (Advantage+ catalog) ads.

- Feed synced from the e-commerce platform `[daily] TODO:`; accuracy rules match the Google Shopping feed standards in the [Google Ads Playbook](google-ads.md#5-merchant-center--the-shopping-feed).
- Titles lead with what buyers search: shape, carat, metal, style ("1.0 ct Oval Solitaire Engagement Ring, Platinum").
- Certification (GIA/IGI) stated in descriptions; prices always accurate - a wrong price in an ad is a broken promise.
- Suppress items we cannot fulfill; feed disapproval rate kept near zero.

## 6. Campaign architecture

Keep the account **simple and consolidated** - Meta's delivery optimizes best with fewer, bigger ad sets and clear jobs per campaign.

| # | Campaign | Objective | Audience | Budget share (planning) |
|---|---|---|---|---|
| 1 | **Prospecting - Advantage+ / broad** | Purchase (or Lead for guide download) | Broad + Advantage+ audience, `[25-45] TODO:` age floor tests | `[45%] TODO:` |
| 2 | **Prospecting - interest/lookalike tests** | Purchase / Lead | Engaged-shopper interests (newly engaged, wedding planning), 1-5% lookalikes of purchasers and high-LTV customers | `[15%]` |
| 3 | **Retargeting - consideration** | Purchase | Site visitors 30-180d, IG/FB engagers, video viewers 50%+, guide downloaders (excl. purchasers) | `[25%]` |
| 4 | **Retargeting - catalog (DPA)** | Catalog sales | ViewContent/AddToCart 14-30d, dynamic product ads | `[10%]` |
| 5 | **Advocacy / post-purchase** | Engagement / conversions | Purchasers: wedding-band cross-sell (ring buyers 30-180d post-purchase), anniversary re-entry, referral invites | `[5%]` |

**Architecture rules**

- One purchase-optimized prospecting campaign is the workhorse; don't fragment budget across micro-audiences.
- **Exclude purchasers** from acquisition and same-item retargeting; ring buyers flow into the band cross-sell track instead.
- Retargeting windows are long (up to 180 days) because the buying cycle is long - but frequency-cap and sequence the message so persistence never becomes pressure.
- Lead campaigns (buying-guide download) are legitimate conversions for this category - a captured email mid-cycle is a win (see [Marketing Strategy §5](../marketing-strategy.md#5-the-customer-journey--funnel)).

### Retargeting message sequence (consideration track)

| Recency | Message | Asset |
|---|---|---|
| 0-14 days | "Here's what you were looking at" + education | DPA, style guides |
| 14-45 days | Proof: reviews, certification, guarantees | Review creative, GIA/IGI explainer |
| 45-120 days | Confidence: honest pricing, consult offer, financing | Founder/expert video, consult CTA |
| Seasonal windows | Deadline: "order by" dates for gifting peaks | Countdown creative |

## 7. Creative playbook

Creative is the main performance lever in modern Meta - targeting is largely algorithmic.

| Creative type | Job | Notes |
|---|---|---|
| **Short video (9:16)** | Prospecting reach | Hook in 1.5s; craft footage, honest-pricing explainers, proposal stories; captions always on |
| **Review / UGC-style** | Trust at retargeting | Real customers, real testimonials (with consent); screenshot-style review creative outperforms polish |
| **Static + carousel** | Style discovery | Hero photography, style roundups ("5 solitaire settings compared") |
| **Catalog / DPA** | Recency retargeting | Clean feed imagery; overlay certification badge where supported |
| **Partnership ads** | Borrowed trust | Whitelisted creator content with paid-partnership label - see [Instagram Playbook §6](instagram.md#6-influencer--collab-mechanics-on-instagram) |

**Creative rules**

- 3-5 fresh concepts per month into prospecting; kill fatigued ads (CTR decay, frequency > `[3-4] TODO:`) weekly.
- Every claim documentable: grades, prices, service promises. No fake urgency, no countdown timers that reset.
- Angles to rotate: fear-relief ("nervous about overpaying?"), craft proof, certification proof, real proposals, honest trade-offs.
- Brand voice everywhere - warm, plain, precise; see [Voice & Tone](../../01-brand/voice-and-tone.md).

## 8. Budget, bidding & pacing

- **Bidding:** default to lowest-cost (highest volume) on Purchase; introduce cost caps only after stable CPA baselines exist. Lead campaigns bid to a target cost per qualified lead `TODO:` set from funnel math.
- **Budget type:** campaign budget (Advantage campaign budget) on consolidated campaigns; ad-set budgets only for deliberate tests.
- **Learning phase:** aim for `[>= 50] TODO:` optimization events/week per ad set; consolidate if under.
- **Seasonality:** ramp budgets 2-4 weeks before peaks (engagement season, Valentine's, Mother's Day, holiday - see [Marketing Strategy §8](../marketing-strategy.md#8-seasonality--the-marketing-calendar)); never cold-start a campaign the week of a peak.
- **Guardrails:** CAC and payback targets from [Marketing Strategy §7](../marketing-strategy.md#7-cac-ltv--payback-thinking); prospecting is allowed a higher CPA than blended because it fills the long-cycle pool.

## 9. Measurement & KPIs

Meta's attributed ROAS **overstates** on retargeting and **understates** demand creation in a long cycle. Read it accordingly.

| Layer | Metric | Use |
|---|---|---|
| Platform | CPA/ROAS (7-day click, 1-day view), CPM, CTR, frequency, thumb-stop rate | In-flight optimization only |
| Blended | MER, blended CAC, new-customer revenue | Weekly truth check - see [Marketing Strategy §9](../marketing-strategy.md#9-measurement--kpis) |
| Incrementality | Geo holdouts or spend-scaling tests `[quarterly] TODO:` | Validates that Meta spend creates sales, not just claims them |
| Lead quality | Guide download → consult → purchase rate by campaign | Prevents optimizing to junk leads |

**Reporting cadence:** weekly pacing/CPA/fatigue review; monthly campaign P&L and creative league table; quarterly incrementality and budget re-allocation.

## 10. Testing framework

| Test type | Method | Cadence |
|---|---|---|
| Creative concepts | 3-5 new concepts/month into prospecting; judge on CPA + hook retention | Monthly |
| Audience | A/B broad vs interest vs lookalike (proper A/B test tool, not eyeballing) | Quarterly |
| Landing page | Ad → category vs guide vs consult page | Quarterly |
| Offer framing | Free insured shipping vs financing vs consult-first (never discount-led by default) | Seasonal |

One variable per test; pre-register the success metric; kill losers fast and write down the learning.

## 11. Compliance & guardrails

- **Meta ad policies for jewelry/personal finance adjacency:** financing claims must be accurate and compliant; no before/after body imagery rules apply to us lightly, but avoid anything implying personal attributes ("since you got engaged...") - Meta prohibits personal-attribute callouts in ad copy.
- No fake scarcity, fabricated reviews, or misleading prices - platform rules and our honesty value align here.
- Special ad category rules do not apply to jewelry, but re-verify if we ever run credit/financing-focused ads `TODO:` legal review of financing ad copy.
- Consent-based data only in custom audiences; honor opt-outs in list uploads - see [Data Privacy & Security](../../05-compliance-ethics/data-privacy-and-security.md).
- Paid partnerships always labeled; creator content rights secured in writing before whitelisting.

## 12. Launch checklist (per campaign)

- [ ] Pixel + CAPI events verified firing and deduplicated on the destination page.
- [ ] Audience exclusions set (purchasers, current customers where relevant).
- [ ] UTMs on every ad URL; naming convention followed.
- [ ] Creative claims audited (grades, prices, service terms all documentable).
- [ ] Landing page matches the ad's promise; mobile experience verified.
- [ ] Budget, bid strategy, and CPA guardrail recorded in the campaign log.
- [ ] Frequency caps / sequencing set on retargeting.

---

## Related documents
- [Instagram Playbook](instagram.md)
- [Google Ads Playbook](google-ads.md)
- [Channels & Social](../channels-and-social.md)
- [Marketing Strategy](../marketing-strategy.md)
- [Data Privacy & Security](../../05-compliance-ethics/data-privacy-and-security.md)
- [CRM & Clienteling](../../04-sales-cx/crm-and-clienteling.md)
