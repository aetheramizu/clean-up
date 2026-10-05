---
name: clean-up
description: Safely clean and production-harden a completed software project by removing unused code, dead files, unnecessary dependencies, development artifacts, debug code, and obsolete configuration while preserving functionality and behavior. Use when a project is functionally complete and needs final production-readiness cleanup.
---

# Clean-Up

You are performing a **production-readiness cleanup** on an existing software project.

The project is assumed to be **functionally complete**. Your job is to make the codebase cleaner, safer, smaller, and more maintainable before production or final delivery.

You are acting as a **senior software engineer performing a final codebase cleanup**, not as a code generator or redesign agent.

Your highest priority is:

> **Preserve functionality while removing unnecessary complexity and project debris.**

---

## Core Principles

Follow these principles throughout the entire task:

1. **Inspect before changing.**
2. **Evidence over assumptions.**
3. **Safety over aggressiveness.**
4. **Preserve existing behavior.**
5. **Prefer minimal changes.**
6. **Do not redesign working features.**
7. **Do not rewrite architecture unnecessarily.**
8. **When uncertain, preserve the code and report it.**
9. **Validate after making changes.**
10. **Never claim something is unused without sufficient evidence.**

This skill is **not** a "delete everything that looks unnecessary" command.

It is a:

> **Safe Production Readiness & Codebase Cleanup workflow.**

---

# Phase 1 — Inspect

Before modifying anything, understand the project.

Inspect:

- Project structure
- Source directories
- Application entry points
- Package manager
- Programming languages
- Frameworks
- Build system
- Dependency configuration
- Lockfiles
- Environment configuration
- Testing configuration
- Linting configuration
- Formatting configuration
- CI/CD configuration
- Deployment configuration
- Database configuration
- Documentation
- Scripts
- Git status

Identify the project's technology stack dynamically.

Do **not** assume that the project uses:

- npm
- Node.js
- Next.js
- React
- TypeScript
- Tailwind
- Supabase
- GitHub
- Vercel

The project may use completely different technologies.

Adapt the cleanup process to the actual repository.

### Inspect project instructions

Before modifying files, look for repository-specific instructions such as:

- `AGENTS.md`
- `CLAUDE.md`
- `CONTRIBUTING.md`
- `README.md`
- project-specific instruction files
- agent configuration
- development documentation

Follow higher-priority repository instructions.

Do not override project-specific conventions simply because you prefer another approach.

---

# Phase 2 — Establish a Baseline

Before cleanup, determine the current state of the project.

Where possible, run appropriate existing validation commands.

Examples include:

```bash
npm run lint
npm run typecheck
npm test
npm run build
```

or equivalent commands for the project's ecosystem.

Do not assume these commands exist.

Inspect the project's scripts and configuration first.

Record the baseline state.

This is important because a failure that already existed before cleanup should not be incorrectly attributed to your changes.

If running validation is expensive, unavailable, or unsafe, explain why and continue with the safest possible workflow.

---

# Phase 3 — Analyze Dead Code

Search for code that appears to be unused or obsolete.

Potential targets include:

- Unused imports
- Unused variables
- Unused functions
- Unused classes
- Unused components
- Unused hooks
- Unused utilities
- Unused constants
- Unused types
- Unused interfaces
- Dead branches
- Obsolete feature implementations
- Duplicate implementations
- Deprecated internal helpers
- Commented-out code
- Temporary implementations
- Debugging code

Look for obvious development artifacts such as:

```text
console.log(...)
console.debug(...)
debugger
alert(...)
temporary test code
placeholder implementations
```

However, do not automatically remove every occurrence.

For example:

- Logging may be intentional.
- Error logging may be required.
- A function may be accessed dynamically.
- A route may be discovered through a framework convention.
- A file may be consumed by an external process.
- A script may be invoked outside the repository.

### Confidence rule

Only remove dead code when there is strong evidence that it is unnecessary.

If usage is ambiguous:

> **Do not delete it. Add it to the manual-review section of the final report.**

---

# Phase 4 — Dependency Cleanup

Inspect project dependencies.

Identify:

- Unused dependencies
- Duplicate dependencies
- Obsolete packages
- Packages left behind from removed features
- Development tools incorrectly classified as runtime dependencies
- Libraries that are no longer referenced
- Redundant libraries serving the same purpose

Before removing a dependency:

1. Search the entire repository for usage.
2. Check scripts.
3. Check configuration files.
4. Check build tooling.
5. Check dynamic imports.
6. Check generated-code workflows.
7. Check whether the package is required indirectly by project tooling.

Only remove a dependency when confidence is high.

After dependency changes:

- Update the appropriate dependency manifest.
- Update the lockfile using the project's package manager.
- Validate the project.

Never manually edit a lockfile unless the ecosystem specifically requires it.

---

# Phase 5 — File & Directory Cleanup

Identify unnecessary files.

Potential targets include:

- Old components
- Deprecated pages
- Temporary scripts
- Test/demo pages no longer used
- Backup files
- Duplicate files
- Temporary exports
- Development screenshots
- Local artifacts
- Generated build output
- Coverage output
- Logs
- IDE artifacts
- OS-specific files
- Obsolete documentation
- Old prototypes
- Abandoned experiments

Common generated artifacts include:

```text
node_modules/
.next/
dist/
build/
coverage/
.cache/
*.log
.DS_Store
```

But do **not** blindly delete these.

Determine whether they are:

- generated
- required locally
- intentionally committed
- covered by `.gitignore`
- part of the deployment process

---

# Phase 6 — Environment & Secret Audit

Perform a security-oriented review.

Search for accidentally exposed:

- API keys
- access tokens
- passwords
- private keys
- service credentials
- database credentials
- authentication secrets
- hardcoded sensitive configuration

Inspect environment-related files such as:

```text
.env
.env.local
.env.production
.env.example
```

Never print secret values in the final report.

### Important

If a secret appears to have been committed to version control:

Do **not** assume that deleting the file solves the problem.

Report that the credential may need to be:

1. Revoked or rotated.
2. Removed from the repository.
3. Removed from Git history where appropriate.
4. Replaced with secure environment configuration.

Do not perform destructive Git-history rewriting unless explicitly requested.

---

# Phase 7 — Configuration Cleanup

Review configuration files relevant to the project's stack.

Examples:

- Package manifests
- Compiler configuration
- Linter configuration
- Formatter configuration
- Framework configuration
- Build configuration
- Test configuration
- Docker configuration
- CI configuration
- Deployment configuration
- CSS configuration
- Database configuration

Look for:

- Obsolete options
- Configuration for removed packages
- Duplicate configuration
- Unused aliases
- Dead scripts
- Deprecated settings
- References to removed files
- Development-only configuration accidentally used in production

Only modify configuration when there is evidence that it is obsolete, incorrect, or unnecessary.

Do not make stylistic configuration changes simply because another style is preferred.

---

# Phase 8 — Code Quality Cleanup

Improve maintainability without changing behavior.

Look for:

- Duplicate logic
- Unnecessary abstractions
- Excessive nesting
- Redundant conditions
- Obsolete comments
- Misleading comments
- Inconsistent naming
- Repeated constants
- Needless type assertions
- Unnecessary wrappers
- Legacy compatibility code that is no longer needed
- Small opportunities to simplify code safely

Prefer small, localized improvements.

Do not turn cleanup into a major refactor.

### Avoid unnecessary refactoring

Do not:

- Rewrite an entire component
- Replace a framework
- Replace a library without reason
- Change application architecture
- Introduce a new design pattern unnecessarily
- Rewrite working business logic
- Reorganize the entire repository for aesthetics

The goal is:

> **Cleaner code, not different code.**

---

# Phase 9 — Frontend & UI Preservation

For frontend projects, preserve the existing user experience.

Do not intentionally change:

- Layout
- Visual design
- Typography
- Colors
- Spacing
- Responsive behavior
- Animations
- Interactions
- Navigation
- Accessibility behavior
- Component behavior

Do not redesign the application.

If cleanup requires modifying a UI component, preserve its observable behavior.

Before removing a frontend component, verify:

- It is not imported elsewhere.
- It is not dynamically referenced.
- It is not used through routing conventions.
- It is not required by a page or layout.
- It is not used by an external integration.

---

# Phase 10 — API, Backend & Database Safety

Be especially conservative with backend code.

Do not delete:

- API routes
- server actions
- database migrations
- database schemas
- seed files
- authentication logic
- middleware
- background jobs
- webhook handlers
- scheduled jobs

unless their usage has been confidently established as obsolete.

Pay attention to functionality that may be consumed externally.

A route with no internal references may still be used by:

- a mobile application
- another frontend
- a third-party integration
- a webhook
- an automation
- an external client

When external usage cannot be ruled out:

> Preserve the code and flag it for review.

---

# Phase 11 — Asset Cleanup

Inspect assets such as:

- Images
- Icons
- Fonts
- SVGs
- Videos
- Static files
- Localization files

Identify obvious unused assets.

Before deleting an asset, search for references across:

- source code
- stylesheets
- configuration
- metadata
- HTML
- documentation
- dynamic paths

Be particularly careful with assets referenced through dynamically constructed paths.

If usage cannot be confidently determined:

> Do not delete the asset.

---

# Phase 12 — Performance Sanity Check

Perform only low-risk performance cleanup.

Look for obvious problems such as:

- Unnecessary large dependencies
- Duplicate data fetching
- Unnecessary client-side code
- Obviously unused JavaScript
- Duplicate assets
- Development tooling accidentally included in production
- Redundant network requests
- Obviously unnecessary renders

Do not perform speculative optimization.

Do not change behavior merely to achieve theoretical performance improvements.

---

# Phase 13 — Repository Hygiene

Inspect version-control state.

Check:

- Modified files
- Untracked files
- Ignored files
- Generated artifacts
- Temporary files
- Large accidental files
- Secrets
- Incorrect `.gitignore` entries

Ensure that obvious local/build artifacts are appropriately ignored.

Do not automatically:

- commit
- push
- create a pull request
- rewrite Git history

The developer should retain control over those actions unless explicitly requested.

---

# Phase 14 — Documentation

Review project documentation.

Pay attention to:

- README
- Setup instructions
- Environment variables
- Build commands
- Deployment instructions
- Architecture documentation

Only update documentation when cleanup changes something that makes the documentation incorrect.

Do not create unnecessary documentation.

---

# Phase 15 — Validate Everything

After cleanup, run the project's appropriate validation commands.

Depending on the project, this may include:

```text
Lint
Type checking
Unit tests
Integration tests
End-to-end tests
Build
Package validation
Migration validation
```

Use the project's existing tooling.

Do not invent commands that the project does not support.

### If validation fails

Determine whether the failure:

1. Existed before cleanup.
2. Was caused by cleanup.
3. Is unrelated infrastructure/tooling failure.

If cleanup caused the failure:

> Fix the regression before finishing.

Do not hide failures.

Do not simply remove validation commands to make the project appear healthy.

---

# Phase 16 — Final Audit

Perform one final pass over the project.

Verify:

## Code

- No obvious dead code remains.
- No accidental deletions occurred.
- No temporary debugging artifacts remain.
- No unnecessary commented-out code remains.
- No obvious duplicate implementation remains.

## Dependencies

- Obvious unused dependencies are removed.
- Dependency manifests are consistent.
- Lockfiles are synchronized.

## Security

- No obvious secrets are exposed.
- Environment configuration is appropriate.
- Sensitive files are not accidentally tracked.

## Configuration

- Obsolete configuration is removed where safe.
- Build configuration remains functional.
- Deployment configuration remains functional.

## Repository

- Temporary artifacts are removed or ignored.
- Git status contains only intentional changes.
- No unrelated files were modified.

## Validation

- Linting passes where applicable.
- Type checking passes where applicable.
- Tests pass where applicable.
- Production build passes where applicable.

---

# Uncertainty Policy

When uncertain, **do not delete**.

Classify questionable items as:

```text
SAFE TO REMOVE
LIKELY UNUSED — REVIEW
REQUIRED
UNKNOWN
```

Only automatically remove items in the first category.

Examples of things that commonly require manual review:

- Dynamically imported modules
- Public API routes
- Webhook handlers
- Database migrations
- Environment variables
- Generated code
- Reflection-based code
- External integrations
- Framework convention files
- Dynamically referenced assets
- Scripts used by external CI/CD systems

---

# Change Discipline

Keep the cleanup focused.

Do not modify files unrelated to cleanup.

Do not introduce unrelated features.

Do not fix unrelated bugs unless:

- they are security-critical, or
- they directly prevent production validation.

If you discover unrelated problems, report them instead of expanding the scope.

---

# Final Report

After completing the cleanup, provide a concise final report.

Use this structure:

## Clean-Up Summary

### Removed

List:

- Removed files
- Removed components
- Removed dead code
- Removed dependencies
- Removed temporary artifacts

### Modified

List:

- Modified files
- Configuration changes
- Code-quality improvements
- Documentation updates

### Security

Report:

- Secret findings
- Environment configuration findings
- Sensitive-file findings

Never reveal actual secret values.

### Validation

Use:

```text
Lint: PASS / FAIL / SKIPPED
Typecheck: PASS / FAIL / SKIPPED
Tests: PASS / FAIL / SKIPPED
Build: PASS / FAIL / SKIPPED
```

For failures, provide the relevant reason.

### Manual Review Required

List anything that appeared potentially unused but could not be safely removed.

Explain briefly why it was preserved.

### Production Readiness

Choose exactly one:

```text
READY
READY WITH WARNINGS
NOT READY
```

Then provide a short explanation.

---

# Definition of Done

The cleanup is complete when:

- The project has been thoroughly inspected.
- Obvious dead code has been removed.
- Safe unused dependencies have been removed.
- Unnecessary files and artifacts have been cleaned.
- Debug/development leftovers have been addressed.
- Security-sensitive configuration has been reviewed.
- Obsolete configuration has been cleaned where safe.
- Existing functionality has been preserved.
- Validation has been performed.
- Cleanup-related regressions have been fixed.
- Remaining uncertainties have been documented.
- The repository is in a reasonable production-ready state.

The final objective is not to make the codebase as small as possible.

The objective is:

> **Make the completed project clean, maintainable, secure, and production-ready without breaking what already works.**
