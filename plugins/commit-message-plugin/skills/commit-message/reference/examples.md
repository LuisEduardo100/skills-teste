# Commit Message Examples

## Good Examples

### Simple bug fix
```
fix(auth): prevent token refresh race condition

Multiple concurrent requests could trigger simultaneous token refreshes,
causing some requests to fail with 401. Added a mutex to ensure only one
refresh happens at a time while others wait for the result.
```

### New feature
```
feat(api): add pagination to user listing endpoint

GET /api/users now supports cursor-based pagination via `cursor` and
`limit` query parameters. Default limit is 20, max is 100. This
replaces the previous unbounded query that caused timeouts on large
datasets.
```

### Refactoring
```
refactor(database): extract query builder from repository classes

Moved shared query construction logic into a dedicated QueryBuilder
class. Repositories now compose queries instead of duplicating SQL
string concatenation. No behavior change.
```

### Dependency update
```
chore(deps): upgrade express from 4.18 to 4.19

Includes security patch for CVE-2024-XXXX (path traversal in static
file serving). No breaking changes in this minor version bump.
```

### Multiple files, single purpose
```
feat(notifications): add email digest for weekly activity summary

Added digest template, scheduling job, and user preference toggle.
Users can opt in via settings. Digest runs every Monday at 8am UTC
and includes: new comments, PR reviews, and deployment status.
```

## Anti-patterns to Avoid

```
# Too vague
fix: fix bug

# Too long subject
fix(authentication): fix the bug where users cannot log in when their session token expires and they try to refresh it

# Not imperative mood
fix(auth): fixed the login bug

# Describes HOW instead of WHY
refactor: changed forEach to map and extracted function

# Mixed concerns in one commit
feat(auth, api, ui): add login page with API endpoint and auth middleware
```
