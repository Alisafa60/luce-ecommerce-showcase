# LUCE Ecommerce Platform

LUCE is a full-stack ecommerce platform designed for modest fashion and headscarf retail.

The project was built from the perspective of a business owner in a niche retail space where generic ecommerce tools often fall short. Headscarf products are not only browsed by name, price, and category, but also by fabric, shape, opacity, color family, printed palette, styling need, and how well they pair with essentials such as underscarves and accessories.

LUCE explores what a more tailored software experience for this category can look like: a premium mobile-first storefront, structured commerce search, color-aware product discovery, personalized recommendations, secure customer accounts, and admin workflows designed around real catalog and merchandising needs.

The product is planned for public launch after final product photography and catalog preparation. Until then, this repository presents the product concept, UI/UX direction, screenshots, architecture, and implementation thinking behind the platform. The source code is private.

I designed and implemented the full UI/UX, frontend, backend, search, recommendation logic, authentication model, and admin workflows end to end.

---

## Preview

![LUCE desktop hero](assets/screenshots/desktop/desktop-hero-editorial.png)

---

## What I Built

LUCE is a full-stack ecommerce system shaped around how modest fashion and scarf products are browsed, styled, searched, recommended, and sold.

It includes:

- A premium responsive storefront with a mobile-first, app-like feel
- Category discovery built around scarf shapes, fabrics, styling needs, essentials, and accessories
- Product grids with color and palette-aware presentation
- Product detail and quick-view flows optimized for uninterrupted browsing
- Lucene.NET-powered structured search with suggestions, facets, and fallback stages
- Color-aware recommendation logic for matching scarves with essentials and accessories
- Cart flows with contextual recommendations
- Customer authentication with refresh-token-based sessions
- Admin catalog tooling for products, media, inventory, attributes, and merchandising metadata
- Backend architecture designed around maintainability, performance, and secure account flows

---

## Why This Product Exists

Many small fashion retailers rely on generic ecommerce tools that treat every product like a simple item with a name, price, and image.

That is not enough for headscarves and modest fashion. Customers care about fabric, shape, opacity, color families, printed palettes, matching underscarves, accessories, styling intent, and whether a product works with what they already selected.

LUCE models those details directly. The platform is built from the perspective of a real business owner who needs the storefront, search, recommendations, and admin tools to reflect how the products are actually sold.

---

## Tech Stack

### Frontend

- React + TypeScript
- Responsive, mobile-first UI
- Zustand for lightweight client-side state management
- Native CSS with TypeScript-driven interactions
- Custom bottom sheets, overlays, and touch interactions
- Selective Framer Motion usage for isolated micro-transitions

### Backend

- ASP.NET Core Web API
- PostgreSQL
- Entity Framework Core
- Layered Controller-Service-Repository architecture
- JWT authentication with database-backed refresh tokens
- Lucene.NET search service
- Server-side image processing with ImageSharp

---

## Product Experience

The storefront is intentionally restrained and product-led. It uses large imagery, generous spacing, subtle typography, soft transitions, and minimal card chrome so the catalog feels premium instead of noisy.

The mobile experience uses familiar app-like patterns such as bottom sheets, quick views, swipe-aware interactions, scroll-reactive controls, and full-screen discovery surfaces. Desktop layouts preserve the same visual direction while using the available space for richer browsing.

<img src="assets/screenshots/mobile/mobile-hero.png" alt="Mobile hero" width="260" />

![Desktop category discovery](assets/screenshots/desktop/desktop-category-discovery.png)

---

## Navigation And Discovery

Navigation is organized around how customers shop this category: by shape, purpose, fabric, styling need, and accessory type instead of only generic menu labels.

Customers can browse scarf categories, essentials, basics, extensions, and accessories with supporting imagery. One category section opens by default to give a clear starting point while still exposing the full product structure.

<img src="assets/screenshots/mobile/mobile-navigation-menu.png" alt="Mobile navigation" width="260" />

![Desktop navigation](assets/screenshots/desktop/desktop-navigation-menu.png)

---

## Product Browsing

The product grid keeps attention on the products while still exposing the information that matters for scarf shopping.

Plain products can show selectable color swatches that update the product image. Printed products can show compact palette previews, with fuller color details available from the product detail or quick-view flow.

<img src="assets/screenshots/mobile/mobile-product-grid.png" alt="Mobile product grid" width="260" />

![Desktop product grid](assets/screenshots/desktop/desktop-product-grid.png)

<img src="assets/screenshots/mobile/mobile-product-grid-selected-colors.png" alt="Selected color behavior" width="260" />

Product details open without interrupting the browsing flow. On mobile, details appear in a bottom sheet. On desktop, they appear as a modal-style view over the product grid.

<img src="assets/screenshots/mobile/mobile-product-quick-view.png" alt="Mobile product quick view" width="260" />

![Desktop product modal](assets/screenshots/desktop/desktop-product-modal.png)

---

## Search And Recommendations

Search is powered by Lucene.NET and designed around structured ecommerce discovery, not only free-text product lookup.

The system interprets customer intent around attributes such as category, fabric, color, texture, print, size, and tags. It supports strict, relaxed, and fuzzy fallback search stages, inventory-aware suggestions, and dynamic refinements that stay useful without losing the customer's intent.

For example, a query like `crimson lulua` can be treated as structured intent: color = crimson and fabric = lulua. The main results can stay precise while refinements still help the customer explore related available inventory.

<img src="assets/screenshots/mobile/mobile-search-results.png" alt="Mobile search results" width="260" />

<img src="assets/screenshots/mobile/mobile-search-refinement-sheet.png" alt="Search refinement sheet" width="260" />

Recommendations are placement-aware and color-aware. Matching logic can use selected scarf colors, printed palettes, cart contents, customer behavior, and product classification to suggest useful essentials, accessories, or inspiration products.

<img src="assets/screenshots/mobile/mobile-recommendation-sheet.png" alt="Recommendation sheet" width="260" />

Detailed writeups:

- [Search design](docs/search.md)
- [Recommendation system](docs/recommendations.md)

---

## Cart And Account Flow

The cart is designed as part of the shopping experience rather than a disconnected final page. It supports variant-aware cart items, quantity updates, item deletion, total price display, and contextual recommendations.

Essentials can be quick-added with a recommended color, while main scarves are shown as inspiration with a `VIEW` action instead of receiving an unwanted preselected color.

<img src="assets/screenshots/mobile/mobile-cart.png" alt="Mobile cart" width="260" />

Customer accounts use short-lived JWT access tokens and database-backed refresh tokens stored in `HttpOnly` cookies. Guest browsing remains available, and guest recommendation sessions can be connected to a customer profile after login or signup.

Detailed writeup:

- [Authentication model](docs/auth.md)

---

## Admin Platform

The admin workspace supports catalog workflows where color accuracy, product imagery, fabric metadata, stock state, search behavior, and recommendation behavior directly affect the storefront.

Admin functionality includes product creation and editing, reusable attribute libraries, category and inventory management, plain versus printed product configuration, product-level and color-specific image mapping, media validation, and recommendation classification fields.

![Admin product workspace](assets/screenshots/admin/admin-product-workspace.png)

Detailed writeup:

- [Admin workflows](docs/admin-workflows.md)

---

## Architecture Highlights

The backend follows a layered architecture:

```txt
Controller -> Service -> Repository -> DbContext -> PostgreSQL
```

The platform separates storefront behavior, catalog management, search indexing, recommendation logic, authentication, and media handling into focused backend responsibilities. Lucene search results are separated from relational product retrieval, and performance-sensitive areas use cached vocabulary, indexed fields, stored Lucene fields, and bounded result windows.

Detailed writeups:

- [Architecture](docs/architecture.md)
- [Data modeling](docs/data-modeling.md)
- [Performance considerations](docs/performance.md)

---

## What This Demonstrates

LUCE demonstrates full-stack product engineering across frontend, backend, search, data modeling, authentication, recommendations, admin tooling, and UX.

The strongest parts of the project are:

- Building software around a real business domain rather than a generic demo brief
- Translating niche product behavior into data models, UI flows, and backend logic
- Designing a premium mobile-first ecommerce experience
- Implementing structured Lucene.NET search with suggestions, facets, and fallback behavior
- Building color-aware recommendations for scarf-to-essential matching
- Designing secure account sessions with refresh-token rotation
- Creating admin workflows that support real catalog operations
- Thinking about performance, maintainability, and launch-readiness from the start
