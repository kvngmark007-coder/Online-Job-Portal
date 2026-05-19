# Online Job Portal

A full-stack online job portal with:
- **Backend**: Spring Boot + Spring Security + JWT + MySQL
- **Frontend**: Static HTML/CSS/JavaScript dashboards for Job Seeker, Recruiter, and Admin

## Project Structure

```text
Online-Job-Portal/
├── backend/      # Spring Boot REST API
└── frontend/     # Static web app
```

## Prerequisites

Install these tools before setup:
- **Java 17**
- **Maven 3.9+**
- **MySQL 8+**
- (Optional) **Docker**

## 1) Backend Setup (Local)

The backend reads configuration from environment variables with safe defaults.

### Environment variables

You can set these in your terminal before starting the app:

```bash
export MYSQL_HOST=localhost
export MYSQLPORT=3306
export MYSQLDATABASE=job_portal
export MYSQL_USER=root
export MYSQLPASSWORD=your_password
export JWT_SECRET=your_very_long_random_secret
export PORT=8080
```

If you do not set them, the application uses defaults from `application.properties`.

### Run backend

```bash
cd backend
mvn clean install
mvn spring-boot:run
```

The API will start at:

- `http://localhost:8080`
- Base API path used by frontend: `http://localhost:8080/api`

## 2) Frontend Setup (Local)

The frontend is static files and can be served with any simple HTTP server.

### Option A: Python server

```bash
cd frontend
python3 -m http.server 5500
```

Open:

- `http://localhost:5500/index.html`

### Option B: VS Code Live Server

- Open `frontend/index.html`
- Start with the Live Server extension

> Note: `frontend/js/api.js` already points to `http://localhost:8080/api` when running on localhost.

## 3) Quick Start Order

1. Start MySQL.
2. Start backend (`mvn spring-boot:run`).
3. Serve frontend (`python3 -m http.server 5500`).
4. Open `index.html` and register/login.

## 4) Docker (Backend Only)

A backend Dockerfile is provided.

```bash
cd backend
docker build -t online-job-portal-backend .
docker run --rm -p 8080:8080 \
  -e MYSQL_HOST=host.docker.internal \
  -e MYSQLPORT=3306 \
  -e MYSQLDATABASE=job_portal \
  -e MYSQL_USER=root \
  -e MYSQLPASSWORD=your_password \
  -e JWT_SECRET=your_very_long_random_secret \
  online-job-portal-backend
```

## 5) Common Issues

- **Cannot connect to MySQL**
  - Verify MySQL is running and credentials are correct.
  - Confirm `MYSQL_HOST` and `MYSQLPORT` match your DB server.

- **401 Unauthorized from frontend**
  - Log in again to refresh token in local storage.
  - Make sure backend is running on port `8080`.

- **CORS or wrong API URL**
  - Ensure frontend is opened via HTTP server (not `file://`).
  - Confirm `frontend/js/api.js` local URL is `http://localhost:8080/api`.

## 6) Useful Commands

```bash
# Run backend tests
cd backend && mvn test

# Build backend jar
cd backend && mvn clean package
```

---

If you want, I can also add:
- a `.env.example` for backend variables,
- Docker Compose for MySQL + backend,
- and one-command startup instructions.
