# Roaport Go Auth API (Archived)

**⚠️ This repository is archived and is no longer in use. The authentication logic for the Roaport project has been migrated to the main `roaport-website` repository, which uses NextAuth.js with a Keycloak provider. This repository is kept for historical and reference purposes only.**

---

This repository contains the source code for a minimal authentication microservice for the Roaport project, written in **Go**. It was developed during the initial phases of the project to provide a standalone service for user registration and login, interfacing with a **Keycloak** authentication server.

## Original Purpose & Features

The primary goal of this service was to act as a backend-for-frontend (BFF) for the Roaport mobile app, handling all direct interactions with Keycloak.

- **User Registration**: Provided a `POST /register` endpoint that took user details (name, email, password), created a new user in Keycloak via the Keycloak Admin API, and then immediately logged the user in to return access and refresh tokens.
- **User Login**: Provided a `POST /login` endpoint that exchanged user credentials for Keycloak tokens.
- **Token Refresh**: Included a `POST /refresh` endpoint to allow clients to use a refresh token to obtain a new access token.
- **Keycloak Integration**:
  - Used an admin-level service account to perform administrative tasks like user creation.
  - Interfaced with Keycloak's OpenID Connect token endpoint to handle authentication flows.
- **Environment-Based Configuration**: All Keycloak connection details (URL, realm, client IDs, admin credentials) were managed via a `.env` file.

## Tech Stack

- **Language**: [Go](https://go.dev/) (Golang)
- **Primary Dependencies**:
  - `net/http` (for the web server)
  - `encoding/json` (for handling JSON payloads)
  - `github.com/joho/godotenv` (for managing environment variables)
- **Authentication Server**: [Keycloak](https://www.keycloak.org/)

## Reason for Archival

As the project evolved, the authentication requirements became more complex, especially for integrating the web-based admin dashboard with role-based access control. The decision was made to centralize all authentication logic within the main `roaport-website` Next.js application using the **NextAuth.js** library.

This new approach offered several advantages over the standalone Go service:
- **Simplified Architecture**: Reduced the number of microservices to maintain.
- **Seamless Web Integration**: NextAuth provides tight integration with Next.js for protecting pages and API routes on the server side.
- **Robust Session Management**: Leveraged NextAuth's mature handling of cookies, sessions, and token rotation.
- **Unified Auth Flow**: Provided a single, consistent authentication system for both the web admin panel and the mobile app's API endpoints.

While this Go service was a valuable exercise in building a standalone microservice, the integrated NextAuth solution proved to be a more practical and feature-rich choice for the project's final architecture.

## API Endpoints (For Reference)

### `POST /register`

- **Request Body**:
  ```json
  {
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "phoneNumber": "5551234567",
    "password": "SecurePassword123!"
  }
  ```
- **Success Response**:
  ```json
  {
    "status": true,
    "message": "User registered successfully",
    "data": {
      "user": { ... },
      "access_token": "...",
      "refresh_token": "..."
    }
  }
  ```

### `POST /login`

- **Request Body**:
  ```json
  {
    "email": "john.doe@example.com",
    "password": "SecurePassword123!"
  }
  ```

### `POST /refresh`

- **Request Body**:
  ```json
  {
    "refreshToken": "..."
  }
  ```

## Setup Instructions (For Historical Reference)

### Environment Variables

A `.env` file was required with the following structure:

```env
KEYCLOAK_URL=http://your-keycloak-url
REALM=your-realm-name
ADMIN_USERNAME=your-admin-username
ADMIN_PASSWORD=your-admin-password
ADMIN_CLIENT_ID=admin-cli
MOBILE_CLIENT_ID=your-mobile-client-id
```

### Running the Server

1.  **Install dependencies:**
    ```bash
    go mod tidy
    ```
2.  **Run the server:**
    ```bash
    go run main.go
    ```
