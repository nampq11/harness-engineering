<!-- Template: Replace [bracketed placeholders] with your project details -->

# CLAUDE.md

[Project Name] — a [brief one-line description of what this is, built with, and its purpose].

## Project map

- `src/` — Application source code
- `tests/` — Test files mirroring src structure
- `scripts/` — Enforcement and documentation scripts
- `docs/` — Topic-specific documentation

<important if="you need to run commands to build, test, lint, or generate code">

### Development
```bash
npm start                    # Run the application
npm run dev                  # Development mode with hot reload
npm run build                # Production build
npm run lint                 # Run linter
```

### Testing
```bash
npm test                           # Unit tests
npm run test:integration           # Integration tests
npm run test:all                   # All tests (used by pre-push hook)
npm test tests/some-file.test.js   # Single file (preferred during dev)
npm test -- --coverage             # Coverage report
```

### Enforcement
```bash
node scripts/check-secrets.js        # Scan staged files for secrets
node scripts/check-file-sizes.js     # Check staged files against 300-line limit
node scripts/generate-docs.js        # Regenerate auto sections in CLAUDE.md
node scripts/generate-docs.js --check # Verify auto sections are current (CI mode)
node scripts/validate-docs.js        # Pre-commit: warn if CLAUDE.md may need update
node scripts/validate-docs.js --full # Full: compare CLAUDE.md against codebase
```
</important>

## Architecture

```
┌─────────────────────────────────────────────────┐
│                   [Your App]                     │
│                      |                           │
│          ┌───────────┼───────────┐               │
│          |           |           |               │
│          v           v           v               │
│     [Layer 1]   [Layer 2]   [Layer 3]           │
└─────────────────────────────────────────────────┘
```

Data flow: `User action → [Entry point] → [Service layer] → [Data layer] → Response`

<!-- AUTO:tree -->
src/
├── index.js           # Application entry point
├── routes/
│   ├── api.js         # API route definitions
│   └── auth.js        # Authentication routes
├── services/
│   ├── user.js        # User business logic
│   └── billing.js     # Billing service
└── utils/
    ├── logger.js       # Structured logger
    └── validators.js   # Input validation helpers
<!-- /AUTO:tree -->

<!-- AUTO:modules -->
| Module | Purpose | Key Exports |
|--------|---------|-------------|
| `index.js` | Application entry point | `start()`, `stop()` |
| `services/user.js` | User business logic | `createUser()`, `findUser()`, `updateUser()` |
<!-- /AUTO:modules -->

<important if="you are creating or modifying files">

### File size limits (hard limits)
- Any file: 300 lines max
- Any function: 50 lines max
- If exceeded, MUST refactor immediately
</important>

<important if="you are adding, removing, or renaming files in src/, bin/, or scripts/">

### Documentation sync (hard rule)
Any commit that adds, removes, or renames files in these directories MUST include a CLAUDE.md update in the same commit. The pre-commit hook will warn if CLAUDE.md is not staged alongside tracked file changes.
</important>

<important if="you are writing or modifying code">

### Complexity red flags
STOP and refactor immediately if you see:
- **>5 nested if/else statements** → Extract to separate functions
- **>3 try/catch blocks in one function** → Split error handling
- **>10 imports** → Consider splitting the module
- **Duplicate logic** → Extract to shared utilities

```bash
# Monitor file sizes
find src -name "*.js" -exec wc -l {} + | sort -n
```
</important>

<important if="you are committing or pushing code">

### Git hooks (managed by husky)

**pre-commit** (fast, <2s): lint-staged → secret scan → file size check → doc generation → doc drift warning

**pre-push** (thorough): `npm run test:all` (unit + integration, SHA-cached) → `npm audit` (warn-only)

Test caching: `.test-passed` stores SHA of last successful test run. If HEAD matches, tests are skipped.
</important>

<important if="you are adding logging or output">

Use centralized logger module, not `console.log`. Route logs to stderr if stdout is used for program output. See `src/utils/logger.js`.
</important>

<important if="you are writing or modifying code">

### Language standards
- Use modern language features and idioms
- Enforce consistent style via linter configuration (see `.eslintrc.js`)
- Use doc comments for all public APIs
</important>

<important if="you encounter unexpected errors or silent failures">

## Critical gotchas

<!-- TIP: Document non-obvious things that cause silent failures or confusing errors. -->

- **[Gotcha 1]**: [Brief explanation of the trap and the correct approach]
- **[Gotcha 2]**: [Brief explanation of the trap and the correct approach]
</important>

## Docs map

| Topic | File |
|-------|------|
| API reference and CLI commands | `docs/usage.md` |
| Testing strategy and patterns | `docs/testing.md` |
| Configuration and environment variables | `docs/configuration.md` |
| Troubleshooting common issues | `docs/troubleshooting.md` |

---

Auto-generated sections (`<!-- AUTO:name -->`) are maintained by `scripts/generate-docs.js`. Do NOT edit by hand.
