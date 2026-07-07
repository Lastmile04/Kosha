# 05 - Invariants & Rules

## Core Invariants
1. Every Resource belongs to exactly one User.
2. Every Topic belongs to exactly one User.
3. A Resource may exist with zero Topics (unassigned/"Inbox" state) — this resolves the earlier deletion contradiction.
4. A Resource may belong to many Topics; a Topic may contain many Resources (many-to-many).
5. All data is private to the owning User; there is no cross-user visibility in v0.1.
6. A Resource's `url` is treated as its identity within a User's account — saving the same URL twice should link/update rather than duplicate (see Rule below).

## Deletion Rules
- Deleting a Topic removes only the Topic and its ResourceTopic links. It never deletes the underlying Resources.
- Deleting a Resource removes it and all its ResourceTopic links. It never deletes the Topics it was linked to.
- Deleting a User cascades to delete all owned Topics, Resources, and links.

## Duplicate Handling
- If a User attempts to save a URL that already exists in their account, Kosha should offer to link the existing Resource to the new Topic rather than create a duplicate.

## Mutability Rules
- `title`, `note`, `status`, and Topic links are mutable at any time.
- `url` is editable (e.g. http → https, or a moved doc page) but changing it does not change the Resource's identity/history.
