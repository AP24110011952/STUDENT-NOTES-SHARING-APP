# 📚 Scholar Notes — MERN Stack Student Notes Sharing Platform

A full-stack student notes sharing application built with the **MERN stack** (MongoDB, Express.js, React, Node.js). Students can upload, browse, like, comment on, and save PDF notes — all within a polished, academic-themed UI.

---

## ✨ Features

- 🔐 **JWT Authentication** — Secure register/login with hashed passwords
- 📄 **PDF Upload & Viewing** — Upload notes as PDFs, served statically
- 👍 **Likes & 💬 Comments** — Engage with notes from other students
- 🔖 **Save Notes** — Bookmark notes to your personal dashboard
- 🗂️ **Category Filtering** — Browse notes by subject/category
- 👤 **User Dashboard** — Manage your uploaded and saved notes
- 🛡️ **Admin Panel** — Moderate notes and manage users
- 📱 **Fully Responsive** — Works on all screen sizes

---

## 🗂️ Project Structure

```
MERN STACK PROJECT/
├── client/                  # React + Vite frontend
│   └── src/
│       ├── components/      # Reusable UI components (Navbar, NoteCard, …)
│       ├── context/         # AuthContext (global auth state)
│       ├── pages/           # Page-level components
│       │   ├── LandingPage
│       │   ├── LoginPage / RegisterPage
│       │   ├── NotesPage
│       │   ├── NoteDetailPage
│       │   ├── UploadPage
│       │   ├── DashboardPage
│       │   ├── ProfilePage
│       │   └── AdminPage
│       └── services/        # Axios API service layer
│
└── server/                  # Express.js backend
    ├── controllers/         # Route handler logic
    ├── middleware/          # Auth & upload middleware
    ├── models/              # Mongoose schemas
    │   ├── User
    │   ├── Note
    │   ├── Comment
    │   ├── Like
    │   ├── SavedNote
    │   └── Category
    ├── routes/              # API route definitions
    │   ├── authRoutes
    │   ├── noteRoutes
    │   ├── adminRoutes
    │   └── categoryRoutes
    ├── uploads/             # Uploaded PDF files (local storage)
    ├── seed.js              # Database seeder script
    └── index.js             # Server entry point
```

---

## 🔧 Tech Stack

| Layer       | Technology                                   |
|-------------|----------------------------------------------|
| Frontend    | React 18, Vite, React Router v6              |
| Styling     | Vanilla CSS (Scholar / warm editorial theme) |
| State       | React Context API                            |
| HTTP Client | Axios                                        |
| Backend     | Node.js, Express.js v5                       |
| Database    | MongoDB + Mongoose                           |
| Auth        | JWT + bcryptjs                               |
| File Upload | Multer (local disk storage)                  |
| Logging     | Morgan                                       |
| Validation  | express-validator                            |

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18+
- [MongoDB](https://www.mongodb.com/try/download/community) running locally **or** a MongoDB Atlas URI

---

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd "MERN STACK PROJECT"
```

---

### 2. Configure the Server

```bash
cd server
cp .env.example .env
```

Edit `server/.env` with your values:

```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/notes-sharing-app
JWT_SECRET=your_super_secret_jwt_key_change_in_production
JWT_EXPIRE=7d
NODE_ENV=development
```

Install server dependencies:

```bash
npm install
```

---

### 3. Configure the Client

```bash
cd ../client
npm install
```

---

### 4. Seed the Database *(optional)*

```bash
cd ../server
npm run seed
```

---

### 5. Run the App

Open **two terminals**:

**Terminal 1 — Backend:**
```bash
cd server
npm run dev        # starts with nodemon on http://localhost:5000
```

**Terminal 2 — Frontend:**
```bash
cd client
npm run dev        # starts Vite dev server on http://localhost:5173
```

Visit **http://localhost:5173** in your browser.

---

## 📡 API Endpoints

| Method | Route                    | Description                    | Auth Required |
|--------|--------------------------|--------------------------------|:-------------:|
| POST   | `/api/auth/register`     | Register a new user            | ❌            |
| POST   | `/api/auth/login`        | Login and receive JWT          | ❌            |
| GET    | `/api/notes`             | Get all notes (with filters)   | ❌            |
| GET    | `/api/notes/:id`         | Get a single note              | ❌            |
| POST   | `/api/notes`             | Upload a new note (PDF)        | ✅            |
| DELETE | `/api/notes/:id`         | Delete a note                  | ✅            |
| POST   | `/api/notes/:id/like`    | Like / unlike a note           | ✅            |
| POST   | `/api/notes/:id/comment` | Add a comment                  | ✅            |
| POST   | `/api/notes/:id/save`    | Save / unsave a note           | ✅            |
| GET    | `/api/categories`        | List all categories            | ❌            |
| GET    | `/api/admin/stats`       | Admin dashboard stats          | ✅ Admin      |
| GET    | `/api/health`            | Server health check            | ❌            |

---

## 🔒 Authentication Flow

1. User registers → password hashed with **bcryptjs** and stored in MongoDB
2. On login → server signs a **JWT** (expires in 7 days)
3. Client stores token and attaches it as `Authorization: Bearer <token>` on protected requests
4. `authMiddleware` on the server verifies the token on every protected route

---

## 👮 Roles

| Role    | Permissions                                          |
|---------|------------------------------------------------------|
| `user`  | Browse, upload, like, comment, save, manage own notes |
| `admin` | All user permissions + access to the Admin Panel      |

---

## 🌱 Environment Variables Reference

| Variable    | Description                              | Default                                      |
|-------------|------------------------------------------|----------------------------------------------|
| `PORT`      | Port the Express server listens on       | `5000`                                       |
| `MONGO_URI` | MongoDB connection string                | `mongodb://localhost:27017/notes-sharing-app` |
| `JWT_SECRET`| Secret key used to sign JWTs            | *(set a strong random string)*               |
| `JWT_EXPIRE`| JWT expiry duration                      | `7d`                                         |
| `NODE_ENV`  | Environment (`development`/`production`) | `development`                                |

---

## 📦 Dependencies

### Server
| Package             | Purpose                      |
|---------------------|------------------------------|
| express             | Web framework                |
| mongoose            | MongoDB ODM                  |
| bcryptjs            | Password hashing             |
| jsonwebtoken        | JWT auth tokens              |
| multer              | File (PDF) upload handling   |
| cors                | Cross-Origin Resource Sharing|
| dotenv              | Environment variable loading |
| express-validator   | Request validation           |
| morgan              | HTTP request logging         |
| nodemon *(dev)*     | Auto-restart on file changes |

### Client
| Package          | Purpose                      |
|------------------|------------------------------|
| react            | UI library                   |
| react-router-dom | Client-side routing          |
| axios            | HTTP requests to the API     |
| react-hot-toast  | Toast notifications          |
| vite             | Build tool & dev server      |

---

## 🖥️ Pages Overview

| Route            | Page            | Access        |
|------------------|-----------------|---------------|
| `/`              | Landing Page    | Public        |
| `/login`         | Login           | Public        |
| `/register`      | Register        | Public        |
| `/notes`         | Browse Notes    | Public        |
| `/notes/:id`     | Note Detail     | Public        |
| `/upload`        | Upload Note     | Authenticated |
| `/dashboard`     | My Dashboard    | Authenticated |
| `/profile`       | Profile         | Authenticated |
| `/admin`         | Admin Panel     | Admin only    |

---

## 📝 License

This project is for educational purposes. Feel free to use it as a reference or starting point.
