# STAFFR

A hiring and project management platform that integrates with Slack for team collaboration and application tracking.

## Overview

STAFFR is a full-stack web application consisting of:
- **Frontend (STAFFR-f)**: A Next.js application for managing projects, roles, and applications
- **Backend (STAFFR-b)**: A NestJS API with Slack OAuth authentication, WebSocket support, and PostgreSQL database

## Tech Stack

| Component | Technology |
|-----------|------------|
| Frontend | Next.js 16, React 19, TypeScript, TailwindCSS |
| Backend | NestJS, TypeScript, Prisma, PostgreSQL |
| Auth | Slack OAuth 2.0 with JWT tokens |
| Real-time | Socket.IO |
| Deployment | Railway (backend), Vercel (frontend recommended) |

## Prerequisites

- Node.js 18+
- pnpm (recommended) or npm
- PostgreSQL database
- Redis instance (for queues)
- Slack app credentials

## Environment Variables

### Backend (.env in STAFFR-b/)

```bash
DATABASE_URL=postgresql://...
REDIS_URL=redis://...
JWT_SECRET=...
REFRESH_TOKEN_SECRET=...
SLACK_CLIENT_ID=...
SLACK_CLIENT_SECRET=...
SLACK_SIGNING_SECRET=...
SLACK_BOT_TOKEN=...
APP_URL=http://localhost:3000
API_URL=http://localhost:4000
```

### Frontend (.env.local in STAFFR-f/)

```bash
NEXT_PUBLIC_API_URL=http://localhost:4000
```

## Running the Application

### 1. Start the Backend

The backend uses NestJS and requires a PostgreSQL database and Redis.

```bash
cd STAFFR-b

# Install dependencies
pnpm install

# Generate Prisma client
pnpm prisma:generate

# Run database migrations
pnpm prisma:migrate

# Start development server (watch mode)
pnpm dev
```

The backend will be available at `http://localhost:4000`.

For production deployment on Railway, the build command is `pnpm build` and start command is `pnpm start`.

### 2. Start the Frontend

The frontend uses Next.js 16.

```bash
cd STAFFR-f

# Install dependencies
pnpm install

# Start development server
pnpm dev
```

The frontend will be available at `http://localhost:3000`.

### 3. Access the Application

1. Open `http://localhost:3000` in your browser
2. Click "Sign in with Slack" to authenticate
3. You'll be redirected to Slack OAuth (ensure your Slack app is configured correctly)
4. After successful authentication, you'll be redirected to the dashboard

## Project Structure

```
CFT/
├── STAFFR-b/          # Backend (NestJS API)
│   ├── src/
│   │   ├── auth/      # Slack OAuth and JWT authentication
│   │   ├── users/     # User management
│   │   ├── projects/  # Project CRUD operations
│   │   ├── applications/ # Application management
│   │   ├── slack/     # Slack integration
│   │   ├── reports/   # Hiring analytics
│   │   ├── gateway/   # WebSocket gateway
│   │   └── prisma/    # Database client
│   ├── prisma/        # Database schema and migrations
│   ├── package.json
│   └── railway.toml   # Railway deployment config
│
└── STAFFR-f/          # Frontend (Next.js)
    ├── app/           # App router pages
    │   ├── (dashboard)/ # Protected dashboard routes
    │   └── (auth)/    # Authentication pages
    ├── components/    # UI components
    ├── hooks/         # React hooks
    ├── lib/           # API client and utilities
    └── package.json
```

## Available Scripts

### Backend (STAFFR-b)

| Script | Description |
|--------|-------------|
| `pnpm dev` | Start dev server with watch mode |
| `pnpm build` | Build the application |
| `pnpm start` | Start production server |
| `pnpm prisma:generate` | Generate Prisma client |
| `pnpm prisma:migrate` | Run migrations |
| `pnpm prisma:seed` | Seed database |
| `pnpm lint` | Run ESLint |
| `pnpm test` | Run tests |

### Frontend (STAFFR-f)

| Script | Description |
|--------|-------------|
| `pnpm dev` | Start Next.js dev server |
| `pnpm build` | Build for production |
| `pnpm start` | Start production server |

## Features

- **Slack OAuth Authentication**: Users sign in with their Slack workspace accounts
- **Role-based Access**: SUPER_ADMIN, ADMIN, PROJECT_MANAGER, TEAM_MEMBER roles
- **Project Management**: Create and manage hiring projects with multiple roles
- **Application Tracking**: Review and manage candidate applications through hiring funnel
- **Real-time Updates**: WebSocket support for live notifications
- **Reporting**: Hiring funnel analytics, fill rates, and time-to-hire metrics
- **Slack Integration**: Post announcements and collect applications directly in Slack