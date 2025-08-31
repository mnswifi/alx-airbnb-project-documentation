# Airbnb Clone - Use Case Documentation

## Project Overview

This document outlines the use case diagram for the Airbnb Clone backend system, visualizing interactions between users and the system for key functionalities.

---

## Use Case Diagram

The use case diagram illustrates the interactions between different actors and the Airbnb Clone system.

### Actors

- **Guest** – Users who browse and book properties  
- **Host** – Users who list and manage properties  
- **Admin** – System administrators who manage platform operations  
- **Payment Gateway** – External payment processing system  

---

## Core Use Cases

### Authentication & Profile Management

- Register Account  
- Login to System  
- Manage Profile  

### Property Management (Host Functions)

- Create Listing  
- Edit Listing  
- Delete Listing  

### Booking System (Guest Functions)

- Search Properties  
- Book Property  
- Cancel Booking  

### Payment Processing

- Process Payment  
- Issue Refund  

### Reviews & Ratings

- Write Review  
- Respond to Review  

### Administrative Functions

- Manage Users  
- Moderate Content  

---

## Relationships

### Association Relationships

- **Guests** can: Register, Login, Manage Profile, Search Properties, Book Properties, Cancel Bookings, Write Reviews  
- **Hosts** can: Register, Login, Manage Profile, Create Listings, Edit Listings, Delete Listings, Respond to Reviews  
- **Admins** can: Manage Users, Moderate Content  
- **Payment Gateway**: Processes Payments, Issues Refunds  

### Include Relationships

- Booking a Property **includes** Processing Payment  
- Canceling a Booking **includes** Issuing a Refund  

---

## System Boundaries

The Airbnb Clone system encompasses all functionality related to:  
- User authentication and management
- Property listing management  
- Booking and reservation system  
- Payment processing  
- Review system  
- Administrative controls  

---

## 📊 Diagram Reference

The following diagram represents the Use Case Diagram for the Airbnb Clone:

👉 [Use Case Diagram](./use-case-diagram.png)  

---

📌 *This documentation is part of the **ALX Airbnb Clone** project requirements.*
