# Documentation Standards & Authoring Brief

> **Purpose:** This is the canonical reference for anyone writing or maintaining Palencia Diamonds' organizational documentation. Read it before editing any document in `/docs`.

| | |
|---|---|
| **Owner** | Operations / Knowledge Management |
| **Audience** | All employees who author or maintain internal docs |
| **Review cadence** | Annually |
| **Status** | Living document |

---

## 1. Company snapshot (source of truth)

Use these facts consistently across all documents. Where a fact is unknown, use a clearly marked placeholder in `[brackets]` and flag it as a `TODO`.

| Attribute | Value |
|---|---|
| **Company** | Palencia Diamonds |
| **Website** | www.palenciadiamonds.com |
| **Business model** | Online-first (e-commerce) fine jewelry retailer |
| **Category** | Certified diamonds & handcrafted fine jewelry |
| **Brand promise** | *"Certified diamonds. Handcrafted jewelry. Honest prices."* |
| **Core products** | Engagement rings, wedding bands, necklaces, earrings, bracelets, pendants & charms, custom ring design |
| **Metals** | Gold (yellow / white / rose) and platinum; hand-set |
| **Certification** | GIA & IGI independent grading reports on center stones |
| **Service promises** | Free insured shipping (signature confirmation), complimentary resizing where design allows, manufacturing-defect coverage, custom design with material & carat selection |
| **Target customer** | Engaged couples and quality-conscious fine-jewelry buyers |
| **Company stage** | Established, 10+ employees, growing, departmentalized |

## 2. Brand voice for internal docs

- **Clear over clever.** Plain, confident, specific. No filler or corporate cliché.
- **Warm and human.** We sell meaningful, emotional purchases. Even internal docs carry that care.
- **Honest and transparent.** "Honest prices" is a company value — our documents model the same candor.
- **Precise.** In a certified-diamond business, precision *is* the brand. Use exact terminology (4Cs, GIA/IGI, hallmarks).

## 3. Document format standard

Every document should follow this skeleton:

```markdown
# Document Title

> One-sentence purpose statement.

| | |
|---|---|
| **Owner** | [Role/Department accountable] |
| **Last reviewed** | [YYYY-MM-DD] |
| **Review cadence** | [Quarterly / Annually / ...] |
| **Status** | [Draft / Active / Living document] |

---

## Sections...

---

## Related documents
- [Doc name](../path/to/doc.md)
```

## 4. Conventions

- **Format:** GitHub-flavored Markdown.
- **Headings:** One `#` H1 per document (the title). Use `##`/`###` below.
- **Tables & checklists:** Prefer them over long prose for procedures, roles, and criteria.
- **Cross-linking:** Link related documents with relative paths. Keep a "Related documents" section at the end.
- **Placeholders:** Unknown company-specifics go in `[brackets]` and are tracked as `TODO:` so they're easy to grep and fill in later.
- **Specificity:** Write for the diamond & fine-jewelry industry specifically. Reference the real standards we operate against (Kimberley Process, RJC Code of Practices, OECD Due Diligence Guidance, GIA/IGI, FinCEN AML rules for dealers in precious stones/metals/jewels). Avoid generic boilerplate that could apply to any company.
- **Actionable:** Documents should help someone *do the job*, not just describe it abstractly.

## 5. Disclaimer

These documents are operational and strategic references, **not legal advice**. Policies touching law (AML/KYC, privacy, employment, tax) must be reviewed by qualified counsel and adapted to the jurisdictions in which Palencia Diamonds operates before being treated as binding.

---

## Related documents
- [Documentation Home](../README.md)
- [Company Overview](00-company/company-overview.md)
- [Mission, Vision & Values](00-company/mission-vision-values.md)
