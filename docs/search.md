# Search Design

LUCE search is built with Lucene.NET and designed around structured ecommerce discovery, not only free-text product lookup.

The goal is to understand how customers search for modest fashion and scarf products: by category, fabric, color, texture, print, size, styling need, and product type. Search behavior is tied to real indexed inventory so suggestions and refinements stay useful instead of becoming generic keyword matches.

---

## Query Interpretation

Before Lucene search runs, the raw query is normalized and interpreted.

The interpreter detects structured intent such as:

- Categories
- Fabrics
- Colors
- Tags
- Texture patterns
- Print names
- Size shapes
- Color modifiers

The system uses both curated taxonomy and Lucene inventory vocabulary.

The curated taxonomy handles business language, synonyms, aliases, and canonical mappings. The inventory vocabulary reflects real indexed catalog values, which helps the search system stay aligned with what actually exists in the catalog.

Known aliases can be rewritten before searching. For example:

- `under scarf` can map to `undercap`
- `olive` can map through the broader `green` color family
- `rectangle` can map to `rectangular hijab`

This bridges customer language and internal catalog structure without relying on fragile product-name matching.

---

## Search Stages

Search runs through staged retrieval:

1. Strict
2. Relaxed
3. Fuzzy fallback

Strict search is preferred for explicit structured intent. Relaxed and fuzzy stages are used when needed to avoid empty or unhelpful results.

This keeps precise searches precise, while still supporting imperfect queries and typos.

---

## Suggestions

Search is explicit and press-to-search. Typing fetches suggestions only; it does not automatically run a full product search.

Suggestions are Lucene-backed and inventory-aware. They are built from indexed, in-stock products rather than live database scans.

Suggestion sources include:

- Categories
- Fabrics
- Colors
- Textures
- Prints
- Tags
- Size fields
- Parent category, fabric, and color fields
- Printed product colors
- Taxonomy aliases that resolve to available inventory

Suggestions also use query context. For example, if the customer types `red co`, the backend can treat `co` as the active suggestion segment while using `red co` as context, allowing it to rank complementary suggestions such as fabrics or categories above more colors.

Suggestion chips are grouped in the frontend by type, such as category, fabric, color, texture, print, use, and size.

---

## Facets And Refinements

Facets are calculated in a way that supports both precision and discovery.

Facet groups are disjunctive: each group can be calculated by excluding its own active constraint while preserving the rest of the search intent.

For example, in a search like `crimson lulua`, the main result set can stay strict, while the fabric facet can show other fabrics available in crimson.

Color facets are intentionally tighter than fabric facets because broad color expansion can become noisy. If a customer searches for red, the color refinements stay focused on direct red-family values instead of showing unrelated colors from loosely matching products.

Facet values are built from stored Lucene document fields, not hydrated database products, which keeps refinement calculation fast and tied to indexed search data.

---

## Frontend Search UX

The frontend keeps two search states:

- `query`: what the customer is typing
- `submittedQuery`: what has actually been searched

This creates a controlled search experience:

- Typing fetches suggestions only
- Pressing search runs a product search
- Clicking refinements or category chips updates the submitted search

The search UI supports:

- Category shortcut chips
- Removable selected category chip
- Grouped suggestion chips
- Facet/refinement bottom sheet
- Infinite loading
- Did-you-mean correction clicks
- Search outcome and improvement metadata
