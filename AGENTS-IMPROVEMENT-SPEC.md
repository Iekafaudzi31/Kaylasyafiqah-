# AGENTS Improvement Spec

Audit date: 2026-05-16  
Auditor: Ona

---

## Current State

| Artifact | Status | Notes |
|---|---|---|
| `AGENTS.md` | ✅ Created (was missing) | Placeholder content — project has no stack yet |
| `.ona/skills/` | ❌ Missing | No skill files exist |
| `.cursor/rules/` | ❌ Missing | No Cursor rule files exist |
| `README.md` | ⚠️ Inadequate | Contains only "Barang" — no purpose, stack, or setup info |
| `.devcontainer/devcontainer.json` | ⚠️ Suboptimal | Uses 10 GB universal image; no `postCreateCommand`, no extensions |
| `.gitignore` | ❌ Missing | No dependency directories are excluded yet |
| Source code | ❌ None | Repository has no application code |
| Tests | ❌ None | No test framework configured |
| CI/CD | ❌ None | No GitHub Actions or other pipeline |

---

## What's Good

- Dev container exists — the environment is reproducible.
- `AGENTS.md` now exists with a clear placeholder structure.
- Single commit history is clean.

---

## What's Missing

1. **Project definition** — no stated purpose, language, or framework.
2. **`.gitignore`** — must exist before any dependencies are installed.
3. **Skill files** — no `.ona/skills/` workflows for repeatable tasks.
4. **README content** — no setup instructions, no description.
5. **Stack-specific AGENTS.md sections** — build commands, test commands, style rules.
6. **CI pipeline** — no automated checks on PRs.
7. **Dev container optimisation** — universal image is slow; no lifecycle hooks.

---

## What's Wrong

1. **`README.md` is a stub.** "Barang" is not a description. Agents and contributors cannot determine what this project does.
2. **No `.gitignore`.** If a developer runs `npm install` or `pip install` today, dependency directories will be committed.
3. **Dev container uses the universal image** (`~10 GB`). This causes slow environment startup with no benefit until a stack is chosen.
4. **`AGENTS.md` (newly created) is intentionally sparse** because the stack is unknown. It will become stale if not updated when the project gains code.

---

## Improvement Spec

### Priority 1 — Immediate (before any code is written)

#### 1.1 Define the project

The owner must answer:
- What does this project do?
- What language/framework will be used?
- Who is the intended user?

Update `README.md` and `AGENTS.md` with the answers.

#### 1.2 Add `.gitignore`

Create a `.gitignore` matched to the chosen stack before installing any dependencies.

Minimum content regardless of stack:
```
# Editor
.vscode/
.idea/
*.swp
.DS_Store

# Secrets
.env
.env.*
!.env.example
```

Add language-specific patterns (e.g. `node_modules/`, `__pycache__/`, `venv/`) once the stack is known.

#### 1.3 Improve `README.md`

Minimum sections:
- **What it is** — one-sentence description.
- **Prerequisites** — runtime versions required.
- **Setup** — how to install dependencies and run locally.
- **Testing** — how to run the test suite.

---

### Priority 2 — When stack is chosen

#### 2.1 Right-size the dev container

Replace the universal image with a stack-specific one:

| Stack | Image |
|---|---|
| Node.js | `mcr.microsoft.com/devcontainers/javascript-node:22` |
| Python | `mcr.microsoft.com/devcontainers/python:3.13` |
| Go | `mcr.microsoft.com/devcontainers/go:1.24` |

Add a `postCreateCommand` to install dependencies automatically:
```json
"postCreateCommand": "npm install"
```

Add relevant VS Code extensions under `customizations.vscode.extensions`.

#### 2.2 Update `AGENTS.md` with stack details

Fill in the placeholder sections:
- Build and run commands.
- Test command and coverage threshold.
- Linter/formatter and how to run it.
- Directory map (src, tests, assets, config).
- Naming conventions.

#### 2.3 Add `.ona/skills/`

Create skill files for repeatable agent workflows. Suggested initial skills:

| Skill file | Purpose |
|---|---|
| `.ona/skills/add-feature.md` | Workflow for adding a new feature (branch → implement → test → PR) |
| `.ona/skills/fix-bug.md` | Workflow for bug fixes (reproduce → fix → test → PR) |
| `.ona/skills/review-pr.md` | Checklist for reviewing pull requests |

Each skill file should contain:
1. Trigger conditions (when to use this skill).
2. Step-by-step workflow.
3. Verification steps.
4. Anti-patterns to avoid.

---

### Priority 3 — When the first PR is opened

#### 3.1 Add CI pipeline

Create `.github/workflows/ci.yml` with at minimum:
- Install dependencies.
- Run linter.
- Run tests.
- Report coverage.

#### 3.2 Add PR template

Create `.github/pull_request_template.md`:
```markdown
## What
<!-- One-sentence summary of the change -->

## Why
<!-- Motivation or linked issue -->

## Testing
<!-- How was this tested? -->
```

---

## Acceptance Criteria

A well-configured repository for this project should satisfy all of the following:

- [ ] `README.md` describes the project, prerequisites, setup, and test commands.
- [ ] `AGENTS.md` contains stack, build commands, test commands, style rules, and directory map.
- [ ] `.gitignore` excludes dependency directories, build artifacts, and secrets.
- [ ] Dev container uses a stack-specific image with `postCreateCommand`.
- [ ] At least one `.ona/skills/` file documents a repeatable agent workflow.
- [ ] CI runs on every PR and blocks merge on failure.
- [ ] PR template exists.
