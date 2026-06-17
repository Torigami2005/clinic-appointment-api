# Clinic Appointment API

This project is a Clinic Appointment API with authentication built using FastAPI and Docker.

## Laboratory Context

This project was developed in an offline Windows 11 laboratory environment.
Python was not installed directly on the computer. The application was executed using Docker and a
prebuilt Docker image named clinic-fastapi-base:1.0.

## Features

- User authentication with Bearer token

- Login endpoint to obtain access tokens

- View current authenticated user information

- Create clinic appointments

- View all appointments

- View one appointment

- Update appointment details

- Cancel appointments

## Technologies Used

- Python

- FastAPI

- Pydantic (for data validation)

- HTTPBearer (for authentication)

- Docker

- Git

## How to Run

```bash
docker compose up --build
```

Open http://localhost:8000/docs to access the Swagger UI.

## Authentication

The API requires Bearer token authentication for most endpoints.

**Default credentials:**
- Username: `admin`
- Password: `clinic123`

**Steps to authenticate:**
1. Use the `/login` endpoint with your username and password
2. Obtain the access token from the response
3. Include the token in the Authorization header as `Bearer <token>` for subsequent requests

## Logout and Token Management

**Why is there no logout endpoint?**

This implementation uses stateless token-based authentication. The server does not maintain any session state, meaning the token is valid until it expires or is no longer used by the client.

**How logout works in production token-based systems:**

1. **Client-side logout**: The client simply discards the token from local storage or memory. No server request is needed.

2. **Token expiration**: Tokens should have a short expiration time (e.g., 15-30 minutes). Users need to re-authenticate to get a new token.

3. **Token blacklisting**: For real logout functionality, a production system would:
   - Maintain a database of invalidated tokens
   - Check against this blacklist during token verification
   - Add tokens to the blacklist when a logout request is made

4. **Refresh tokens**: Use a two-token system:
   - Short-lived access tokens (for API requests)
   - Long-lived refresh tokens (to obtain new access tokens)
   - Logout invalidates the refresh token, preventing new access tokens from being issued

5. **Revocation list (Redis/Cache)**: Store invalidated tokens in a fast cache like Redis with TTL matching the token expiration time.

For this simple demonstration, client-side logout (discarding the token) is sufficient.

## API Endpoints

- `GET /` - Welcome message
- `POST /login` - Authenticate and get access token
- `GET /me` - Get current authenticated user information
- `GET /appointments` - List all appointments (requires authentication)
- `GET /appointments/{appointment_id}` - Get specific appointment (requires authentication)
- `POST /appointments` - Create new appointment (requires authentication)
- `PUT /appointments/{appointment_id}` - Update appointment (requires authentication)
- `DELETE /appointments/{appointment_id}` - Cancel appointment (requires authentication)