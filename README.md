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

## API Endpoints

- `GET /` - Welcome message
- `POST /login` - Authenticate and get access token
- `GET /me` - Get current authenticated user information
- `GET /appointments` - List all appointments (requires authentication)
- `GET /appointments/{appointment_id}` - Get specific appointment (requires authentication)
- `POST /appointments` - Create new appointment (requires authentication)
- `PUT /appointments/{appointment_id}` - Update appointment (requires authentication)
- `DELETE /appointments/{appointment_id}` - Cancel appointment (requires authentication)