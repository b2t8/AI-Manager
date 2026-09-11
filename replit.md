# رَصْد — AI Executive Agent

وكيل تنفيذي عربي يحوّل الأوامر الطبيعية إلى خطط واضحة وقرارات قابلة للتنفيذ عبر لوحة قيادة RTL داكنة.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm --filter @workspace/ai-executive-agent run dev` — run the Arabic executive web app
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/ai-executive-agent/src/` — Vite frontend, shared shell, and executive pages
- `artifacts/api-server/src/routes/executive.ts` — dashboard, task CRUD, activity, memory, and agent endpoints
- `lib/api-spec/openapi.yaml` — source of truth for generated API hooks and validation schemas

## Architecture decisions

- The existing Gemini-oriented agent contract is preserved behind `/api/agent/run`; the server uses the saved Gemini key when available and a safe Arabic planning fallback otherwise.
- Executive pages use generated Orval hooks rather than handwritten client fetch calls.
- Device actions are represented as permission-aware executive workflows; the web app does not claim unsupported operating-system control.

## Product

يوفر التطبيق نظرة تنفيذية لليوم، مساحة تفويض للوكيل، إدارة مهام، مواعيد، رحلات، مصروفات، ذاكرة شخصية، وإعدادات للشخصية والأجهزة والخصوصية.

## User preferences

_Populate as you build — explicit user instructions worth remembering across sessions._

## Gotchas

_Populate as you build — sharp edges, "always run X before Y" rules._

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
