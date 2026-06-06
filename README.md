# LUCE Ecommerce Platform

LUCE is a personal full-stack fashion ecommerce platform built with React, TypeScript, ASP.NET Core, PostgreSQL, and Lucene.NET.

The project was built from the perspective of a business owner in the modest fashion and headscarf space, where many retailers rely on generic ecommerce tools that do not fully reflect how their products are browsed, styled, searched, recommended, and sold.

LUCE explores what a more tailored software experience for this category can look like: a premium mobile-first storefront, structured commerce search, color-aware product discovery, personalized recommendations, secure customer accounts, and admin workflows designed around real catalog and merchandising needs.

The source code is private, but this repository presents the product concept, UI/UX direction, screenshots, architecture, and implementation thinking behind the platform.

---

## Preview

![LUCE desktop hero](assets/screenshots/desktop/desktop-hero-editorial.png)

---

## Overview

LUCE is designed around how modest fashion and scarf products are browsed, styled, searched, recommended, and purchased.

The platform supports a variety of fashion products, with special handling for scarf-specific behavior such as plain colors, printed palettes, fabric differences, color variants, essentials, basics, extensions, and accessories.

The project is not only a storefront UI. It includes product modeling, structured search and filtering, personalized recommendations, customer authentication, admin catalog management, and backend architecture designed around maintainability, security, and performance.

Key product goals include:

- A premium, mobile-first shopping experience
- Accurate product presentation for plain and printed scarf products
- Search behavior that understands fashion-specific attributes
- Inventory-aware suggestions and refinements
- Color-aware recommendations for essentials and add-ons
- Secure customer accounts with refresh-token-based sessions
- Admin tools for managing catalog, media, inventory, and merchandising data

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
- Lucene.NET-powered search service
- Server-side image processing with ImageSharp

### Product Discovery

- Lucene.NET full-text indexing and retrieval
- Structured query interpretation
- Taxonomy-aware search behavior
- Exact, relaxed, and fuzzy fallback search stages
- Inventory-aware suggestions
- Dynamic faceting and refinements
- Color-aware product matching and ranking
- Placement-aware recommendation logic
- Customer preference tracking for personalization

---

## Product and UX Direction

The app is designed with a mobile-first, app-like shopping experience.

The UI is intentionally restrained. Instead of relying on heavy visual effects, the design uses large product images, generous spacing, subtle typography, soft transitions, and clear product hierarchy.

Important UX decisions include:

- Full-screen immersive homepage hero
- Purpose-based navigation with category imagery
- Large product cards with minimal visual noise
- Bottom sheets for filters, product details, account flows, and recommendations
- Press-to-search behavior for more controlled results
- Search suggestions while typing
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
- Basics and extensions
- Accessories

<img src="assets/screenshots/mobile/mobile-navigation-menu.png" alt="Mobile navigation" width="260" />

![Desktop navigation](assets/screenshots/desktop/desktop-navigation-menu.png)

---

## Product Grid

The product grid is designed to keep attention on the products.

It uses large imagery, generous padding, minimal card chrome, quick product actions, and color or palette indicators depending on the product type.

Plain products can show selectable color swatches that update the product image. Printed or palette-based products can show compact color previews, with fuller color details available in the product detail or quick product view.

This keeps the grid minimal while preserving accurate color, variant, and browsing behavior.

<img src="assets/screenshots/mobile/mobile-product-grid.png" alt="Mobile product grid" width="260" />

![Desktop product grid](assets/screenshots/desktop/desktop-product-grid.png)

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

## Structured Search and Product Discovery

Search is built with Lucene.NET and designed around structured ecommerce discovery, not only free-text product lookup.

The system interprets customer intent around product attributes such as category, fabric, color, texture, print, size, and tags. This allows searches like `crimson lulua` to be understood as structured intent: color = crimson and fabric = lulua.

Main search results stay strict when the customer gives explicit intent, while refinements remain useful for discovery. For example, a search for `crimson lulua` can keep the main result set limited to crimson lulua products, while fabric refinements may still show other fabrics that exist in crimson.

The search system understands product concepts such as:

- Main and child categories
- Direct and parent colors
- Direct and parent fabrics
- Textures and tags
- Product types
- Print names and palette names
- Printed palette colors
- Plain selectable colors
- Size and shape attributes

For example, a broad search for `green` can match an olive product through its parent color relationship, while the refinement UI still shows the actual direct product value, such as `olive`, instead of only showing the parent term `green`.

### Query Interpretation

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

### Search Stages

The search runs through staged retrieval:

1. Strict
2. Relaxed
3. Fuzzy fallback

Strict search is preferred for explicit structured intent. Relaxed and fuzzy stages are used when needed to avoid empty or unhelpful results.

This keeps precise searches precise, while still supporting imperfect queries and typos.

### Suggestions

Search is explicit and press-to-search. Typing only fetches suggestions; it does not automatically run a full product search.

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

### Facets and Refinements

Facets are calculated in a way that supports both precision and discovery.

Facet groups are disjunctive: each group can be calculated by excluding its own active constraint while preserving the rest of the search intent.

For example, in a search like `crimson lulua`, the main result set can stay strict, while the fabric facet can show other fabrics available in crimson.

Color facets are intentionally tighter than fabric facets because broad color expansion can become noisy. If a customer searches for red, the color refinements stay focused on direct red-family values instead of showing every unrelated color from loosely matching products.

Facet values are built from stored Lucene document fields, not hydrated database products, which keeps refinement calculation fast and tied to indexed search data.

### Search UX

The frontend keeps two search states:

- `query`: what the customer is typing
- `submittedQuery`: what has actually been searched

This creates a controlled search experience:

- Typing fetches suggestions only.
- Pressing search runs a product search.
- Clicking refinements or category chips updates the submitted search.

The search UI supports:

- Category shortcut chips
- Removable selected category chip
- Grouped suggestion chips
- Facet/refinement bottom sheet
- Infinite loading
- Did-you-mean correction clicks
- Search outcome and improvement metadata

<img src="assets/screenshots/mobile/mobile-search-results.png" alt="Mobile search results" width="260" />

<img src="assets/screenshots/mobile/mobile-search-refinement-sheet.png" alt="Search refinement sheet" width="260" />

---

## Filters

Filters are designed to be easy to reach without taking over the shopping experience.

The product listing supports dynamic filters such as color, fabric, texture, price, and category tags. Color filters are generated from the current product set and ordered to feel visually natural instead of random or purely alphabetical.

On mobile, filters appear in a bottom sheet with a native-feeling interaction pattern.

<img src="assets/screenshots/mobile/mobile-filter-sheet.png" alt="Mobile filter sheet" width="260" />

---

## Personalized Recommendations

LUCE includes a placement-aware recommendation system designed around a scarf-first ecommerce model.

Recommendations are not treated as generic upsells. They adapt based on where they appear in the shopping flow and use product context, selected colors, cart contents, and customer behavior to suggest items that feel useful and relevant.

Recommendation placements include:

- **Add-to-cart popup**: matching essentials for the scarf or color the customer just added
- **Cart recommendations**: useful add-ons and style inspiration based on the full cart
- **Home page**: broader personalized picks, with preference toward main scarves
- **Search empty state**: personalized starter picks before the customer searches

### Color-Aware Essentials

For essentials such as underscarves, bonnets, basics, extensions, and accessories, recommendations can use the selected scarf color when available.

The matching flow prioritizes:

1. Exact color match
2. Closest wearable color using perceptual color distance
3. Same color-family match
4. Soft neutral fallback

This is especially useful for products like underscarves and bonnets, where customers often want a matching or complementary color.

The scarf-to-underscarf matching logic uses CIEDE2000 color distance with hue and lightness guards to avoid visually poor matches. Manual styling metadata such as color temperature, mood, neutral group, and soft-neutral classification can provide small scoring nudges, but the core matching remains visual and still works for colors without metadata.

For printed scarves, the recommendation logic evaluates configured palette colors such as base, dominant, and printed colors, then chooses the best overall match instead of assuming one color should always drive the recommendation.

### Cart-Aware Logic

Cart recommendations separate two different recommendation goals:

- **Essentials** are shown as quick-add items with a recommended color.
- **Main scarves** are shown as inspiration with a `VIEW` action instead of quick-add.

This prevents main scarves from receiving an unwanted preselected color, while still allowing color-matched essentials to be added quickly.

### Preference Tracking

The system tracks customer behavior to improve personalization over time.

Tracked events include:

- Product views
- Add to cart
- Recommendation clicks
- Recommendation add-to-cart
- Purchases

Guest sessions are tracked with a local recommendation session id and can be merged into the customer profile after login or signup.

<img src="assets/screenshots/mobile/mobile-recommendation-sheet.png" alt="Recommendation sheet" width="260" />

---

## Cart

The cart is designed as part of the shopping experience rather than a disconnected final page.

It supports product review, quantity updates, variant-aware cart items, item deletion, total price display, and contextual recommendations in a mobile-first layout.

Cart recommendations use the full cart context to suggest useful additions. Essentials can be quick-added with a recommended color, while main scarf recommendations are shown as inspiration and opened with a `VIEW` action.

<img src="assets/screenshots/mobile/mobile-cart.png" alt="Mobile cart" width="260" />

---

## Authentication and Account Flow

LUCE includes a customer and admin authentication flow built around short-lived JWT access tokens and database-backed refresh tokens.

The goal is to support secure customer accounts without interrupting the guest shopping experience. Customers can still browse products, search, use cart flows, and continue shopping without logging in.

### Auth Model

- Access tokens are returned to the frontend after login or signup.
- Refresh tokens are stored in an `HttpOnly` cookie.
- Refresh tokens are hashed before being stored in the database.
- Expired or revoked refresh tokens cannot be reused.
- Refresh token rotation is used when refreshing a session.
- Logout and logout-from-all-devices behavior is supported through the refresh token model.

### Customer Accounts

Customer accounts are designed to support:

- Saved delivery details
- Faster checkout
- Personalized recommendations
- Order history
- Account preferences

Guest shopping remains available, and guest recommendation sessions can be connected to the customer profile after login or signup.

### Admin Accounts

Admins use the same login flow, but receive an admin role claim in the access token.

Admin-only routes are protected with role-based authorization, and admin account creation is restricted to authenticated admins.

---

## Admin and Catalog Management

The platform includes admin-facing catalog workflows for managing products, attributes, media, inventory, recommendation data, and product discovery data.

The admin workspace is designed for catalog workflows where color accuracy, product imagery, fabric metadata, stock state, product presentation, search behavior, and recommendation behavior directly affect the shopping experience.

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
- Product classification fields used by search and recommendations
- Protected admin account creation

![Admin product workspace](assets/screenshots/admin/admin-product-workspace.png)

---

## Backend Architecture

The backend follows a layered architecture:

```txt
Controller → Service → Repository → DbContext → PostgreSQL
```

The backend handles product catalog management, categories, colors, palettes, product images, inventory behavior, recommendation logic, customer authentication, refresh token sessions, and Lucene.NET search indexing.

Product behavior is modeled around variant handling, palette relationships, search metadata, recommendations, customer preference tracking, and media mapping, keeping the storefront logic consistent across listing, detail, search, cart, and account flows.

The search implementation is organized around a Lucene search service with helper components for query interpretation, indexed vocabulary, search stages, suggestions, facets, and cache-aware retrieval.

---

## Data Modeling

The data model is designed around catalog consistency, product discovery, accurate storefront behavior, personalization, and secure account flows.

It supports structured relationships between products, colors, images, categories, fabrics, textures, tags, inventory, recommendations, customer preferences, refresh tokens, and admin-managed attributes.

This allows the frontend to present products accurately without relying on fragile UI-only assumptions.

For example:

- Product images can be mapped to specific colors or product states.
- Plain and printed products can have different presentation behavior.
- Search can distinguish direct color matches from contained palette colors.
- Parent and child attributes can support both broad search and accurate direct refinements.
- Recommendations can use selected product context, perceptual color distance, color families, and soft-neutral fallback options.
- Customer behavior can influence future recommendation results.
- Refresh token records can support secure session rotation, revocation, logout, and logout from all devices.

Recommendation behavior is supported by explicit product classification fields such as `ProductFamily` and `ProductType`.

Examples include:

- `MainScarf`
- `Underscarf`
- `Extension`
- `Accessory`
- `BasicTop`

Color-aware recommendation behavior is also supported by optional manual styling metadata such as color temperature, mood, neutral group, and soft-neutral classification. These fields help guide recommendation scoring without replacing the visual matching logic.

---

## Performance Considerations

The platform is built with attention to practical performance concerns.

Important considerations include:

- Avoiding N+1 query patterns
- Returning product card data in frontend-friendly shapes
- Separating Lucene search results from relational product retrieval
- Avoiding unnecessary over-fetching
- Using Lucene-stored fields for fast facet calculation
- Capping search and facet result windows to avoid expensive reads
- Caching search responses, suggestions, inventory vocabulary, and disjunctive facets
- Versioning search cache entries so index rebuilds and product updates invalidate stale results naturally
- Optimizing uploaded product media for different storefront uses
- Using cache invalidation patterns for stale-data control
- Designing APIs around actual UI usage instead of generic data dumping
- Indexing frequently queried relational fields used by search, catalog browsing, recommendations, authentication, and personalization
- Keeping recommendation and authentication queries efficient as customer behavior, cart context, and catalog size grow
- Using a database-backed refresh token model that supports rotation, revocation, logout, and logout from all devices

Relevant database fields are indexed to improve lookup performance for product discovery, recommendations, authentication, and account flows. This helps avoid unnecessary full-table scans when resolving product relationships, filtering catalog data, matching recommendation candidates, validating refresh tokens, and loading customer-specific data.

---

## What This Project Demonstrates

LUCE demonstrates full-stack product engineering across frontend, backend, search, data modeling, authentication, recommendations, and UX.

It highlights:

- Premium mobile-first UI design
- Responsive desktop and mobile layouts
- App-like ecommerce interactions
- Custom touch behavior without a heavy UI component framework
- Business-specific product modeling
- Lucene.NET search integration
- Structured query interpretation
- Taxonomy-aware filtering and search behavior
- Inventory-aware suggestions
- Dynamic color and palette systems
- Disjunctive facet and refinement logic
- Placement-aware personalized recommendations
- Perceptual color-matching logic for scarf-to-essential recommendations
- Lightweight styling metadata used to guide recommendation scoring
- Cart-aware recommendation logic
- Customer preference tracking
- Secure JWT and refresh token authentication
- Role-based admin authorization
- Performance-aware backend design
- Clean separation between controllers, services, repositories, and database access
