# 🧹 Clean-Up

> A production-readiness cleanup skill for AI coding agents.

**Clean-Up** is a reusable AI-agent skill that safely cleans completed software projects before production or final delivery.

It helps AI coding agents identify and remove:

- Dead and unused code
- Unused dependencies
- Obsolete files
- Temporary development artifacts
- Debugging code
- Obsolete configuration
- Duplicate implementations
- Unused assets
- Development leftovers
- Repository hygiene issues

while prioritizing **functionality, safety, and minimal changes**.

---

## Why Clean-Up?

AI coding agents are very good at building features.

But once a project is finished, the codebase often contains:

```text
unused components
unused dependencies
temporary files
debugging statements
old implementations
duplicate utilities
unused assets
obsolete configuration
development artifacts
```

Manually finding all of these is tedious.

Simply telling an AI agent:

> "Clean up this project."

can also be dangerous.

An agent may remove something that appears unused but is actually required by:

- Dynamic imports
- Framework conventions
- External APIs
- Webhooks
- Database migrations
- CI/CD
- Environment configuration
- External applications
- Dynamically referenced assets

**Clean-Up** provides a structured workflow designed to make this process safer.

---

## ✨ Features

### 🔍 Project Inspection

The agent first understands the project before making changes.

It analyzes:

- Project structure
- Framework
- Language
- Dependencies
- Build system
- Configuration
- Scripts
- Environment setup
- Git state
- Existing project instructions

---

### 🗑️ Dead Code Detection

Identifies potentially unnecessary:

- Imports
- Variables
- Functions
- Components
- Hooks
- Utilities
- Types
- Constants
- Routes
- Experimental implementations
- Commented-out code
- Debugging code

The agent only removes code when there is sufficient evidence that it is unused.

---

### 📦 Dependency Cleanup

Finds and removes safely unused dependencies.

It checks:

- Source imports
- Scripts
- Configuration
- Build tooling
- Dynamic usage
- Project conventions

before removing anything.

---

### 📁 File & Artifact Cleanup

Finds unnecessary:

- Temporary files
- Backup files
- Old components
- Demo pages
- Development screenshots
- Build artifacts
- Logs
- IDE artifacts
- OS-specific files
- Obsolete documentation

---

### 🔐 Security Audit

Checks for accidentally exposed:

- API keys
- Tokens
- Passwords
- Private keys
- Database credentials
- Hardcoded secrets

It also reviews environment configuration.

**Secret values are never printed in the final report.**

---

### ⚙️ Configuration Cleanup

Reviews configuration for:

- Obsolete settings
- Removed dependencies
- Dead scripts
- Unused aliases
- Deprecated configuration
- Development-only configuration

---

### 🎨 UI Preservation

For frontend projects, Clean-Up explicitly prioritizes preserving:

- Design
- Layout
- Typography
- Colors
- Responsive behavior
- Animations
- Interactions
- Accessibility
- Existing UX

Clean-Up is **not a redesign tool**.

---

### 🧪 Production Validation

After cleanup, the agent validates the project using its existing tooling.

Depending on the project:

```text
Lint
Typecheck
Tests
Build
Integration tests
E2E tests
```

Cleanup-related regressions must be fixed before completion.

---

### 🛡️ Safety First

The skill follows a simple rule:

> **When uncertain, don't delete.**

Potentially dangerous items are preserved and reported for manual review.

---

# Installation

Clean-Up is designed to be **agent-agnostic**.

The exact installation location depends on the AI coding agent you use.

Clone or download this repository:

```bash
git clone https://github.com/aetheramizu/clean-up.git
```

Then place the `SKILL.md` file in the skill/instruction directory supported by your AI coding agent.

The skill itself does not depend on OpenCode, Claude Code, Codex, Cursor, or any particular framework.

---

# OpenCode

If your OpenCode installation supports skills, place the skill where OpenCode discovers project or global skills.

For example:

```text
your-project/
└── .opencode/
    └── skills/
        └── clean-up/
            └── SKILL.md
```

Then ask the agent to use the `clean-up` skill.

> Check the current OpenCode documentation for the exact skill discovery path, as agent configuration conventions can change.

---

# Claude Code

For Claude Code installations that support project skills, place the skill in the project's skill directory.

For example:

```text
your-project/
└── .claude/
    └── skills/
        └── clean-up/
            └── SKILL.md
```

Then invoke the skill using the appropriate Claude Code skill mechanism.

> Check the current Claude Code documentation for the exact installation and invocation syntax.

---

# Codex

For Codex environments that support reusable skills, install `SKILL.md` in the appropriate skills directory.

For example:

```text
your-project/
└── .codex/
    └── skills/
        └── clean-up/
            └── SKILL.md
```

Then make the skill available to the Codex agent.

> Check the current Codex documentation for the exact skill discovery path.

---

# Cursor

Cursor can use project-level agent instructions and reusable workflows depending on the current version.

A common approach is to place the skill or its instructions inside the project's agent configuration.

For example:

```text
your-project/
└── .cursor/
    └── skills/
        └── clean-up/
            └── SKILL.md
```

If your Cursor version uses a different mechanism, adapt the installation location while keeping the `SKILL.md` content unchanged.

---

# Other AI Agents

The skill can be adapted to any AI coding agent that supports:

- Markdown-based instructions
- Agent skills
- Reusable prompts
- Project-level instructions
- Tool-using coding agents

The core skill is intentionally **platform-independent**.

If your agent does not support a formal `SKILL.md` system, you can use the contents of `SKILL.md` as the agent's project instruction or system prompt.

---

# Usage

Once installed, invoke the skill when the project is functionally complete.

For example:

```text
Use the clean-up skill on this project.
```

Or:

```text
Run clean-up on this project and prepare it for production.
```

The agent should then follow the workflow defined in `SKILL.md`.

---

# Recommended Workflow

Clean-Up is intended to be used **after development**, not continuously during feature development.

A typical workflow looks like:

```text
Build
  ↓
Develop Features
  ↓
Test
  ↓
Fix Bugs
  ↓
Project Functionally Complete
  ↓
🧹 Clean-Up
  ↓
Validate
  ↓
Manual Review
  ↓
Production
```

---

# What Clean-Up Does NOT Do

Clean-Up is deliberately conservative.

It does **not**:

- Redesign your application
- Rewrite your architecture
- Replace your framework
- Replace libraries unnecessarily
- Delete database migrations blindly
- Delete potentially externally-used APIs
- Rewrite Git history
- Commit changes automatically
- Push changes automatically
- Remove secrets from Git history automatically
- Make speculative performance optimizations
- Fix unrelated bugs
- Add unrelated features

Its purpose is cleanup, not redevelopment.

---

# Safety Philosophy

Clean-Up uses the following priority:

```text
Correctness
    ↓
Safety
    ↓
Existing Functionality
    ↓
Maintainability
    ↓
Cleanliness
```

This means a slightly messy piece of code is preferable to accidentally breaking production functionality.

If the agent cannot confidently determine whether something is safe to remove, it should preserve it and report it.

---

# Final Report

After running Clean-Up, the agent should report:

```text
## Clean-Up Summary

### Removed
...

### Modified
...

### Security
...

### Validation

Lint: PASS
Typecheck: PASS
Tests: PASS
Build: PASS

### Manual Review Required
...

### Production Readiness

READY
```

Possible production-readiness states are:

```text
READY
READY WITH WARNINGS
NOT READY
```

---

# Example

Before:

```text
src/
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── OldDashboard.tsx
│   └── TestComponent.tsx
├── utils/
│   ├── api.ts
│   ├── oldApi.ts
│   └── debug.ts
└── pages/
    └── index.tsx

package.json
```

After a safe cleanup:

```text
src/
├── components/
│   ├── Navbar.tsx
│   └── Footer.tsx
├── utils/
│   └── api.ts
└── pages/
    └── index.tsx

package.json
```

The important difference is that `OldDashboard.tsx`, `TestComponent.tsx`, `oldApi.ts`, and `debug.ts` should only be removed if the agent has verified that they are actually unnecessary.

---

# Contributing

Contributions are welcome.

If you want to improve the skill:

1. Fork the repository.
2. Create a feature branch.
3. Improve `SKILL.md`.
4. Test the skill against real projects.
5. Document meaningful changes.
6. Open a pull request.

When proposing changes, prioritize:

- Safety
- Portability
- Compatibility
- Predictability
- Production-readiness

Avoid adding instructions that are specific to one AI coding agent unless they are placed in the documentation rather than the core skill.

---

# License

This project is licensed under the MIT License.

See [LICENSE](LICENSE) for details.
