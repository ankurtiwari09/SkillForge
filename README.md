# 🎓 E-Learning Portal

A full-stack e-learning web application where instructors can create and publish courses, and students can browse, purchase, and track their learning progress — built with the **MERN stack**.

---

## 🚀 Features

### For Students
- Register, log in, and manage your profile
- Browse and search published courses with filters
- Purchase courses via **Stripe** payment integration
- Watch lecture videos and track course progress
- View enrolled courses in "My Learning" dashboard

### For Instructors / Admins
- Create, edit, and publish courses with thumbnails
- Add and manage lectures with video uploads
- View dashboard with course analytics (Recharts)
- Toggle course visibility (published / draft)

### General
- JWT-based authentication (stored in HTTP-only cookies)
- Dark / light mode support via `next-themes`
- Media uploads (images & videos) via **Cloudinary**
- Rich text editor for course descriptions (React Quill)
- Fully responsive UI with **Tailwind CSS** + **shadcn/ui**

---

## 🛠️ Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| React 18 + Vite | UI framework & build tool |
| Redux Toolkit + RTK Query | State management & API calls |
| React Router v6 | Client-side routing |
| Tailwind CSS + shadcn/ui | Styling & component library |
| Radix UI | Accessible headless components |
| React Player | Video playback |
| React Quill | Rich text editor |
| Recharts | Analytics charts |
| Axios | HTTP client |

### Backend
| Technology | Purpose |
|---|---|
| Node.js + Express 5 | Server & REST API |
| MongoDB + Mongoose | Database & ODM |
| JWT + bcryptjs | Authentication & password hashing |
| Cloudinary SDK | Cloud media storage |
| Stripe | Payment processing |
| Cookie-Parser + CORS | Middleware |

---

## 📁 Project Structure

```
E-Learning-Portal/
├── client/                  # React frontend (Vite)
│   └── src/
│       ├── app/             # Redux store & root reducer
│       ├── components/      # Shared UI components
│       ├── features/        # RTK Query API slices (auth, course, purchase, progress)
│       ├── pages/
│       │   ├── admin/       # Instructor dashboard, course & lecture management
│       │   └── student/     # Course browse, detail, progress, profile pages
│       └── layout/          # MainLayout wrapper
│
└── server/                  # Express backend
    ├── controllers/         # Business logic (user, course, purchase, progress)
    ├── models/              # Mongoose schemas (User, Course, Lecture, Purchase, Progress)
    ├── routes/              # API route definitions
    ├── middlewares/         # JWT auth middleware
    └── utils/               # Cloudinary helpers, JWT generator, Multer config
```

---

## ⚙️ Getting Started

### Prerequisites
- Node.js (v18+)
- MongoDB (local or Atlas)
- Cloudinary account
- Stripe account

---

### 1. Clone the repository

```bash
git clone https://github.com/your-username/E-Learning-Portal.git
cd E-Learning-Portal
```

---

### 2. Setup the Server

```bash
cd server
npm install
```

Create a `.env` file inside the `server/` directory:

```env
PORT=3000
MONGO_URI=your_mongodb_connection_string
SECRET_KEY=your_jwt_secret_key

# Cloudinary
CLOUD_NAME=your_cloudinary_cloud_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret
```

Start the server:

```bash
node index.js
```

> The server runs on `http://localhost:3000`

---

### 3. Setup the Client

```bash
cd ../client
npm install
npm run dev
```

> The client runs on `http://localhost:5173`

---

## 🔌 API Endpoints

### Auth (`/api/v1/user`)
| Method | Endpoint | Description |
|---|---|---|
| POST | `/register` | Register a new user |
| POST | `/login` | Login & receive JWT cookie |
| GET | `/logout` | Logout & clear cookie |
| GET | `/profile` | Get logged-in user profile |
| PUT | `/profile/update` | Update profile (with photo upload) |

### Courses (`/api/v1/course`)
| Method | Endpoint | Description |
|---|---|---|
| POST | `/` | Create a new course |
| GET | `/` | Get all courses by creator |
| GET | `/published-courses` | Get all published courses |
| GET | `/search` | Search courses by keyword/filter |
| PUT | `/:courseId` | Edit course details |
| PATCH | `/:courseId` | Toggle publish/unpublish |
| POST | `/:courseId/lecture` | Add a lecture |
| GET | `/:courseId/lecture` | Get all lectures for a course |

### Purchase (`/api/v1/purchase`)
| Method | Endpoint | Description |
|---|---|---|
| POST | `/checkout/create-checkout-session` | Create Stripe checkout session |
| POST | `/webhook` | Handle Stripe webhook events |
| GET | `/course/:courseId/detail-with-status` | Get course with purchase status |

### Progress (`/api/v1/progress`)
| Method | Endpoint | Description |
|---|---|---|
| GET | `/:courseId` | Get progress for a course |
| POST | `/:courseId/lecture/:lectureId/view` | Mark lecture as viewed |
| POST | `/:courseId/complete` | Mark entire course as complete |

---

## 🔐 Authentication Flow

1. On login/register, the server signs a **JWT** and sets it as an **HTTP-only cookie** (expires in 1 day).
2. All protected routes use the `isAuthenticated` middleware, which reads and verifies the cookie token.
3. The frontend uses **Redux + RTK Query** to manage auth state and conditionally render protected routes.

---

## 🌐 Environment Variables Summary

| Variable | Used In | Description |
|---|---|---|
| `MONGO_URI` | Server | MongoDB connection string |
| `SECRET_KEY` | Server | JWT signing secret |
| `CLOUD_NAME` | Server | Cloudinary cloud name |
| `API_KEY` | Server | Cloudinary API key |
| `API_SECRET` | Server | Cloudinary API secret |
| `STRIPE_SECRET_KEY` | Server | Stripe secret key |
| `STRIPE_WEBHOOK_SECRET` | Server | Stripe webhook verification secret |

---
## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
