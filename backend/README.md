# User Endpoints Documentation

## User Registration Endpoint

### Endpoint: `/users/register`

#### Method: POST

#### Description:
This endpoint is used to register a new user. It validates the input data, hashes the user's password, and stores the user information in the database. Upon successful registration, it returns a JSON Web Token (JWT) and the user details.

#### Request Body:
The request body must be a JSON object containing the following fields:

- `fullname`: An object containing:
  - `firstname`: A string with a minimum length of 3 characters (required).
  - `lastname`: A string with a minimum length of 3 characters (optional).
- `email`: A string representing the user's email address (required, must be a valid email).
- `password`: A string with a minimum length of 6 characters (required).

Example:
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "password123"
}
```

## User Login Endpoint

### Endpoint: `/users/login`

#### Method: POST

#### Description:
This endpoint is used to authenticate a user. It validates the input data, checks the user's credentials, and returns a JSON Web Token (JWT) and the user details upon successful authentication.

#### Request Body:
The request body must be a JSON object containing the following fields:

- `email`: A string representing the user's email address (required, must be a valid email).
- `password`: A string with a minimum length of 6 characters (required).

Example:
```json
{
  "email": "john.doe@example.com",
  "password": "password123"
}
```

### Example Response:
```json
{
  "token": "JWT_TOKEN",
  "user": {
    "_id": "USER_ID",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  }
}
```

## User Profile Endpoint

### Endpoint: `/users/profile`

#### Method: GET

#### Description:
This endpoint retrieves the authenticated user's profile information. Requires a valid JWT token in the Authorization header.

#### Headers:
- `Authorization`: Bearer JWT_TOKEN (required)

#### Responses:

##### Success (200 OK):
- **Description**: User profile retrieved successfully.
- **Body**:
  ```json
  {
    "_id": "USER_ID",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john.doe@example.com"
  }
  ```



## User Logout Endpoint

### Endpoint: `/users/logout`

#### Method: GET

#### Description:
This endpoint logs out the current user by invalidating their JWT token. Requires authentication.

#### Authentication:
- Requires valid JWT token in Authorization header
- Format: `Bearer <token>`

#### Responses:

##### Success (200 OK):
- **Description**: User logged out successfully
- **Body**:
  ```json
  {
    "message": "Logged out successfully"
  }

# Captain Endpoints Documentation

## Captain Registration Endpoint

### Endpoint: `/captain/register`

#### Method: POST

#### Description:
This endpoint registers a new captain with their vehicle details. It validates the input data and stores the captain information in the database.

#### Request Body:
The request body must be a JSON object containing:

- `fullname`: An object containing:
  - `firstname`: String, minimum 3 characters (required)
  - `lastname`: String (optional)
- `email`: String, valid email format (required)
- `password`: String, minimum 6 characters (required)
- `vehicle`: An object containing:
  - `color`: String, minimum 3 characters (required)
  - `plate`: String, minimum 3 characters (required)
  - `capacity`: Integer, minimum 1 (required)
  - `vehicleType`: String, must be one of: 'car', 'bike', 'auto' (required)

#### Example Request:
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.captain@example.com",
  "password": "password123",
  "vehicle": {
    "color": "Black",
    "plate": "ABC123",
    "capacity": 4,
    "vehicleType": "car"
  }
}
