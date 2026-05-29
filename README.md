# Student Assignment Manager

![Node.js](https://img.shields.io/badge/Node.js-22-339933)
![Express](https://img.shields.io/badge/Express-v4-000000)
![React](https://img.shields.io/badge/React-18-61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-5.5-3178C6)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-ready-4169E1)
![Prisma](https://img.shields.io/badge/Prisma-6.1-2D3748)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.4-06B6D4)
![Vite](https://img.shields.io/badge/Vite-5.4-646CFF)
![Docker](https://img.shields.io/badge/Docker-ready-2496ED)

A full-stack web application for managing student assignments, cohorts, and performance tracking. Built with a Node.js/Express backend and a React/TypeScript frontend, this dashboard provides an intuitive interface for educators to manage students, chapters, reports, and settings.

## Table of Contents

- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Screenshots](#screenshots)
- [Prerequisites](#prerequisites)
- [Installation and Setup](#installation-and-setup)
- [Environment Variables](#environment-variables)
- [Running the Project](#running-the-project)
- [Database Setup](#database-setup)
- [Docker Usage](#docker-usage)
- [API Routes](#api-routes)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Student Management** — Add, update, and delete student records with cohort assignments
- **Dashboard** — Overview of key metrics and student activity
- **Chapter Organization** — Organize and manage course chapters
- **Reports** — Generate and view student performance reports
- **Settings** — Configure application preferences
- **Responsive Design** — Mobile-friendly sidebar navigation with toggle functionality
- **Real-time State Management** — Zustand-powered global state for user data

## Tech Stack

### Backend
- **Runtime:** Node.js 22
- **Framework:** Express 4.21
- **ORM:** Prisma 6.1
- **Database:** PostgreSQL
- **Middleware:** CORS, dotenv

### Frontend
- **Framework:** React 18 with TypeScript 5.5
- **Build Tool:** Vite 5.4
- **Styling:** Tailwind CSS 3.4
- **State Management:** Zustand 5.0
- **Routing:** React Router DOM 6.22
- **HTTP Client:** Axios 1.7
- **Icons:** Lucide React 0.344

## Project Structure

```
assignment/
├── backend/
│   ├── prisma/
│   │   ├── schema.prisma
│   │   └── migrations/
│   ├── index.js
│   ├── package.json
│   ├── .env.example
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   └── layout/
│   │   │       ├── Sidebar.tsx
│   │   │       └── Header.tsx
│   │   ├── pages/
│   │   │   ├── Dashboard.tsx
│   │   │   ├── Students.tsx
│   │   │   ├── Chapter.tsx
│   │   │   ├── Reports.tsx
│   │   │   └── Settings.tsx
│   │   ├── store/
│   │   │   └── store.ts
│   │   ├── App.tsx
│   │   ├── main.tsx
│   │   └── index.css
│   ├── vite.config.ts
│   ├── tailwind.config.js
│   └── package.json
└── README.md
```

## Screenshots

<!-- Add screenshots of your application here -->

> _Screenshots coming soon_

## Prerequisites

- **Node.js** >= 22
- **npm** or **yarn**
- **PostgreSQL** database (local or cloud, e.g., Supabase)
- **Docker** (optional, for containerized backend)

## Installation and Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/shivanshsin0203/assignment.git
   cd assignment
   ```

2. **Install backend dependencies:**
   ```bash
   cd backend
   npm install
   ```

3. **Install frontend dependencies:**
   ```bash
   cd ../frontend
   npm install
   ```

## Environment Variables

Create a `.env` file in the `backend/` directory with the following variables:

```env
# Connect to Supabase via connection pooling with Supavisor.
DATABASE_URL="paste connection string here"

# Direct connection to the database. Used for migrations.
DIRECT_URL="paste direct connection string here"
```

> **Note:** Replace the placeholder values with your actual PostgreSQL connection strings. For local development, use `postgresql://user:password@localhost:5432/dbname`.

## Running the Project

### Backend

```bash
cd backend
npm run dev
```

The server will start on port 3001 by default (configurable via `PORT` environment variable).

### Frontend

```bash
cd frontend
npm run dev
```

The Vite development server will start, typically on port 5173.

### Build Frontend for Production

```bash
cd frontend
npm run build
npm run preview
```

## Database Setup

1. **Ensure PostgreSQL is running** and you have a database created.

2. **Configure your `.env` file** with the correct `DATABASE_URL` and `DIRECT_URL`.

3. **Run Prisma migrations:**
   ```bash
   cd backend
   npx prisma migrate dev --name init
   ```

4. **Generate Prisma client:**
   ```bash
   npx prisma generate
   ```

The database schema includes a `User` model with the following fields:
- `id` — Auto-incrementing integer (primary key)
- `name` — String (optional)
- `cohort` — String (required)
- `createdAt` — DateTime (auto-set)
- `updatedAt` — DateTime (auto-updated)

## Docker Usage

Build and run the backend using Docker:

```bash
cd backend
docker build -t assignment-backend .
docker run -p 3001:3001 --env-file .env assignment-backend
```

The Dockerfile uses Node.js 22 Alpine and:
- Copies package files and Prisma schema
- Generates Prisma client
- Installs dependencies
- Exposes port 3001
- Starts the server with `node index.js`

## API Routes

| Method | Endpoint       | Description                |
|--------|----------------|----------------------------|
| GET    | `/`            | Health check               |
| POST   | `/addUser`     | Create a new user          |
| GET    | `/users`       | Get all users              |
| PUT    | `/users/:id`   | Update a user by ID        |
| DELETE | `/users/:id`   | Delete a user by ID        |

### Example Request: Create User

```bash
curl -X POST http://localhost:3001/addUser \
  -H "Content-Type: application/json" \
  -d '{"name": "John Doe", "cohort": "2024-A"}'
```

### Example Response

```json
{
  "message": "Blog created successfully",
  "data": {
    "id": 1,
    "name": "John Doe",
    "cohort": "2024-A",
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T00:00:00.000Z"
  }
}
```

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License.