# ✈️ Flight Booking Use Case — Happy Flow

## 🎯 Objective

Provide a seamless experience for users to search, book, and complete flight reservations smoothly, without any errors or exceptions.

---

## 👤 Actor

**User (Traveler)** — Logged-in user searching and booking a flight.

---

## 🌤️ Flow Steps

### 1. **Search Flights**

* User enters:

  * From: *San Francisco (SFO)*
  * To: *New York (JFK)*
  * Date: *15 Dec 2025*
  * Passengers: *1 Adult*
  * Class: *Economy*
* System fetches flights via integrated APIs.
* Displays list of flights sorted by price and duration.

### 2. **Select Flight**

* User taps preferred option → *Delta Airlines, Flight DL145*.
* System shows details: timings, duration, baggage, and cancellation policy.
* User confirms selection.

### 3. **Add Passenger Details**

* User enters personal details:

  * Name: *Fide Beckn*
  * DOB: *20 Jan 1995*
  * Email: *[beckn@eminds.ai](mailto:beckn@eminds.ai)*
  * Phone: *+1 555 123 4567*
* System validates data and saves profile for future use.

### 4. **Add Optional Add-ons**

* User adds:

  * 1 checked baggage
  * Window seat preference
  * Travel insurance
* System updates fare in real time.

### 5. **Payment**

* User selects **Credit Card** as payment method.
* Enters card details → confirms payment.
* System processes payment successfully.
* Booking confirmed → generates **PNR: DL9X21**.

### 6. **Booking Confirmation**

* Confirmation screen shows:

  * Flight: *Delta DL145, 15 Dec 2025, 09:30 AM*
  * Seat: *12A*
  * Fare: *$320.00*
  * Status: *Confirmed*
* User receives email, SMS, and in-app receipt.

### 7. **Pre-Travel Notifications**

* 24 hours before flight → App notifies: *“Check-in now open”*.
* User taps link → completes online check-in.
* Boarding pass downloaded and saved to app wallet.

### 8. **Travel Day Experience**

* App shows gate, terminal, and baggage details.
* Push alert for *“Gate changed to 14B”* if applicable.

### 9. **Post-Travel Feedback**

* After flight, user receives prompt: *“Rate your Delta flight”*.
* User gives ⭐⭐⭐⭐⭐ rating and short feedback.
* Loyalty points automatically credited.

---

## ✅ Success Outcome

* Flight booked and confirmed successfully.
* Payment processed without issue.
* User receives timely notifications and completes journey smoothly.
* Positive post-trip rating recorded.

---

**End of the Flow**
