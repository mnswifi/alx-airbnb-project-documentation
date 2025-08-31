# Airbnb Clone - Data Flow Diagram (DFD)

## Project Overview

This document describes the Data Flow Diagram (DFD) for the Airbnb Clone backend system, illustrating how data moves through the system for core operations.

---

## DFD Components

### External Entities

- **Guest** – User who books properties  
- **Host** – User who lists properties  
- **Admin** – System administrator  
- **Payment Gateway** – External payment service (Stripe/PayPal)  
- **Email Service** – External notification service (SendGrid/Mailgun)  

### Processes

- **User Authentication** – Handle registration, login, and profile management  
- **Property Management** – Create, update, and delete property listings  
- **Search & Filtering** – Process property searches and filters  
- **Booking Management** – Handle booking creation, updates, and cancellations  
- **Payment Processing** – Manage payment transactions and payouts  
- **Review System** – Handle reviews and ratings  
- **Notification System** – Send emails and in-app notifications  
- **Admin Dashboard** – Provide administrative controls and analytics  

### Data Stores

- **Users Database** – Stores user profiles and credentials  
- **Properties Database** – Stores property listings and details  
- **Bookings Database** – Stores booking information and status  
- **Payments Database** – Stores transaction records  
- **Reviews Database** – Stores reviews and ratings  
- **Cache (Redis)** – Stores frequently accessed data for performance  

---

## Data Flows

### Authentication Flow

- Guest/Host → (Registration Data) → User Authentication → (User Record) → Users Database  
- Guest/Host → (Login Credentials) → User Authentication → (Session Token) → Guest/Host  
- User Authentication → (Profile Data) → Users Database  

### Property Management Flow

- Host → (Property Details) → Property Management → (Property Record) → Properties Database  
- Property Management → (Updated Data) → Properties Database  
- Properties Database → (Property Data) → Search & Filtering  

### Booking Flow

- Guest → (Search Criteria) → Search & Filtering → (Property Results) → Guest  
- Guest → (Booking Request) → Booking Management → (Booking Record) → Bookings Database  
- Booking Management → (Payment Request) → Payment Processing  
- Payment Processing → (Transaction) → Payment Gateway → (Confirmation) → Payment Processing  
- Payment Processing → (Payment Record) → Payments Database  
- Booking Management → (Notification) → Notification System → (Email/SMS) → Guest/Host  

### Review Flow

- Guest → (Review Data) → Review System → (Review Record) → Reviews Database  
- Host → (Response) → Review System → (Updated Review) → Reviews Database  

### Admin Flow

- Admin → (Query) → Admin Dashboard → (Data) → Various Databases  
- Admin → (Action) → Admin Dashboard → (Update) → Various Databases  

---

## Key Data Elements

### User Data

- email, password_hash, name, profile_pic, role, preferences  

### Property Data

- title, description, location, price, amenities, availability, images  

### Booking Data

- guest_id, property_id, check_in, check_out, guests, status, total_price  

### Payment Data

- booking_id, amount, currency, status, transaction_id, payout_date  

### Review Data

- booking_id, rating, comment, host_response, timestamp  

---

## Security Considerations

- All sensitive data (passwords, payment info) is **encrypted**  
- API endpoints use **JWT authentication**  
- **Rate limiting** prevents abuse of services  
- **Input validation** prevents injection attacks  

---

## Performance Optimizations

- **Redis caching** for frequently accessed data (search results, property details)  
- **Database indexing** for faster queries  
- **Pagination** for large result sets  
- Optimized database queries  

---

## 📊 Diagram Reference

The following diagram represents the Use Case Diagram for the Airbnb Clone:

👉 [Data Flow Diagram](./data-flow.png)  

---

📌 This DFD documentation provides a comprehensive view of how data flows through the Airbnb Clone system and will guide implementation decisions.
