# Good Morning App

This repository contains a simple "Good Morning" full-stack application. It allows a user to submit their name, phone number, and email address, which are then saved to a PostgreSQL database.

It includes:
- A local PostgreSQL database setup.
- A Node.js + Express backend REST API.
- A ReactJS frontend web application.
- A Flutter mobile application.

## Prerequisites
Ensure you have the following installed on your machine:
- Node.js & npm
- PostgreSQL (or Docker/docker-compose to run it via container)
- Flutter SDK (for mobile)

## 1. Database Setup
You can either run the database using Docker or run it locally.

### Using Docker (Recommended):
From the root directory, run:
```bash
docker-compose up -d
```
This starts a PostgreSQL instance on `localhost:5432` with a database named `mydb`, username `myuser`, and password `mypassword`. The `init.sql` script is automatically executed to create the `users` table.

### Manual Setup:
1. Ensure PostgreSQL is running locally.
2. Create a user: `CREATE USER myuser WITH PASSWORD 'mypassword';`
3. Create the database: `CREATE DATABASE mydb OWNER myuser;`
4. Connect to `mydb` and run the queries in `init.sql` to create the table.
5. Grant permissions if necessary:
   ```sql
   GRANT ALL PRIVILEGES ON TABLE users TO myuser;
   GRANT USAGE, SELECT ON SEQUENCE users_id_seq TO myuser;
   ```

## 2. Backend Setup
The backend is a Node.js + Express app running on port 3000.

1. Navigate to the backend directory:
   ```bash
   cd backend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the server:
   ```bash
   node index.js
   ```
   The backend will run at `http://localhost:3000`.

## 3. Frontend Setup (React)
The frontend is a React application built with Vite.

1. Navigate to the frontend directory:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
4. Open the displayed URL (e.g., `http://localhost:5173`) in your browser to see the "Good Morning" page.

## 4. Mobile Setup (Flutter)
The mobile app is built with Flutter and runs the same "Good Morning" interface.

1. Navigate to the mobile directory:
   ```bash
   cd mobile
   ```
2. Fetch dependencies:
   ```bash
   flutter pub get
   ```
3. Run the application (choose your target device or run on web):
   ```bash
   flutter run
   ```
   *(Note: For Android/iOS emulators, ensure they are running, or run on Chrome via `flutter run -d chrome`).*

## API Endpoints
- `POST /submit` : Accepts a JSON body `{"name": "...", "phone": "...", "email": "..."}` and inserts the data into the PostgreSQL `users` table. Returns the created record.
- `GET /users` : Returns all submitted users from the database.