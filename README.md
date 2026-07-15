# 🧠📄 AI Research Paper Tutor

> Upload any research paper and instantly get simplified summaries, flashcards, quizzes, mind maps, formula/diagram explanations, translations, and voice narration — powered by Gemini AI.

## ✨ Features

- 🔐 **Full JWT Authentication** — register, login, logout, forgot/reset password, change password, profile & avatar, refresh tokens
- 📤 **Upload & Processing** — drag-and-drop PDF/DOCX/TXT upload with automatic section detection (abstract, methodology, results, etc.)
- 🤖 **22 AI Summary Styles** — from a one-line summary to a full ELI5 explanation, in 9 languages
- ➗ **Formula Explainer** — step-by-step breakdown of equations: meaning, variables, units, derivation, worked example
- 🖼️ **Diagram Explainer** — plain-language descriptions of detected figures/tables
- 🃏 **Flashcards** — auto-generated, flippable, favoritable, shuffleable
- ❓ **Quizzes** — MCQ (10/20), true/false, fill-in-the-blank, short answer, with instant scoring and a per-user leaderboard
- 🧭 **Interactive Mind Maps** — zoomable SVG mind map with PNG export
- 🔊 **Text-to-Speech** — play/pause/resume/stop, voice & speed selection
- 🔖 **Bookmarks & Search** — save and search papers, summaries, flashcards, quizzes
- 📊 **Analytics Dashboard** — weekly/monthly charts, learning streak, achievements
- 🛡️ **Admin Panel** — manage users & papers, system analytics, API usage
- 🎨 **Premium UI** — glassmorphism, animated gradients, dark/light mode, Framer Motion

## 🛠️ Tech Stack

**Frontend:** Next.js 15 (App Router) · React 19 · TypeScript · Tailwind CSS · Framer Motion · Recharts · React Hook Form + Zod · React Hot Toast

**Backend:** Node.js · Express.js · MongoDB · Mongoose · JWT · bcrypt · Multer · pdf-parse · mammoth · Helmet · Morgan · express-rate-limit

**AI:** Google Gemini 1.5 Flash, with an automatic offline mock engine when no API key is set — the app is fully usable without any AI key.

## 📁 Folder Structure

```
ai-research-paper-tutor/
├── backend/
│   ├── config/          # DB connection, constants
│   ├── controllers/     # Route handlers
│   ├── middleware/      # auth, error handling, rate limiting, upload, validation
│   ├── models/          # Mongoose schemas
│   ├── routes/          # Express routers
│   ├── services/        # Gemini AI service, prompt templates, document parser, analytics
│   ├── utils/           # token generation, streak tracking, admin seed script
│   ├── app.js
│   └── server.js
└── frontend/
    ├── app/              # Next.js App Router pages
    ├── components/       # Reusable UI components
    ├── context/          # Auth & Theme providers
    ├── lib/              # API client, utilities
    └── types/            # TypeScript types
```

## 🚀 Getting Started

### Prerequisites
- Node.js 18+
- MongoDB (local or MongoDB Atlas)
- (Optional) A Gemini API key from [Google AI Studio](https://aistudio.google.com/) — the app runs fine without one, using a built-in mock AI engine

### 1. Backend Setup

```bash
cd backend
cp .env.example .env
# edit .env with your MONGO_URI, JWT secrets, and (optionally) GEMINI_API_KEY
npm install
npm run seed:admin   # creates a default admin account
npm run dev
```

The API runs at `http://localhost:5000`.

### 2. Frontend Setup

```bash
cd frontend
cp .env.example .env.local
npm install
npm run dev
```

The app runs at `http://localhost:3000`.

### Default Admin Login
After running `npm run seed:admin`:
- Email: `admin@researchtutor.ai`
- Password: `Admin@12345` (change this immediately after first login)

## 🔑 Environment Variables

**backend/.env**
```
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://127.0.0.1:27017/ai-research-paper-tutor
JWT_SECRET=change_this_to_a_long_random_secret
JWT_REFRESH_SECRET=change_this_to_another_long_random_secret
JWT_EXPIRES_IN=15m
JWT_REFRESH_EXPIRES_IN=7d
GEMINI_API_KEY=
CLIENT_URL=http://localhost:3000
```

**frontend/.env.local**
```
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

## 🌐 Deployment

- **Frontend → Vercel**: import the `frontend` folder as a project, set `NEXT_PUBLIC_API_URL` to your deployed backend URL.
- **Backend → Render**: deploy the `backend` folder as a Web Service, set all backend env vars, and set `CLIENT_URL` to your deployed frontend URL.
- **Database → MongoDB Atlas**: create a free cluster and use its connection string as `MONGO_URI`.

## 📡 API Overview

| Area | Base path |
|---|---|
| Auth | `/api/auth` |
| Papers | `/api/papers` |
| AI (summaries, formulas, diagrams, translation) | `/api/ai` |
| Flashcards | `/api/flashcards` |
| Quizzes | `/api/quizzes` |
| Mind Maps | `/api/mindmap` |
| Bookmarks | `/api/bookmarks` |
| Analytics | `/api/analytics` |
| Admin | `/api/admin` |

Health check: `GET /api/health`

## 🧭 Notes on AI & Mock Mode

Every AI-backed endpoint (summaries, flashcards, quizzes, mind maps, formula/diagram explanations, translation) automatically falls back to a deterministic mock response if `GEMINI_API_KEY` is unset or a live call fails — so the full app is demoable and testable without any external API key. Add a real key to unlock live Gemini-generated content.

## 🔭 Future Improvements

- PDF/Word export for summaries, flashcards, and quizzes (currently plain-text export)
- Real-time collaborative study rooms
- Spaced-repetition scheduling for flashcards
- OCR support for scanned PDFs
- Email delivery for password reset tokens

## 📄 License

MIT
