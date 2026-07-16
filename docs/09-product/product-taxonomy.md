# Product Taxonomy

> How the Palencia Diamonds catalog is organized — categories, attributes, and SKUs — so every piece is described consistently and customers can find, filter, and trust what they see.

| | |
|---|---|
| **Owner** | Merchandising & Sourcing |
| **Last reviewed** | 2026-07-16 |
| **Review cadence** | Semi-annually |
| **Status** | Living document |

---

## 1. Why taxonomy matters

A taxonomy is the shared skeleton beneath the whole catalog. Get it right and everything downstream works: the site navigates cleanly, filters return honest results, search surfaces the right pieces, inventory reconciles, and merchandising can tell a story. Get it wrong and the same ring shows up in two categories, a filter misses stock, and a customer can't trust that "1 ct, VS1, H" means the same thing on every page.

This document defines **how we classify products, what we capture about each, and how we name them** — the single reference for merchandisers, content authors, photographers, and engineers.

---

## 2. Category tree

The catalog is organized into **Categories → Subcategories → Styles**. Every product lives in exactly **one primary category** (for navigation and SKUs) but may be tagged into others for discovery (e.g., a diamond pendant surfaced under both "Pendants & Charms" and a "Diamonds" edit).

```
Palencia Catalog
│
├── Engagement Rings (ENG)
│   ├── Solitaire
│   ├── Halo
│   ├── Hidden Halo
│   ├── Three-Stone
│   └── Custom  → see Custom Design
│
├── Wedding Bands (WED)
│   ├── Classic / Plain
│   ├── Pavé
│   ├── Eternity (full)
│   ├── Half-Eternity
│   └── Matching Sets (bridal sets)
│
├── Necklaces (NEK)
│   ├── Chains
│   ├── Station
│   ├── Tennis (line)
│   └── Rivière
│
├── Earrings (EAR)
│   ├── Studs
│   ├── Hoops
│   ├── Drops
│   └── Dangles
│
├── Bracelets (BRC)
│   ├── Tennis
│   ├── Bangles
│   └── Station
│
├── Pendants & Charms (PEN)
│   ├── Solitaire
│   ├── Halo
│   ├── Cluster
│   └── Initials / Letters
│
└── Custom Rings (CUS)
    └── Made-to-order (customer selects setting, metal, stone, carat)
```

### 2.1 Category reference

| Category | Code | Subcategories | Notes |
|---|---|---|---|
| **Engagement Rings** | `ENG` | Solitaire, Halo, Hidden Halo, Three-Stone, Custom | Center-stone driven; the flagship category |
| **Wedding Bands** | `WED` | Classic, Pavé, Eternity, Half-Eternity, Matching Sets | Sold singly or as bridal sets; sizing critical |
| **Necklaces** | `NEK` | Chains, Station, Tennis, Rivière | Length is a required attribute |
| **Earrings** | `EAR` | Studs, Hoops, Drops, Dangles | Sold as **pairs** unless noted (e.g., single stud) |
| **Bracelets** | `BRC` | Tennis, Bangles, Station | Length/circumference required; clasp type captured |
| **Pendants & Charms** | `PEN` | Solitaire, Halo, Cluster, Initials | Chain may be included or sold separately — state clearly |
| **Custom Rings** | `CUS` | Made-to-order | Configured from options; see §5 |

---

## 3. Product classification model

### 3.1 One-of-a-kind vs. collection vs. custom

Every product falls into one of three fulfillment/inventory types. This distinction drives how it's stocked, priced, and displayed.

| Type | Definition | Inventory behavior | Example |
|---|---|---|---|
| **Collection (made-to-order-able)** | A repeatable design produced to spec | Setting is a repeatable style; center stone selected from live inventory | A solitaire setting paired with any qualifying round |
| **One-of-a-kind (OOAK)** | A single finished piece tied to a specific stone | Quantity of exactly 1; sells once, then retires | A specific 1.51 ct oval three-stone ring |
| **Custom** | Configured by the customer from options | Built on order; not held in stock | A customer's chosen setting + metal + stone + carat |

> **Ring-builder note:** Engagement rings are frequently sold as **setting + loose stone** pairings. The **setting** is a collection style (repeatable); the **loose diamond** is one-of-a-kind (a specific certified stone). The finished ring's identity combines both — see SKU composition in §4.3.

### 3.2 Collections

A **collection** is a curated, named grouping used for merchandising and storytelling (e.g., a signature pavé family across rings, bands, and pendants). Collections cut **across** categories and are a tag/attribute, not a place in the category tree. A product can belong to one named collection.

---

## 4. SKU naming convention

### 4.1 Goals

A good SKU is **human-readable, stable, unique, and sortable**. Ours encodes just enough to identify a piece at a glance without trying to embed every spec (specs live in the attribute record, not the SKU).

### 4.2 Structure — finished pieces

```
PAL-<CAT>-<SUB>-<METAL>-<SEQ>[-<SIZE>]
```

| Segment | Meaning | Examples |
|---|---|---|
| `PAL` | Brand prefix (constant) | `PAL` |
| `<CAT>` | Category code (§2.1) | `ENG`, `WED`, `NEK`, `EAR`, `BRC`, `PEN`, `CUS` |
| `<SUB>` | 3-letter subcategory | `SOL` (solitaire), `HAL` (halo), `HHL` (hidden halo), `3ST` (three-stone), `PAV` (pavé), `ETY` (eternity), `TEN` (tennis), `STA` (station), `RIV` (rivière), `STU` (studs), `HOP` (hoops), `DRP` (drops), `DNG` (dangles), `BNG` (bangle), `CLU` (cluster), `INI` (initials), `CHN` (chain) |
| `<METAL>` | Metal code (§4.4) | `14Y`, `14W`, `14R`, `18Y`, `18W`, `18R`, `PLT` |
| `<SEQ>` | Zero-padded style sequence | `0142` |
| `<SIZE>` | Optional variant (ring size, chain length) | `R6.5`, `L18` (18-inch), `B7` (7-inch bracelet) |

**Examples**
- `PAL-ENG-SOL-14W-0142-R6.5` — solitaire engagement ring, 14k white gold, style 142, size 6.5
- `PAL-NEK-TEN-18Y-0031-L16` — tennis necklace, 18k yellow gold, 16-inch
- `PAL-EAR-STU-PLT-0088` — platinum diamond studs (pair)

### 4.3 Loose stones & ring-builder pairings

Loose certified diamonds get their own identity keyed to the **grading report number** so the physical stone is always traceable:

```
PAL-DIA-<ORIGIN>-<CERTLAB><CERT#>
```
- `<ORIGIN>` = `N` (natural) or `L` (lab-grown)
- Example: `PAL-DIA-N-GIA2447xxxxxx`

A **built ring** links a setting SKU to a stone SKU:

```
PAL-ENG-SOL-14W-0142 + PAL-DIA-N-GIA2447xxxxxx
```

This keeps the setting reusable while binding the finished order to one specific, certified stone.

### 4.4 Metal codes

| Code | Metal |
|---|---|
| `10Y / 10W / 10R` | 10k yellow / white / rose gold |
| `14Y / 14W / 14R` | 14k yellow / white / rose gold |
| `18Y / 18W / 18R` | 18k yellow / white / rose gold |
| `22Y` | 22k yellow gold |
| `PLT` | Platinum |

---

## 5. Attributes & specifications captured per product

Every product record stores a consistent attribute set. **Required** attributes must be present before a product goes live (they power filters and honest disclosure). **Conditional** attributes apply to certain categories.

### 5.1 Core attributes (all products)

| Attribute | Applies to | Example / values | Required? | Powers |
|---|---|---|---|---|
| **Product title** | All | "Classic Solitaire Engagement Ring" | Yes | Search, display |
| **Category / Subcategory** | All | Engagement Rings / Solitaire | Yes | Nav, filters |
| **SKU** | All | `PAL-ENG-SOL-14W-0142` | Yes | Everything |
| **Product type** | All | Collection / OOAK / Custom | Yes | Inventory |
| **Collection** | All | e.g., "Signature Pavé" | No | Merchandising |
| **Metal** | All | 14k white gold | Yes | Filter, price |
| **Metal weight (g)** | All | 3.8 g | Yes | Pricing vs. spot |
| **Price** | All | Transparent, defensible | Yes | Display |
| **Availability / qty** | All | In stock / made-to-order | Yes | Inventory |
| **Images / video** | All | Asset set | Yes | Display, trust |

### 5.2 Center-stone attributes (rings, pendants, solitaire pieces)

| Attribute | Example / values | Required? |
|---|---|---|
| **Stone origin** | Natural / Lab-grown | **Yes** (disclosure) |
| **Shape** | Round, Princess, Oval, Emerald, Cushion, Pear, Marquise, Radiant, Asscher, Heart | Yes |
| **Carat weight** | 1.02 ct | Yes |
| **Cut grade** | Excellent / VG / … (rounds; N/A for fancies) | Yes where graded |
| **Color grade** | D–Z | Yes |
| **Clarity grade** | FL–I3 | Yes |
| **Polish / Symmetry** | Excellent / VG / … | Yes |
| **Fluorescence** | None–Very Strong | Yes |
| **Measurements (mm)** | 6.48 × 6.51 × 4.01 | Yes |
| **Cert lab** | GIA / IGI | Yes |
| **Cert number** | Report # (links to report) | Yes |
| **Eye-clean (verified)** | Yes / No / Note | Yes for center stones |

### 5.3 Melee / accent-stone attributes (pavé, halo, tennis, station)

| Attribute | Example |
|---|---|
| **Number of stones** | 42 |
| **Total carat weight (tcw)** | 0.75 ct tcw |
| **Average color / clarity** | G–H / VS–SI |
| **Setting style** | Pavé / shared-prong / bezel / channel |

### 5.4 Dimensional & construction attributes (conditional)

| Attribute | Applies to | Example |
|---|---|---|
| **Ring size** | Rings | 6.5 (resizable? Y/N) |
| **Length** | Necklaces, bracelets | 16" / 18" / 7" |
| **Chain type / width** | Chains, pendants | Cable, 1.1 mm |
| **Clasp type** | Necklaces, bracelets | Lobster, box-with-safety |
| **Earring back** | Earrings | Push-back, screw-back, lever-back |
| **Band width / profile** | Rings, bands | 2.0 mm, comfort-fit |
| **Sold as** | Earrings/bands | Pair / single / set |
| **Chain included?** | Pendants | Yes (18") / No |

---

## 6. How taxonomy powers the storefront

### 6.1 Navigation

Top-level nav mirrors the category tree (§2). Subcategories become second-level menus. Because each product has exactly one **primary** category, nav counts are honest and a piece never appears "lost" between menus.

### 6.2 Search & filtering

Attributes are the filters. A well-populated attribute record means a customer can filter down to exactly what they want — and every result genuinely matches.

| Filter (facet) | Backed by attribute |
|---|---|
| Metal & color (yellow/white/rose/platinum) | Metal |
| Shape | Center-stone shape |
| Carat range | Carat weight / tcw |
| Color, Clarity, Cut | Grade attributes |
| Natural vs. Lab-grown | Stone origin |
| Certification (GIA/IGI) | Cert lab |
| Price range | Price |
| Length / size | Dimensional attributes |
| Style (solitaire, halo, pavé, …) | Subcategory |

> **Honesty rule for filters:** A product only appears under a filter value if it truly has that attribute. We never tag a stone "eye-clean" or "GIA" to win a filter it doesn't qualify for. Filters are a promise.

### 6.3 Merchandising

Collections, "just under a carat" value edits, metal stories, and shape guides are all built by **querying attributes and collection tags** — no manual, drift-prone lists. Cross-category collections let us tell one design story across a ring, band, and pendant.

---

## 7. Governance & data quality

- **Single source of truth:** The product record (PIM/catalog) is authoritative; the storefront and inventory read from it.
- **No product goes live** without required attributes (§5) and, for certified stones, a linked GIA/IGI report number.
- **One primary category** per product; additional discovery via tags/collections only.
- **SKUs are permanent.** Once assigned, a SKU is never reused for a different design.
- **Certified stone = traceable stone.** Every center stone's record ties to its physical report number and (for lab-grown) its inscription.

---

## Related documents
- [Diamond Education — 4Cs](diamond-education-4cs.md) — the specs behind stone attributes
- [Materials & Metals](materials-and-metals.md) — the metal codes and properties referenced here
- [Inventory Management](../03-operations/inventory-management.md) — how stock, OOAK, and built rings are tracked
- [Content & SEO](../06-marketing/content-and-seo.md) — how taxonomy feeds titles, filters, and structured data
- [Documentation Home](../../README.md)
