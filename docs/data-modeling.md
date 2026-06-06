# Data Modeling

LUCE's data model is designed around catalog consistency, product discovery, accurate storefront behavior, personalization, and secure account flows.

It supports structured relationships between products, colors, images, categories, fabrics, textures, tags, inventory, recommendations, customer preferences, refresh tokens, and admin-managed attributes.

---

## Product Presentation

The product model supports scarf-specific presentation behavior:

- Product images can be mapped to specific colors or product states
- Plain and printed products can have different browsing behavior
- Plain products can expose selectable color variants
- Printed products can expose palette information
- Search can distinguish direct color matches from contained palette colors
- Parent and child attributes can support both broad search and accurate direct refinements

---

## Recommendation Metadata

Recommendation behavior is supported by explicit product classification fields such as `ProductFamily` and `ProductType`.

Examples include:

- `MainScarf`
- `Underscarf`
- `Extension`
- `Accessory`
- `BasicTop`

Color-aware recommendation behavior is also supported by optional manual styling metadata such as color temperature, mood, neutral group, and soft-neutral classification. These fields help guide recommendation scoring without replacing the visual matching logic.

---

## Why The Model Matters

The storefront can present products accurately because the backend models the domain directly instead of relying on fragile UI-only assumptions.

This matters for:

- Color swatches and palette previews
- Product detail accuracy
- Variant-aware cart items
- Search refinements
- Matching essentials with scarves
- Admin catalog quality control
