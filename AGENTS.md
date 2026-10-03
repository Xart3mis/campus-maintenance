# AGENTS.md — Campus Maintenance

## Project

- Backend: NestJS + Mongoose in `apps/api`
- Frontend: Next.js App Router + shadcn/ui in `apps/web`
- Database: MongoDB Atlas; API documentation: Swagger/OpenAPI
- Read `specs/campus-maintenance.md` before changing behavior.

## Engineering rules

- Keep MVC boundaries clear: controllers handle HTTP, services handle business logic, schemas handle persistence, and DTOs validate input.
- The frontend must call the API; it must never access MongoDB directly.
- Validate and sanitize all external input. Reject unknown DTO properties.
- Preserve the API contract: requests contain `title`, `description`, `location`, and a supported `category`; status is backend-controlled.
- Prefer existing utilities and `components/ui`; avoid unnecessary dependencies and out-of-scope features.
- Use precise types. Avoid `any` unless unavoidable and documented.
- Add or update focused tests for behavior changes and keep Swagger and generated API types current.
- Never expose or modify `.env` files, credentials, tokens, API keys, or connection strings.

## Verification

Run the smallest relevant checks, then review the diff:

```bash
cd apps/api && npm test && npm run lint
cd apps/web && npm run lint
npm run format:check
```

After API changes, refresh `apps/web/lib/api-types.ts` from the local Swagger endpoint:

```bash
npx openapi-typescript http://localhost:3001/api-json -o apps/web/lib/api-types.ts
```
