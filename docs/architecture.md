# Architecture

LUCE is organized as a full-stack ecommerce platform with a React frontend, ASP.NET Core backend, PostgreSQL database, Lucene.NET search layer, and server-side image processing.

The backend follows a layered architecture:

```txt
Controller -> Service -> Repository -> DbContext -> PostgreSQL
```

---

## Backend Responsibilities

The backend handles:

- Product catalog management
- Categories, colors, palettes, fabrics, textures, and tags
- Product images and color-specific media mapping
- Inventory behavior
- Recommendation logic
- Customer authentication and refresh-token sessions
- Admin authorization
- Lucene.NET indexing and search retrieval
- Media optimization for storefront and admin use

---

## Search Boundary

Search behavior is separated from relational product retrieval.

Lucene handles full-text and structured retrieval, suggestions, indexed vocabulary, stored fields, facets, and search-stage behavior. Relational product retrieval handles the hydrated storefront shapes needed by the frontend.

This separation keeps search fast and keeps the product API aligned with actual UI needs instead of returning generic database entities.

---

## Frontend Responsibilities

The frontend focuses on product presentation, controlled search state, cart interactions, quick-view flows, bottom sheets, filters, mobile gestures, and responsive desktop/mobile layouts.

State is kept lightweight. Local UI state is separated from submitted search state so the customer can type, review suggestions, and explicitly run searches without the product grid changing unexpectedly.

---

## Launch-Oriented Design

The architecture is designed around maintainability and eventual business launch:

- Clear backend layering
- Domain-specific product models
- Dedicated search and recommendation logic
- Secure account sessions
- Admin workflows for catalog operations
- Performance-aware query and cache boundaries
- Server-side media processing for storefront assets
