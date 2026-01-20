# 🚀 JoinUp - Community Events Platform

> A modern community events app with QR code social connectivity and affordable subscriptions.

[![CI/CD](https://github.com/yourusername/joinup-app/workflows/CI/CD/badge.svg)](https://github.com/yourusername/joinup-app/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

![JoinUp App Preview](docs/assets/preview.png)

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Environment Variables](#-environment-variables)
- [Database Setup](#-database-setup)
- [API Documentation](#-api-documentation)
- [Deployment](#-deployment)
- [Testing](#-testing)
- [Contributing](#-contributing)
- [Troubleshooting](#-troubleshooting)
- [Roadmap](#-roadmap)
- [License](#-license)

## ✨ Features

### Core Features
- 🎫 **Event Discovery** - Browse, search, and filter local events
- 📱 **QR Code Profiles** - Share all social links with one scan
- 💳 **Ticket Sales** - Integrated Stripe payments with 2% platform fee
- 💬 **Real-time Chat** - Event group chats and direct messaging
- 🔔 **Push Notifications** - Event reminders and updates
- 🗺️ **Map View** - See events on an interactive map
- ⭐ **Reviews & Ratings** - Rate events after attending

### Social Features
- 🔗 **Multi-Platform Linking** - Connect Instagram, Twitter, TikTok, LinkedIn
- 👥 **Follow System** - Follow hosts and get notified of new events
- 📸 **Photo Sharing** - Upload and share event photos
- 🤝 **People Discovery** - Find people with mutual interests

### Subscription Tiers
| Free | Connect ($2.99/mo) | Creator ($6.99/mo) |
|------|-------------------|-------------------|
| 3 events/month | Unlimited events | Everything in Connect |
| Basic profile | QR code profile | Host unlimited events |
| | 3 social links | Unlimited social links |
| | | Analytics dashboard |
| | | Ticket sales (2% fee) |

## 🛠 Tech Stack

### Mobile App (Expo/React Native)
- **Framework:** Expo SDK 50+
- **Language:** TypeScript
- **State Management:** Zustand
- **Navigation:** Expo Router
- **UI Components:** React Native Paper + Custom
- **Forms:** React Hook Form + Zod

### Backend API (Node.js)
- **Runtime:** Node.js 20 LTS
- **Framework:** Express.js + TypeScript
- **Database:** PostgreSQL 15
- **ORM:** Prisma
- **Cache:** Redis
- **Queue:** BullMQ
- **Auth:** JWT + Passport.js

### Infrastructure
- **Hosting:** Railway / Render / AWS
- **Database:** Supabase / Railway PostgreSQL
- **Storage:** AWS S3 / Cloudflare R2
- **CDN:** Cloudflare
- **Monitoring:** Sentry
- **Analytics:** PostHog

### Third-Party Services
- **Payments:** Stripe Connect
- **Push Notifications:** Expo Notifications
- **Email:** Resend
- **SMS:** Twilio (optional)
- **Maps:** Mapbox / Google Maps

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    MOBILE APP (Expo)                            │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐          │
│  │  Screens │ │Components│ │  Hooks   │ │  Store   │          │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘          │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼ HTTPS
┌─────────────────────────────────────────────────────────────────┐
│                 API GATEWAY / LOAD BALANCER                     │
│              (Rate Limiting, SSL Termination)                   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                    BACKEND API (Node.js)                        │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐          │
│  │  Routes  │ │Controllers│ │ Services │ │  Models  │          │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘          │
│                                                                 │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐                       │
│  │   Auth   │ │ Payments │ │WebSockets│                       │
│  │Middleware│ │ (Stripe) │ │(Socket.io)│                       │
│  └──────────┘ └──────────┘ └──────────┘                       │
└─────────────────────────────────────────────────────────────────┘
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   PostgreSQL    │ │     Redis       │ │   Job Queue     │
│   (Primary DB)  │ │ (Cache/Sessions)│ │   (BullMQ)      │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

## 🚀 Getting Started

### Prerequisites

- **Node.js** 20+ ([Download](https://nodejs.org/))
- **pnpm** 8+ (`npm install -g pnpm`)
- **Docker** & Docker Compose ([Download](https://docker.com/))
- **Expo CLI** (`npm install -g expo-cli`)
- **iOS Simulator** (Mac only) or **Android Studio**

### Quick Start (Development)

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/joinup-app.git
cd joinup-app

# 2. Install dependencies
pnpm install

# 3. Set up environment variables
cp .env.example .env.local
# Edit .env.local with your values (see Environment Variables section)

# 4. Start infrastructure (PostgreSQL, Redis)
docker-compose up -d

# 5. Set up database
pnpm db:migrate
pnpm db:seed

# 6. Start development servers
pnpm dev
```

This starts:
- 📱 Mobile app: Expo DevTools (scan QR with Expo Go)
- 🖥️ Backend API: http://localhost:3001
- 📊 Prisma Studio: http://localhost:5555

### First-Time Setup Checklist

- [ ] Clone repository
- [ ] Install dependencies (`pnpm install`)
- [ ] Copy `.env.example` to `.env.local`
- [ ] Set up [Stripe account](https://stripe.com) and add keys
- [ ] Set up [Supabase](https://supabase.com) or local PostgreSQL
- [ ] Set up [Resend](https://resend.com) for emails
- [ ] Run database migrations
- [ ] Start development servers

## 📁 Project Structure

```
joinup-app/
├── .github/                    # GitHub configuration
│   ├── workflows/              # CI/CD pipelines
│   │   ├── ci.yml             # Continuous Integration
│   │   ├── deploy-api.yml     # Backend deployment
│   │   ├── deploy-mobile.yml  # Mobile app deployment
│   │   └── codeql.yml         # Security scanning
│   ├── ISSUE_TEMPLATE/        # Issue templates
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── dependabot.yml         # Dependency updates
│
├── apps/                       # Application code
│   ├── mobile/                # Expo React Native app
│   │   ├── app/               # Expo Router screens
│   │   ├── components/        # Reusable components
│   │   ├── hooks/             # Custom React hooks
│   │   ├── lib/               # Utilities & API client
│   │   ├── store/             # Zustand state management
│   │   ├── types/             # TypeScript types
│   │   ├── assets/            # Images, fonts
│   │   ├── app.json           # Expo configuration
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   └── api/                   # Node.js backend
│       ├── src/
│       │   ├── routes/        # API route definitions
│       │   ├── controllers/   # Request handlers
│       │   ├── services/      # Business logic
│       │   ├── models/        # Prisma client extensions
│       │   ├── middleware/    # Express middleware
│       │   ├── validators/    # Zod schemas
│       │   ├── utils/         # Helper functions
│       │   ├── config/        # Configuration
│       │   ├── jobs/          # Background job processors
│       │   ├── websocket/     # Socket.io handlers
│       │   └── index.ts       # Entry point
│       ├── prisma/
│       │   ├── schema.prisma  # Database schema
│       │   ├── migrations/    # Database migrations
│       │   └── seed.ts        # Seed data
│       ├── tests/             # API tests
│       ├── package.json
│       └── tsconfig.json
│
├── packages/                   # Shared packages
│   ├── shared/                # Shared types & utilities
│   │   ├── src/
│   │   │   ├── types/         # Shared TypeScript types
│   │   │   ├── constants/     # Shared constants
│   │   │   └── utils/         # Shared utilities
│   │   └── package.json
│   │
│   ├── eslint-config/         # Shared ESLint config
│   └── tsconfig/              # Shared TypeScript config
│
├── docs/                       # Documentation
│   ├── API.md                 # API documentation
│   ├── DEPLOYMENT.md          # Deployment guide
│   ├── ARCHITECTURE.md        # Architecture details
│   ├── CONTRIBUTING.md        # Contribution guide
│   └── assets/                # Documentation images
│
├── scripts/                    # Utility scripts
│   ├── setup.sh               # Initial setup script
│   ├── generate-keys.sh       # Generate secure keys
│   └── backup-db.sh           # Database backup script
│
├── docker/                     # Docker configurations
│   ├── api.Dockerfile         # Backend Dockerfile
│   └── nginx.conf             # Nginx configuration
│
├── .env.example               # Environment variables template
├── .gitignore                 # Git ignore rules
├── .prettierrc                # Prettier configuration
├── docker-compose.yml         # Local development services
├── package.json               # Root package.json (workspaces)
├── pnpm-workspace.yaml        # pnpm workspace config
├── turbo.json                 # Turborepo configuration
└── README.md                  # This file
```

## 🔐 Environment Variables

### Backend API (`apps/api/.env`)

```bash
# ===========================================
# APPLICATION
# ===========================================
NODE_ENV=development
PORT=3001
API_URL=http://localhost:3001
APP_URL=http://localhost:8081
APP_NAME=JoinUp

# ===========================================
# DATABASE
# ===========================================
DATABASE_URL="postgresql://postgres:password@localhost:5432/joinup_dev?schema=public"

# ===========================================
# REDIS
# ===========================================
REDIS_URL="redis://localhost:6379"

# ===========================================
# AUTHENTICATION
# ===========================================
# Generate with: openssl rand -base64 64
JWT_ACCESS_SECRET="your-super-secret-access-key-min-32-chars"
JWT_REFRESH_SECRET="your-super-secret-refresh-key-min-32-chars"
JWT_ACCESS_EXPIRES_IN="15m"
JWT_REFRESH_EXPIRES_IN="7d"

# ===========================================
# ENCRYPTION
# ===========================================
# Generate with: openssl rand -hex 32
ENCRYPTION_KEY="your-32-byte-hex-encryption-key"

# ===========================================
# STRIPE
# ===========================================
STRIPE_SECRET_KEY="sk_test_..."
STRIPE_WEBHOOK_SECRET="whsec_..."
STRIPE_CONNECT_CLIENT_ID="ca_..."

# Subscription Price IDs (create in Stripe Dashboard)
STRIPE_PRICE_CONNECT_MONTHLY="price_..."
STRIPE_PRICE_CREATOR_MONTHLY="price_..."

# ===========================================
# OAUTH - INSTAGRAM
# ===========================================
INSTAGRAM_CLIENT_ID=""
INSTAGRAM_CLIENT_SECRET=""
INSTAGRAM_REDIRECT_URI="http://localhost:3001/api/auth/instagram/callback"

# ===========================================
# OAUTH - TWITTER
# ===========================================
TWITTER_CLIENT_ID=""
TWITTER_CLIENT_SECRET=""
TWITTER_REDIRECT_URI="http://localhost:3001/api/auth/twitter/callback"

# ===========================================
# OAUTH - TIKTOK
# ===========================================
TIKTOK_CLIENT_KEY=""
TIKTOK_CLIENT_SECRET=""
TIKTOK_REDIRECT_URI="http://localhost:3001/api/auth/tiktok/callback"

# ===========================================
# OAUTH - LINKEDIN
# ===========================================
LINKEDIN_CLIENT_ID=""
LINKEDIN_CLIENT_SECRET=""
LINKEDIN_REDIRECT_URI="http://localhost:3001/api/auth/linkedin/callback"

# ===========================================
# EMAIL (Resend)
# ===========================================
RESEND_API_KEY="re_..."
EMAIL_FROM="JoinUp <hello@yourdomain.com>"

# ===========================================
# FILE STORAGE (S3/R2)
# ===========================================
S3_BUCKET="nexus-uploads"
S3_REGION="us-east-1"
S3_ACCESS_KEY_ID=""
S3_SECRET_ACCESS_KEY=""
S3_ENDPOINT="" # For Cloudflare R2

# ===========================================
# PUSH NOTIFICATIONS (Expo)
# ===========================================
EXPO_ACCESS_TOKEN=""

# ===========================================
# MONITORING
# ===========================================
SENTRY_DSN=""

# ===========================================
# MAPS
# ===========================================
MAPBOX_ACCESS_TOKEN=""
```

### Mobile App (`apps/mobile/.env`)

```bash
# API Configuration
EXPO_PUBLIC_API_URL=http://localhost:3001
EXPO_PUBLIC_WS_URL=ws://localhost:3001

# Stripe (Publishable Key)
EXPO_PUBLIC_STRIPE_PUBLISHABLE_KEY="pk_test_..."

# Maps
EXPO_PUBLIC_MAPBOX_ACCESS_TOKEN=""

# Sentry
EXPO_PUBLIC_SENTRY_DSN=""
```

### Generating Secure Keys

```bash
# Run this script to generate all required secrets
./scripts/generate-keys.sh

# Or manually:
# JWT Secrets (64 bytes base64)
openssl rand -base64 64

# Encryption Key (32 bytes hex)
openssl rand -hex 32
```

## 🗄 Database Setup

### Option 1: Local Docker (Development)

```bash
# Start PostgreSQL and Redis
docker-compose up -d

# Run migrations
pnpm db:migrate

# Seed sample data
pnpm db:seed

# Open Prisma Studio (GUI)
pnpm db:studio
```

### Option 2: Supabase (Production)

1. Create project at [supabase.com](https://supabase.com)
2. Copy connection string to `DATABASE_URL`
3. Run migrations: `pnpm db:migrate:deploy`

### Database Commands

```bash
# Development
pnpm db:migrate        # Create and apply migrations
pnpm db:seed          # Seed database with sample data
pnpm db:studio        # Open Prisma Studio GUI
pnpm db:reset         # Reset database (WARNING: deletes all data)

# Production
pnpm db:migrate:deploy # Apply migrations without prompts
pnpm db:generate      # Generate Prisma client
```

## 📚 API Documentation

Full API documentation available at `/api/docs` when running the server.

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login user |
| POST | `/api/auth/logout` | Logout user |
| POST | `/api/auth/refresh` | Refresh access token |
| POST | `/api/auth/forgot-password` | Request password reset |
| POST | `/api/auth/reset-password` | Reset password |
| GET | `/api/auth/me` | Get current user |

### Events Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/events` | List events (paginated) |
| GET | `/api/events/:id` | Get event details |
| POST | `/api/events` | Create event |
| PUT | `/api/events/:id` | Update event |
| DELETE | `/api/events/:id` | Delete event |
| POST | `/api/events/:id/join` | Join event |
| POST | `/api/events/:id/leave` | Leave event |
| GET | `/api/events/:id/attendees` | List attendees |

### Users Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/users/:id` | Get user profile |
| PUT | `/api/users/:id` | Update profile |
| POST | `/api/users/:id/follow` | Follow user |
| DELETE | `/api/users/:id/follow` | Unfollow user |
| GET | `/api/users/:id/followers` | Get followers |
| GET | `/api/users/:id/following` | Get following |

### Payments Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/payments/checkout` | Create checkout session |
| POST | `/api/payments/subscription` | Create subscription |
| DELETE | `/api/payments/subscription` | Cancel subscription |
| POST | `/api/payments/webhook` | Stripe webhook |

See [docs/API.md](docs/API.md) for complete documentation.

## 🚢 Deployment

### Backend Deployment (Railway)

1. **Connect Repository**
   - Go to [railway.app](https://railway.app)
   - Create new project from GitHub repo
   - Select `apps/api` as root directory

2. **Add Services**
   - PostgreSQL database
   - Redis

3. **Set Environment Variables**
   - Copy all variables from `.env.example`
   - Set production values

4. **Deploy**
   - Railway auto-deploys on push to `main`

### Mobile Deployment (EAS)

```bash
# Install EAS CLI
npm install -g eas-cli

# Login to Expo
eas login

# Configure project
eas build:configure

# Build for stores
eas build --platform ios
eas build --platform android

# Submit to stores
eas submit --platform ios
eas submit --platform android
```

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed guide.

## 🧪 Testing

```bash
# Run all tests
pnpm test

# Run with coverage
pnpm test:coverage

# Run specific package tests
pnpm --filter api test
pnpm --filter mobile test

# E2E tests
pnpm test:e2e
```

### Test Structure

```
tests/
├── unit/           # Unit tests
├── integration/    # Integration tests
├── e2e/           # End-to-end tests
└── fixtures/      # Test data
```

## 🤝 Contributing

See [CONTRIBUTING.md](docs/CONTRIBUTING.md) for guidelines.

### Development Workflow

1. Create feature branch: `git checkout -b feature/my-feature`
2. Make changes
3. Run tests: `pnpm test`
4. Run linting: `pnpm lint`
5. Commit with conventional commits: `git commit -m "feat: add feature"`
6. Push and create PR

### Commit Convention

```
feat: add new feature
fix: bug fix
docs: documentation changes
style: formatting, missing semicolons, etc
refactor: code refactoring
test: adding tests
chore: maintenance tasks
```

## 🔧 Troubleshooting

### Common Issues

<details>
<summary><strong>Database connection failed</strong></summary>

```bash
# Check if Docker is running
docker ps

# Restart containers
docker-compose down && docker-compose up -d

# Check logs
docker-compose logs db
```
</details>

<details>
<summary><strong>Prisma client out of sync</strong></summary>

```bash
# Regenerate Prisma client
pnpm db:generate

# If still failing, reset
pnpm db:reset
```
</details>

<details>
<summary><strong>Expo build failing</strong></summary>

```bash
# Clear cache
expo start -c

# Delete node_modules and reinstall
rm -rf node_modules
pnpm install
```
</details>

<details>
<summary><strong>Stripe webhook not working locally</strong></summary>

```bash
# Install Stripe CLI
brew install stripe/stripe-cli/stripe

# Forward webhooks
stripe listen --forward-to localhost:3001/api/payments/webhook
```
</details>

## 🗺 Roadmap

### Phase 1: MVP (Current)
- [x] User authentication
- [x] Event CRUD
- [x] QR code profiles
- [x] Basic payments
- [ ] Push notifications
- [ ] Real-time chat

### Phase 2: Growth
- [ ] Event recommendations (ML)
- [ ] Advanced analytics
- [ ] Affiliate program
- [ ] Event series/recurring events
- [ ] Waitlist management

### Phase 3: Scale
- [ ] Multi-language support
- [ ] White-label solution
- [ ] API for third-party integrations
- [ ] Advanced fraud detection

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.

## 🙏 Acknowledgments

- [Expo](https://expo.dev) for the amazing React Native framework
- [Stripe](https://stripe.com) for payment infrastructure
- [Prisma](https://prisma.io) for the excellent ORM
- All open-source contributors

---

<p align="center">
  Made with ❤️ by Solo Developer
</p>

<p align="center">
  <a href="https://twitter.com/yourusername">Twitter</a> •
  <a href="https://discord.gg/yourserver">Discord</a> •
  <a href="https://joinup-app.com">Website</a>
</p>
