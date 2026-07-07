# 06 - Lifecycle

## Resource Lifecycle
1. **Create**: User saves a URL + title + note + type. Resource is created with zero or more Topic links.
2. **Organize**: User links/unlinks the Resource to one or more Topics at any time.
3. **Update**: User edits note, status, or metadata as understanding evolves.
4. **Unlink**: Removing a Topic link does not delete the Resource; it may become unassigned.
5. **Delete**: User deletes the Resource. All ResourceTopic links for it are removed. Gone permanently (no soft delete in v0.1).

## Topic Lifecycle
1. **Create**: User names a Topic (e.g. "Networking").
2. **Populate**: User links existing or new Resources to it.
3. **Rename/Edit**: Name and description are editable anytime.
4. **Delete**: Topic and its links are removed. Linked Resources survive, becoming unassigned if that was their only Topic.

## Edge Cases (failure paths)
- User saves an invalid/unreachable URL → Resource is still saved (Kosha does not validate reachability); only format is validated.
- User saves a duplicate URL → prompt to link existing Resource instead of creating a new one.
- User deletes a Topic that is the only link for several Resources → those Resources become unassigned, visible in an "Unassigned" view, not deleted.
- User searches with no matches → empty state shown, no error.
