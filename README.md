# Made-to-Measure Curtain Configurator & Dynamic Dimension Pricing Engine

A production-ready Made-to-Measure Curtain Product Detail Page (PDP) section built for Shopify Online Store 2.0 (Dawn Theme). Features dynamic real-time dimension pricing, panel calculation, zero Cumulative Layout Shift (CLS), visual fabric swatch architecture, and Ajax Cart API serialization with confidential fulfillment metrics.

---

## 🚀 Live Demo
* **Preview URL:** https://tuczukl6osuj76nh-80317448418.shopifypreview.com/products_preview?preview_key=3127fb27516bcefc12ef1fd84a7a080d
* **Storefront Password:** jsa

---

## 🛠️ Tech Stack & Constraints
* **Shopify Online Store 2.0** architecture (Dawn theme).
* **Vanilla ES6+ JavaScript** encapsulating an HTML5 Custom Element (`<curtain-configurator>`).
* **Zero Third-Party Dependencies:** 100% native Liquid, Web Components, and Vanilla JS (No jQuery, external UI libraries, or math packages).
* **Shopify Metaobjects & Metafields:** Decoupled data model for pricing matrix and manufacturing rules.
* **Shopify Ajax Cart API & Section Rendering API:** Real-time cart payload serialization and seamless cart drawer re-rendering.

---

## 📐 1. Mathematical Pricing Calculation

The pricing calculation is completely decoupled from the codebase and driven dynamically by the product's associated `Curtain Pricing Tier` Metaobject entries:

### Variables:
* **Width (cm):** Customer inputted width.
* **Drop (cm):** Customer selected drop interval (`150cm`, `200cm`, `250cm`).
* **Matched Tier:** Metaobject entry where `min_width <= Width <= max_width`.
* **Base Price (`base_price`):** Starting cost for the matched width tier.
* **Price Per Drop Tier (`price_per_drop_tier`):** Incremental cost for longer drop lengths.
* **Drop Tier Index:**
  * `150 cm` -> Index `0` (Base interval)
  * `200 cm` -> Index `1` (+1 tier increment)
  * `250 cm` -> Index `2` (+2 tier increments)

### Mathematical Formula:
```text
Final Price = base_price + (drop_tier_index * price_per_drop_tier)
Panels Required = matched_tier.panels_required

Confidential Manufacturing Metrics (_fabric_panels):
Intermediate fulfillment metrics are passed with a leading underscore:

JSON
{
  "id": 4829104812,
  "quantity": 1,
  "properties": {
    "Width": "180cm",
    "Drop": "200cm",
    "Fabric": "Natural Linen",
    "Custom Calculated Price": "$95.00",
    "_fabric_panels": 2
  }
}
