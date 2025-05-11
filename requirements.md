## **1. User Authentication**

### **Functional Requirements**

* **User Registration**: Allow users to sign up as guests or hosts by providing necessary information such as name, email, password, and account type.
* **User Login**: Allow users to log in using their email and password or OAuth services (e.g., Google, Facebook).
* **Profile Management**: Allow users to update personal information like profile picture, contact info, and preferences.
* **Role-based Access Control**: Ensure users have access only to features relevant to their role (guest, host, admin).

### **Technical Requirements**

* **Authentication Mechanism**:

  * Use **JWT** (JSON Web Token) for session management.
  * Store user passwords securely with **bcrypt** for hashing.
  * Implement **OAuth** for third-party logins (Google, Facebook).
* **API Endpoints**:

  **POST /api/auth/register**

  * **Input**:

    * `email` (string, required)
    * `password` (string, required)
    * `name` (string, required)
    * `role` (string: 'guest' or 'host', required)
  * **Output**:

    * Success: `{"message": "User registered successfully", "status": 201}`
    * Failure: `{"message": "Error registering user", "status": 400}`

  **POST /api/auth/login**

  * **Input**:

    * `email` (string, required)
    * `password` (string, required)
  * **Output**:

    * Success: `{"token": "JWT Token", "user": {...}, "status": 200}`
    * Failure: `{"message": "Invalid email or password", "status": 401}`

  **POST /api/auth/login/google** (OAuth)

  * **Input**: Google OAuth token.
  * **Output**:

    * Success: `{"token": "JWT Token", "user": {...}, "status": 200}`
    * Failure: `{"message": "OAuth error", "status": 401}`

  **PUT /api/auth/update-profile**

  * **Input**:

    * `name` (string, optional)
    * `contactInfo` (string, optional)
    * `profilePicture` (file, optional)
  * **Output**:

    * Success: `{"message": "Profile updated", "status": 200}`
    * Failure: `{"message": "Failed to update profile", "status": 400}`

### **Validation Rules**:

* **Email Validation**: Check if email follows valid format (`email@example.com`).
* **Password Validation**: Ensure password length is at least 8 characters and contains both letters and numbers.
* **Role Validation**: Ensure role is either "guest" or "host".

### **Performance Criteria**:

* **Response Time**: All authentication endpoints should respond in under 200ms for 95% of requests.
* **Rate Limiting**: Implement a rate limit of 5 login attempts per minute to prevent brute-force attacks.

---

## **2. Property Management**

### **Functional Requirements**

* **Add Property**: Hosts should be able to add property listings with necessary details (title, description, price, location, amenities, etc.).
* **Edit Property**: Hosts should be able to modify details of an existing property listing.
* **Delete Property**: Hosts should be able to remove a property listing from the system.
* **View Property**: Both guests and hosts should be able to view details of the property.

### **Technical Requirements**

* **Database Schema**:

  * **Properties Table**:

    * `id` (integer, primary key)
    * `hostId` (foreign key, references `Users`)
    * `title` (string, required)
    * `description` (text, required)
    * `location` (string, required)
    * `price` (decimal, required)
    * `amenities` (json, optional)
    * `createdAt` (timestamp)
    * `updatedAt` (timestamp)

* **API Endpoints**:

  **POST /api/properties**

  * **Input**:

    * `hostId` (integer, required)
    * `title` (string, required)
    * `description` (text, required)
    * `location` (string, required)
    * `price` (decimal, required)
    * `amenities` (json, optional)
  * **Output**:

    * Success: `{"message": "Property added successfully", "propertyId": 123, "status": 201}`
    * Failure: `{"message": "Error adding property", "status": 400}`

  **PUT /api/properties/{propertyId}**

  * **Input**:

    * `title` (string, optional)
    * `description` (text, optional)
    * `location` (string, optional)
    * `price` (decimal, optional)
    * `amenities` (json, optional)
  * **Output**:

    * Success: `{"message": "Property updated successfully", "status": 200}`
    * Failure: `{"message": "Property not found", "status": 404}`

  **DELETE /api/properties/{propertyId}**

  * **Input**: `propertyId` (integer, required)
  * **Output**:

    * Success: `{"message": "Property deleted successfully", "status": 200}`
    * Failure: `{"message": "Property not found", "status": 404}`

  **GET /api/properties/{propertyId}**

  * **Input**: `propertyId` (integer, required)
  * **Output**:

    * Success: `{"property": {...}, "status": 200}`
    * Failure: `{"message": "Property not found", "status": 404}`

### **Validation Rules**:

* **Title Validation**: Ensure title is a non-empty string.
* **Location Validation**: Ensure location is a valid geographical address.
* **Price Validation**: Ensure price is a positive decimal number.

### **Performance Criteria**:

* **Caching**: Cache property details for 5 minutes to reduce database load and improve performance.
* **Response Time**: Property endpoints should respond in under 300ms for 95% of requests.

---

## **3. Booking System**

### **Functional Requirements**

* **Create Booking**: Guests should be able to book a property for a specified duration (check-in and check-out dates).
* **Cancel Booking**: Guests and hosts should be able to cancel a booking based on predefined cancellation policies.
* **Booking Status**: Track booking statuses (pending, confirmed, canceled, completed) and notify users accordingly.
* **Search for Availability**: Guests should be able to check the availability of properties before booking.

### **Technical Requirements**

* **Database Schema**:

  * **Bookings Table**:

    * `id` (integer, primary key)
    * `guestId` (foreign key, references `Users`)
    * `propertyId` (foreign key, references `Properties`)
    * `checkIn` (timestamp)
    * `checkOut` (timestamp)
    * `status` (enum: 'pending', 'confirmed', 'canceled', 'completed')
    * `createdAt` (timestamp)
    * `updatedAt` (timestamp)

* **API Endpoints**:

  **POST /api/bookings**

  * **Input**:

    * `guestId` (integer, required)
    * `propertyId` (integer, required)
    * `checkIn` (timestamp, required)
    * `checkOut` (timestamp, required)
  * **Output**:

    * Success: `{"message": "Booking created successfully", "bookingId": 456, "status": 201}`
    * Failure: `{"message": "Booking conflict", "status": 400}`

  **PUT /api/bookings/{bookingId}/cancel**

  * **Input**: `bookingId` (integer, required)
  * **Output**:

    * Success: `{"message": "Booking canceled successfully", "status": 200}`
    * Failure: `{"message": "Booking not found or cancellation not allowed", "status": 404}`

  **GET /api/bookings/{bookingId}**

  * **Input**: `bookingId` (integer, required)
  * **Output**:

    * Success: `{"booking": {...}, "status": 200}`
    * Failure: `{"message": "Booking not found", "status": 404}`

  **GET /api/bookings/availability**

  * **Input**:

    * `propertyId` (integer, required)
    * `checkIn` (timestamp, required)
    * `checkOut` (timestamp, required)
  * **Output**:

    * Success: `{"available": true, "status": 200}`
    * Failure: `{"message": "Property is not available", "status": 400}`

### **Validation Rules**:

* **Date Validation**: Ensure `checkIn` is before `checkOut`, and dates are not in the past.
* **Availability Check**: Ensure there is no existing booking for the same property during the specified period.

### **Performance Criteria**:

* **Response Time**: Booking endpoints should respond in under 500ms for 95% of requests.
* **Concurrency Handling**: Ensure database transactions are handled to prevent race conditions during bookings.
