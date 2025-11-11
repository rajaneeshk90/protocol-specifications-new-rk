# Hawaiian Macadamia Nuts - Retail Use Case

Complete user journey covering the entire lifecycle from search to post-purchase.

---

## 🔍 1. Search & Discovery

### User Inputs

The user opens the retail section or searches directly:

**Search query**: `"Hawaiian macadamia nuts"`

**Location context**:
- Current location (auto-detected via GPS or chosen city, e.g., Honolulu, Hawaii)
- Optional: "Deliver to hotel" / "Pick up at airport"

### System Actions

Query product catalog filtered by:
- `location_id` or `geo_radius`
- `category = packaged_food`
- `search_term = hawaiian macadamia nuts`
- Retrieve all active sellers within delivery/pickup range

---

## 📦 2. Catalog Response

### Catalog Structure

Each product result (SKU) includes:

#### Product Details
- `product_id`
- `name`: "Honey-Roasted Hawaiian Macadamia Nuts"
- `description`
- `images[]`
- `weight / packaging`
- `origin`: "Big Island, Hawaii"

#### Pricing & Seller Info
- `price`
- `currency`
- `seller_id` + `seller_name`
- `delivery_modes`: delivery / pickup
- `delivery ETA` or `pickup slot`

#### Availability
- `stock_qty`
- `min_order_qty`, `max_order_qty`

#### Ratings
- Average rating + number of reviews

### Example Catalog

| Product | Seller | Price | Delivery | Rating |
|---------|--------|-------|----------|--------|
| Honey Roasted Macadamia Nuts 150g | Mauna Loa Store | $12.99 | 1-Day Hotel Delivery | ⭐4.8 |
| Classic Salted Macadamias 200g | Island Treats Co. | $10.50 | Airport Pickup | ⭐4.6 |
| Chocolate Covered Macadamias Box | Aloha Foods | $15.00 | 2-Day Delivery | ⭐4.9 |

---

## 🛒 3. Product Selection & Cart

### User Actions

1. Select a product → view detail page
2. Adjust quantity (e.g., 3 units)
3. Choose delivery method (hotel delivery or pickup)
4. Tap **"Add to Cart"**

### System Actions

1. Validate stock
2. Estimate shipping cost or taxes
3. Update cart summary

---

## 💳 4. Checkout Flow

### User Inputs

1. Confirm delivery address or pickup point
2. Select delivery slot (if required)
3. Choose payment method:
   - Card / Wallet / Points / BNPL
4. Apply discount or loyalty coupon

### System Actions

1. Create Order ID
2. Lock stock
3. Calculate total price (incl. taxes/shipping)
4. Process payment via gateway
5. Send confirmation email/SMS/in-app receipt

---

## 📦 5. Order Fulfillment

### Order States

1. **Order Placed**
2. **Confirmed by Seller**
3. **Packed**
4. **Out for Delivery** or **Ready for Pickup**
5. **Delivered**

### User Notifications

- Push updates for each state
- Real-time delivery tracking (if local courier used)

---

## 🔁 6. Post-Purchase Journey

### Rating & Feedback

After delivery:

**Prompt**: _"How was your macadamia nut order?"_

User provides:
- ⭐ **Rating** (1–5)
- **Optional comment**
- **Photo upload** (optional)

Rating stored per product + seller

---

## ❌ 7. Cancellations & Refunds

### User Actions

1. Go to **Orders** → **Order Details** → **Cancel**
2. Allowed only if `status < packed`
3. Select cancellation reason (e.g., "Changed my mind")

### System Actions

1. Update `order_status = cancelled`
2. Trigger refund workflow
3. Notify seller and finance service

---

## 💬 8. Support & Helpdesk

If there's an issue:

### Support Channels
- **Chat Support** or **Call Support**
- Context auto-filled: `order_id`, `seller_id`, `item_name`

### User Can:
- Report missing/damaged item
- Request refund/replacement
- Track escalation status

---

**End of User Journey**
