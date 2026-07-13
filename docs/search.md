# Search Design

LUCE search is built with Lucene.NET and designed around structured ecommerce discovery, not only basic free-text lookup.

The public showcase keeps this description intentionally high-level. The goal is to demonstrate the engineering approach without exposing the full internal search behavior.

---

## Approach

Search combines full-text retrieval with catalog-aware interpretation so customers can find products through natural shopping language, product attributes, and category context.

The system is designed to support:

- Attribute-aware product discovery
- Typo-tolerant search behavior
- Inventory-aware suggestions
- Refinements that remain aligned with the submitted search
- Stable result handling across listing, search, and product-detail flows

---

## UX Model

The frontend separates typing from submitted search. Typing can show suggestions, while the product grid updates only after the customer explicitly searches or selects a refinement.

This keeps the experience predictable on mobile and avoids constantly reshuffling products while the customer is still composing a query.

---

## Engineering Notes

Search responsibilities are separated from relational product retrieval. Lucene handles search-oriented retrieval and discovery metadata, while the backend product layer returns the storefront-ready product shapes needed by the UI.

This separation keeps search fast, avoids over-fetching, and makes the storefront easier to evolve without coupling every UI change directly to the search index.
