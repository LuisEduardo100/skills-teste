---
name: commit-message
description: Generate conventional commit messages based on staged changes. Use when creating git commits, writing commit messages, or preparing changes for commit.
disable-model-invocation: true
allowed-tools: Bash(git *)
---

# Generate Commit Message

Analyze the current staged changes and generate a commit message following the Conventional Commits specification.

## Steps

1. Check staged changes:
   ```
   git diff --cached --stat
   git diff --cached
   ```

2. If nothing is staged, check unstaged changes and inform the user they need to stage first.

3. Analyze the diff to understand:
   - What files were changed
   - What was the nature of the change (new feature, bug fix, refactor, etc.)
   - What is the intent behind the changes

4. Generate a commit message following the format below.

## Commit Message Format

```
<type>(<scope>): <subject>

<body>
```

### Types
| Type | When to use |
|------|------------|
| `feat` | A new feature or capability |
| `fix` | A bug fix |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `docs` | Documentation only changes |
| `test` | Adding or updating tests |
| `chore` | Build process, dependencies, or tooling changes |
| `perf` | Performance improvement |
| `style` | Formatting, semicolons, etc. (no logic change) |
| `ci` | CI/CD configuration changes |

### Rules
- **Subject**: imperative mood, lowercase, no period, max 50 chars
- **Scope**: optional, the module or area affected (e.g., `auth`, `api`, `ui`)
- **Body**: explain **what** and **why**, not **how**. Wrap at 72 chars.

## Output

Present the generated message and ask the user if they want to:
1. Use it as-is
2. Edit it
3. Regenerate with different focus

For examples of good commit messages, see [reference/examples.md](reference/examples.md).
