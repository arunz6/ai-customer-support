# AI Customer Support

A multi-tenant customer support / ticketing platform built with the MERN stack. Businesses (tenants) can onboard, and their customers can raise support tickets that agents/admins manage — with AI-assisted resolution planned as a core feature.

> ⚠️ **Project status:** actively in development. Auth, tenants, users, and tickets are functional. AI resolution, live messaging (sockets), dashboard analytics, and email notifications are scaffolded but not yet implemented.

## Tech Stack

**Backend**
- Node.js + Express 5
- MongoDB + Mongoose
- JWT authentication + Google OAuth 2.0 (Passport.js)
- bcrypt for password hashing
- express-validator for request validation
- helmet, cors, morgan, cookie-parser

**Frontend**
- React 19 + Vite
- Redux Toolkit + React Redux
- React Router v7
- Tailwind CSS

## Features

- 🏢 **Multi-tenant architecture** — each business (`Tenant`) has its own admins, agents, and customers
- 🔐 **Authentication** — email/password registration & login (JWT in httpOnly cookies) plus "Sign in with Google"
- 🎫 **Support tickets** — customers can open tickets with title, description, priority, and status tracking (`open → in_progress → resolved → closed`)
- 👥 **Role-based access** — `super_admin`, `business_admin`, `agent`, `customer` roles
- 🤖 **AI-assisted resolution** *(in progress)* — tickets can be flagged as AI-resolved
- 💬 **Real-time messaging** *(planned)* — Socket.IO scaffolding for live ticket conversations

## Project Structure

```
ai-customer-support/
├── backend/
│   ├── server.js                 # Entry point
│   └── src/
│       ├── app.js                # Express app & middleware setup
│       ├── config/                # Env config & DB connection
│       ├── controllers/           # Route handlers (auth, tickets, messages, dashboard, AI)
│       ├── middleware/            # Auth middleware
│       ├── models/                # Mongoose schemas (User, Tenant, Ticket, Message)
│       ├── routes/                # Express routers
│       ├── services/              # AI & mail services
│       ├── sockets/                # Socket.IO handlers
│       └── validators/            # Request validation rules
└── frontend/
    └── src/
        ├── app/                   # App shell, routing, Redux store
        └── features/
            ├── admins/            # Admin dashboard
            ├── auth/              # Login & registration
            ├── consumer/          # Customer-facing views
            └── homepage/          # Landing page
```

## Getting Started

### Prerequisites
- Node.js (v18+ recommended)
- MongoDB instance (local or Atlas)
- Google OAuth credentials (for Google login)

### 1. Clone the repository
```bash
git clone https://github.com/arunz6/ai-customer-support.git
cd ai-customer-support
```

### 2. Backend setup
```bash
cd backend
npm install
```

Create a `.env` file in `backend/` with:
```env
PORT=5000
MONGO_URL=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
```

Run the backend:
```bash
npm start
```

### 3. Frontend setup
```bash
cd ../frontend
npm install
npm run dev
```

The frontend will run on `http://localhost:5173` and the backend on the port set in `.env`.

## API Overview

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new admin or customer |
| POST | `/api/auth/login` | Log in with email & password |
| GET | `/api/auth/getcompanies` | List registered companies (tenants) |
| GET | `/api/auth/google` | Start Google OAuth flow |
| GET | `/api/auth/google/callback` | Google OAuth callback |

*(Ticket, message, dashboard, and AI endpoints are in progress.)*

## Roadmap

- [ ] Complete ticket CRUD endpoints
- [ ] AI-powered ticket triage & auto-resolution
- [ ] Real-time chat via Socket.IO
- [ ] Email notifications
- [ ] Admin analytics dashboard

## Contributing

This is a personal learning project. Suggestions and PRs are welcome.

## License

ISC
