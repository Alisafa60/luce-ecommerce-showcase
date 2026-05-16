 # LUCE — Fashion Ecommerce Platform

LUCE is a personal full-stack fashion ecommerce platform built with React, TypeScript, ASP.NET Core, PostgreSQL, and Lucene.NET.

The project was built from the perspective of a business owner in the modest fashion and headscarf space, where many retailers rely on generic ecommerce tools that do not fully reflect how their products are browsed, styled, searched, and sold.

LUCE explores what a more tailored software experience for this category can look like: a premium mobile-first storefront, color-aware product discovery, refined product presentation, intelligent recommendations, and admin workflows designed around real catalog and merchandising needs.

The source code is private, but this repository presents the product concept, UI/UX direction, screenshots, architecture, and implementation thinking behind the platform.

---

## Preview

![LUCE desktop hero](assets/screenshots/desktop/desktop-hero-editorial.png)

---

## Overview

LUCE is designed around how modest fashion and scarf products are browsed, styled, searched, and purchased.

The platform supports a variety of fashion products, with special handling for scarf-specific behavior such as plain colors, printed palettes, fabric differences, color variants, essentials, and accessories. The interface is intentionally minimal and product-first, using photography, spacing, color, and subtle interactions to create a premium shopping experience without overwhelming the customer.

The project is not only a storefront UI. It includes product modeling, search and filtering, color-aware recommendations, admin catalog management, and backend architecture designed around maintainability and performance.

---

## Tech Stack

### Frontend

- React + TypeScript
- Responsive, mobile-first UI
- Native CSS with TypeScript-driven interactions
- Custom bottom sheets, overlays, and touch interactions without a heavy UI component framework
- Selective Framer Motion usage for isolated micro-transitions

### Backend

- ASP.NET Core Web API
- PostgreSQL
- Entity Framework Core
- Layered Controller-Service-Repository architecture using ASP.NET Core Dependency Injection
- Lucene.NET-powered search service
- Server-side image processing with ImageSharp

### Product Discovery

- Lucene.NET full-text indexing and retrieval
- Taxonomy-aware search behavior
- Exact and fuzzy matching support
- Typo-tolerant search handling
- Dynamic faceting and refinements
- Color-aware product matching and ranking

---

## Search and Reliability Highlights

The search system is designed to preserve user intent while still handling imperfect queries, missing terms, and changing catalog data.

Key implementation areas include:

- Search behavior that respects category, fabric, color, and texture intent
- Multi-stage retrieval to balance precision with fallback behavior
- Stable result handling to avoid duplicate or inconsistent search results
- Search UX metadata such as suggestion hints, outcome messages, and matched color chips
- Cache invalidation patterns for keeping catalog/search data consistent
- Media validation to keep product images aligned with database records

---

## Product and UX Direction

The app is designed with a mobile-first, app-like shopping experience.

The UI is intentionally restrained. Instead of relying on heavy visual effects, the design uses large product images, generous spacing, subtle typography, soft transitions, and clear product hierarchy.

Important UX decisions include:

- Full-screen immersive homepage hero
- Purpose-based navigation with category imagery
- Large product cards with minimal visual noise
- Bottom sheets for filters, product details, and recommendations
- Scroll-reactive filter and tag bars
- Swipe-aware mobile interactions
- Desktop layouts that preserve the same premium visual direction while using the available space more effectively

<img src="assets/screenshots/mobile/mobile-hero.png" alt="Mobile hero" width="260" />

![Desktop category discovery](assets/screenshots/desktop/desktop-category-discovery.png)

---

## Navigation

The navigation is built around how customers browse scarf and modest fashion products: by shape, purpose, fabric, styling need, and accessory type instead of a simple generic category menu.

Customers can browse through main and child categories with supporting imagery. One category section is opened by default, giving the customer a clear starting point while still exposing the full product structure.

Example categories include:

- Rectangular scarves
- Squared scarves
- Instant scarves
- Underscarves
- Extensions
- Accessories

<img src="assets/screenshots/mobile/mobile-navigation-menu.png" alt="Mobile navigation" width="260" />

![Desktop navigation](assets/screenshots/desktop/desktop-navigation-menu.png)

---

## Product Grid

The product grid is designed to keep attention on the products.

It uses large imagery, generous padding, minimal card chrome, quick product actions, and color or palette indicators depending on the product type.

<img src="assets/screenshots/mobile/mobile-product-grid.png" alt="Mobile product grid" width="260" />

![Desktop product grid](assets/screenshots/desktop/desktop-product-grid.png)

---

## Product Presentation Behavior

Different product types are presented in ways that match how customers evaluate them.

Plain products can show selectable color swatches that update the product image. Printed or palette-based products can show compact color previews, with fuller color details available in the product detail or quick product view.

This keeps the product grid minimal while preserving accurate color, variant, and browsing behavior.

<img src="assets/screenshots/mobile/mobile-product-grid-selected-colors.png" alt="Selected color behavior" width="260" />

---

## Product Details

Product details can be opened without interrupting the browsing flow.

On mobile, product information appears in a bottom sheet. On desktop, it appears as a larger modal-style view over the product grid.

The detail view includes product images, price, sale price, fabric, dimensions, description, add-to-bag action, and color or palette information.

<img src="assets/screenshots/mobile/mobile-product-quick-view.png" alt="Mobile product quick view" width="260" />

![Desktop product modal](assets/screenshots/desktop/desktop-product-modal.png)

![Desktop product detail](assets/screenshots/desktop/desktop-product-detail.png)

---

## Search and Product Discovery

Search is built with Lucene.NET and designed around real ecommerce discovery behavior.

The search system supports exact matching, fuzzy fallback, typo-tolerant behavior, taxonomy-aware ranking, and attribute-aware product matching.

It understands product concepts such as:

- Main and child categories
- Colors
- Fabrics
- Textures
- Product types
- Printed palette colors
- Plain selectable colors

For example, when searching by color, a plain scarf can show a direct matching swatch, while a printed scarf can match because the print contains that color. The search results respect the difference instead of flattening both products into the same behavior.

<img src="assets/screenshots/mobile/mobile-search-results.png" alt="Mobile search results" width="260" />

<img src="assets/screenshots/mobile/mobile-search-refinement-sheet.png" alt="Search refinement sheet" width="260" />

---

## Filters

Filters are designed to be easy to reach without taking over the shopping experience.

The product listing supports dynamic filters such as color, fabric, texture, price, and category tags. Color filters are generated from the current product set and ordered to feel visually natural instead of random or purely alphabetical.

On mobile, filters appear in a bottom sheet with a native-feeling interaction pattern.

<img src="assets/screenshots/mobile/mobile-filter-sheet.png" alt="Mobile filter sheet" width="260" />

---

## Recommendations

Recommendations are designed around styling and outfit-completion behavior rather than random upsells.

When a customer adds a scarf to the cart, the platform can suggest relevant essentials such as bonnets, underscarves, pins, or accessories based on the selected product context.

This makes recommendations feel connected to how the product is actually worn and styled.

<img src="assets/screenshots/mobile/mobile-recommendation-sheet.png" alt="Recommendation sheet" width="260" />

---

## Cart

The cart is designed as part of the shopping experience rather than a disconnected final page.

It supports product review, quantity updates, variant-aware cart items, item deletion, and total price display in a mobile-first layout.

<img src="assets/screenshots/mobile/mobile-cart.png" alt="Mobile cart" width="260" />

---

## Admin and Catalog Management

The platform includes admin-facing catalog workflows for managing products, attributes, media, inventory, and product discovery data.

The admin workspace is designed for catalog workflows where color accuracy, product imagery, fabric metadata, stock state, and product presentation directly affect the shopping experience.

Admin functionality includes:

- Product creation and editing through a multi-step workspace
- Category, fabric, texture, tag, color, pricing, and inventory management
- Attribute library workflows for maintaining reusable catalog metadata
- Plain versus printed product configuration
- Product-level and color-specific image mapping
- Draft autosave for product creation flows
- Media validation to keep product images aligned with product records
- Server-side media optimization for storefront, detail, and preview usage
- Essential product marking for recommendation behavior

![Admin product workspace](assets/screenshots/admin/admin-product-workspace.png)

---

## Backend Architecture

The backend follows a layered architecture:

`Controller → Service → Repository → DbContext → PostgreSQL`

The backend handles product catalog management, categories, colors, palettes, product images, inventory behavior, essential product marking, recommendation logic, and Lucene.NET search indexing.

Product behavior is modeled around variant handling, palette relationships, search metadata, recommendations, and media mapping, keeping the storefront logic consistent across listing, detail, search, and cart flows.

---

## Data Modeling

The data model is designed around catalog consistency, product discovery, and accurate storefront behavior.

It supports structured relationships between products, colors, images, categories, fabrics, textures, tags, inventory, recommendations, and admin-managed attributes.

This allows the frontend to present products accurately without relying on fragile UI-only assumptions.

For example:

- Product images can be mapped to specific colors or product states.
- Plain and printed products can have different presentation behavior.
- Search can distinguish direct color matches from contained palette colors.
- Recommendations can use selected product context, color families, and neutral fallback options.

---

## Performance Considerations

The platform is built with attention to practical performance concerns.

Important considerations include:

- Avoiding N+1 query patterns
- Returning product card data in frontend-friendly shapes
- Separating Lucene search results from relational product retrieval
- Avoiding unnecessary over-fetching
- Keeping product discovery queries efficient
- Optimizing uploaded product media for different storefront uses
- Using cache invalidation patterns for stale-data control
- Designing APIs around actual UI usage instead of generic data dumping

---

## What This Project Demonstrates

LUCE demonstrates full-stack product engineering across frontend, backend, search, data modeling, and UX.

It highlights:

- Premium mobile-first UI design
- Responsive desktop and mobile layouts
- App-like ecommerce interactions
- Custom touch behavior without a heavy UI component framework
- Business-specific product modeling
- Lucene.NET search integration
- Taxonomy-aware filtering and query interpretation
- Dynamic color and palette systems
- Color-aware recommendations
- Performance-aware backend design
- Clean separation between controllers, services, repositories, and database
