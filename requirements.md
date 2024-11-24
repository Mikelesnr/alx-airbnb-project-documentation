# Airbnb Clone Backend Requirements

## 1. User Authentication

### API Endpoints

- **POST /api/register**
  - **Input**:
    ```json
    {
      "username": "string",
      "email": "string",
      "password": "string"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "User registered successfully",
      "userId": "string"
    }
    ```
- **POST /api/login**
  - **Input**:
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  - **Output**:
    ```json
    {
      "token": "JWT token",
      "userId": "string"
    }
    ```

### Validation Rules

- Email must be a valid email format.
- Password must be at least 8 characters long.
- Username must be unique.

### Performance Criteria

- Registration and login processes should complete within 2 seconds.
- JWT tokens should be securely generated and validated.

## 2. Property Management

### API Endpoints

- **POST /api/properties**
  - **Input**:
    ```json
    {
      "title": "string",
      "description": "string",
      "location": "string",
      "price": "number",
      "amenities": ["string"],
      "availability": {
        "startDate": "date",
        "endDate": "date"
      }
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Property listed successfully",
      "propertyId": "string"
    }
    ```
- **PUT /api/properties/{propertyId}**
  - **Input**:
    ```json
    {
      "title": "string",
      "description": "string",
      "location": "string",
      "price": "number",
      "amenities": ["string"],
      "availability": {
        "startDate": "date",
        "endDate": "date"
      }
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Property updated successfully"
    }
    ```
- **DELETE /api/properties/{propertyId}**
  - **Output**:
    ```json
    {
      "message": "Property deleted successfully"
    }
    ```

### Validation Rules

- Title must be between 5 and 100 characters.
- Description must be between 20 and 1000 characters.
- Price must be a positive number.
- Availability dates must be valid and in the future.

### Performance Criteria

- Property listing and updates should complete within 3 seconds.
- Data should be securely stored and retrieved from the database.

## 3. Booking System

### API Endpoints

- **POST /api/bookings**
  - **Input**:
    ```json
    {
      "propertyId": "string",
      "userId": "string",
      "startDate": "date",
      "endDate": "date"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Booking created successfully",
      "bookingId": "string"
    }
    ```
- **PUT /api/bookings/{bookingId}**
  - **Input**:
    ```json
    {
      "startDate": "date",
      "endDate": "date"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Booking updated successfully"
    }
    ```
- **DELETE /api/bookings/{bookingId}**
  - **Output**:
    ```json
    {
      "message": "Booking canceled successfully"
    }
    ```

### Validation Rules

- Booking dates must be valid and not overlap with existing bookings.
- PropertyId and userId must be valid and exist in the database.

### Performance Criteria

- Booking creation and updates should complete within 2 seconds.
- Booking data should be securely stored and retrieved from the database.

## 4. Search and Filtering

### API Endpoints

- **GET /api/properties/search**
  - **Input**:
    ```json
    {
      "location": "string",
      "priceRange": {
        "min": "number",
        "max": "number"
      },
      "guests": "number",
      "amenities": ["string"],
      "page": "number",
      "limit": "number"
    }
    ```
  - **Output**:
    ```json
    {
      "properties": [
        {
          "propertyId": "string",
          "title": "string",
          "description": "string",
          "location": "string",
          "price": "number",
          "amenities": ["string"],
          "availability": {
            "startDate": "date",
            "endDate": "date"
          }
        }
      ],
      "totalPages": "number",
      "currentPage": "number"
    }
    ```

### Validation Rules

- Location must be a valid string.
- Price range must include valid numbers.
- Guests must be a positive integer.
- Page and limit must be positive integers.

### Performance Criteria

- Search results should be returned within 2 seconds.
- Pagination should handle large datasets efficiently.

## 5. Reviews and Ratings

### API Endpoints

- **POST /api/reviews**
  - **Input**:
    ```json
    {
      "bookingId": "string",
      "rating": "number",
      "comment": "string"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Review added successfully",
      "reviewId": "string"
    }
    ```
- **PUT /api/reviews/{reviewId}**
  - **Input**:
    ```json
    {
      "rating": "number",
      "comment": "string"
    }
    ```
  - **Output**:
    ```json
    {
      "message": "Review updated successfully"
    }
    ```
- **DELETE /api/reviews/{reviewId}**
  - **Output**:
    ```json
    {
      "message": "Review deleted successfully"
    }
    ```

### Validation Rules

- Rating must be a number between 1 and 5.
- Comment must be between 10 and 500 characters.
- BookingId must be valid and exist in the database.

### Performance Criteria

- Reviews should be linked to specific bookings to prevent abuse.
- Review operations should complete within 2 seconds.

---
