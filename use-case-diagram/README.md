### Flow Diagram Overview:

The diagram will cover three main functionalities:

1. **User Registration**
2. **Property Booking**
3. **Payment Processing**

### Key Elements to Include:

* **Users** (Guests, Hosts, Admins)
* **System components** (Backend, Database, Third-Party Services like Stripe/PayPal)
* **Actions** (Register, Login, List Property, Search Properties, Book, Pay, Review)

Here’s how you can lay out the diagram:

#### 1. **User Registration Flow:**

* **Start:** User accesses the registration page.
* **Action:** User enters email, password, and other details.

  * **For Guests:** Choose guest account type.
  * **For Hosts:** Choose host account type.
* **Authentication:** JWT token is generated after successful registration.
* **System action:** Store user data in the database.
* **End:** User is registered and logged in.

#### 2. **Property Booking Flow:**

* **Start:** Guest searches for properties.
* **Action:** User applies filters (location, price range, etc.) to search for properties.
* **System Action:** Backend fetches results from the database, displaying matching properties.
* **Action:** Guest selects a property and checks availability for specific dates.
* **Action:** Guest books the property by selecting dates and confirming details.
* **System Action:** Booking is created in the database with status as "pending."
* **End:** Confirmation sent to both guest and host.

#### 3. **Payment Flow:**

* **Start:** Guest proceeds to checkout for booking confirmation.
* **Action:** User selects payment method (Stripe/PayPal).
* **System Action:** Payment gateway API processes the payment.
* **Action:** Once payment is successful, system updates booking status to "confirmed."
* **System Action:** Host receives payment, and system processes payout.
* **End:** Payment and booking are confirmed, notification sent.

#### 4. **Review System:**

* **Start:** After booking completion, the guest is prompted to review the property.
* **Action:** Guest submits review with rating.
* **System Action:** Store review in the database linked to the booking.
* **Action:** Host can respond to the review.
* **End:** Review is published.

### Visualization:

1. **Users** are depicted at the top (Guests, Hosts, Admins).
2. **Key system actions** like user registration, property listing, booking, payment, and review submission are illustrated as processes.
3. **External services** like Stripe/PayPal for payments and email services like SendGrid for notifications are shown as external entities.
4. **Database interactions** (e.g., storing user info, property details, booking status) are shown between the system and the database.
