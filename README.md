# Memory Management Skill for Claude Code

Teach Claude Code how to efficiently manage its native auto-memory feature.

## The Problem

Claude Code's auto-memory only loads the first **200 lines** of `MEMORY.md` at session start. If Claude dumps everything into one file, most context is invisible when you start working.

## The Solution

This skill instructs Claude to:
1. Keep `MEMORY.md` as a concise **index** (< 200 lines)
2. Segment detailed notes into **topic files** (debugging.md, patterns.md, etc.)
3. Use **pointers** in MEMORY.md to reference topic files
4. Use **grep** before reading entire files
5. Maintain **memory hygiene** with regular audits

## Installation

### Option 1: Add to Project CLAUDE.md

Copy the contents of `CLAUDE-SNIPPET.md` into your project's `CLAUDE.md` or `.claude/CLAUDE.md`.

### Option 2: Add as Rule File

Copy `memory-management-rule.md` to your project's `.claude/rules/` directory.

### Option 3: User-Level (All Projects)

Add to `~/.claude/CLAUDE.md` to apply across all your projects.

## Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Full documentation and reference |
| `CLAUDE-SNIPPET.md` | Copy-paste snippet for CLAUDE.md |
| `memory-management-rule.md` | Ready-to-use rule file |
| `MEMORY-TEMPLATE.md` | Starter template for MEMORY.md |

## Key Concepts

- **200-line limit**: Only first 200 lines of MEMORY.md are in system prompt
- **Topic files**: debugging.md, patterns.md, etc. are read on-demand
- **Pointers**: MEMORY.md points to topic files with `→ See file.md`
- **Grep first**: Search before reading to minimize context usage

## Example MEMORY.md Structure

```markdown
# Project Index

## Commands
- Dev: `pnpm dev`
- Test: `pnpm test`

## Files
- Entry: `src/index.ts`
- Config: `src/config.ts`

## Topics
→ debugging.md (bug fixes)
→ patterns.md (conventions)
→ gotchas.md (known issues)

## Active Work
- Building auth flow
```

## Credits

Created for the [Agent Architects](https://skool.com/agent-architects) community.
