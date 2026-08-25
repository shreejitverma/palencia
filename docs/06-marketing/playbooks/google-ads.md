# Google Ads Playbook

> The end-to-end Google Ads (formerly AdWords) strategy for Palencia Diamonds - search, Shopping and Performance Max, Demand Gen and YouTube campaigns, the Merchant Center feed, bidding, budgets, and measurement - the system that captures the highest-intent diamond demand on the internet.

| | |
|---|---|
| **Owner** | Marketing & Brand (Performance / Growth) |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Role in the funnel

Google Ads is our **demand-capture workhorse**: it meets buyers at the exact moment of expressed intent - "1 carat oval engagement ring platinum" - and it protects the demand every other channel creates.

| Campaign family | Funnel stage | Demand type |
|---|---|---|
| Brand search | Purchase (protect) | Capture |
| Non-brand search | Consideration → Purchase | Capture |
| Shopping / Performance Max | Purchase | Capture |
| Demand Gen / YouTube | Awareness → Consideration | Create |
| Remarketing (RLSA, Demand Gen) | Consideration → Purchase | Nurture |

Per the allocation principles in [Marketing Strategy §6](../marketing-strategy.md#6-budget-allocation-across-channels): **protect capture first** - never let demand created by social, influencer, and content leak to a competitor's ad on the last search.

## 2. Account architecture

Keep the account consolidated enough for smart bidding to learn, segmented enough to control message and budget by intent.

| # | Campaign | Purpose | Budget share (planning) |
|---|---|---|---|
| 1 | **Brand search** | Own every branded query ("palencia diamonds", "palencia reviews"); cheapest, highest-converting clicks; controls the message above organic | `[5%] TODO:` |
| 2 | **Non-brand search - engagement rings** | Core commercial terms by style, shape, metal, carat | `[30%]` |
| 3 | **Non-brand search - fine jewelry & gifts** | Studs, tennis bracelets, pendants, occasion terms ("anniversary gift diamond") | `[15%]` |
| 4 | **Shopping / Performance Max** | Feed-driven capture at the moment of visual comparison | `[30%]` |
| 5 | **Demand Gen + YouTube** | Demand creation to in-market/life-event audiences; video strategy in the [YouTube Playbook](youtube.md#5-youtube-advertising) | `[15%]` |
| 6 | **Remarketing** | RLSA bid adjustments + Demand Gen re-engagement of the long cycle | `[5%]` |

**Structure rules**

- Search ad groups are **tightly themed** (one intent per ad group: "oval engagement rings" ≠ "oval lab diamond rings") so ads and landing pages match the query exactly.
- Performance Max runs **asset groups per category** (engagement rings, bands, studs, tennis, pendants) with tailored creative and audience signals; brand terms excluded from PMax so it cannot cannibalize campaign 1.
- One conversion goal set per campaign purpose: Purchase for capture campaigns; qualified Lead (guide download / consult booking) allowed for Demand Gen.

## 3. Keyword strategy

### 3.1 The intent ladder

| Intent tier | Example queries | Action |
|---|---|---|
| **Transactional (bid to win)** | "1 carat solitaire engagement ring", "platinum diamond studs", "oval halo ring buy" | Exact/phrase, highest bids, product/category landing pages |
| **Commercial (bid to compete)** | "best place to buy engagement ring online", "GIA certified engagement rings", "lab grown vs natural ring price" | Comparison and guide landing pages with strong trust proof |
| **Informational (mostly don't bid)** | "what are the 4Cs", "how to clean a diamond ring" | Serve organically via [Content & SEO](../content-and-seo.md); bid only where content + capture economics prove out |
| **Branded** | "palencia diamonds", "+reviews", "+returns" | Always covered by campaign 1 |
| **Competitor** | Competitor brand names | `TODO:` decide policy - typically low quality score and high CPC; test cautiously if at all, never in ad copy |

### 3.2 Match types & negatives

- Start exact + phrase on money terms; add broad match only paired with smart bidding and a mature negative list.
- **Negative lists are maintained weekly** (this is where budget dies): free, cheap, fake, CZ, moissanite (unless stocked), rental, repair, appraisal-only, jobs, wholesale, DIY, and every irrelevant celebrity-ring news query. Shared negative lists across campaigns.
- Search-terms report reviewed weekly; every irrelevant paid click becomes a negative.

## 4. Ads & landing pages

### 4.1 Ad copy standard (responsive search ads)

Every ad leads with the fear we relieve and the proof - per [Marketing Strategy §3](../marketing-strategy.md#3-positioning-driven-messaging):

- Headlines rotate our three pillars: **GIA/IGI-certified** | **handcrafted** | **honest, transparent prices**, plus service proof: free insured shipping, complimentary resizing, financing `TODO:` confirm financing wording with compliance.
- Include the query's own words (dynamic relevance without dishonest gimmicks); pin a brand headline where control matters.
- **Assets (extensions) fully built:** sitelinks (Reviews, Buying Guide, Financing, Returns & Warranty, Custom Design), callouts (Free Insured Shipping, GIA & IGI Certified, Signature Delivery), structured snippets (styles, metals), price and promotion assets used honestly, seller-rating eligibility maintained via review volume.

### 4.2 Landing-page rules

- Ad → page message match is absolute: a "platinum oval solitaire" click lands on that filtered category or product page, never the homepage.
- Every paid landing page shows: certification badge/report access, reviews, price transparency, shipping/returns promise - above the fold on mobile.
- Page speed per the Core Web Vitals standards in [Content & SEO §5](../content-and-seo.md#5-technical--product-page-seo-for-jewelry-e-commerce) - paid traffic pays twice for slow pages (CPC and conversion).

## 5. Merchant Center & the Shopping feed

The feed is a product in its own right; feed quality is Shopping performance.

| Element | Standard |
|---|---|
| Titles | Lead with what buyers search: shape, carat, style, metal ("1.0 ct Oval Solitaire Engagement Ring - Platinum - GIA Certified") |
| Descriptions | Honest, specific, spec-complete (4Cs, metal, measurements); no supplier boilerplate |
| Identifiers & categories | Correct Google product category (jewelry taxonomy), GTIN/MPN where applicable, item groups for variants (size, metal) |
| Images | High-resolution on clean background per Shopping policy; supplemental lifestyle images |
| Price & availability | Always exactly accurate and synced `[daily] TODO:`; mismatches cause disapprovals and broken trust |
| Ratings | Product ratings and seller ratings feeds connected (review program in [Channels & Social §7](../channels-and-social.md#7-reviews--ugc--the-trust-engine)) |
| Disapprovals | Reviewed weekly; kept near zero |
| Structured data | Product/Offer/AggregateRating schema on product pages must match the feed - see [Content & SEO §6](../content-and-seo.md#6-structured-data--rich-results) |

**Free listings:** an accurate feed also earns unpaid Shopping-tab placement - feed hygiene pays twice.

## 6. Bidding & budgets

| Stage | Approach |
|---|---|
| Cold start | Maximize clicks (capped) or manual to gather conversion data; conversion tracking verified first |
| Learning | Maximize conversions / conversion value once `[>= 30-50] TODO:` conversions/month per campaign |
| Mature | Target ROAS on capture campaigns, tuned to the CAC and payback guardrails in [Marketing Strategy §7](../marketing-strategy.md#7-cac-ltv--payback-thinking); tCPA on lead-optimized campaigns |
| High-AOV nuance | Low conversion volume + high order values make smart bidding noisy: use portfolio bidding across related campaigns, feed cart values accurately, be patient with 2-4 week evaluation windows, and never react to single-order swings |

**Budget rules**

- Brand search is never budget-capped (losing a branded impression is losing a customer we already earned).
- Impression share on priority transactional terms tracked; lost-IS-to-budget on winners triggers reallocation.
- Seasonal ramp 2-4 weeks pre-peak with bid targets loosened `[10-20%] TODO:` during peaks (auction pressure rises); seasonality adjustments applied around known conversion-rate spikes.

## 7. Demand Gen & YouTube campaigns

Demand creation inside Google's ecosystem - full video creative strategy in the [YouTube Playbook](youtube.md#5-youtube-advertising).

- **Audiences:** in-market (engagement rings, fine jewelry), life events (recently engaged), custom segments built from our converting search terms, customer-match and site-visitor lookalikes `TODO:` confirm consent coverage for customer match.
- **Creative:** education-led video and strong stills; proof assets (reviews, certification) for re-engagement.
- **Optimization:** qualified lead (guide download / consult) or site engagement - not last-click purchase, which under-credits creation.

## 8. Remarketing across the long cycle

- **RLSA:** bid up on searchers who already visited (they're comparing finalists); expand keyword coverage slightly for this audience only.
- **Demand Gen re-engagement:** sequenced proof messaging over 30-180 days mirroring the Meta retargeting ladder in the [Facebook & Meta Ads Playbook §6](facebook.md#6-campaign-architecture).
- **Exclusions:** purchasers excluded everywhere except the wedding-band cross-sell track; frequency caps mandatory.
- Consent-compliant tagging only - see [Data Privacy & Security](../../05-compliance-ethics/data-privacy-and-security.md).

## 9. Measurement & KPIs

| Foundation | Standard |
|---|---|
| Conversion tracking | Google Ads tag + GA4 linked; **enhanced conversions** enabled (consented, hashed first-party data) to recover modeled conversions |
| Conversion values | True order values passed; guide download and consult booking tracked as secondary conversions with assigned values `TODO:` set values from funnel math |
| Attribution | Data-driven attribution in-platform; decisions made on **blended MER/CAC + incrementality**, never platform-reported ROAS alone (see [Marketing Strategy §9](../marketing-strategy.md#9-measurement--kpis)) |
| Brand-spend honesty | Brand-campaign ROAS is reported separately from non-brand - blending them flatters the account and hides real acquisition cost |

### KPI scorecard

| Campaign family | Primary KPIs | Planning target |
|---|---|---|
| Brand search | Impression share (**>= 95%**), CPC, conversion rate | `TODO:` |
| Non-brand search | CAC, ROAS, conversion rate, impression share on priority terms | `TODO:` set from [Marketing Strategy §7](../marketing-strategy.md#7-cac-ltv--payback-thinking) |
| Shopping / PMax | ROAS, CAC, feed disapproval rate (~0), share of new customers | `TODO:` |
| Demand Gen / YouTube | Cost per qualified lead, view rate, assisted conversions, branded-search lift | `TODO:` |
| Account | Blended non-brand CAC & payback; quality score trend; search-terms waste rate | `TODO:` |

### Review rhythm

| Cadence | Activity |
|---|---|
| Weekly | Spend pacing, CAC/ROAS by campaign, search-terms → negatives, feed disapprovals, impression-share losses |
| Monthly | Campaign P&L, ad/asset performance, landing-page conversion review, PMax placement/channel audit |
| Quarterly | Keyword-portfolio and bid-target review, incrementality read, budget reallocation, seasonal retrospective |

## 10. Testing framework

- **Ad copy:** rotate 2-3 pillar-led variants per ad group; judge on conversion rate, not CTR alone.
- **Landing pages:** category vs guide vs consult destinations for commercial terms (Google Ads experiments).
- **Bid targets:** step tROAS changes `[+/- 10-15%] TODO:`, one change per learning window; never whipsaw smart bidding.
- **Incrementality:** brand-search holdout test `[annually] TODO:` (does brand spend add sales over organic?); geo tests on PMax where volume allows.
- One variable per test; success metric pre-registered; learnings logged in the campaign log.

## 11. Compliance & guardrails

- **Google Ads policies:** accurate pricing and availability (feed and site must match), no misleading claims, restricted-content rules checked if financing promotion is used `TODO:` compliance review of financing copy.
- Never advertise stock we cannot fulfill (policy in [Channels & Social §4.1](../channels-and-social.md#4-paid-media) and an honesty commitment).
- Certification claims in ads must be documentable per piece.
- Trademark rules respected in copy; competitor names never used in ad text.
- Customer-match lists built from consented data only; honor opt-outs on every sync.

## 12. Launch checklist (per campaign)

- [ ] Conversion tracking verified end-to-end (test conversion recorded with correct value).
- [ ] Campaign goal, bid strategy, and CAC/ROAS guardrail recorded in the campaign log.
- [ ] Ad groups tightly themed; RSAs with full asset coverage; all extensions built.
- [ ] Landing pages match query intent; mobile speed checked.
- [ ] Negative lists attached; brand excluded from PMax/non-brand where applicable.
- [ ] Audience exclusions (purchasers) and consent-compliant tagging confirmed.
- [ ] Budget pacing and seasonal calendar alignment confirmed.

---

## Related documents
- [YouTube Playbook](youtube.md)
- [Facebook & Meta Ads Playbook](facebook.md)
- [Content & SEO](../content-and-seo.md)
- [Channels & Social](../channels-and-social.md)
- [Marketing Strategy](../marketing-strategy.md)
- [Pricing Strategy](../../08-finance/pricing-strategy.md)
