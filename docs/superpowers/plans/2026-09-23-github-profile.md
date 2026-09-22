# GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a polished English GitHub Profile README for an AI Agent tooling developer with Go and full-stack engineering depth.

**Architecture:** Keep the profile as one dependency-light root `README.md`. Use native GitHub Markdown for content and static Shields images only in the hero so the profile remains readable, responsive, and stable without third-party statistics services.

**Tech Stack:** GitHub Flavored Markdown, HTML alignment supported by GitHub, static Shields.io badges

**Spec:** `docs/superpowers/specs/2026-09-23-github-profile-design.md`

## Global Constraints

- All profile copy is English.
- AI Agent tooling is the primary identity; Go and full-stack engineering are the supporting identity.
- Do not add animated widgets, visitor counters, activity statistics, or generated metric cards.
- Do not modify `LICENSE`.
- Use only public repository links and HTTPS image URLs.
- The page must remain understandable if badge images do not load.

---

### Task 1: Create and validate the Profile README

**Files:**
- Create: `README.md`
- Test: shell validation commands against `README.md` and public URLs

**Interfaces:**
- Consumes: public repositories at `https://github.com/mmungdong/skills`, `https://github.com/mmungdong/nav-next`, and `https://github.com/mmungdong/full-stack-devkit`
- Produces: a root `README.md` rendered automatically by GitHub on `https://github.com/mmungdong`

- [x] **Step 1: Run the baseline validation and confirm the profile is absent**

Run:

```bash
test -s README.md
```

Expected: FAIL because `README.md` does not exist yet.

- [x] **Step 2: Create the minimal complete Profile README**

Create `README.md` with this content:

```markdown
<div align="center">

# Hi, I'm mungdong.

**AI Agent Tooling · Go & Full-stack Engineering**

I build reliable developer tools and agent workflows that turn complex systems into practical software.

![AI Agent Tooling](https://img.shields.io/badge/AI_Agent-Tooling-7C3AED?style=flat-square)
![Go](https://img.shields.io/badge/Go-Engineering-00ADD8?style=flat-square&logo=go&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-Full--stack-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Open Source](https://img.shields.io/badge/Open_Source-Builder-238636?style=flat-square&logo=github&logoColor=white)

</div>

---

## Current focus

- Designing reusable AI Agent Skills and workflows for real development tasks.
- Building Go-based tools for automation, integration, and dependable backend systems.
- Shipping full-stack products that connect thoughtful interfaces with maintainable services and infrastructure.

## Selected work

| Project | What it is | Focus |
| --- | --- | --- |
| [`skills`](https://github.com/mmungdong/skills) | A curated collection of AI Agent Skills I use, maintain, and share across coding agents. | Agent tooling · Python |
| [`nav-next`](https://github.com/mmungdong/nav-next) | A lightweight navigation product built with TypeScript. | Frontend · Product engineering |
| [`full-stack-devkit`](https://github.com/mmungdong/full-stack-devkit) | A practical toolkit for full-stack development, centered on Go workflows. | Go · Developer tooling |

## Toolbox

- **Agent systems:** reusable Skills, workflow orchestration, context design, and prompt engineering
- **Backend:** Go, Python, API design, automation, and service integration
- **Frontend:** TypeScript, React, Next.js, and Vue
- **Platform:** Docker, Kubernetes, Terraform, CI/CD, and cloud infrastructure

## Engineering principles

> Build tools around real workflows, not demos.  
> Make automation observable, reversible, and maintainable.  
> Never let AI conclusions outrun their evidence or permissions.

---

I'm always interested in practical AI Agent tooling, Go systems, and developer infrastructure.  
[Explore my repositories](https://github.com/mmungdong?tab=repositories) or follow along as I build.
```

- [x] **Step 3: Validate the Markdown content contract**

Run:

```bash
test -s README.md
grep -q '^# Hi, I' README.md
grep -q '^## Current focus$' README.md
grep -q '^## Selected work$' README.md
grep -q '^## Toolbox$' README.md
grep -q '^## Engineering principles$' README.md
test "$(grep -c 'https://img.shields.io/' README.md)" -eq 4
! grep -Eqi 'github-readme-stats|streak-stats|komarev|visitor' README.md
```

Expected: PASS with no output.

- [x] **Step 4: Verify public links and HTTPS image sources**

Run:

```bash
for url in \
  https://github.com/mmungdong/skills \
  https://github.com/mmungdong/nav-next \
  https://github.com/mmungdong/full-stack-devkit \
  'https://github.com/mmungdong?tab=repositories'
do
  curl -fsSL -o /dev/null "$url"
done

! grep -oE '<img[^>]+>' README.md | grep -vq 'alt='
! grep -oE 'https?://[^ )]+' README.md | grep -q '^http://'
```

Expected: PASS with no output.

- [x] **Step 5: Check the diff and whitespace**

Run:

```bash
git diff --check
git diff -- README.md
```

Expected: no whitespace errors; the diff contains only the approved README content.

- [x] **Step 6: Commit the profile**

```bash
git add README.md docs/superpowers/specs/2026-09-23-github-profile-design.md docs/superpowers/plans/2026-09-23-github-profile.md
git commit -m "feat(profile): add GitHub profile README"
```
