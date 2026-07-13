# Authentication Model

LUCE includes customer and admin authentication built around token-based sessions and protected admin access.

The goal is to support secure customer accounts without interrupting the guest shopping experience. Customers can browse products, search, use cart flows, and continue shopping without logging in.

---

## Session Model

- Customer sessions are designed to avoid interrupting guest browsing
- Session state is handled through backend-controlled account flows
- Sensitive session handling is kept out of frontend-only storage patterns
- Logout and multi-device session behavior are supported by the backend model

---

## Customer Accounts

Customer accounts are designed to support:

- Saved delivery details
- Faster checkout
- Order history
- Account preferences

Guest shopping remains available, with account features layered on top when the customer chooses to sign in.

---

## Admin Accounts

Admin-only routes and account-management actions are protected through backend authorization.
