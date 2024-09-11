1. Flight Search Microservice
GET /api/flights/search
Description: Search for available flights based on criteria.
Request Payload:
json
Copy code
{
  "departureCity": "New York",
  "arrivalCity": "Los Angeles",
  "departureDate": "2024-12-15",
  "returnDate": "2024-12-20",
  "passengers": {
    "adults": 1,
    "children": 0
  },
  "class": "Economy"
}
Response Payload:
json
Copy code
{
  "flights": [
    {
      "flightId": "FL123",
      "airline": "Airways A",
      "departureCity": "New York",
      "arrivalCity": "Los Angeles",
      "departureDate": "2024-12-15T10:00:00Z",
      "arrivalDate": "2024-12-15T13:00:00Z",
      "price": {
        "amount": 300,
        "currency": "USD"
      },
      "seatsAvailable": 50
    }
  ]
}
GET /api/flights/{id}
Description: Retrieve flight details by ID.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "airline": "Airways A",
  "departureCity": "New York",
  "arrivalCity": "Los Angeles",
  "departureDate": "2024-12-15T10:00:00Z",
  "arrivalDate": "2024-12-15T13:00:00Z",
  "price": {
    "amount": 300,
    "currency": "USD"
  },
  "seatsAvailable": 50,
  "aircraft": {
    "model": "Boeing 737",
    "capacity": 180
  },
  "amenities": [
    "Wi-Fi",
    "In-flight entertainment",
    "Meal service"
  ]
}
POST /api/flights
Description: Create a new flight entry.
Request Payload:
json
Copy code
{
  "airline": "Airways A",
  "departureCity": "New York",
  "arrivalCity": "Los Angeles",
  "departureDate": "2024-12-15T10:00:00Z",
  "arrivalDate": "2024-12-15T13:00:00Z",
  "price": {
    "amount": 300,
    "currency": "USD"
  },
  "seatsAvailable": 100
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Created"
}
PUT /api/flights/{id}
Description: Update flight details by ID.
Request Payload:
json
Copy code
{
  "price": {
    "amount": 320,
    "currency": "USD"
  },
  "seatsAvailable": 90
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Updated"
}
DELETE /api/flights/{id}
Description: Delete a flight entry by ID.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Deleted"
}
GET /api/flights/availability/{id}
Description: Retrieve flight seat availability.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "seatsAvailable": 50,
  "seatMap": [
    {"row": 1, "seats": 6},
    {"row": 2, "seats": 6}
  ]
}
GET /api/flights/price/{id}
Description: Retrieve the price of a specific flight.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "basePrice": 250,
  "taxes": 50,
  "totalPrice": 300,
  "currency": "USD"
}
2. Booking Microservice
POST /api/bookings
Description: Create a new booking.
Request Payload:
json
Copy code
{
  "userId": "user123",
  "flightId": "FL123",
  "passengers": [
    {
      "name": "John Doe",
      "age": 30,
      "passportNumber": "X1234567"
    }
  ],
  "contactDetails": {
    "email": "john.doe@example.com",
    "phone": "+1234567890"
  },
  "payment": {
    "amount": 300,
    "currency": "USD",
    "paymentMethod": "credit_card",
    "cardDetails": {
      "cardNumber": "4111111111111111",
      "expiryDate": "2025-12",
      "cvv": "123"
    }
  }
}
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "flightId": "FL123",
  "userId": "user123",
  "status": "Confirmed",
  "totalPrice": {
    "amount": 300,
    "currency": "USD"
  },
  "departureDate": "2024-12-15T10:00:00Z",
  "arrivalDate": "2024-12-15T13:00:00Z",
  "passengers": [
    {
      "name": "John Doe",
      "age": 30
    }
  ]
}
GET /api/bookings/{id}
Description: Retrieve booking details by ID.
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "flight": {
    "flightId": "FL123",
    "departureCity": "New York",
    "arrivalCity": "Los Angeles",
    "departureDate": "2024-12-15T10:00:00Z",
    "arrivalDate": "2024-12-15T13:00:00Z"
  },
  "user": {
    "userId": "user123",
    "name": "John Doe",
    "contactDetails": {
      "email": "john.doe@example.com",
      "phone": "+1234567890"
    }
  },
  "passengers": [
    {
      "name": "John Doe",
      "age": 30
    }
  ],
  "totalPrice": {
    "amount": 300,
    "currency": "USD"
  },
  "status": "Confirmed"
}
PUT /api/bookings/{id}
Description: Update booking details by ID.
Request Payload:
json
Copy code
{
  "passengers": [
    {
      "name": "John Doe",
      "age": 31
    }
  ],
  "contactDetails": {
    "email": "john.doe@newemail.com",
    "phone": "+0987654321"
  }
}
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "status": "Updated"
}
DELETE /api/bookings/{id}
Description: Cancel a booking by ID.
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "status": "Cancelled"
}
GET /api/bookings/user/{userId}
Description: Retrieve all bookings for a user.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "bookings": [
    {
      "bookingId": "BK123456",
      "flightId": "FL123",
      "status": "Confirmed"
    }
  ]
}
POST /api/bookings/{id}/add-passenger
Description: Add a new passenger to an existing booking.
Request Payload:
json
Copy code
{
  "passenger": {
    "name": "Jane Doe",
    "age": 28,
    "passportNumber": "X7654321"
  }
}
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "status": "Passenger Added"
}
POST /api/bookings/{id}/update-payment
Description: Update payment details for a booking.
Request Payload:
json
Copy code
{
  "paymentMethod": "credit_card",
  "cardDetails": {
    "cardNumber": "4111111111111112",
    "expiryDate": "2026-01",
    "cvv": "124"
  }
}
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "status": "Payment Updated"
}
3. Payment Microservice
POST /api/payments
Description: Process a new payment.
Request Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "amount": 300,
  "currency": "USD",
  "paymentMethod": "credit_card",
  "cardDetails": {
    "cardNumber": "4111111111111111",
    "expiryDate": "2025-12",
    "cvv": "123"
  }
}
Response Payload:
json
Copy code
{
  "paymentId": "PY123456",
  "status": "Processed",
  "amount": 300,
  "currency": "USD"
}
GET /api/payments/{id}
Description: Retrieve payment details by ID.
Response Payload:
json
Copy code
{
  "paymentId": "PY123456",
  "bookingId": "BK123456",
  "amount": 300,
  "currency": "USD",
  "status": "Processed",
  "paymentMethod": "credit_card"
}
PUT /api/payments/{id}
Description: Update payment details by ID.
Request Payload:
json
Copy code
{
  "amount": 320,
  "currency": "USD"
}
Response Payload:
json
Copy code
{
  "paymentId": "PY123456",
  "status": "Updated"
}
DELETE /api/payments/{id}
Description: Delete a payment record by ID.
Response Payload:
json
Copy code
{
  "paymentId": "PY123456",
  "status": "Deleted"
}
GET /api/payments/booking/{bookingId}
Description: Retrieve all payments for a booking.
Response Payload:
json
Copy code
{
  "bookingId": "BK123456",
  "payments": [
    {
      "paymentId": "PY123456",
      "amount": 300,
      "currency": "USD",
      "status": "Processed"
    }
  ]
}
GET /api/payments/user/{userId}
Description: Retrieve all payments for a user.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "payments": [
    {
      "paymentId": "PY123456",
      "amount": 300,
      "currency": "USD",
      "status": "Processed"
    }
  ]
}
POST /api/payments/{id}/refund
Description: Process a refund for a payment.
Request Payload:
json
Copy code
{
  "amount": 150,
  "currency": "USD",
  "refundReason": "Flight canceled"
}
Response Payload:
json
Copy code
{
  "paymentId": "PY123456",
  "status": "Refunded",
  "refundAmount": 150,
  "currency": "USD"
}
4. User Management Microservice
POST /api/users
Description: Register a new user.
Request Payload:
json
Copy code
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "password": "password123",
  "phone": "+1234567890"
}
Response Payload:
json
Copy code
{
  "userId": "user123",
  "name": "John Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890",
  "status": "Registered"
}
POST /api/users/login
Description: Authenticate a user.
Request Payload:
json
Copy code
{
  "email": "john.doe@example.com",
  "password": "password123"
}
Response Payload:
json
Copy code
{
  "userId": "user123",
  "token": "jwt-token",
  "status": "Authenticated"
}
GET /api/users/{id}
Description: Retrieve user details by ID.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "name": "John Doe",
  "email": "john.doe@example.com",
  "phone": "+1234567890"
}
PUT /api/users/{id}
Description: Update user details by ID.
Request Payload:
json
Copy code
{
  "name": "John D.",
  "phone": "+0987654321"
}
Response Payload:
json
Copy code
{
  "userId": "user123",
  "status": "Updated"
}
DELETE /api/users/{id}
Description: Delete a user by ID.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "status": "Deleted"
}
POST /api/users/{id}/change-password
Description: Change user password.
Request Payload:
json
Copy code
{
  "oldPassword": "password123",
  "newPassword": "newpassword456"
}
Response Payload:
json
Copy code
{
  "userId": "user123",
  "status": "Password Changed"
}
GET /api/users/{id}/bookings
Description: Retrieve all bookings for a user.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "bookings": [
    {
      "bookingId": "BK123456",
      "flightId": "FL123",
      "status": "Confirmed"
    }
  ]
}
5. Notification Microservice
POST /api/notifications
Description: Send a notification to a user.
Request Payload:
json
Copy code
{
  "userId": "user123",
  "message": "Your booking has been confirmed.",
  "type": "BookingConfirmation"
}
Response Payload:
json
Copy code
{
  "notificationId": "NT123456",
  "userId": "user123",
  "status": "Sent"
}
GET /api/notifications/{id}
Description: Retrieve notification details by ID.
Response Payload:
json
Copy code
{
  "notificationId": "NT123456",
  "userId": "user123",
  "message": "Your booking has been confirmed.",
  "type": "BookingConfirmation",
  "status": "Sent"
}
PUT /api/notifications/{id}
Description: Update notification details by ID.
Request Payload:
json
Copy code
{
  "message": "Your booking has been updated.",
  "status": "Updated"
}
Response Payload:
json
Copy code
{
  "notificationId": "NT123456",
  "status": "Updated"
}
DELETE /api/notifications/{id}
Description: Delete a notification by ID.
Response Payload:
json
Copy code
{
  "notificationId": "NT123456",
  "status": "Deleted"
}
GET /api/notifications/user/{userId}
Description: Retrieve all notifications for a user.
Response Payload:
json
Copy code
{
  "userId": "user123",
  "notifications": [
    {
      "notificationId": "NT123456",
      "message": "Your booking has been confirmed.",
      "type": "BookingConfirmation",
      "status": "Sent"
    }
  ]
}
POST /api/notifications/{id}/resend
Description: Resend a notification.
Response Payload:
json
Copy code
{
  "notificationId": "NT123456",
  "status": "Resent"
}
GET /api/notifications/status/{status}
Description: Retrieve notifications by status.
Response Payload:
json
Copy code
{
  "status": "Sent",
  "notifications": [
    {
      "notificationId": "NT123456",
      "userId": "user123",
      "message": "Your booking has been confirmed."
    }
  ]
}
6. Pricing Microservice
GET /api/pricing/{flightId}
Description: Retrieve pricing details for a flight.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "basePrice": 500,
  "currency": "USD",
  "tax": 50,
  "totalPrice": 550
}
PUT /api/pricing/{flightId}
Description: Update pricing details for a flight.
Request Payload:
json
Copy code
{
  "basePrice": 520,
  "tax": 55
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Updated"
}
POST /api/pricing
Description: Set pricing details for a flight.
Request Payload:
json
Copy code
{
  "flightId": "FL123",
  "basePrice": 500,
  "currency": "USD",
  "tax": 50
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Set"
}
DELETE /api/pricing/{flightId}
Description: Delete pricing details for a flight.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Deleted"
}
GET /api/pricing/flight/{flightId}/discounts
Description: Retrieve all discounts for a flight.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "discounts": [
    {
      "discountId": "DS123",
      "amount": 50,
      "currency": "USD",
      "type": "Seasonal"
    }
  ]
}
POST /api/pricing/{flightId}/discounts
Description: Apply a discount to a flight.
Request Payload:
json
Copy code
{
  "amount": 50,
  "currency": "USD",
  "type": "Seasonal"
}
Response Payload:
json
Copy code
{
  "discountId": "DS123",
  "status": "Applied"
}
DELETE /api/pricing/discounts/{discountId}
Description: Remove a discount from a flight.
Response Payload:
json
Copy code
{
  "discountId": "DS123",
  "status": "Removed"
}
7. Flight Microservice
POST /api/flights
Description: Add a new flight.
Request Payload:
json
Copy code
{
  "flightId": "FL123",
  "departure": "2024-09-15T08:00:00Z",
  "arrival": "2024-09-15T10:00:00Z",
  "origin": "NYC",
  "destination": "LAX"
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Added"
}
GET /api/flights/{id}
Description: Retrieve flight details by ID.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "departure": "2024-09-15T08:00:00Z",
  "arrival": "2024-09-15T10:00:00Z",
  "origin": "NYC",
  "destination": "LAX"
}
PUT /api/flights/{id}
Description: Update flight details by ID.
Request Payload:
json
Copy code
{
  "departure": "2024-09-15T09:00:00Z"
}
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Updated"
}
DELETE /api/flights/{id}
Description: Delete a flight by ID.
Response Payload:
json
Copy code
{
  "flightId": "FL123",
  "status": "Deleted"
}
GET /api/flights/origin/{origin}
Description: Retrieve all flights from a specific origin.
Response Payload:
json
Copy code
{
  "origin": "NYC",
  "flights": [
    {
      "flightId": "FL123",
      "departure": "2024-09-15T08:00:00Z",
      "arrival": "2024-09-15T10:00:00Z",
      "destination": "LAX"
    }
  ]
}
GET /api/flights/destination/{destination}
Description: Retrieve all flights to a specific destination.
Response Payload:
json
Copy code
{
  "destination": "LAX",
  "flights": [
    {
      "flightId": "FL123",
      "departure": "2024-09-15T08:00:00Z",
      "arrival": "2024-09-15T10:00:00Z",
      "origin": "NYC"
    }
  ]
}
GET /api/flights/schedule/{date}
Description: Retrieve all flights scheduled for a specific date.
Response Payload:
json
Copy code
{
  "date": "2024-09-15",
  "flights": [
    {
      "flightId": "FL123",
      "departure": "2024-09-15T08:00:00Z",
      "arrival": "2024-09-15T10:00:00Z",
      "origin": "NYC",
      "destination": "LAX"
    }
  ]
}






