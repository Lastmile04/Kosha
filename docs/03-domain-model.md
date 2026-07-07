# 03 - Domain Model

## Core Principle
Kosha is not a collection of resources — it is a system that preserves the relationships between resources and the topics they contribute to. Resources are the primary objects; Topics are the organizational lens.

## Resolved Design Decisions
These were the open questions from planning. They are now closed for v0.1 — see `decisions/` for full reasoning.

1. **A Resource can belong to multiple Topics** (many-to-many). Beej's Guide can live under both "Networking" and "C". → `decisions/0001-multiple-topics-per-resource.md`
2. **A Topic is a catalog, not a folder.** It is an organizational view over Resources, not an exclusive owner of them.
3. **A Resource does NOT require a Topic to exist.** A Resource can be saved unassigned ("Inbox" state) and organized later. This removes the deletion contradiction raised during review (deleting a Topic can never leave a Resource in an invalid state).

## Core Entities

### Resource (central entity)
The fundamental, independently-existing unit of Kosha. Represents any learning material.
- `id`
- `user_id`
- `url` (has identity — the same URL saved twice is the same logical resource; see invariants)
- `title`
- `note` (short text — the "why I saved this")
- `resource_type` (enum: youtube, article, docs, repo, pdf, book, other)
- `status` (enum: to_learn, in_progress, completed)
- `metadata` (jsonb — thumbnail, duration, etc., optional)
- `saved_at`, `updated_at`

### Topic
A user-defined organizational context that groups related Resources for browsing and recall. Does not alter what a Resource "is."
- `id`
- `user_id`
- `name`
- `description` (optional)
- `created_at`, `updated_at`

### ResourceTopic (join entity)
Represents the many-to-many relationship. This table is the real backbone of the domain.
- `resource_id`
- `topic_id`
- `linked_at`

### Note
Not a separate entity in v0.1. A Note is simply the `note` field on a Resource — describing why it was saved. This keeps the model minimal; Kosha does not model general knowledge, only resources and the context around them. (Notes-on-Topics deferred to v0.2 if needed.)

### User
Owns Topics and Resources. All data is private by default.

## Relationships
- User 1 → N Topics
- User 1 → N Resources
- Resource N ↔ N Topics (via ResourceTopic)

## Glossary
- **Resource**: Any piece of learning material with identity (a URL), independent of any Topic.
- **Topic**: A meaningful, user-defined context used to group and rediscover Resources.
- **Context / Note**: The short personal text explaining why a Resource matters.
- **Kosha**: Sanskrit for "treasure" or "sheath" — a container of valuable things.
