---
name: code-review
description: Review code for quality, security, performance, and maintainability. Use when reviewing pull requests, examining code changes, or analyzing code quality before merging.
argument-hint: "[file-or-pr-number]"
context: fork
allowed-tools: Read, Grep, Glob, Bash(git *)
---

# Code Review

Review the code specified by the user. If a file path is provided via `$ARGUMENTS`, focus on that file. If no argument is given, review the current staged or unstaged changes.

## Review Checklist

Analyze the code across these dimensions, in order of priority:

### 1. Correctness
- Logic errors, off-by-one mistakes, null/undefined handling
- Edge cases not covered
- Race conditions or concurrency issues

### 2. Security
- Input validation and sanitization
- SQL injection, XSS, command injection risks
- Hardcoded secrets or credentials
- Insecure dependencies

### 3. Performance
- Unnecessary loops or redundant operations
- N+1 query patterns
- Missing indexes or inefficient data structures
- Memory leaks

### 4. Maintainability
- Code clarity and naming conventions
- Single Responsibility Principle adherence
- Excessive complexity (deeply nested conditionals, long functions)
- Missing or misleading comments

### 5. Testing
- Are critical paths tested?
- Are edge cases covered?
- Test quality and readability

## Context Gathering

Before reviewing, gather context:
- Read the files involved
- Check git history for recent changes: `git log --oneline -10 -- <file>`
- Understand the broader module structure

## Output Format

Structure your review as:

**Summary**: 1-2 sentence overview of the changes and their quality.

**Issues Found** (grouped by severity):
- **Critical**: Must fix before merging
- **Warning**: Should fix, but not a blocker
- **Suggestion**: Nice to have improvements

**What's Good**: Highlight positive patterns or well-written code.

For detailed review guidelines, see [reference/review-guide.md](reference/review-guide.md).
