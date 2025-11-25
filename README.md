# Anki Chinese MVP

**Study Chinese with AI-generated flashcards.**

A full-stack web application for learning Chinese with intelligent flashcard generation powered by OpenAI's API.

Built with **Next.js 16** (App Router), **Convex** (serverless backend), **Clerk** (authentication), and **React 19**.

---

## 🚀 Quick Start

### Prerequisites
- Node.js 18+
- npm 9+

### Setup (5 minutes)

```bash
# 1. Install dependencies
npm install

# 2. Start Convex backend (Terminal 1)
npx convex dev

# 3. Start Next.js frontend (Terminal 2)
npm run dev

# 4. Visit http://localhost:3000
```

**Important**: See documentation below for real Clerk credentials and OpenAI API setup.

---

## 📚 Documentation

### Getting Started

| Document | Purpose | Time |
|----------|---------|------|
| **[ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md)** | Complete setup guide with troubleshooting | 15 min |
| **[SETUP_COMPLETE.md](./SETUP_COMPLETE.md)** | Confirms environment is configured | 2 min |

### Credentials & Configuration

| Document | Purpose | Time |
|----------|---------|------|
| **[CLERK_SETUP_GUIDE.md](./CLERK_SETUP_GUIDE.md)** | Get real Clerk authentication keys | 15 min |
| **[OPENAI_SETUP_GUIDE.md](./OPENAI_SETUP_GUIDE.md)** | Configure OpenAI for card generation | 7 min |

### Architecture & Development

| Document | Purpose |
|----------|---------|
| **[CLAUDE.md](./CLAUDE.md)** | Architecture overview, API reference, code patterns |
| **[DEV.md](./DEV.md)** | Detailed development guide and workflows |
| **[PROD.md](./PROD.md)** | Deployment instructions for Cloudflare Pages |

### Analysis & Strategy

| Document | Purpose |
|----------|---------|
| **[ARCHITECTURE_REVIEW.md](./ARCHITECTURE_REVIEW.md)** | Professional tech stack assessment + Vercel migration recommendation |
| **[AUDIT.md](./AUDIT.md)** | Security audit, dependency analysis, quality metrics |
| **[MIGRATION_TO_VERCEL.md](./MIGRATION_TO_VERCEL.md)** | Step-by-step migration from Cloudflare to Vercel |

---

## 🛠 Tech Stack

### Frontend
- **Next.js 16** (App Router)
- **React 19** with TypeScript 5.9
- **TailwindCSS** (styling)
- **React Hook Form + Zod** (validation)
- **Zustand** (state management)
- **nuqs** (URL-based state)

### Backend
- **Convex 1.29+** (serverless database + functions)
- **OpenAI gpt-4o-mini** (card generation)
- **Upstash Redis** (rate limiting)

### Auth & Hosting
- **Clerk** (authentication)
- **Cloudflare Pages** (current)
- **Vercel** (recommended - see ARCHITECTURE_REVIEW.md)

---

## 📋 Features

✅ **User Authentication** - Email/password and OAuth via Clerk
✅ **Folder Management** - Create and organize card collections
✅ **AI Card Generation** - Generate flashcards from Chinese words using OpenAI
✅ **Full-Text Search** - Search cards by word or translation
✅ **Card Editing** - Modify, delete, or move cards between folders
✅ **Rate Limiting** - 5 cards/minute, 20 cards/day per user

---

## 🚦 Current Status

### ✅ Ready to Run
- Code is complete and tested
- All dependencies installed
- Development environment configured
- Documentation comprehensive

### ⚠️ Next Steps
1. **Get Clerk credentials** (15 min) → Follow [CLERK_SETUP_GUIDE.md](./CLERK_SETUP_GUIDE.md)
2. **Set OpenAI key** (7 min, optional) → Follow [OPENAI_SETUP_GUIDE.md](./OPENAI_SETUP_GUIDE.md)
3. **Run dev server** → Follow [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md)

---

## 📖 Common Commands

```bash
# Development
npx convex dev              # Start Convex backend
npm run dev                 # Start Next.js dev server
npm run type-check          # Check TypeScript
npm run lint                # Run ESLint

# Testing
npx playwright test         # Run E2E tests
npx playwright show-report  # View test report

# Production
npm run build               # Build for production
npm start                   # Run production server

# Convex Environment Variables
npx convex env list        # List Convex env vars
npx convex env set KEY VAL # Set Convex env var
```

---

## 🔧 Environment Variables

### Development (.env.local)

**Required:**
```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...
CLERK_JWT_ISSUER_DOMAIN=https://your-account-id.clerk.accounts.dev
NEXT_PUBLIC_CONVEX_URL=http://localhost:8000
CONVEX_DEPLOYMENT=dev:your-project-id
```

**Optional (via Convex CLI):**
```bash
npx convex env set OPENAI_API_KEY sk-proj-...
```

**Getting these values:**
- Clerk keys → [CLERK_SETUP_GUIDE.md](./CLERK_SETUP_GUIDE.md)
- OpenAI key → [OPENAI_SETUP_GUIDE.md](./OPENAI_SETUP_GUIDE.md)

---

## 🏗️ Architecture

### Data Model
- **Folders** - User collections for organizing cards
- **Cards** - Flashcards with Chinese word, translation, and character breakdown
- All data scoped to authenticated user

### Auth Flow
1. User signs in via Clerk
2. Clerk validates identity and issues JWT
3. Convex verifies JWT and grants data access
4. All Convex functions verify user before returning data

### Generation Pipeline
1. User submits Chinese word
2. Frontend validates with Zod
3. Convex backend checks rate limits (5/min, 20/day)
4. OpenAI API generates card with structured JSON
5. Zod validates response
6. Card saved to Convex database
7. UI updates in real-time

---

## 🚀 Deployment

### Current: Cloudflare Pages + Convex
- See [PROD.md](./PROD.md) for Cloudflare Pages deployment
- Set environment variables in Cloudflare dashboard

### Recommended: Vercel + Convex
- See [MIGRATION_TO_VERCEL.md](./MIGRATION_TO_VERCEL.md) for step-by-step migration
- Read [ARCHITECTURE_REVIEW.md](./ARCHITECTURE_REVIEW.md) for why Vercel is superior for this stack
- Migration takes ~2 hours with zero code changes

---

## 🔐 Security

- ✅ All Convex functions require authentication
- ✅ User data fully isolated by userId
- ✅ No SQL injection or XSS vulnerabilities
- ✅ Environment variables never exposed to client
- ✅ Rate limiting prevents abuse
- ✅ TypeScript strict mode enabled
- See [AUDIT.md](./AUDIT.md) for detailed security report

---

## 📊 Code Quality

- **Type Safety**: Full TypeScript, strict mode
- **Formatting**: Prettier
- **Linting**: ESLint
- **Testing**: Playwright E2E tests
- **Validation**: Zod schemas on client and server

See [AUDIT.md](./AUDIT.md) for detailed quality metrics.

---

## 🆘 Troubleshooting

### Clerk Error: "Publishable key not valid"
→ See [CLERK_SETUP_GUIDE.md](./CLERK_SETUP_GUIDE.md#troubleshooting)

### OpenAI Error: "SERVER_MISCONFIGURED"
→ See [OPENAI_SETUP_GUIDE.md](./OPENAI_SETUP_GUIDE.md#troubleshooting)

### Dev server won't start
→ See [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md#common-issues--solutions)

### Types not found: "@/convex/_generated/api"
→ See [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md#issue-cannot-find-module-convex_generatedapi)

---

## 📞 Support

- **Architecture questions**: See [CLAUDE.md](./CLAUDE.md)
- **Setup issues**: See [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md)
- **Deployment**: See [MIGRATION_TO_VERCEL.md](./MIGRATION_TO_VERCEL.md) or [PROD.md](./PROD.md)
- **Security details**: See [AUDIT.md](./AUDIT.md)

---

## 📈 Next Steps

1. ✅ Read this README
2. 🔄 Follow [ENVIRONMENT_SETUP.md](./ENVIRONMENT_SETUP.md)
3. 🔄 Follow [CLERK_SETUP_GUIDE.md](./CLERK_SETUP_GUIDE.md) (15 min)
4. 🔄 Follow [OPENAI_SETUP_GUIDE.md](./OPENAI_SETUP_GUIDE.md) (optional, 7 min)
5. 🚀 Run `npm run dev` and start building!

---

**Status**: ✅ Ready to run. All documentation complete.
