# 🏨 Hotel Booking Use Case — Flow

## 🎯 Objective

Deliver a smooth and intuitive booking experience for users looking to reserve a hotel stay without any interruptions or failures.

---

## 👤 Actor

**User (Traveler)** — Logged-in user booking accommodation.

---

## 🌤️ Flow Steps

### 1. **Search Hotels**

* User enters:

  * Destination: *Bangkok, Thailand*
  * Check-in: *10 Dec 2025*
  * Check-out: *15 Dec 2025*
  * Guests: *2 Adults, 1 Room*
* System fetches available hotels from partner APIs.
* Displays a curated list of hotels with photos, ratings, and prices.

### 2. **Apply Filters & Choose Hotel**

* User applies filters:

  * Price range: *$80–$150/night*
  * Amenities: *Free Wi-Fi, Breakfast Included, Pool*
* System updates results in real-time.
* User selects *Grand Siam Hotel* (4.5⭐, near city center).

### 3. **View Hotel Details & Select Room**

* System shows:

  * Hotel photos, map, and guest reviews.
  * Available rooms: *Deluxe Room with Breakfast*, *Suite Room with City View*.
* User chooses *Deluxe Room with Breakfast*.

### 4. **Enter Guest Details**

* User provides:

  * Guest name: *Fide Beckn*
  * Email: *[beckn@eminds.ai](mailto:beckn@eminds.ai)*
  * Phone: *+1 555 123 4567*
  * Special request: *Late check-in*
* System validates input and confirms availability.

### 5. **Payment**

* User reviews booking summary:

  * Room: *Deluxe Room with Breakfast*
  * Price: *$120/night × 5 nights = $600 + taxes*
* User selects **Credit Card** payment method.
* Payment processed successfully.
* System generates **Booking ID: HBNK1025**.

### 6. **Booking Confirmation**

* Confirmation screen displays:

  * Hotel name: *Grand Siam Hotel*
  * Address and map link
  * Check-in/out dates
  * Room details and total fare
  * Status: *Confirmed*
* User receives instant email and SMS confirmation.

### 7. **Pre-Arrival Notification**

* 24 hours before check-in → Push notification: *“Your stay at Grand Siam Hotel starts tomorrow!”*
* User can view check-in instructions and hotel contact info.

### 8. **During Stay**

* App provides in-stay options:

  * Request room service
  * Book cab to local attractions
  * View hotel amenities
* System ensures seamless connection to hotel’s concierge service.

### 9. **Check-Out & Feedback**

* After check-out, user receives message: *“How was your stay at Grand Siam Hotel?”*
* User rates 5 stars and writes: *“Amazing experience, very clean and friendly staff!”*
* Loyalty points credited automatically.

---

## ✅ Success Outcome

* Hotel booking confirmed without issues.
* Payment and confirmation completed instantly.
* User enjoys a smooth stay and gives positive feedback.
* Post-stay loyalty reward successfully applied.

---

**End of the Flow**
