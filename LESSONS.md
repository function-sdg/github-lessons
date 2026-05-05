# Git/GitHub Lessons — Progress and Plan

This file tracks an ongoing learning series. A future Claude session reading this should be able to pick up where the last one left off without re-deriving context.

## Learner

Simon (GitHub: `function-sdg`). Product Manager self-teaching engineering, focused on tools used to deploy code. Learns by doing — favor hands-on exercises over abstract explanation, but explain the *why* behind each command (he's building a mental model from scratch). Smart adult, not a beginner who needs hand-holding — give him the real tool with good scaffolding.

## Repo state at end of Lesson 1

- Live repo: `github.com/function-sdg/github-lessons`
- Branch state: only `main`. Two PRs already merged (`#1` via merge commit, `#2` via squash, plus a third via rebase from VS Code).
- Files: `index.html`, `style.css` (currently the wobbling-rainbow-blob practice version Simon edited), `README.md`.
- Global git config: `user.email` = noreply (`194493721+function-sdg@users.noreply.github.com`), `fetch.prune` = true.
- `gh` CLI installed and authenticated.
- VS Code with **GitHub Pull Requests and Issues** extension installed and signed in.

## Lesson 1 — Completed (2026-05-04)

**Topic:** Basic git + pull requests on GitHub.

Key concepts he now understands:
- Working directory / staging area / repository — the three "places" a file lives
- Remotes are nicknames in *local* `.git/config` for another copy of the repo; `origin` is just convention
- Storage model: commits = snapshots, content-addressed via SHA, made of commit/tree/blob objects
- Branch = movable pointer to a commit
- PR = metadata view comparing two branches, not a copy of code
- Three merge strategies and the graph shapes they produce: merge commit (diamond), squash (linear, one commit on main, original branch commits become orphans), rebase (linear, all commits replayed onto main)
- Three interfaces over the same GitHub API: web UI, `gh` CLI, VS Code extension
- Cleanup mechanics: branch deletion, prune, the `fetch.prune=true` config
- Why squash + good PR description is the right pattern for AI-assisted "vibe coding": granular commits = scratch work / safety net during iteration, squash = clean durable record

He's also asked about / understood:
- GitHub Desktop's checkbox-based "fused" stage+commit (still supports partial commits per file/hunk)
- VS Code's `git.enableSmartCommit` setting
- `git worktree add` for parallel branch exploration

## Lesson 2 — CI/CD with GitHub Actions + GitHub Pages (planned, not started)

**Goal:** end with a live deployed website at `function-sdg.github.io/github-lessons`, served via a real CI/CD pipeline that runs checks on every PR and auto-deploys on merge.

**Decisions already made:**
- Continue on the same `github-lessons` repo
- Static site (no build step in first pass)
- Default `*.github.io/...` URL, no custom domain
- Same incremental hands-on pace as Lesson 1 — Simon runs commands, Claude explains the why before each step

### Proposed parts

**Part 1 — Actions fundamentals**
- What Actions, workflows, jobs, steps, runners actually are
- The `.github/workflows/` folder + YAML structure
- Trigger events: `push`, `pull_request`, `workflow_dispatch` (manual)
- Write a "hello world" workflow that prints a message — watch the **Checks** tab light up

**Part 2 — A real CI check on PRs**
- Add HTML validation (`html-validate` or `htmlhint`) that runs on every PR
- Intentionally break HTML on a branch → check fails → fix → check passes
- Optional: enable branch protection so GitHub blocks merge until checks pass

**Part 3 — Deploy to GitHub Pages via Actions**
- Configure Pages in repo settings to use the Actions deployment source (not branch-based)
- Write a deploy workflow using `actions/configure-pages`, `actions/upload-pages-artifact`, `actions/deploy-pages`
- First successful deploy → visit live URL
- Tour the deploy logs

**Part 4 — Full pipeline in action**
- Open a PR with a visible website change
- Watch Part 2's check run on the PR
- Merge → watch Part 3's deploy fire automatically
- See the live site update

**Part 5 (optional stretch) — Add a build step**
- Static site generator (Eleventy or Astro) OR a Tailwind build
- Demonstrates artifact-based deploys (build → upload artifact → deploy artifact) — the pattern Vercel/Netlify/Cloudflare/S3 all use

## How to resume

Start Lesson 2 by greeting Simon, confirming the assumptions above are still good, and beginning **Part 1 — Actions fundamentals**. Don't re-teach Lesson 1 material unless he asks. If he wants to revisit a concept, this file plus the `git log` of the repo should give enough context.
