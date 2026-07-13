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
- Reusable catalog attributes
- Product images and media mapping
- Inventory behavior
- Recommendation services
- Customer authentication and refresh-token sessions
- Admin authorization
- Lucene.NET indexing and search retrieval
- Media optimization for storefront and admin use

---

## Search Boundary

Search behavior is separated from relational product retrieval.

Lucene handles search-oriented retrieval, suggestions, and indexed discovery metadata. Relational product retrieval handles the hydrated storefront shapes needed by the frontend.

This separation keeps search fast and keeps the product API aligned with actual UI needs instead of returning generic database entities.

---

## Frontend Responsibilities

The frontend focuses on product presentation, controlled search state, cart interactions, quick-view flows, bottom sheets, filters, mobile gestures, and responsive desktop/mobile layouts.

State is kept lightweight and organized around actual UI behavior so customer interactions remain predictable across mobile and desktop.

---

## Launch-Oriented Design

The architecture is designed around maintainability and eventual business launch:

- Clear backend layering
- Domain-aware product models
- Dedicated search and recommendation boundaries
- Secure account sessions
- Admin workflows for catalog operations
- Performance-aware query and cache boundaries
- Server-side media processing for storefront assets
