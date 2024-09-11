To include a "Copy code" button in your `README.md` file on GitHub, you'll need to use GitHub's built-in Markdown features for code blocks. Unfortunately, GitHub's Markdown doesn't support adding a "Copy code" button directly. However, you can enhance the readability of your code snippets by using proper Markdown formatting. Users can then manually copy the code snippets.

Here’s how you can format your `README.md` file to display code snippets clearly:

```markdown
# Flight Search Microservice

## GET /api/flights/search
**Description**: Search for available flights based on criteria.

**Request Payload**:
```json
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
```

**Response Payload**:
```json
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
```

## GET /api/flights/{id}
**Description**: Retrieve flight details by ID.

**Response Payload**:
```json
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
```

## POST /api/flights
**Description**: Create a new flight entry.

**Request Payload**:
```json
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
```

**Response Payload**:
```json
{
  "flightId": "FL123",
  "status": "Created"
}
```

## PUT /api/flights/{id}
**Description**: Update flight details by ID.

**Request Payload**:
```json
{
  "price": {
    "amount": 320,
    "currency": "USD"
  },
  "seatsAvailable": 90
}
```

**Response Payload**:
```json
{
  "flightId": "FL123",
  "status": "Updated"
}
```

## DELETE /api/flights/{id}
**Description**: Delete a flight entry by ID.

**Response Payload**:
```json
{
  "flightId": "FL123",
  "status": "Deleted"
}
```

## GET /api/flights/availability/{id}
**Description**: Retrieve flight seat availability.

**Response Payload**:
```json
{
  "flightId": "FL123",
  "seatsAvailable": 50,
  "seatMap": [
    {"row": 1, "seats": 6},
    {"row": 2, "seats": 6}
  ]
}
```

## GET /api/flights/price/{id}
**Description**: Retrieve the price of a specific flight.

**Response Payload**:
```json
{
  "flightId": "FL123",
  "basePrice": 250,
  "taxes": 50,
  "totalPrice": 300,
  "currency": "USD"
}
```

# Booking Microservice

## POST /api/bookings
**Description**: Create a new booking.

**Request Payload**:
```json
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
```

**Response Payload**:
```json
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
```

(And so on for the other sections...)

```

