# Before & After

## Before

A completed project may contain:

- Unused components
- Debugging statements
- Unused dependencies
- Old experimental files
- Temporary screenshots
- Obsolete configuration
- Build artifacts

Example:

```text
src/
├── components/
│   ├── Navbar.tsx
│   ├── Footer.tsx
│   ├── OldDashboard.tsx
│   ├── TestComponent.tsx
│   └── DebugPanel.tsx
├── utils/
│   ├── api.ts
│   ├── oldApi.ts
│   ├── debug.ts
│   └── tempHelper.ts
├── pages/
│   ├── index.tsx
│   ├── dashboard.tsx
│   └── test-page.tsx
├── assets/
│   ├── logo.png
│   ├── screenshot-old.png
│   └── temp-image.jpg
└── scripts/
    ├── build.js
    └── old-deploy.sh

package.json (with 15 unused dependencies)
```

## After

After a safe cleanup:

```text
src/
├── components/
│   ├── Navbar.tsx
│   └── Footer.tsx
├── utils/
│   └── api.ts
├── pages/
│   ├── index.tsx
│   └── dashboard.tsx
└── assets/
    └── logo.png

package.json (only necessary dependencies)
```

## What Got Removed

### Files
- `OldDashboard.tsx` — Verified unused, replaced by current dashboard
- `TestComponent.tsx` — Development test component, no production usage
- `DebugPanel.tsx` — Debug-only component with no references
- `oldApi.ts` — Deprecated API client, replaced by current api.ts
- `debug.ts` — Development utilities, console.log helpers
- `tempHelper.ts` — Temporary utility with no references
- `test-page.tsx` — Development test page, not in production routes
- `screenshot-old.png` — Old documentation screenshot
- `temp-image.jpg` — Temporary asset with no references
- `old-deploy.sh` — Obsolete deployment script

### Dependencies
- Removed 15 unused npm packages that were left behind from removed features
- Kept all dependencies that are actually used in the codebase

## Important Principle

The important principle is that files are only removed when the agent has enough evidence that they are actually unused.

For example:

### ✅ Safe to Remove
```typescript
// Component with no imports anywhere
export function UnusedComponent() {
  return <div>Never used</div>
}
```

### ⚠️ Preserve for Review
```typescript
// API route that might be used externally
export async function POST(req: Request) {
  // No internal references, but external client might use it
  return Response.json({ status: 'ok' })
}
```

### ✅ Safe to Remove
```typescript
// Obvious debug code
console.log('DEBUG: user data', user)
debugger
```

### ⚠️ Preserve for Review
```typescript
// Intentional error logging
console.error('Payment processing failed:', error)
```

## Real-World Example

### Before Cleanup

**package.json**
```json
{
  "dependencies": {
    "react": "^18.0.0",
    "axios": "^1.0.0",
    "lodash": "^4.17.21",
    "moment": "^2.29.4",
    "jquery": "^3.6.0",
    "redux": "^4.2.0",
    "old-ui-library": "^1.0.0"
  }
}
```

**src/utils/debug.ts**
```typescript
export function debugLog(msg: string) {
  console.log('[DEBUG]', msg)
  alert(msg) // Debug alerts
}

export function logEverything(data: any) {
  console.log(JSON.stringify(data, null, 2))
}
```

### After Cleanup

**package.json**
```json
{
  "dependencies": {
    "react": "^18.0.0",
    "axios": "^1.0.0"
  }
}
```

**src/utils/debug.ts** — File removed completely

### What Happened

1. **Searched** the entire codebase for usage
2. **Verified** that `moment`, `lodash`, `jquery`, `redux`, and `old-ui-library` had no references
3. **Confirmed** that `debug.ts` was only imported in removed development files
4. **Validated** that the project still builds and runs correctly
5. **Documented** all changes in the cleanup report

---

This example demonstrates the difference between:

- **Aggressive cleanup** — Delete everything that looks unused
- **Safe cleanup** — Delete only what is proven unused

Clean-Up always chooses the latter.
