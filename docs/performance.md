# Performance Considerations

LUCE is built with attention to practical performance concerns across backend APIs, search, catalog retrieval, recommendations, and media handling.

---

## Backend And Database

Important considerations include:

- Avoiding N+1 query patterns
- Returning product card data in frontend-friendly shapes
- Avoiding unnecessary over-fetching
- Designing APIs around actual UI usage instead of generic data dumping
- Indexing frequently queried relational fields used by search, catalog browsing, recommendations, authentication, and personalization
- Keeping recommendation and authentication queries efficient as customer behavior, cart context, and catalog size grow

Relevant database fields are indexed to improve lookup performance for product discovery, recommendations, authentication, and account flows.

---

## Search Performance

Search performance considerations include:

- Separating Lucene search results from relational product retrieval
- Using Lucene-stored fields for fast facet calculation
- Capping search and facet result windows to avoid expensive reads
- Caching search responses, suggestions, inventory vocabulary, and disjunctive facets
- Versioning search cache entries so index rebuilds and product updates invalidate stale results naturally

---

## Media And Storefront

The platform includes server-side media optimization for different storefront uses, including product cards, detail views, previews, and admin workflows.

This keeps uploaded catalog media aligned with how the frontend actually displays images.
