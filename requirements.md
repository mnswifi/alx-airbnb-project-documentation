# 🏡 Airbnb Clone - Backend Requirements Specification

This document specifies the **backend requirements** for the Airbnb Clone project.  
It includes **functional requirements, technical specifications, API details, validation rules, performance criteria, and security standards**.

---

## 1. 🔑 User Authentication System

### Functional Requirements

- Users can register with **email/password** or **OAuth providers** (Google, Facebook).
- Users can log in and receive a **JWT token**.
- Users can reset forgotten passwords.
- Users can update their profiles.
- Role-based access control (**Guest, Host, Admin**).

### API Endpoints

```text
POST /api/auth/register
POST /api/auth/login
POST /api/auth/logout
POST /api/auth/forgot-password
POST /api/auth/reset-password
GET  /api/auth/me
PUT  /api/auth/profile
```

### Input/Output Specifications

#### Registration Request

```json
{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "firstName": "Sanusi",
  "lastName": "Lamido",
  "role": "guest"
}
```

#### Registration Response

```json
{
  "id": "user_12345",
  "email": "user@example.com",
  "firstName": "John",
  "lastName": "Doe",
  "role": "guest",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### Validation Rules

- Email must be valid format and unique.
- Password must be at least 8 characters with uppercase, lowercase, number, and special character.
- First and last name: 2–50 characters.
- Role must be either "guest" or "host".

### Performance Criteria

- Registration API response time: < 500ms.
- Login API response time: < 300ms.
- System should support 1000 concurrent authentication requests.
- JWT token expiration: 24 hours.

## 2. 🏠 Property Management System

### Property Functional Requirements

- Hosts can create property listings with details and photos.
- Hosts can update and delete their listings.
- Properties can be searched and filtered.
- Property availability calendar management.
- Admin can moderate and manage all listings.

### Property API Endpoints

```test
POST   /api/properties
GET    /api/properties
GET    /api/properties/:id
PUT    /api/properties/:id
DELETE /api/properties/:id
GET    /api/properties/search
POST   /api/properties/:id/availability
```

### Property Input/Output Specifications

#### Create Property Request

```json
{
  "title": "Beautiful Terrace Apartment",
  "description": "Luxury property with amazing views",
  "location": {
    "address": "123 Maitama District",
    "city": "Abuja",
    "state": "FCT",
    "country": "Nigeria",
    "coordinates": {
      "lat": 25.7617,
      "lng": -80.1918
    }
  },
  "pricePerNight": 250,
  "bedrooms": 3,
  "bathrooms": 2,
  "maxGuests": 6,
  "amenities": ["wifi", "pool", "parking", "kitchen"],
  "houseRules": ["No smoking", "No pets", "No parties"]
}

```

#### Create Property Response

```json
{
  "id": "prop_67890",
  "title": "Beautiful Terrace Apartment",
  "hostId": "user_12345",
  "pricePerNight": 250,
  "averageRating": 4.8,
  "reviewCount": 45,
  "images": ["image1.jpg", "image2.jpg"],
  "availability": ["2024-01-15", "2024-01-16", "2024-01-20"]
}
```

#### Property Validation Rules

- Title: 10–100 characters required.
- Description: 50–2000 characters required.
- Price must be a positive number.
- Location coordinates must be valid.
- Amenities must be from predefined list.
- Host must be authenticated and have host role.

#### Property Performance Criteria

- Property search response time: < 200ms.
- Property creation: < 800ms (including image processing).
- Support pagination with up to 50 items per page.
- Search should handle 10+ filter criteria simultaneously.

## 3. 📅 Booking Management System

### Booking Functional Requirements

- Guests can book available properties.
- Prevent double-bookings.
- Booking confirmation and status tracking.
- Cancellation with policy enforcement.
- Payment processing integration.

### Booking API Endpoints

```json
POST   /api/bookings
GET    /api/bookings
GET    /api/bookings/:id
PUT    /api/bookings/:id/cancel
GET    /api/properties/:id/availability
POST   /api/bookings/:id/payment
```

### Booking Input/Output Specifications

#### Create Booking Request

```json
{
  "propertyId": "prop_67890",
  "checkInDate": "2024-02-15",
  "checkOutDate": "2024-02-20",
  "numberOfGuests": 4,
  "totalPrice": 1250,
  "specialRequests": "Early check-in if possible"
}
```

#### Create Booking Response

```json
{
  "id": "book_abc123",
  "propertyId": "prop_67890",
  "guestId": "user_67890",
  "checkInDate": "2024-02-15",
  "checkOutDate": "2024-02-20",
  "numberOfGuests": 4,
  "totalPrice": 1250,
  "status": "confirmed",
  "createdAt": "2024-01-10T10:30:00Z",
  "cancellationPolicy": "strict"
}
```

#### Booking Validation Rules

- Check-in date must be in the future.
- Check-out date must be after check-in date.
- Number of guests cannot exceed property maximum.
- Dates must be available on property calendar.
- Guest must have a valid payment method.

#### Payment Processing

- Integration with Stripe/PayPal.
- Support for multiple currencies.
- Secure payment handling (PCI compliant).
- Refund processing for cancellations.

#### Booking Performance Criteria

- Booking creation: < 1000ms (including payment processing).
- Availability check: < 100ms.
- System should handle 500 concurrent booking requests.
- Payment success rate: > 99.5%.
