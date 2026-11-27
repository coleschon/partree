---
name: conventional-commits
description: Use whenever creating a git commit or writing a commit message in this repo.
---

# Conventional Commits (v1.0.0)

Spec: https://www.conventionalcommits.org/en/v1.0.0/
CI enforces this with commitlint (`@commitlint/config-conventional`, see `.commitlintrc.yml`).

## Format

```
<type>(<optional scope>)<optional !>: <description>

<optional body>

<optional footer(s)>
```

## Header
- **type**: one of `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
  - `feat`: a new feature (SemVer minor). `fix`: a bug fix (SemVer patch).
- **scope** (optional): a noun for the area touched, e.g. `fix(parser): ...`.
- **description**: imperative mood ("add", not "added"), lowercase, no trailing period.
- The whole header must be ≤ 100 characters.

## Body
- Separate it from the header with one blank line.
- Explain *why* the change was made, not a restatement of the diff.

## Footers
- Separate them from the body with one blank line. Each footer is `Token: value` (tokens use `-` instead of spaces, e.g. `Co-Authored-By:`).
- **Breaking changes** (SemVer major): add `!` before the `:` in the header, add a `BREAKING CHANGE: <explanation>` footer, or both.

## Examples

```
feat(cli): add --depth flag to limit tree output
```

```
fix: handle empty input without crashing

Previously an empty file caused an index error during parsing.
```

```
refactor(api)!: rename parse() to parseTree()

BREAKING CHANGE: parse() has been removed; call parseTree() instead.
```

## Splitting work
Keep one logical change per commit. If a change needs two types (e.g. a fix plus unrelated docs), make two commits.
