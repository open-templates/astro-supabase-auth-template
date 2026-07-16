---
type: Reference
title: Key files
description: Source map for auth, API, layout, and pages.
tags: [reference, files]
timestamp: 2026-07-15T00:00:00Z
---

# Key files

| Path | Role |
|------|------|
| `src/pages/index.astro` | Astro page shell; mounts Vue SPA |
| `src/vue/main.ts` | Vue app entrypoint (registers vue-router) |
| `src/vue/App.vue` | Root Vue component + auth provider |
| `src/vue/composables/useAuth.ts` | Supabase auth state and methods |
| `src/vue/router/index.ts` | Routes and navigation guards |
| `src/vue/api/api.ts` | Shared `apiFetch` with JWT + retry |
| `src/vue/components/layout/AppHeader.vue` | Global header + health dot |
| `src/vue/views/HomeView.vue` | Authenticated landing page |
