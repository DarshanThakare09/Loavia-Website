# 🍪 LOAVIA — Project Requirements Document
### *Healthy Inside, Yummy Outside*

> **Prepared for:** Antigravity Development Team  
> **Project:** LOAVIA Cookie Brand Web Platform  
> **Version:** v1.0 — Full Build Requirements  
> **Date:** May 2026

---

## 📋 Table of Contents

1. [Project Overview](#1-project-overview)
2. [Technology Stack](#2-technology-stack)
3. [Complete Page Architecture](#3-complete-page-architecture)
4. [Core System Logic & Backend Requirements](#4-core-system-logic--backend-requirements)
5. [Database Schema](#5-database-schema)
6. [API Endpoints](#6-api-endpoints)
7. [UI/UX & Animation Requirements](#7-uiux--animation-requirements)
8. [Payment Integration](#8-payment-integration)
9. [Notifications](#9-notifications)
10. [Advanced & Future-Ready Features](#10-advanced--future-ready-features)
11. [Development Phases & Delivery Order](#11-development-phases--delivery-order)
12. [Pre-Development Handoff Checklist](#12-pre-development-handoff-checklist)

---

## 1. Project Overview

LOAVIA is a **premium cookie brand** with the tagline *"Healthy Inside, Yummy Outside."*

This document defines the complete requirements for building LOAVIA's web platform — a **brand website combined with a fully functional e-commerce system**. The platform must serve as both a storytelling vehicle for the brand and a high-conversion shopping experience.

### 1.1 Mission

> Build a high-conversion, premium cookie e-commerce platform that combines **fast ordering**, **emotional brand engagement**, **product customization**, and a **scalable backend architecture**.

### 1.2 Target Experience

The website must feel:

| Quality | Meaning |
|---|---|
| **Fast** | Low friction — user should be able to go from landing to checkout in under 3 clicks |
| **Visual** | Product-first — cookies are the hero, always |
| **Emotional** | Cravings-driven — the design should make people hungry |
| **Interactive** | Micro-engagements — hover effects, animations, live previews |

### 1.3 Business Objectives

1. Drive **impulse purchases** through visual, emotion-first design
2. Enable **gifting use-cases** with occasion-based customization
3. Provide an **interactive brand experience** through animations and 3D elements
4. Build **repeat customers** through a loyalty and reward points system
5. Maintain a **scalable, API-first backend** architecture ready for future mobile app integration

### 1.4 Design Philosophy

- Premium, luxury, and modern UI — **no generic or template-looking layouts**
- Brand-focused color palette: warm **browns, creams, golds** — derived from the LOAVIA logo
- **Mobile-first** and fully responsive across all device sizes
- High-quality product imagery with **smooth, purposeful animations** (GSAP scroll effects, Three.js 3D cookies)
- **Fast loading speed** — optimized images, lazy loading, performance-first code

---

## 2. Technology Stack

> ⚠️ The following stack is required. No substitutions without prior client discussion.

### Frontend

| Technology | Purpose |
|---|---|
| **React.js / Next.js** | Component-based UI, SSR for SEO |
| **Tailwind CSS** | Utility-first responsive styling |
| **GSAP (GreenSock)** | Scroll-triggered animations, section transitions |
| **Three.js** | 3D cookie model in Hero section and product pages |

### Backend

| Technology | Purpose |
|---|---|
| **Node.js + Express.js** | REST API server |
| **MongoDB** | Primary database (document/collection model) |
| **Redis** | Cart caching and session optimization |
| **JWT (JSON Web Tokens)** | Stateless authentication |
| **Bcrypt / Argon2** | Password hashing |

### Services

| Service | Purpose |
|---|---|
| **Razorpay** (primary) | UPI, Cards, Net Banking, Wallets payment gateway |
| **Stripe** (optional/secondary) | International payments |
| **Cloudinary or AWS S3** | Product image hosting and CDN delivery |
| **Nodemailer / SendGrid** | Email notifications |

### Deployment

| Target | Platform |
|---|---|
| **Frontend** | Vercel |
| **Backend** | VPS (DigitalOcean / AWS EC2) |
| **Database** | MongoDB Atlas |
| **SSL** | Let's Encrypt / Cloudflare (HTTPS required) |

### Architecture Type

```
Decoupled Monolith → designed to be modular and scalable to microservices in the future
```

---

## 3. Complete Page Architecture

The platform has **16 total pages** across 3 access levels.

```
Public Pages (6)         →  No login required
User Pages (8)           →  Authenticated users only
Admin Panel (5 sections) →  Admin role only (separate system)
```

---

### 3.1 Public Pages

#### 📄 Page 1 — Homepage `/`

**Purpose:** Brand storytelling, product discovery, conversion entry point.

Required sections in order:

1. **Fixed Navigation Bar** — logo, nav links, search, account icon, cart icon with badge
2. **Hero Section** — full-viewport, 3D cookie element (Three.js), bold headline, "Shop Now" CTA, GSAP entrance animation
3. **Shop by Mood** — interactive mood-based browsing (e.g., Craving Something Sweet, Gifting, Healthy)
4. **Best Sellers** — product card grid with hover interactions
5. **Categories** — visual category tiles
6. **Build Your Box Highlight** — CTA banner linking to the custom box builder
7. **Gifting Section** — occasion-based gifting CTA
8. **Limited Edition / Seasonal** — time-sensitive product highlight
9. **Customer Testimonials** — star ratings + review previews
10. **Footer** — logo, quick links, support links, social icons, copyright

---

#### 📄 Page 2 — Shop / Product Listing `/shop`

**Purpose:** Browse all products.

- Product grid — 4 columns (desktop), 2 (tablet), 1 (mobile)
- Filter sidebar: category, price range, flavor tags, rating
- Sort options: price low→high, high→low, popularity, newest
- Quick "Add to Cart" button on card hover
- Pagination OR infinite scroll

---

#### 📄 Page 3 — Product Detail Page `/product/:slug`

**Purpose:** Deep product interaction and conversion.

**Left column:** Image gallery with thumbnail switcher  
**Right column:** Product info

- Image gallery — main image + thumbnails, swipeable on mobile
- Product name, short tagline, star rating (average + review count)
- Pricing — original price, discounted price, discount % badge
- Quantity selector (increment / decrement with validation)
- **Add to Cart** button and **Buy Now** button
- Flavor / Mood tags
- Tabbed content section below:
  - `Description` | `Ingredients` | `Reviews` | `Related Products`

---

#### 📄 Page 4 — Login / Register `/auth`

- Toggle between Login and Signup views
- **Login:** email + password + Forgot Password link
- **Signup:** name, email, phone, password, confirm password
- Client-side + server-side form validation
- On successful login → redirect to previous page or homepage

---

#### 📄 Page 5 — About `/about`

- Brand origin story and narrative
- Ingredients philosophy / health-forward messaging
- Lifestyle imagery — baking, ingredients, team

---

#### 📄 Page 6 — Contact `/contact`

- Contact form: name, email, subject, message
- Support email and phone number display
- Social media icon links

---

### 3.2 Authenticated User Pages

> All pages below require a valid login session. Unauthenticated users are redirected to `/auth`.

---

#### 📄 Page 7 — Cart `/cart`

- List of all cart items: image, name, price, quantity controls, remove button
- Price breakdown: subtotal, discount, estimated shipping, **total**
- Coupon / promo code input with validation
- "Proceed to Checkout" CTA button

---

#### 📄 Page 8 — Checkout `/checkout`

Multi-step checkout flow:

1. **Address** — Select saved address or add new. Validate ZIP/phone via regex.
2. **Delivery Method** — Available shipping options with estimated delivery dates
3. **Apply Offers** — Coupon codes, auto-applicable discounts
4. **Payment** — Razorpay/Stripe integration (UPI, Cards, Net Banking)
5. **Order Summary** — Final review with all details before placing order

---

#### 📄 Page 9 — Order Confirmation & Tracking `/orders/:id`

- Success message + Order ID display
- Order status **timeline tracker:**
  ```
  Pending → Paid → Preparing → Shipped → Delivered
  ```
- Each status shows a timestamp
- Full order details: items, address, payment method

---

#### 📄 Page 10 — Order History `/orders`

- List of all past orders with date, total, item count
- Status badge per order
- "View Details" link per order
- Invoice / receipt download (PDF) per order

---

#### 📄 Page 11 — Wishlist `/wishlist`

- Grid of saved products
- "Move to Cart" button (with stock check)
- "Remove" button per item

---

#### 📄 Page 12 — User Profile `/profile`

Tabbed layout:

| Tab | Content |
|---|---|
| **Personal Info** | Name, phone, email — all editable |
| **Addresses** | Add, edit, delete saved delivery addresses |
| **Orders** | Shortcut to order history |
| **Rewards** | Loyalty points balance and redemption history |

---

#### 📄 Page 13 — Build Your Box `/build-box`

- Cookie selection grid — tap/click to add items to box
- Box size selector (e.g., 6-pack, 12-pack, 24-pack)
- **Live preview panel** — shows selected cookies inside a visual box
- **Dynamic pricing** — total updates in real-time as items are added/removed
- Add custom box to cart as a single cart item

---

#### 📄 Page 14 — Gift Page `/gift`

- Occasion selector: Birthday, Anniversary, Festival, Corporate, etc.
- Packaging selection with visual preview
- Personalized message input (with character limit display)
- Delivery date scheduling (date picker)
- Add to cart as a gift order (marked with gift flag)

---

### 3.3 Admin Panel `/admin`

> Separate authenticated system. Only users with `role: admin` can access. All other users get HTTP 403.

---

#### 🔧 Admin 1 — Dashboard `/admin/dashboard`

- KPI cards: Total Sales, Today's Revenue, Active Orders, Total Users
- Sales chart with daily / weekly / monthly toggle
- Recent orders table with quick status update

---

#### 🔧 Admin 2 — Product Management `/admin/products`

- Full product table with search and filter
- **Add product form:**
  - Name, slug, description, ingredients (array input)
  - Category, image upload (Cloudinary integration)
  - Base price, discount %, stock quantity, active toggle
- Edit and delete existing products
- Toggle product `is_active` status (hides from storefront without deleting)

---

#### 🔧 Admin 3 — Order Management `/admin/orders`

- All orders list with filter by status
- View full order details
- **Manually override order status** (e.g., mark as Shipped)
- Trigger cancellation → auto-restore stock + initiate refund

---

#### 🔧 Admin 4 — User Management `/admin/users`

- View all registered users with search
- View any user's profile and order history
- Manage user roles: `user` → `admin` and vice versa

---

#### 🔧 Admin 5 — Offers & Coupons `/admin/offers`

- Create coupon codes:
  - Type: flat discount or percentage
  - Usage limit (e.g., max 100 uses)
  - Expiry date
  - Minimum cart value (optional)
- Toggle coupons active/inactive
- Auto-discount rules based on cart total value

---

## 4. Core System Logic & Backend Requirements

> These are exact business rules the backend must implement. Non-negotiable.

---

### 4.1 Authentication System

```
User Registration  →  Hash password (Bcrypt/Argon2)  →  Store in DB  →  Return JWT
User Login         →  Verify password hash  →  Return signed JWT
Authenticated req  →  Validate JWT on every request via middleware
Password Reset     →  Send email OTP or time-limited reset link
```

**User data model:**
```
user_id        : UUID
email          : String (unique index, indexed)
password_hash  : String (Bcrypt/Argon2)
name           : String
phone          : String
role           : Enum ["user", "admin"]
saved_addresses: Array of address objects
created_at     : Timestamp
```

---

### 4.2 Product & Pricing Logic

**Pricing formula** — calculated at **application layer** before serving the API:

```
final_price = base_price − (base_price × discount_pc / 100)
```

**Availability logic:**
```
status = (stock_qty > 0 AND is_active == true) ? "IN_STOCK" : "OUT_OF_STOCK"
```

**Validation:**
- If `discount_pc < 0` or `discount_pc > 100` → return HTTP 400 Bad Request
- If `discount_pc == 0` → `final_price = base_price`

**Time-based discounts:**
- Products have `start_date` and `end_date` fields
- Backend middleware checks: `IF current_time WITHIN (start_date, end_date)` → apply `discount_pc`

---

### 4.3 Cart System

**Persistence:** Redis (for speed) OR DB (for long-term), linked to `user_id` or `session_id`

**Calculations:**
```
line_item_total = final_price × quantity
cart_subtotal   = Σ (all line_item_totals)
```

**Constraints:**
```
IF requested_qty > current_stock_qty
  → Return Error: "Insufficient Stock"
  → Do NOT add to cart
```

**Guest Cart Merge:**
```
When guest user logs in
  → Merge session cart items into user's DB cart
  → No items should be lost
  → If same product exists in both: take the higher quantity (or sum — define behavior)
```

---

### 4.4 Checkout — Exact Transactional Sequence

> This sequence must be followed exactly. Any deviation breaks inventory integrity.

```
Step 1:  Validate all product_ids  →  confirm they exist and is_active = true
Step 2:  Inventory Soft-Lock       →  UPDATE stock_qty = stock_qty - qty
                                       WHERE id = X AND stock_qty > 0
Step 3:  Capture delivery address  →  validate ZIP/phone via regex
Step 4:  Apply coupon/offers       →  recalculate cart_total
Step 5:  Initiate payment          →  send cart_total to Razorpay/Stripe
Step 6a: On payment.success        →  set order status = PAID
                                       hard-deduct inventory (confirm soft-lock)
                                       send confirmation email/SMS
Step 6b: On payment.failure        →  Release soft-lock
         or timeout                    UPDATE stock_qty = stock_qty + qty
                                       notify user, allow retry
```

> ⚠️ **CRITICAL:** The price at checkout must be **locked at the moment the checkout session starts** (TTL-based price lock). If an admin updates a product price while a user is mid-checkout, the in-progress order must honor the price at checkout start.

---

### 4.5 Order Management System (OMS)

**Order entity:**
```
order_id       : UUID
user_id        : Reference → Users
items          : JSON blob (snapshot of cart at purchase)
total_amount   : Decimal
tax            : Decimal
shipping_fee   : Decimal
payment_ref    : String (gateway transaction ID)
order_status   : Enum (see below)
address_snapshot: Object (copy of address at time of order)
placed_at      : Timestamp
shipped_at     : Timestamp
delivered_at   : Timestamp
cancelled_at   : Timestamp
```

**Status flow:**
```
PENDING → PAID → PREPARING → SHIPPED → DELIVERED
                                      ↘ CANCELLED (from any stage, triggers refund + stock restore)
```

- Each status transition **records a timestamp**
- Admin can manually override status
- Cancellation triggers: refund logic + `stock_qty` restoration

---

### 4.6 Review & Rating System

**Verified Buyer Gate** — user may only submit a review if:
```sql
SELECT COUNT(*) FROM Orders
WHERE user_id = X
  AND product_id = Y
  AND status = 'DELIVERED'
> 0
```

**Average rating:**
```
AvgRating = Σ(ratings) / total_review_count
```

> ⚠️ Cache this value in the Product document. **Do NOT recalculate on every page load.** Update the cached value each time a new review is submitted.

---

### 4.7 Loyalty & Rewards System

- Users earn points on every completed (DELIVERED) order
  - Example: 1 point per ₹10 spent
- Points can be redeemed at checkout as a discount
- **Points Ledger model:**
  ```
  user_id           : Reference
  points            : Integer
  type              : Enum ["earn", "redeem"]
  order_ref         : Reference → Orders
  created_at        : Timestamp
  ```
- User's current balance = `Σ(earn points) - Σ(redeem points)`

---

### 4.8 Recommendation Engine

**Content-Based (Ingredient Similarity):**
```
Calculate Jaccard Similarity between ingredient arrays of products.

Example: User views "Dark Chocolate Sea Salt"
  → Recommend products with "Dark Chocolate" in their ingredients array
  → Sort by highest similarity score
```

**Collaborative Filtering (Behavioral):**
```
"Users who bought X also bought Y"
  → Query Orders table for most frequent product pairs
    associated with the current item's category
```

---

### 4.9 Cookie Customization — Build Your Box Logic

```
User selects cookies from grid
  → Each selection: product_id, name, image, price
  → Box has a size (e.g., 6, 12, 24 cookies)
  → Dynamic pricing = Σ(selected cookie prices)
  → Live preview renders selected cookies visually in a box

On "Add to Cart":
  → Create a special cart item type: "custom_box"
  → Payload: { type: "custom_box", items: [...], total_price, box_size }
```

---

### 4.10 Edge Cases & Race Condition Handling

| Scenario | Required Solution |
|---|---|
| Two users buy the last item simultaneously | Database transactions with `SELECT FOR UPDATE` or Optimistic Concurrency Control |
| Out-of-stock product | API returns `can_purchase: false` → frontend disables "Add to Cart" button |
| Price changes during active checkout | Honor price at checkout session start — TTL-based price lock |
| Payment timeout | Auto-release soft-lock, restore `stock_qty` |
| Guest adds to cart, then logs in | Merge guest session cart into user's stored cart |
| Admin cancels order | Restore stock + initiate refund via payment gateway |

---

## 5. Database Schema

Primary database: **MongoDB** (Atlas). Redis for cart/session caching.

### Collections

#### `users`
```json
{
  "_id": "UUID",
  "email": "string (unique, indexed)",
  "password_hash": "string",
  "name": "string",
  "phone": "string",
  "role": "user | admin",
  "saved_addresses": [
    {
      "label": "Home",
      "street": "string",
      "city": "string",
      "state": "string",
      "zip": "string",
      "is_default": true
    }
  ],
  "created_at": "timestamp"
}
```

#### `products`
```json
{
  "_id": "UUID",
  "name": "string",
  "slug": "string (unique, indexed)",
  "description": "string",
  "ingredients": ["dark chocolate", "sea salt", "oats"],
  "category_id": "reference → categories",
  "image_urls": ["https://cdn.cloudinary.com/..."],
  "base_price": 299.00,
  "discount_pc": 10,
  "stock_qty": 150,
  "is_active": true,
  "average_rating": 4.5,
  "review_count": 42,
  "created_at": "timestamp"
}
```

#### `cart`
```json
{
  "_id": "UUID",
  "user_id": "reference → users (or session_id for guests)",
  "product_id": "reference → products",
  "quantity": 2,
  "added_at": "timestamp"
}
```

#### `orders`
```json
{
  "_id": "UUID",
  "user_id": "reference → users",
  "items": "JSON blob (snapshot)",
  "total_amount": 598.00,
  "tax": 47.84,
  "shipping_fee": 50.00,
  "payment_ref": "pay_XXXXXXX",
  "order_status": "PENDING | PAID | PREPARING | SHIPPED | DELIVERED | CANCELLED",
  "address_snapshot": {},
  "placed_at": "timestamp",
  "shipped_at": "timestamp | null",
  "delivered_at": "timestamp | null",
  "cancelled_at": "timestamp | null"
}
```

#### `order_items`
```json
{
  "_id": "UUID",
  "order_id": "reference → orders",
  "product_id": "reference → products",
  "product_name_snapshot": "string",
  "price_at_purchase": 299.00,
  "quantity": 2
}
```

#### `reviews`
```json
{
  "_id": "UUID",
  "product_id": "reference → products",
  "user_id": "reference → users",
  "rating": 5,
  "comment": "string",
  "is_verified": true,
  "created_at": "timestamp"
}
```

#### `coupons`
```json
{
  "_id": "UUID",
  "code": "LOAVIA20",
  "type": "flat | percent",
  "value": 20,
  "min_cart_value": 500,
  "usage_limit": 100,
  "used_count": 12,
  "expiry_date": "timestamp",
  "is_active": true
}
```

#### `wishlist`
```json
{
  "_id": "UUID",
  "user_id": "reference → users",
  "product_id": "reference → products",
  "added_at": "timestamp"
}
```

#### `loyalty_ledger`
```json
{
  "_id": "UUID",
  "user_id": "reference → users",
  "points": 30,
  "type": "earn | redeem",
  "order_ref": "reference → orders",
  "created_at": "timestamp"
}
```

#### `categories`
```json
{
  "_id": "UUID",
  "name": "Chocolate",
  "slug": "chocolate",
  "image_url": "string"
}
```

---

## 6. API Endpoints

All endpoints follow RESTful conventions.  
Authenticated routes require: `Authorization: Bearer <JWT>` header.

### Auth Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/api/auth/register` | ❌ | User registration |
| POST | `/api/auth/login` | ❌ | Login, returns JWT |
| POST | `/api/auth/forgot-password` | ❌ | Send password reset email |
| POST | `/api/auth/reset-password` | ❌ | Reset password with token |

### Product Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/products` | ❌ | List all products — supports `?category`, `?sort`, `?minPrice`, `?maxPrice`, `?page`, `?limit` |
| GET | `/api/products/:slug` | ❌ | Single product detail |
| POST | `/api/products` | Admin | Create product |
| PUT | `/api/products/:id` | Admin | Edit product |
| DELETE | `/api/products/:id` | Admin | Delete product |

### Cart Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/cart` | ✅ | Get current user's cart |
| POST | `/api/cart/add` | ✅ | Add item `{ product_id, quantity }` |
| PUT | `/api/cart/update` | ✅ | Update item quantity |
| DELETE | `/api/cart/remove/:productId` | ✅ | Remove item from cart |
| DELETE | `/api/cart/clear` | ✅ | Clear entire cart |

### Checkout & Order Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/api/checkout/initiate` | ✅ | Validate cart, soft-lock inventory, return payment order |
| POST | `/api/payment/webhook` | ❌ (signed) | Handle Razorpay/Stripe webhooks |
| GET | `/api/orders` | ✅ | User's order history |
| GET | `/api/orders/:id` | ✅ | Single order detail + tracking |
| PUT | `/api/orders/:id/status` | Admin | Update order status |
| POST | `/api/orders/:id/cancel` | ✅ | Cancel order (user or admin) |

### Wishlist Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/wishlist` | ✅ | Get wishlist items |
| POST | `/api/wishlist` | ✅ | Add to wishlist `{ product_id }` |
| DELETE | `/api/wishlist/:productId` | ✅ | Remove from wishlist |
| POST | `/api/wishlist/:productId/move-to-cart` | ✅ | Move item to cart |

### Review Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/reviews/:productId` | ❌ | Get reviews for a product |
| POST | `/api/reviews/:productId` | ✅ | Submit review (verified buyer check) |

### User Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/users/profile` | ✅ | Get profile |
| PUT | `/api/users/profile` | ✅ | Update profile |
| POST | `/api/users/addresses` | ✅ | Add delivery address |
| PUT | `/api/users/addresses/:id` | ✅ | Edit address |
| DELETE | `/api/users/addresses/:id` | ✅ | Delete address |
| GET | `/api/users/loyalty` | ✅ | Get loyalty points balance |

### Coupon & Offers Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/api/coupons/validate` | ✅ | Validate coupon code, returns discount value |
| GET | `/api/admin/coupons` | Admin | List all coupons |
| POST | `/api/admin/coupons` | Admin | Create coupon |
| PUT | `/api/admin/coupons/:id` | Admin | Edit coupon |

### Admin Routes

| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/admin/dashboard` | Admin | Sales metrics and analytics |
| GET | `/api/admin/orders` | Admin | All orders with filters |
| GET | `/api/admin/users` | Admin | All users |
| PUT | `/api/admin/users/:id/role` | Admin | Change user role |

---

## 7. UI/UX & Animation Requirements

> These are not suggestions — they are core to the LOAVIA brand experience.

### 7.1 Navigation Bar

- **Fixed/sticky** — stays visible on scroll
- **Left:** LOAVIA logo (SVG). Click → homepage
- **Center:** `Home` | `Shop` | `About` | `Contact` — hover animation (underline slide or color shift)
- **Right:**
  - 🔍 Search icon → expands to search input on click
  - 👤 Account icon → dropdown (Login/Signup if guest; Profile/Orders/Logout if logged in)
  - 🛒 Cart icon → shows item count badge (number, not dot)
- **Mobile:** Hamburger menu → side drawer, same items in vertical layout

### 7.2 Hero Section

- Full viewport height (`100vh`)
- **3D cookie model (Three.js)** — slow rotation or floating particle animation
- Bold headline + short supporting tagline
- `Shop Now` CTA button — hover: elevate/color shift
- **GSAP entrance animation** on page load: text staggers in, cookie fades/scales in
- Layout: text and visual must not overlap — breathing room on all sizes

### 7.3 Product Cards

```
Default state  → product image, name, price
Hover state    → image zooms slightly, "Add to Cart" or "Quick View" button appears
Click          → navigate to product detail page
```

- Consistent card dimensions across all grids
- Smooth CSS transition — no layout shift
- `Best Seller` / `Popular` / `New` / `Out of Stock` badge on card when applicable

### 7.4 Scroll Animations (GSAP ScrollTrigger)

- **Sections fade/slide** up as user scrolls down
- **Product cards stagger-animate** into view (each card with slight delay)
- **Testimonials** — horizontal scroll carousel or fade auto-slider
- Animations must **not block page performance** — use `will-change` sparingly, lazy init off-screen elements

### 7.5 Page Load & Transitions

- Light **fade-in** on initial page load — no abrupt flash
- **Smooth route transitions** (200–300ms) between pages
- **Skeleton loaders** for product grids while data is fetching

### 7.6 Color Palette

Derived from the LOAVIA logo:

| Role | Color | Hex |
|---|---|---|
| Primary Brown | Deep warm brown | `#5C3317` |
| Accent Gold | Logo gold | `#A0772A` |
| Background Cream | Warm off-white | `#F5ECD7` |
| Surface Light | Very light tan | `#F9F6F1` |
| Text Primary | Near-black | `#1A1A1A` |
| Text Secondary | Warm gray | `#555555` |
| Success | Standard green | `#10B981` |
| Error | Standard red | `#EF4444` |

### 7.7 Typography

| Usage | Font Style | Example |
|---|---|---|
| Brand headings / hero | Elegant serif | Playfair Display, Cormorant Garamond |
| Section headings | Modern serif or styled sans | |
| Body text | Clean, readable sans-serif | Inter, DM Sans |
| Price / numbers | Tabular sans-serif | |

> All text must pass **WCAG 2.1 AA contrast** requirements.

### 7.8 Responsive Breakpoints

| Breakpoint | Width | Layout |
|---|---|---|
| Mobile | `< 640px` | 1 column, hamburger nav |
| Tablet | `640px – 1024px` | 2 columns, condensed nav |
| Desktop | `> 1024px` | Full layout, 3–4 columns |

---

## 8. Payment Integration

### Gateway

- **Primary:** Razorpay — UPI, Credit/Debit Cards, Net Banking, Wallets
- **Secondary (optional):** Stripe — for international support
- **SSL required** — all payment data exclusively over HTTPS

### Flow

```
Frontend → POST /api/checkout/initiate
         ← Returns Razorpay order_id + amount

Frontend → Opens Razorpay payment modal
         ← User completes payment

Razorpay → POST /api/payment/webhook (server-to-server, signed)
         → Verify webhook signature
         → On payment.success:
              set order status = PAID
              hard-deduct inventory
              generate invoice
              send confirmation email/SMS
         → On payment.failed:
              release soft-lock inventory
              notify user
              allow retry
```

### Invoice Generation

- Automatic PDF invoice generated on every successful order
- Invoice includes: order ID, items, prices, address, payment reference, date
- Available for download from Order History page

---

## 9. Notifications

### Email Notifications (Required — Phase 1)

| Trigger | Recipient | Content |
|---|---|---|
| Successful registration | User | Welcome email |
| Order placed | User | Order confirmation + invoice |
| Order status change | User | Status update with tracking link |
| Password reset | User | Reset link (expires in 15 minutes) |
| Low stock alert | Admin | Product name + current stock qty |

### SMS Notifications (Phase 2 / Optional)

- Order confirmation
- Shipped notification with tracking number

### In-App Notifications

- Cart icon badge — item count updates in real-time
- Order tracking page — live status timeline
- Stock warnings — "Only 3 left!" on product cards when `stock_qty < 5`

### Admin Automated Alerts

- **Low stock warning:** Email to admin when any product's `stock_qty < 10`
- Triggered by backend cron job or post-order webhook

---

## 10. Advanced & Future-Ready Features

> Design the system to support these. Some may be implemented in Phase 2.

### Subscription Cookie Boxes
- Recurring monthly cookie box orders
- Stripe Billing / Razorpay Subscriptions integration
- User can manage, pause, or cancel subscription from profile

### Real-Time Stock Updates
- WebSocket (Socket.io) — push stock count changes to all connected clients
- When last item sells → all browsers showing that product update to "Out of Stock" immediately

### SEO Optimization
- Next.js **SSR / SSG** for all product and category pages
- Proper `<meta>` tags, Open Graph, Twitter Card
- XML sitemap + robots.txt
- Structured data (Schema.org Product markup) for product pages
- Google Analytics integration

### Future Mobile App API
- All REST APIs must be **designed to serve both web and a future React Native mobile app**
- Use consistent, documented response schemas
- No web-specific dependencies in API responses

### Advanced Recommendation Engine
- Content-based filtering using ingredient Jaccard similarity
- Behavioral collaborative filtering from order history

### Other
- **Invoice download** (PDF) from Order History
- **Cookie gift sets** with custom packaging and message cards
- **Seasonal / Limited Edition** product management from Admin

---

## 11. Development Phases & Delivery Order

> Build in this exact order. **Do not start a new phase before the previous one is delivered and reviewed.**

| Phase | Name | Deliverables |
|---|---|---|
| **Phase 0** | Planning ✅ | Page architecture, feature list, system logic, tech stack — **COMPLETE** |
| **Phase 1** | UI/UX Design | Figma wireframes → final high-fidelity designs for all 16 pages. No coding yet. |
| **Phase 2** | Frontend (Mock Data) | React/Next.js project setup. All pages built with hardcoded mock data. GSAP animations + Three.js hero fully implemented. |
| **Phase 3** | API Simulation | Replace all mock data with an API service layer. UI calls fake endpoints. App behaves as if a real backend exists. |
| **Phase 4** | Backend Development | Express server + all REST API endpoints (auth, products, cart, checkout, orders, payment). |
| **Phase 5** | Database Integration | MongoDB Atlas collections + Redis setup. Connect backend to DB. All queries operational. |
| **Phase 6** | Integration | Connect frontend to real backend. Replace all fake API services with real endpoints. Full E2E flow works. |
| **Phase 7** | Payment Integration | Razorpay live/test integration. Webhook handler. Invoice PDF generation. |
| **Phase 8** | Testing | UI responsiveness, animation performance, all API responses, payment success/failure flows, all edge cases. |
| **Phase 9** | Deployment | Frontend → Vercel. Backend → VPS. MongoDB Atlas. Domain connection. SSL. Environment variables. |
| **Phase 10** | Post-Launch | Monitoring setup. Bug fixes. Performance optimization. |

### Common Mistakes to Avoid

```
❌ Starting backend before frontend mock is complete
❌ Skipping the API simulation phase
❌ Hardcoding data anywhere in production code
❌ No testing before deployment
❌ Building without considering "Can this be replaced by an API later?"
```

---

## 12. Pre-Development Handoff Checklist

Before writing the **first line of code**, confirm ALL of the following:

- [ ] All 16 pages are defined, understood, and agreed upon
- [ ] All feature systems understood: auth, cart, checkout, OMS, wishlist, reviews, loyalty, gifting, cookie customization
- [ ] All 3 user flows mapped: Standard Purchase | Quick Order | Custom Box | Gifting
- [ ] Backend business logic confirmed: pricing formula, soft-lock mechanism, race condition handling
- [ ] Database schema reviewed and agreed upon
- [ ] Tech stack confirmed — no deviations without written agreement
- [ ] **Razorpay account** set up (or in progress) by client
- [ ] **Cloudinary / AWS S3** account for image storage confirmed
- [ ] Domain name and hosting plan confirmed by client
- [ ] Brand color palette and logo assets (SVG) delivered to development team
- [ ] Figma designs approved by client before Phase 2 coding begins

---

## Project Summary

| Attribute | Details |
|---|---|
| **Brand** | LOAVIA |
| **Tagline** | Healthy Inside, Yummy Outside |
| **Platform Type** | Brand website + Full E-Commerce |
| **Total Pages** | 16 (6 public, 8 user, 5 admin sections) |
| **Feature Systems** | 14 core systems |
| **User Flows** | 4 (standard, quick order, custom box, gifting) |
| **Backend Services** | Auth, Product, Cart, Checkout, Order, Payment |
| **Database** | MongoDB + Redis |
| **Payments** | Razorpay (primary) + Stripe (optional) |
| **Animations** | GSAP + Three.js |
| **Deployment** | Vercel (FE) + VPS (BE) + MongoDB Atlas (DB) |

---

> *This document contains the complete product requirements for the LOAVIA web platform.*  
> *Any changes to scope must be agreed upon in writing before implementation begins.*  
> *Questions or clarifications should reference section numbers from this document.*

---

**© 2026 LOAVIA. All rights reserved.**
