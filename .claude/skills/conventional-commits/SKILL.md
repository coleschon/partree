---
name: conventional-commits
description: Use whenever creating a git commit, writing a commit message, or opening/editing a pull request in this repo.
---

# Conventional Commits (v1.0.0)

Spec: https://www.conventionalcommits.org/en/v1.0.0/
CI enforces this on PR titles with commitlint (`@commitlint/config-conventional`, see `.github/commitlint.yml`).

## How changes land on main
PRs are squash-merged with the **PR title as the entire commit message**. The PR description stays on the PR and is not copied into the commit. The only body on `main` is the `Co-authored-by:` trailers GitHub adds automatically at merge.

## Header
```
<type>(<optional scope>)<optional !>: <description>
```
- **type**: one of `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
  - `feat`: a new feature (SemVer minor). `fix`: a bug fix (SemVer patch).
- **scope** (optional): a noun for the area touched, e.g. `fix(parser): ...`.
- **!** marks a breaking change (SemVer major). It is the **only** way to signal one here.
- **description**: atomic action ("add", not "added"), lowercase, no trailing period.
- The whole header must be ≤ 100 characters.

## Breaking changes
- Signal them only with `!` in the header, e.g. `refactor(api)!: rename parse() to parseTree()`.
- Do not write `BREAKING CHANGE:` footers. Footers are dropped at merge, so the signal would be lost. Explain the break and any migration steps in the PR description instead.

## Examples
```
feat(cli): add --depth flag to limit tree output
fix: handle empty input without crashing
refactor(api)!: rename parse() to parseTree()
```

## Pull requests
- The title follows the header rules above. It is the only text that reaches `main`, so make it stand on its own.
- Write the description from `.github/pull_request_template.md`. Fill in `## Description`, include optional sections only when they apply, and remove the `<!--optional-->` markers and placeholder text. `gh pr create --body` and the API skip the template, so copy its structure yourself.
- The description is for reviewers, not a commit body, so don't add footers to it.

## Branch commits
Branch commits are squashed away, but keep them readable for review:
- Use a conventional header. Add a body when it helps explain *why*.
- `Co-Authored-By:` trailers are fine; GitHub collects them into the squash commit. Don't add other footers.

## Splitting work
Keep one logical change per PR. If a change needs two types (e.g. a fix plus unrelated docs), open two PRs.
