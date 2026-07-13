# Recommendation System

LUCE includes a context-aware recommendation system for storefront, cart, and discovery surfaces.

The public showcase keeps recommendation details intentionally high-level. The implementation contains more domain-specific logic than is documented here.

---

## Approach

Recommendations are designed to feel useful inside the shopping flow rather than appearing as generic upsells.

The system can account for:

- Where the recommendation appears in the customer journey
- Product context from the current page or cart
- Available catalog and inventory state
- Customer or guest-session behavior when available
- Product relationships managed through the admin workflow

---

## Storefront Behavior

Recommendation surfaces are used in places where they can support browsing or checkout without interrupting the customer.

Examples include cart suggestions, add-to-cart follow-ups, home page discovery, and empty-state discovery surfaces.

---

## Engineering Notes

Recommendation logic is kept behind backend boundaries instead of being hardcoded into UI components. This allows the storefront to render consistent recommendation results while the backend owns the rules, data access, and performance considerations.
