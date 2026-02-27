---
description: Optimizes Claude's native auto-memory management
---

# Memory Management

## Core Rule

MEMORY.md is an INDEX, not a dump. Keep it under 200 lines at all times.

## Architecture

```
memory/
├── MEMORY.md        ← Index only (< 200 lines, auto-loaded)
├── debugging.md     ← Bug solutions (read on-demand)
├── architecture.md  ← System design (read on-demand)
├── patterns.md      ← Code conventions (read on-demand)
└── gotchas.md       ← Known issues (read on-demand)
```

## Writing Rules

### To MEMORY.md (Index)
- Commands: `- Dev: \`pnpm dev\``
- Paths: `- Entry: \`src/index.ts\``
- Pointers: `→ See debugging.md`
- Max 200 lines total

### To Topic Files
- Bug fix discovered → debugging.md
- Pattern established → patterns.md
- Gotcha found → gotchas.md
- Decision made → architecture.md

## Reading Rules

Grep before reading full files:
```bash
grep -n "keyword" debugging.md
sed -n '10,20p' debugging.md
```

## Line Count Check

Before adding to MEMORY.md:
```bash
wc -l MEMORY.md
```

If > 180 lines: move content to topic files first.

## Format for Topic Entries

```markdown
## [Topic] - [Date]
**Context:** When this applies
**Problem:** What happened
**Solution:** What fixed it
```
