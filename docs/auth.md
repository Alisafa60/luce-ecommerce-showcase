# Authentication Model

LUCE includes customer and admin authentication built around short-lived JWT access tokens and database-backed refresh tokens.

The goal is to support secure customer accounts without interrupting the guest shopping experience. Customers can browse products, search, use cart flows, and continue shopping without logging in.

---

## Session Model

- Access tokens are returned to the frontend after login or signup
- Refresh tokens are stored in an `HttpOnly` cookie
- Refresh tokens are hashed before being stored in the database
- Expired or revoked refresh tokens cannot be reused
- Refresh token rotation is used when refreshing a session
- Logout and logout-from-all-devices behavior is supported through the refresh token model

---

## Customer Accounts

Customer accounts are designed to support:

- Saved delivery details
- Faster checkout
- Personalized recommendations
- Order history
- Account preferences

Guest shopping remains available, and guest recommendation sessions can be connected to the customer profile after login or signup.

---

## Admin Accounts

Admins use the same login flow, but receive an admin role claim in the access token.

Admin-only routes are protected with role-based authorization, and admin account creation is restricted to authenticated admins.
