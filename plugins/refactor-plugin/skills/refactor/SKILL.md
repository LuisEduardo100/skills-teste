---
name: refactor
description: Refactor code to improve readability, reduce complexity, and follow best practices. Use when cleaning up code, reducing duplication, simplifying complex functions, or improving code structure.
argument-hint: "[file-path]"
allowed-tools: Read, Grep, Glob, Edit, Bash(git *), Bash(npm test*), Bash(npx jest*), Bash(python -m pytest*)
---

# Refactor Code

Refactor the code specified by `$ARGUMENTS`. If no argument is provided, ask the user which file or function to refactor.

## Process

### 1. Understand Before Changing
- Read the target file completely
- Identify the public API (exports, public methods, function signatures)
- Check for tests: search for test files related to this code
- Understand callers: `grep` for usages of the functions being refactored

### 2. Identify Refactoring Opportunities

Focus on these common improvements:

**Reduce Complexity**
- Extract long functions (>30 lines) into smaller, well-named functions
- Flatten deeply nested conditionals using early returns or guard clauses
- Replace complex conditionals with named boolean variables

**Eliminate Duplication**
- Extract repeated code blocks into shared functions
- Consolidate similar switch/if-else branches
- Use data-driven approaches instead of repetitive code

**Improve Naming**
- Rename variables/functions to express intent, not implementation
- Replace abbreviations with full words
- Make boolean names read as questions (`isValid`, `hasPermission`)

**Simplify Structure**
- Remove dead code (unused variables, unreachable branches)
- Replace manual iteration with built-in methods (map, filter, reduce)
- Consolidate related parameters into objects/structs

### 3. Preserve Behavior
- **Do not change the public API** unless explicitly asked
- Run existing tests after each change to verify nothing broke
- Make changes incrementally, not all at once

### 4. Validate
- Run the test suite after refactoring
- If no tests exist, note this as a risk and suggest which tests should be added

## Output

After refactoring, provide:
1. **What changed**: List of specific refactorings applied
2. **Why**: The motivation for each change
3. **Test results**: Did existing tests pass?
4. **Risks**: Any areas where behavior might have subtly changed

For refactoring patterns reference, see [reference/patterns.md](reference/patterns.md).
