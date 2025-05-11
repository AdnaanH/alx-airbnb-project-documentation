# Airbnb Clone Backend - Description

## Overview
The Airbnb Clone backend is a platform where guests can book properties, and hosts can list their properties for booking. It includes core functionalities such as user management, property listing management, booking management, payment processing, reviews and ratings, and an admin dashboard.

## Core Features:
- **User Registration & Authentication:** Allows users to register as guests or hosts and authenticate via email/password or OAuth providers (Google, Facebook).
- **Property Listings Management:** Hosts can add, edit, or remove property listings with various attributes such as title, description, location, amenities, and price.
- **Booking Management:** Guests can search and book properties for specific dates. Booking statuses like pending, confirmed, and completed are tracked.
- **Payment Integration:** Payment gateways like Stripe and PayPal are integrated for processing guest payments and host payouts.
- **Review and Rating System:** Guests can leave reviews and ratings for properties after completing a stay, and hosts can respond to reviews.
- **Admin Dashboard:** Admins can manage users, properties, bookings, and payments.

## User Stories:
This project is built based on the following user stories:

1. **User Registration:**  
   As a guest or host, I want to be able to register an account so that I can access the platform and start booking or listing properties.

2. **User Login and Authentication:**  
   As a user, I want to be able to log in to my account using my email and password or an OAuth provider (Google, Facebook) so that I can securely access my account and perform actions like booking or listing properties.

3. **Property Listing Management:**  
   As a host, I want to be able to add, edit, or remove property listings so that I can manage my available properties for booking.

4. **Booking a Property:**  
   As a guest, I want to be able to search for properties, view their details, and make a booking for specific dates so that I can secure a place to stay.

5. **Payment and Booking Confirmation:**  
   As a guest, I want to be able to pay for my booking securely through integrated payment gateways (Stripe, PayPal), so that I can confirm my reservation and receive a booking confirmation.

## Technology Stack:
- **Database:** PostgreSQL or MySQL
- **Backend:** Node.js with Express
- **Authentication:** JWT, OAuth
- **Payment Integration:** Stripe, PayPal
- **Cloud Storage:** AWS S3, Cloudinary
- **Notifications:** SendGrid, Mailgun
