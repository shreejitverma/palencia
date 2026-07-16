# Content & SEO

> Our owned-content and search strategy — how education-first content earns high-intent traffic, builds trust before the sale, and turns Google into a compounding, low-cost demand engine for certified diamonds and handcrafted jewelry.

| | |
|---|---|
| **Owner** | Marketing & Brand (Content / SEO) |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Purpose & philosophy

A diamond buyer researches for weeks. Most of that research starts with a question typed into a search bar — *"what are the 4Cs,"* *"how much should I spend on an engagement ring,"* *"GIA vs IGI."* If we answer those questions better and more honestly than anyone else, we earn trust **before** the buyer ever compares prices.

Our content strategy is therefore **education-first, not promotion-first**. We teach, we prove, and we let the honesty of the teaching do the selling. This is the on-page expression of our brand promise — *Certified diamonds. Handcrafted jewelry. Honest prices.* — and it directly supports the [Marketing Strategy](marketing-strategy.md) goal of capturing and nurturing a long buying cycle.

**Three jobs of every piece of content:**
1. **Get found** — rank for a real question a buyer is asking (SEO).
2. **Build trust** — answer it honestly, precisely, and completely (brand).
3. **Move forward** — give a clear, low-pressure next step (email capture, guide, or product).

## 2. Content pillars

Content maps to the same three message pillars as our positioning, plus a design/inspiration layer for discovery.

| Pillar | Buyer need | Example content |
|---|---|---|
| **Certified & educated** | "Help me understand what I'm buying" | 4Cs guides, GIA vs IGI, certification explained, lab vs natural |
| **Handcrafted & designed** | "Show me what's possible" | Ring styles, setting guides, metal guides, custom design stories |
| **Honest & confident** | "Help me spend wisely" | Budget guides, price-per-carat explainers, "what actually affects price," buying checklists |
| **Care & aftercare** | "Help me protect it" | Cleaning, resizing, insurance, warranty, travel |

Our flagship educational asset is the [Diamond Education: The 4Cs](../09-product/diamond-education-4cs.md) hub — the anchor of the certification pillar and the destination most top-of-funnel content links to.

## 3. Search strategy: intent, not just keywords

We segment search by **intent**, because intent determines the page type, the CTA, and how we measure success.

| Intent | Example queries | Page type | Goal / KPI |
|---|---|---|---|
| **Informational (early)** | "what are the 4Cs," "how to choose a diamond" | Guide / hub article | Rank, email capture, time-on-page |
| **Commercial (mid)** | "best place to buy engagement rings," "GIA vs IGI," "halo vs solitaire" | Comparison / buying guide | Return visits, guide download, product clicks |
| **Transactional (late)** | "1 carat round diamond ring," "platinum solitaire engagement ring" | Category / product page | Conversion, revenue |
| **Branded** | "Palencia Diamonds reviews," "Palencia return policy" | Brand / reviews / policy page | Protect & convert; trust reinforcement |
| **Local / service** *(if applicable)* | `TODO:` confirm any physical/appointment presence | Service page | `[TBD]` |

**Priority principle:** We win **high-intent transactional and mid-funnel commercial** queries first (they convert), then expand into informational hubs that feed them internal links and authority.

## 4. Topic-cluster model

We organize content as **pillar hubs + supporting cluster pages**, internally linked. Each hub targets a broad head term; clusters target long-tail questions and link up to the hub. This concentrates topical authority and captures the whole question set of a researching buyer.

| Pillar hub (head term) | Supporting cluster pages (long-tail) | Primary intent | Links to |
|---|---|---|---|
| **Diamond Education / 4Cs** | Cut, Color, Clarity, Carat; fluorescence; certification; GIA vs IGI; lab vs natural; how to read a report | Informational | Product category pages, budget guide |
| **Engagement Ring Buying Guide** | How much to spend; ring size guide; how to propose; timeline; financing; surprise vs together | Commercial | Ring categories, 4Cs hub, reviews |
| **Ring Styles & Settings** | Solitaire, halo, hidden halo, three-stone, pavé, bezel; metal guide (yellow/white/rose gold, platinum) | Commercial | Style category pages |
| **Wedding Bands** | Matching sets, eternity, pavé, men's bands, stacking, sizing | Commercial/Transactional | Band categories, engagement hub |
| **Diamond Jewelry Gifting** | Anniversary, tennis bracelets, stud earrings, pendants; gift guides by occasion/budget | Commercial | Category pages, seasonal landing pages |
| **Care & Ownership** | Cleaning, resizing, warranty, insurance, appraisal, travel | Informational/retention | Warranty & policy pages |

**Internal linking rules:**
- Every cluster page links **up** to its hub and **sideways** to 1–2 sibling clusters.
- Every hub links **down** to its clusters and **out** to the most relevant product/category page.
- Educational content always offers a soft path to a relevant product — helpfully, never pushily.

## 5. Technical & product-page SEO for jewelry e-commerce

High-AOV catalogs live or die on **crawlability, page experience, and product-page quality**. Priorities:

### Site & technical
- **Clean, stable URLs** — human-readable, category-based (`/engagement-rings/halo/`), no session junk.
- **Faceted navigation control** — filters (carat, metal, shape, price) must not spawn thousands of thin, duplicate, indexable URLs. Use canonicalization and `noindex`/parameter rules deliberately.
- **Canonical tags** on variant and filtered pages to consolidate signals.
- **Core Web Vitals** — jewelry imagery is heavy; compress, lazy-load, serve modern formats, and keep LCP/CLS/INP in the "good" band.
- **Mobile-first** — most early research is on phones; the whole experience must be excellent on mobile.
- **HTTPS, XML sitemaps, logical robots.txt**, and a flat, crawlable architecture.
- **Fast, accurate internal search** and no orphan pages.

### Product & category page quality
- **Unique, honest descriptions** — never paste supplier boilerplate. Describe the actual piece, metal, setting, and craftsmanship.
- **Certification front-and-center** — display GIA/IGI report details and, where possible, a link/preview of the actual report. This is our differentiator *and* a trust/SEO signal.
- **Complete specs** — the 4Cs, carat, metal, measurements, and service terms (free insured shipping, resizing, warranty) on every product page.
- **High-quality media** — multiple angles, video, on-hand/scale shots, alt text describing the piece.
- **Reviews on the page** — product-level and site-level ratings (see §6 schema).
- **Educational cross-links** — link specs to the relevant 4Cs explainer ("What is VS1 clarity?").

## 6. Structured data & rich results

Structured data helps our pages earn richer, more trustworthy search listings and feeds AI/answer surfaces. Implement and validate these schema types:

| Schema | Where | What it powers |
|---|---|---|
| **Product** | Every product page | Price, availability, brand, and (with Offer) shopping-rich results |
| **AggregateRating / Review** | Product & site | Star ratings in search listings — major trust & CTR lift |
| **FAQPage** | Guides & product pages with genuine Q&A | Expandable FAQ rich results |
| **BreadcrumbList** | All category/product pages | Breadcrumb display; clearer hierarchy |
| **Organization / LocalBusiness** | Site-wide / about | Brand knowledge panel, logo, contact |
| **Article** | Guides & hub content | Eligibility for article/education surfaces |
| **VideoObject** | Pages with product/education video | Video rich results |

**Rules:**
- Mark up **only what is genuinely on the page** — false or invisible markup violates guidelines and risks penalties. Honesty applies to code, too.
- Ratings must be real and earned (see [CRM & Clienteling](../04-sales-cx/crm-and-clienteling.md) for review generation).
- Validate every template with a schema/rich-results test before shipping, and re-check after redesigns.

## 7. On-page content checklist

Use this checklist for every new guide, hub, or major landing page before publishing.

**Intent & structure**
- [ ] One clear primary query/intent identified; page type matches intent.
- [ ] Title tag: primary term + brand, ≤ ~60 chars, compelling.
- [ ] Meta description: honest, benefit-led, ≤ ~155 chars, includes a reason to click.
- [ ] One H1 stating the topic; logical H2/H3 outline covering the question fully.
- [ ] URL is short, readable, and keyword-relevant.

**Content quality (E-E-A-T)**
- [ ] Genuinely answers the query more completely and honestly than page-1 competitors.
- [ ] Demonstrates real expertise (accurate 4Cs, GIA/IGI, hallmark terminology — see [Diamond Education: The 4Cs](../09-product/diamond-education-4cs.md)).
- [ ] Author/reviewer credibility shown where relevant; facts are current and correct.
- [ ] No overclaiming, no fake urgency — matches our [Voice & Tone](../01-brand/voice-and-tone.md).
- [ ] Trade-offs stated honestly (e.g., when to prioritize cut over carat).

**Conversion & linking**
- [ ] Clear, low-pressure next step (guide download / email capture / relevant product).
- [ ] Internal links: up to hub, sideways to siblings, out to 1–2 products.
- [ ] Relevant CTA to email capture for the nurture cycle.

**Media & technical**
- [ ] Original, optimized images/video with descriptive alt text.
- [ ] Structured data added and validated (§6).
- [ ] Mobile layout checked; Core Web Vitals not regressed.
- [ ] Reviewed for accessibility (headings, contrast, alt text).

## 8. How content supports the sale

Content is not a silo — it is the connective tissue of the funnel in the [Marketing Strategy](marketing-strategy.md).

| Funnel stage | Content's job | Example |
|---|---|---|
| **Awareness** | Get discovered on informational queries | "How to choose a diamond" ranks and captures a first visit |
| **Consideration** | Build trust, capture email, educate | 4Cs hub + downloadable buying guide → email nurture |
| **Purchase** | Remove final fear at the point of decision | Certification display, honest specs, reviews, and FAQ on the product page |
| **Loyalty** | Deepen the relationship | Care guides, resizing/warranty content, "how to insure your ring" |

**The trust mechanism:** a buyer who learns the 4Cs *from us*, honestly, tends to return to buy *from us*. Education is the least pushy and most durable form of selling in a high-consideration category.

## 9. Content calendar & operating rhythm

Content is planned against the seasonal calendar in the [Marketing Strategy](marketing-strategy.md), shipped early enough to rank.

| Cadence | Activity |
|---|---|
| **Always-on** | Maintain and refresh evergreen hubs (4Cs, buying guides); fix decaying pages; expand clusters |
| **8–12 weeks pre-season** | Publish/refresh seasonal landing pages & gift guides (engagement season, Valentine's, Mother's Day, holidays) so they rank in time |
| **Monthly** | 2–4 new cluster/guide pieces `TODO:` confirm capacity; internal-link audit; review new-page performance |
| **Quarterly** | Full technical SEO audit (crawl, CWV, schema, index bloat); content pruning/refresh; keyword-gap analysis vs competitors |
| **Annually** | Architecture & pillar review; align with brand and positioning updates |

### Content KPIs

| KPI | Target |
|---|---|
| Non-branded organic sessions | Grow QoQ; `TODO:` set baseline |
| Page-1 rankings for priority head terms | `TODO:` track & grow |
| Email capture rate from content pages | **≥ 5%** |
| Assisted conversions influenced by content | `TODO:` |
| Rich-result coverage (product/review/FAQ) | **≥ 90%** of eligible pages valid |
| Core Web Vitals | All key templates in "good" band |
| Content-influenced revenue | `TODO:` set with analytics |

## 10. Governance & guardrails

- **Accuracy is non-negotiable.** A wrong grade or spec in content breaks trust exactly like it would on an invoice — *precision is the brand*.
- **No black-hat SEO.** No cloaking, keyword stuffing, fake reviews, or misleading schema. We rank by being genuinely the most helpful and honest.
- **One voice.** All content follows [Voice & Tone](../01-brand/voice-and-tone.md) — warm, plain, precise, never luxury-jargon or pressure.
- **Legal/claims review.** Sourcing, certification, and pricing claims must be defensible; coordinate with compliance where claims touch regulated ground.

---

## Related documents
- [Marketing Strategy](marketing-strategy.md)
- [Channels & Social](channels-and-social.md)
- [CRM & Clienteling](../04-sales-cx/crm-and-clienteling.md)
- [Diamond Education: The 4Cs](../09-product/diamond-education-4cs.md)
- [Voice & Tone](../01-brand/voice-and-tone.md)
- [Documentation Home](../../README.md)
