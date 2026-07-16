# astro-supabase-auth-template

Minimal **Astro + Vue + Supabase Auth** starter from [@open-templates](https://github.com/open-templates). Pairs with [cf-hono-supabase-api-template](https://github.com/open-templates/cf-hono-supabase-api-template).

The UI is a **client-only Vue SPA** (`vue-router`) mounted from `src/pages/index.astro` via `client:only="vue"`.

## Quick start

1. **Use this template** on GitHub, then clone your repo.
2. Personalize from `templates/`:

```bash
./scripts/init-from-template.sh
```

3. Install and run:

```bash
bun install
cp .env.example .env
bun run dev
```

See [`templates/ABOUT_TEMPLATES.md`](templates/ABOUT_TEMPLATES.md) and [`docs/INIT_TEMPLATE.md`](docs/INIT_TEMPLATE.md).

## Out-of-the-box features

| Feature | Description |
|---------|-------------|
| Google OAuth | Sign in / sign up via Supabase `signInWithOAuth({ provider: 'google' })` |
| Email auth | Login, signup, password recovery and reset |
| API health indicator | Header polls `GET /health` every 30s |
| Protected home page | Calls `GET /me` with the Supabase JWT |

See [`index.md`](index.md) for routes, API contracts, and extension notes.

Agent docs: [INSTRUCTIONS.md](INSTRUCTIONS.md) · [.agents/skills/](.agents/skills/)

## Stack

- Astro 7, Vue 3, TypeScript, vue-router
- Supabase Auth (`@supabase/supabase-js`)
- Tailwind CSS 4 (`@tailwindcss/vite`)
- Bun (package manager); **Node.js ≥ 22.12** (required by Astro 7)

```bash
bun install
cp .env.example .env
# set VITE_SUPABASE_URL, VITE_SUPABASE_PUBLISHABLE_KEY, VITE_API_BASE_URL
bun run dev
```

Start the API worker first ([cf-hono-supabase-api-template](https://github.com/open-templates/cf-hono-supabase-api-template) on port `8787`) so health and `/me` work locally.

Supabase + Google OAuth setup: [`docs/SUPABASE_SETUP.md`](docs/SUPABASE_SETUP.md)

## Environment variables

| Variable | Required | Purpose |
|----------|----------|---------|
| `VITE_SUPABASE_URL` | Yes | Supabase project URL |
| `VITE_SUPABASE_PUBLISHABLE_KEY` | Yes | Supabase anon/publishable key |
| `VITE_API_BASE_URL` | No | Worker URL (default `http://localhost:8787`) |

## Scripts

- `bun run dev` — Astro dev server
- `bun run build` / `bun run ci` — production build
- `bun run lint` / `bun run typecheck` — quality checks

## Deployment

Target: **Cloudflare Pages**. Build command `bun run build`, output directory `dist`. Set the same `VITE_*` variables in the Pages project settings. `public/_redirects` sends all paths to `index.html` for vue-router history mode.

Maintained by [xarlizard](https://github.com/jane).

## License

MIT
