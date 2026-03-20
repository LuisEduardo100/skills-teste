# Code Review Reference Guide

## Severity Definitions

### Critical
Issues that will cause bugs, data loss, security vulnerabilities, or system outages in production. These **must** be fixed before merging.

Examples:
- Unvalidated user input used in SQL queries
- Missing error handling on critical operations
- Race conditions that can corrupt data
- Hardcoded credentials or API keys

### Warning
Issues that won't immediately break things but will cause problems over time: technical debt, poor patterns, or potential bugs under specific conditions.

Examples:
- Missing null checks on nullable values
- Catch blocks that swallow errors silently
- Functions with too many parameters (>4)
- Duplicated logic that should be extracted

### Suggestion
Improvements for readability, consistency, or minor performance gains. Not blocking.

Examples:
- Variable naming improvements
- Extracting a magic number into a named constant
- Using a more idiomatic language construct
- Adding a clarifying comment for complex logic

## Language-Specific Patterns to Watch

### JavaScript/TypeScript
- `==` vs `===` (prefer strict equality)
- Missing `await` on async calls
- Mutable state in shared contexts
- Unhandled promise rejections

### Python
- Mutable default arguments (`def foo(items=[])`)
- Bare `except:` clauses
- Not using context managers for resources
- Global state mutation

### SQL
- `SELECT *` in production queries
- Missing `WHERE` clauses on `UPDATE`/`DELETE`
- No parameterized queries (SQL injection risk)
- Missing indexes on frequently queried columns

## Tone Guidelines
- Be constructive, not critical
- Explain **why** something is an issue, not just **what**
- Suggest a concrete fix when possible
- Acknowledge good patterns and decisions
