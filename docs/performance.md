# Performance Considerations

LUCE is built with attention to practical performance concerns across backend APIs, search, catalog retrieval, recommendations, and media handling.

---

## Backend And Database

Important considerations include:

- Avoiding N+1 query patterns
- Returning product card data in frontend-friendly shapes
- Avoiding unnecessary over-fetching
- Designing APIs around actual UI usage instead of generic data dumping
- Indexing frequently queried relational fields
- Keeping account, catalog, search, and recommendation queries efficient as usage grows

Relevant database fields are indexed to improve lookup performance across customer-facing and admin-facing flows.

---

## Search Performance

Search performance considerations include:

- Separating Lucene search results from relational product retrieval
- Keeping search-oriented reads bounded
- Caching search-related responses where useful
- Invalidating stale search data when catalog updates occur

---

## Media And Storefront

The platform includes server-side media optimization for different storefront uses, including product cards, detail views, previews, and admin workflows.

This keeps uploaded catalog media aligned with how the frontend actually displays images.
