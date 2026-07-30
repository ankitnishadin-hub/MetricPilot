# MetricPilot

MetricPilot is an AI-powered client report automation platform for Indian digital marketing agencies and freelancers. It connects advertising and analytics accounts, normalizes campaign metrics, generates a plain-English narrative with Gemini, produces an agency-branded PDF, and supports WhatsApp delivery.

## Repository

- `apps/client` — React 18 + Vite frontend
- `apps/server` — Express + Prisma backend
- `packages/shared` — shared TypeScript types and constants

## Local verification

Requirements: Node.js 20, npm 10, Docker, and Docker Compose.

```bash
npm install --no-audit --no-fund --workspaces --include-workspace-root
docker compose -f docker-compose.test.yml up -d --wait
npm run prisma:generate
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/metricpilot_test \
DIRECT_URL=postgresql://postgres:postgres@localhost:5432/metricpilot_test \
npx prisma migrate deploy --schema apps/server/prisma/schema.prisma
npm run typecheck
npm run lint
npm run test
npm run build
docker compose -f docker-compose.test.yml down --volumes
```

The same sequence is available as:

```bash
./scripts/verify-release.sh
```

## Configuration

Copy `.env.example` to a local environment file and provide real credentials only through local secrets or hosting dashboards. Never commit production secrets.

See `docs/EXTERNAL_SERVICES.md`, `docs/POST_LAUNCH_CHECKLIST.md`, and `SECURITY.md` for deployment and operational requirements.
