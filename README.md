# QueuePulse

Full-stack background job queue manager, priority dispatcher and worker throughput studio built with Vite, React, TypeScript, Tailwind CSS v4 and Vercel Serverless Functions.

## Local development

```bash
npm install
npm run dev
```

For local Vercel Functions use `npx vercel dev`. If the API is unavailable, the frontend falls back to an in-browser demo queue.

## Vercel deployment

Import `kennedy-blip/queuex` into Vercel. Build command: `npm run build`; output directory: `dist`.

## API
- `GET /api/jobs` — jobs, queue depths and state counts
- `POST /api/jobs` — enqueue a job
- `PATCH /api/jobs` — claim, complete, fail or retry a job using `{ id, action }`
- `POST /api/tick` — execute a priority-sorted batch using `{ workerConcurrency, simulateFailureRatePct }`

**Production note:** the API uses process memory for this deterministic demo. Vercel Functions are ephemeral and instances do not share memory, so state is not durable. Replace `api/_store.ts` with Redis/Upstash or Postgres and add authentication, idempotency and a durable worker provider before handling production workloads.
