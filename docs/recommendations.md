# Recommendation System

LUCE includes a placement-aware recommendation system designed around a scarf-first ecommerce model.

Recommendations are not treated as generic upsells. They adapt based on where they appear in the shopping flow and use product context, selected colors, cart contents, and customer behavior to suggest items that feel useful and relevant.

---

## Placements

Recommendation placements include:

- Add-to-cart popup: matching essentials for the scarf or color the customer just added
- Cart recommendations: useful add-ons and style inspiration based on the full cart
- Home page: broader personalized picks, with preference toward main scarves
- Search empty state: personalized starter picks before the customer searches

---

## Color-Aware Essentials

For essentials such as underscarves, bonnets, basics, extensions, and accessories, recommendations can use the selected scarf color when available.

The matching flow prioritizes:

1. Exact color match
2. Closest wearable color using perceptual color distance
3. Same color-family match
4. Soft neutral fallback

This is especially useful for products like underscarves and bonnets, where customers often want a matching or complementary color.

The scarf-to-underscarf matching logic uses CIEDE2000 color distance with hue and lightness guards to avoid visually poor matches. Manual styling metadata such as color temperature, mood, neutral group, and soft-neutral classification can provide small scoring nudges, but the core matching remains visual and still works for colors without metadata.

For printed scarves, recommendation logic evaluates configured palette colors such as base, dominant, and printed colors, then chooses the best overall match instead of assuming one color should always drive the recommendation.

---

## Cart-Aware Logic

Cart recommendations separate two different recommendation goals:

- Essentials are shown as quick-add items with a recommended color
- Main scarves are shown as inspiration with a `VIEW` action instead of quick-add

This prevents main scarves from receiving an unwanted preselected color, while still allowing color-matched essentials to be added quickly.

---

## Preference Tracking

The system tracks customer behavior to improve personalization over time.

Tracked events include:

- Product views
- Add to cart
- Recommendation clicks
- Recommendation add-to-cart
- Purchases

Guest sessions are tracked with a local recommendation session id and can be merged into the customer profile after login or signup.
