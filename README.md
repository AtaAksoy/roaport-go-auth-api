# Roaport Backend (Keycloak Registration API)

Welcome to the **Roaport Backend**!  
This is a minimal Go server designed to handle user **registration** and **login** via **Keycloak** authentication system.

## 🚀 Project Structure

```bash
/roaport-backend
├── main.go            # Main Go application (HTTP server + register API)
├── .env.example       # Example environment variables file
```

---

## 👋 Requirements

- Go 1.20+ installed
- Keycloak server running
- Internet access for downloading Go modules

---

## ⚙️ Setup Instructions

1. **Clone the repository**

```bash
git clone https://github.com/AtaAksoy/roaport-go-auth-api
cd roaport-backend
```

2. **Install dependencies**

```bash
go mod tidy
```

(This will install `github.com/joho/godotenv` automatically.)

3. **Configure Environment Variables**

Copy `.env.example` to `.env`:

```bash
cp .env.example .env
```

Then, edit `.env` with your actual Keycloak server information:

```bash
KEYCLOAK_URL=http://your-keycloak-url
REALM=your-realm-name
ADMIN_USERNAME=your-admin-username
ADMIN_PASSWORD=your-admin-password
ADMIN_CLIENT_ID=
MOBILE_CLIENT_ID=
```

4. **Run the server**

```bash
go run main.go
```

Server will start on:

```bash
http://localhost:5000
```

---

## 📩 API Endpoints

### POST `/register`

Registers a new user into the Keycloak server.

**Request Body:**

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "phoneNumber": "5551234567",
  "password": "SecurePassword123!"
}
```

**Response (Success):**

```json
{
  "status": true,
  "message": "User registered successfully",
  "data": {
    "user": {
      "id": "uuid",
      "username": "john.doe@example.com",
      "email": "john.doe@example.com",
      "firstName": "John",
      "lastName": "Doe"
    },
    "access_token": "jwt-token",
    "refresh_token": "jwt-refresh-token"
  }
}
```

**Response (Failure):**

```json
{
  "status": false,
  "message": "Registration failed",
  "data": "Error details"
}
```

---

## 🛆 Technologies Used

- **Golang**
- **Keycloak (Auth Server)**
- **Expo Secure Store (mobile integration)**

---

## ✨ Notes

- Ensure that the admin user has the `manage-users` and `view-users` roles in Keycloak.
- Passwords are **never** exposed in responses.
- Tokens are directly retrieved for seamless mobile app login after registration.
- Do not commit the real `.env` file to public repositories.

---

## 👨‍💼 Author

Made with ❤️ by the **Roaport Team**

---

# 🚀 Let's go build awesome things!