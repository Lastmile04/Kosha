# Kosha

> Sanskrit for "treasure" or "sheath" — a container of valuable things.

**Status:** 🚧 Planning complete / Early development

A personal learning resource organizer for self-taught developers and lifelong learners. Save, organize, and rediscover articles, YouTube videos, docs, repos, and notes under meaningful topics — without losing the context of *why* you saved them.

---

## The Problem

Self-learners collect resources (videos, articles, docs, repos, PDFs) from many places but lose the context and connections between them over time.

- Resources are scattered across bookmarks, playlists, note apps, and downloads.
- The reason a resource was saved is forgotten.
- There is no single view of everything related to one learning topic.
- Rediscovering old resources requires searching across multiple disconnected tools.

We're not bad at collecting resources — we're bad at maintaining the **relationships** between resources and the topics they contribute to.

## What Kosha Is

Kosha is a **resource-centric** system. A Resource (a link, video, doc, or repo you're learning from) is the core object. Topics exist purely to give that resource meaning and context — they're catalogs, not folders, so the same resource can belong to multiple topics (e.g. Beej's Guide under both "C" and "Networking").

- Save a resource with a URL, title, type, and a short note on *why* it matters.
- Organize resources under one or more topics.
- Browse everything under a topic, or search across all saved resources.
- Track basic status: to learn / in progress / completed.

## What Kosha Is Not (v0.1)

- Not a note-taking app or Notion/Obsidian replacement
- Not a flashcard or spaced-repetition system
- Not an AI learning assistant
- Not a file storage or PDF hosting service
- Not a collaboration or sharing tool

## Tech Stack

| Layer | Choice |
|---|---|
| Frontend | Next.js (App Router) + TypeScript, Tailwind CSS |
| Backend | Node.js (Next.js API routes) |
| Database | PostgreSQL |
| ORM | Prisma |
| Auth | JWT + httpOnly cookies (implemented manually) |
| Deployment | Vercel + Railway/Supabase (Postgres) |

## Documentation

Planning was done old-school — behavior and domain first, implementation second. Full docs live in [`docs/`](./docs):

- [`00-vision.md`](./docs/00-vision.md) — why Kosha exists
- [`01-problem.md`](./docs/01-problem.md) — the problem in depth
- [`02-scope.md`](./docs/02-scope.md) — what's in/out for v0.1
- [`03-domain-model.md`](./docs/03-domain-model.md) — core entities and relationships
- [`04-user-stories.md`](./docs/04-user-stories.md) — user stories for v0.1
- [`05-invariants.md`](./docs/05-invariants.md) — rules the system must never break
- [`06-lifecycle.md`](./docs/06-lifecycle.md) — create/update/delete flows and edge cases
- [`decisions/`](./docs/decisions) — architecture decision records (ADRs)

## Core Domain (short version)

```
User 1 → N Topics
User 1 → N Resources
Resource N ↔ N Topics (via ResourceTopic)
```

A Resource can exist with zero topics. Deleting a Topic never deletes its Resources; deleting a Resource never deletes its Topics.

## Getting Started

```bash
git clone git@github.com:Lastmile04/Kosha.git
cd Kosha
npm install
cp .env.example .env   # fill in DATABASE_URL, JWT_SECRET
npx prisma migrate dev
npm run dev
```

## Roadmap

- [x] Problem definition and domain modeling
- [ ] Database schema + migrations
- [ ] Auth (register/login, JWT)
- [ ] Topic CRUD
- [ ] Resource CRUD + topic linking
- [ ] Search across resources
- [ ] Deploy live demo
- [ ] v0.2: browser bookmarklet, metadata auto-fetch, export

## Why This Project

Built by a self-taught developer who also works on systems-level projects (a from-scratch BitTorrent client, a C reimplementation of Unix core utilities). Kosha applies the same "understand it deeply before building it" approach to product and fullstack development.

## License

MIT
