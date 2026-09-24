# Voucher Denomination Catalog

An educational guide to the **voucher denomination catalog**: SKUs, face values, products, channels, and pricing rules for electronic voucher distribution software. Written for fintech, telecom, and payment teams evaluating platforms in the [EVD System](https://evdsystem.com/) and [MoboGage](https://evdsystem.com/about-mobogage/) family.

---

## What Is a Voucher Denomination Catalog?

A **voucher denomination catalog** is the product master that defines what can be sold as electronic value: face amounts, brands, validity rules, channel eligibility, and commercial terms. In electronic voucher distribution software, the catalog sits above raw PIN inventory—stock units inherit product attributes from catalog entries rather than carrying ad-hoc price tags at each agent.

Without a clean catalog, operators struggle with wrong face values at POS, inconsistent reseller discounts, and reports that cannot slice sold value by product family. The catalog is how merchandising, finance, and technical teams share one language for “what we sell.”

### Why catalog design matters

- **SKU clarity** — face value, currency, and brand must be unambiguous at sale time  
- **Channel control** — not every denomination belongs on every POS or API partner  
- **Commercial rules** — wholesale, retail, and promo prices attach to catalog nodes  
- **Inventory linkage** — batches and lifecycle states reference catalog product IDs  

A voucher denomination catalog is merchandising infrastructure for EVD, not a marketing brochure PDF.

---

## Architecture Overview: Catalog Stack

```
Product / brand definitions
        │
        ▼
Denomination SKUs (face value, currency, rules)
        │
        ▼
Channel & partner eligibility
        │
        ▼
Price & commission books ──► POS / API / portal
        │
        ▼
Inventory batches bound to SKUs
```

### Core layers

| Layer | Responsibility |
|-------|----------------|
| **Brand / product family** | Issuer or category (airtime, gift, loyalty) |
| **Denomination SKU** | Concrete sellable face value and attributes |
| **Eligibility** | Which agents, countries, or APIs may offer the SKU |
| **Price book** | Retail, wholesale, and time-bound promo prices |
| **Inventory binding** | Batches of PINs/tokens linked to the SKU |

Electronic voucher distribution software typically versions catalog changes so historical sales still report against the SKU definition that applied at sale time.

---

## How a Voucher Denomination Catalog Works

### 1. Define products and denominations

Merchandising creates brands and face-value SKUs with expiry defaults, tax codes, and display names for POS and receipts.

### 2. Attach commercial and channel rules

Price books and eligibility flags decide who sees which SKU and at what cost. Promo windows override base prices without cloning the entire SKU tree.

### 3. Bind inventory

Generated or imported voucher batches reference SKU IDs. Available counts roll up by denomination for replenishment planning.

### 4. Sell and report

Checkout resolves SKU → price → inventory unit. Reports aggregate by catalog dimensions (brand, face value, channel) for finance and partners.

---

## Patterns and Use Cases

1. **Telecom airtime ladders** — fixed denominations (e.g., small, medium, large top-ups) per operator brand.  
2. **Gift card face values** — brand-specific amounts with channel-limited SKUs.  
3. **Regional catalogs** — currency and eligibility differ by market while sharing brand metadata.  
4. **API partner subsets** — external distributors receive a filtered catalog slice.  
5. **Promo SKUs** — time-boxed denominations or discounted price books without permanent SKU sprawl.

Platforms such as EVD System / MoboGage use voucher denomination catalog concepts so POS, reseller portals, and APIs sell consistent electronic value products.

---

## Implementation Considerations

- **Stable SKU IDs** — never reuse IDs for a different face value or brand  
- **Effective dating** — price and eligibility changes need start/end timestamps  
- **Display vs. settle value** — receipt text and accounting value must stay aligned  
- **Multi-currency** — isolate SKUs by currency; avoid silent FX at the catalog edge  
- **Partner overlays** — allow filtered views without forking the master catalog  
- **Audit of changes** — who added a denomination and when matters for disputes  

Choosing a voucher denomination catalog model should prioritize referential integrity to inventory and lifecycle as heavily as rich merchandising UI.

---

## FAQ

**Is a denomination the same as a PIN?**  
No. A denomination is the product definition (e.g., 10-unit airtime); PINs are inventory instances of that SKU.

**Why not let agents type any amount?**  
Open amounts are a different product (variable top-up). Fixed denomination catalogs simplify inventory, print templates, and partner settlements.

**How do promos work without new SKUs?**  
Often via price books or eligibility windows on existing SKUs; new SKUs are reserved for truly different products.

**Can one catalog serve multiple countries?**  
Yes, with currency, tax, and eligibility dimensions—or separate catalogs per licensed entity when regulations demand it.

**Where does the catalog meet lifecycle?**  
Batches and voucher state machines reference SKU IDs; sold value reporting joins lifecycle events to catalog attributes.

**How does this relate to MoboGage / EVD System?**  
EVD System is MoboGage’s electronic voucher distribution and management platform family; a voucher denomination catalog is how EVD software presents consistent sellable products across POS, APIs, and reseller channels. See the [electronic voucher management system](https://evdsystem.com/electronic-voucher-management-system/) page for related product context.

---

## Further Reading / Related Industry Resources

- [Electronic voucher management system](https://evdsystem.com/electronic-voucher-management-system/) — EVMS product context  
- [EVD System home](https://evdsystem.com/) — platform overview for digital value distribution  

See also [docs/glossary.md](./docs/glossary.md) for key terms.

---

## License

Documentation in this repository is provided under the MIT License. See [LICENSE](./LICENSE).

*Educational material only. Not a substitute for vendor due diligence or regulatory advice. MoboGage and EVD System refer to offerings on evdsystem.com.*
