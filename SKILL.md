# Memory Management Skill for Claude Code

> Add this to your project's CLAUDE.md to optimize how Claude manages its native auto-memory.

---

## Core Principle

**MEMORY.md is an INDEX, not a dump.**

The first 200 lines of MEMORY.md are loaded into the system prompt at session start. Everything beyond line 200 is invisible until manually read. Topic files are never auto-loaded—Claude must read them on-demand.

**Rule: MEMORY.md must NEVER exceed 200 lines.**

---

## Memory Architecture

```
~/.claude/projects/<project>/memory/
├── MEMORY.md              # Index only (< 200 lines)
├── debugging.md           # Bug solutions, error patterns
├── architecture.md        # System design, module relationships
├── patterns.md            # Code conventions, style decisions
├── commands.md            # Build, test, deploy commands
├── gotchas.md             # Known issues, workarounds
├── dependencies.md        # Package notes, version constraints
└── decisions.md           # Why we chose X over Y
```

---

## MEMORY.md Template

```markdown
# Project Memory Index
<!-- LINE COUNT: Keep under 200 lines -->

## Quick Commands
- Dev: `[command]`
- Test: `[command]`
- Build: `[command]`
- Deploy: See →debugging.md

## Key Entry Points
- Main: `[path]`
- Config: `[path]`
- Types: `[path]`

## Topic Pointers
- Debugging solutions → `debugging.md`
- Architecture notes → `architecture.md`
- Code patterns → `patterns.md`
- Known issues → `gotchas.md`

## Active Context
- Current work: [brief description]
- Blocked by: [if any]
- Next: [priority items]

## Core Patterns (only critical ones)
- [Pattern 1]: [one-line description]
- [Pattern 2]: [one-line description]
```

---

## Memory Operations

### When to Write to MEMORY.md (Index)
- New critical command discovered
- Key file location identified
- New topic file created (add pointer)
- Major project pattern established

### When to Write to Topic Files
- Bug solution found → `debugging.md`
- Architecture decision made → `architecture.md`
- Code convention established → `patterns.md`
- Gotcha/workaround discovered → `gotchas.md`
- Dependency note needed → `dependencies.md`

### Topic File Format
```markdown
## [Topic/Date]
**Context:** When this applies
**Problem:** What went wrong
**Solution:** What fixed it
**Command:** `[if applicable]`
```

---

## Line Count Enforcement

Before writing to MEMORY.md:
```bash
wc -l ~/.claude/projects/*/memory/MEMORY.md
```

If approaching 200 lines:
1. Identify detailed entries that belong in topic files
2. Move content to appropriate topic file
3. Replace with pointer: `→ See [topic].md`
4. Verify line count < 200

---

## Grep Optimization

### Fast Memory Search
```bash
# Search all memory files for a term
grep -r "search_term" ~/.claude/projects/<project>/memory/

# Search with context
grep -B2 -A2 "error" ~/.claude/projects/<project>/memory/debugging.md

# Find which file contains a memory
grep -l "redis" ~/.claude/projects/<project>/memory/*.md
```

### Before Reading Topic Files
Instead of reading entire files, grep first:
```bash
# Find relevant section
grep -n "auth" debugging.md
# Then read specific lines
sed -n '15,30p' debugging.md
```

### Memory Audit
```bash
# Line counts across all memory files
wc -l ~/.claude/projects/<project>/memory/*.md

# Find largest files (candidates for splitting)
ls -lS ~/.claude/projects/<project>/memory/
```

---

## Recall Patterns

### Start of Session
MEMORY.md is already in context. For deeper info:
```
"What do I know about [topic]?"
→ grep topic files
→ read relevant sections only
```

### Mid-Session Recall
```bash
# Quick search before reading
grep -l "keyword" *.md
# Read only matching file
```

### Cross-Reference
When documenting, link related topics:
```markdown
## Auth Fix (2024-02-26)
**Solution:** Reset Redis connection pool
**Related:** See →gotchas.md#redis-timeouts
```

---

## Memory Hygiene

### Weekly Audit
1. Check MEMORY.md line count
2. Review topic files for outdated content
3. Consolidate duplicate entries
4. Update pointers if files renamed

### Pruning Rules
- Remove entries older than 90 days if not referenced
- Merge similar entries
- Delete solved gotchas that are now fixed in code
- Archive completed project phases

### Archive Pattern
```markdown
## [ARCHIVED] Old Feature
<!-- Kept for historical reference, low priority -->
```

---

## Anti-Patterns (Avoid)

❌ Dumping everything into MEMORY.md
❌ Exceeding 200 lines in MEMORY.md
❌ Storing code snippets (use file paths instead)
❌ Duplicate entries across files
❌ Reading entire topic files when grep suffices
❌ Forgetting to add pointers for new topic files

---

## Quick Reference

| Action | Location | Format |
|--------|----------|--------|
| Add command | MEMORY.md | `- Name: \`cmd\`` |
| Add file path | MEMORY.md | `- Role: \`path\`` |
| Add bug fix | debugging.md | Full context block |
| Add pattern | patterns.md | Convention + example |
| Add gotcha | gotchas.md | Problem + workaround |
| Add decision | decisions.md | Options + rationale |

---

## Explicit Save Commands

Tell Claude directly:
- "Remember that we use pnpm, not npm"
- "Save to debugging.md: auth breaks if Redis is cold"
- "Add to patterns.md: all API routes use zod validation"
- "Update MEMORY.md: new deploy command is X"

---

*This skill ensures Claude maintains efficient, organized memory that loads fast and stays under the 200-line system prompt limit.*
