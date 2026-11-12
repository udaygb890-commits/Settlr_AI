# Settlr AI

**AI-Powered Group Expense Management, Intelligent Bill Splitting, and Settlement Platform**

Settlr AI pairs **Google Gemini** conversational & voice intelligence with a **deterministic integer-minor-unit financial engine**, **Supabase PostgreSQL + Row Level Security**, and **server-verified PayPal Sandbox settlements**.

---

## Architecture
- `client/` — React, TypeScript, Vite, Tailwind CSS, Framer Motion, Lucide React, Recharts
- `server/` — Node.js, Express, TypeScript, Zod, `@google/genai`, `@supabase/supabase-js`, PayPal Orders API v2
- `supabase/` — PostgreSQL migrations, RLS policies, atomic RPCs, and local seed data
- `docs/` — Architecture & Capstone (`FINAL_SYSTEM_ARCHITECTURE.md`, `FINAL_TEST_REPORT.md`, `HACKATHON_PROJECT_OVERVIEW.md`, `HACKATHON_DEMO_SCRIPT.md`, `KNOWN_LIMITATIONS.md`), Frontend (`FRONTEND_ARCHITECTURE.md`, `DESIGN_SYSTEM.md`, `ROUTING_AND_NAVIGATION.md`, `FRONTEND_API_INTEGRATION.md`, `RESPONSIVE_DESIGN.md`, `FRONTEND_TESTING.md`), Database, Security, Authentication, Gemini AI Agent, Voice Intelligence (`VOICE_ARCHITECTURE.md`, `AUDIO_PRIVACY.md`, `VOICE_API.md`, `VOICE_TESTING.md`), Financial Engine (`FINANCIAL_ENGINE_ARCHITECTURE.md`, `MONEY_AND_CURRENCY.md`, `EXPENSE_SPLITTING.md`, `BALANCE_CALCULATION.md`, `SETTLEMENT_OPTIMIZATION.md`, `FINANCIAL_LEDGER.md`, `FINANCIAL_API.md`, `FINANCIAL_TESTING.md`), PayPal Sandbox (`PAYPAL_ARCHITECTURE.md`, `PAYPAL_SANDBOX_SETUP.md`, `PAYPAL_ORDER_FLOW.md`, `PAYPAL_CAPTURE_FLOW.md`, `PAYPAL_WEBHOOKS.md`, `PAYMENT_STATE_MACHINE.md`, `PAYMENT_RECONCILIATION.md`, `PAYPAL_SECURITY.md`, `PAYPAL_TESTING.md`), and Deployment documentation

## Quick Start (Local Development)

### 1. Install Dependencies
```bash
npm run install:all
```

### 2. Configure Environment Variables
Copy `.env.example` files and fill in your credentials:
- `server/.env` (from `server/.env.example`):
  - `GEMINI_API_KEY`, `GEMINI_MODEL` (default `gemini-3.5-flash`)
  - `VOICE_MAX_FILE_SIZE_MB` (default `15`), `VOICE_MAX_DURATION_SECONDS` (default `120`), `VOICE_ALLOWED_MIME_TYPES`
  - `SUPABASE_URL`, `SUPABASE_ANON_KEY`, `SUPABASE_SERVICE_ROLE_KEY`
  - `PAYPAL_ENVIRONMENT=sandbox`, `PAYPAL_MODE=sandbox`, `PAYPAL_CLIENT_ID`, `PAYPAL_CLIENT_SECRET`, `PAYPAL_WEBHOOK_ID`, `PAYPAL_RECEIVER_MODE=platform_merchant`
- `client/.env` (from `client/.env.example`):
  - `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, `VITE_PAYPAL_CLIENT_ID`, `VITE_PAYPAL_ENVIRONMENT=sandbox`

### 3. Apply Supabase Migrations
Run migrations `001` through `007` in order in your Supabase SQL Editor:
- `001_initial_schema.sql`
- `002_rls_policies.sql`
- `003_financial_rpc.sql`
- `004_phase2_schema_alignment.sql`
- `005_phase5_financial_ledger.sql`
- `006_phase6_paypal_integration.sql`
- `007_phase8_security_hardening.sql`

See `docs/SUPABASE_SETUP.md` and `docs/PAYPAL_SANDBOX_SETUP.md` for details.

### 4. Demo Data Seed (Development Only)
```bash
npm --prefix server run seed:demo
```

### 5. Run Development Servers
```bash
# Terminal 1 (Backend on http://localhost:4000; health probes at /api/health/live & /api/health/ready)
npm run dev:server

# Terminal 2 (Frontend on http://localhost:5173)
npm run dev:client
```

## Deployment Blueprints
- **Frontend**: `client/vercel.json` (Vercel SPA rewrites, `npm --prefix client run build`).
- **Backend**: `render.yaml` (Render Web Service on Node with `/api/health/ready` health checks).

## Verification & Testing
```bash
npm run typecheck
npm test
npm run build
```

