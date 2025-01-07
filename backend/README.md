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

### Endpoint: `/captains/register`

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

# Captain Endpoints Documentation

## 1. Register Captain
### `POST /captains/register`

#### Request Body:
```json
{
  "fullname": {
    "firstname": "John",       // required, min 3 chars
    "lastname": "Doe"         // optional
  },
  "email": "john@example.com", // required, valid email format
  "password": "password123",   // required, min 6 chars
  "vehicle": {
    "color": "Black",         // required, min 3 chars
    "plate": "ABC123",        // required, min 3 chars
    "capacity": 4,            // required, min 1
    "vehicleType": "car"      // required, enum: ["car", "bike", "auto"]
  }
}
{
  "token": "JWT_TOKEN",
  "captain": {
    "_id": "CAPTAIN_ID",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john@example.com",
    "vehicle": {
      "color": "Black",
      "plate": "ABC123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}


## 2. Login Captain
### `POST /captains/register`

#### Request Body:
```json
{
  "email": "john@example.com",    // required, valid email
  "password": "password123"       // required, min 6 chars
}
{
  "token": "JWT_TOKEN",
  "captain": {
    "_id": "CAPTAIN_ID",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john@example.com",
    "vehicle": {
      "color": "Black",
      "plate": "ABC123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}
3. Get Captain Profile
GET /captains/profile
Headers:
{
  "Authorization": "Bearer JWT_TOKEN"    // required
}
{
  "captain": {
    "_id": "CAPTAIN_ID",
    "fullname": {
      "firstname": "John",
      "lastname": "Doe"
    },
    "email": "john@example.com",
    "vehicle": {
      "color": "Black",
      "plate": "ABC123",
      "capacity": 4,
      "vehicleType": "car"
    }
  }
}

4. Logout Captain
GET /captains/logout
Headers:
{
  "Authorization": "Bearer JWT_TOKEN"    // required
}
Success Response (200 OK):
{
  "message": "Logout successfully"
}




/maps/get-coordinates Endpoint

Description
Retrieves the coordinates (latitude and longitude) for a given address.

HTTP Method
GET

Request Parameters
address (string, required): The address for which to retrieve coordinates.

Example Request
GET /maps/get-coordinates?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA

Example Response

{
  "ltd": 37.4224764,
  "lng": -122.0842499
}

/maps/get-distance-time Endpoint
Description
Retrieves the distance and estimated travel time between two locations.

HTTP Method
GET

Request Parameters
origin (string, required): The starting address or location.
destination (string, required): The destination address or location.


Example Request
GET /maps/get-distance-time?origin=New+York,NY&destination=Los+Angeles,CA

Example Response
{
  "distance": {
    "text": "2,789 miles",
    "value": 4486540
  },
  "duration": {
    "text": "1 day 18 hours",
    "value": 154800
  }
}

Error Response
400 Bad Request: If the origin or destination parameter is missing or invalid.
404 Not Found: If the distance and time for the given locations could not be found.

{
  "message": "No routes found"
}


/maps/get-suggestions Endpoint
Description
Retrieves autocomplete suggestions for a given input string.

HTTP Method
GET

Request Parameters
input (string, required): The input string for which to retrieve suggestions.

Example Request
GET /maps/get-suggestions?input=1600+Amphitheatre

Example Response
[
  "1600 Amphitheatre Parkway, Mountain View, CA, USA",
  "1600 Amphitheatre Pkwy, Mountain View, CA 94043, USA"
]

Error Response
400 Bad Request: If the input parameter is missing or invalid.
500 Internal Server Error: If there is an error retrieving suggestions.

{
  "message": "Unable to fetch suggestions"
}


/rides/create Endpoint
Description
Creates a new ride with the provided information.

HTTP Method
POST

Authentication
Requires a valid JWT token in the Authorization header: Authorization: Bearer <token>

Request Body
The request body should be in JSON format and include the following fields:

pickup (string, required): The pickup address (minimum 3 characters).
destination (string, required): The destination address (minimum 3 characters).
vehicleType (string, required): The type of vehicle (must be 'auto', 'car', or 'moto').


Example Response
ride (object):
user (string): User ID.
pickup (string): Pickup address.
destination (string): Destination address.
fare (number): Fare amount.
status (string): Ride status.
duration (number): Duration in seconds.
distance (number): Distance in meters.
otp (string): OTP for the ride.


Error Response
400 Bad Request: If any required field is missing or invalid.
500 Internal Server Error: If there is an error creating the ride.
{
  "message": "Error message"
}

/rides/get-fare Endpoint
Description
Retrieves the fare estimate for a ride between the provided pickup and destination addresses.

HTTP Method
GET

Authentication
Requires a valid JWT token in the Authorization header: `Authorization:

Bearer `

Request Parameters
pickup (string, required): The pickup address (minimum 3 characters).
destination (string, required): The destination address (minimum 3 characters).

Example Request
GET /rides/get-fare?pickup=1600+Amphitheatre+Parkway,+Mountain+View,+CA&destination=1+Infinite+Loop,+Cupertino,+CA

Example Response
{
  "auto": 50.0,
  "car": 75.0,
  "moto": 40.0
}

Error Response
400 Bad Request: If any required parameter is missing or invalid.
500 Internal Server Error: If there is an error calculating the fare.
{
  "message": "Error message"
}