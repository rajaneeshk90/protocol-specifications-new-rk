# 🚕 Cab Booking Use Case — Flow

## 🎯 Objective

Provide a seamless experience for users to search, book, and complete cab rides — from pickup to drop-off — within the travel super app.

---

## 👤 Actor

**User (Traveler)** — Logged-in user booking a cab for airport transfers, city travel, or hotel commutes.

---

## 🌤️ Flow Steps

### 1. **Search for Cabs**

* User enters:

  * Pickup location: *Suvarnabhumi Airport, Bangkok*
  * Drop-off location: *Grand Siam Hotel, Bangkok*
  * Pickup time: *10 Dec 2025, 10:00 AM*
* System detects current or future booking request.
* System fetches available cab types from partners (Economy, Sedan, SUV, Luxury).

### 2. **View Available Options**

* System displays a list of cab options with details:

  | Type    | Fare | ETA    | Capacity |
  | ------- | ---- | ------ | -------- |
  | Economy | $12  | 5 min  | 3 pax    |
  | Sedan   | $18  | 5 min  | 4 pax    |
  | SUV     | $25  | 7 min  | 6 pax    |
  | Luxury  | $40  | 10 min | 3 pax    |
* User selects **Sedan ($18)**.

### 3. **Confirm Ride Details**

* System shows summary:

  * Route distance: *25 km (~40 min)*
  * Estimated fare: *$18*
  * Driver assignment status: *Pending*
* User confirms booking → taps **“Book Cab”**.

### 4. **Driver Assignment**

* System matches available drivers nearby.
* Driver **assigned successfully**:

  * Driver: *Somchai K.*
  * Vehicle: *Toyota Camry (Black)*
  * Plate: *BKK-1234*
  * Contact: *+66 987 654 321*
  * ETA: *5 minutes*
* App displays real-time driver tracking on map.

### 5. **Ride Start**

* Driver arrives at pickup location.
* User receives notification: *“Your driver has arrived!”*
* User verifies driver and vehicle details → starts trip.
* System updates ride status: **In Progress**.

### 6. **Ride Experience**

* App shows:

  * Route progress on map
  * Estimated time of arrival
  * Options: *Call driver*, *Share trip*, *SOS*
* Ride proceeds smoothly.

### 7. **Ride Completion & Payment**

* Trip completed successfully.
* System calculates fare: *$18.50 (with tax)*.
* User pays via:

  * **Wallet / Credit Card / UPI / Points**
* Payment succeeds → Receipt generated.

### 8. **Post-Ride Summary**

* App shows ride summary:

  * Route: *Airport → Grand Siam Hotel*
  * Distance: *25 km*
  * Duration: *38 minutes*
  * Fare: *$18.50*
  * Payment mode: *Wallet*
  * Status: *Completed*
* User receives invoice via email and in-app notification.

### 9. **Rating & Feedback**

* Prompt: *“How was your ride with Somchai?”*
* User rates ⭐⭐⭐⭐⭐ and writes: *“Smooth ride, clean car!”*
* Loyalty points added automatically.

---

## ✅ Success Outcome

* Cab booked successfully and completed without delay.
* Driver assigned promptly.
* Payment processed and receipt delivered.
* User leaves positive feedback and earns rewards.

---

**End of the Flow**
