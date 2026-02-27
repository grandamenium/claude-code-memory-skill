# Memory Management Instructions

## Auto-Memory Strategy

**CRITICAL: MEMORY.md must stay under 200 lines.** Only the first 200 lines are loaded at session start.

### Structure

Use MEMORY.md as an INDEX with pointers to topic files:

```
memory/
├── MEMORY.md        # Index only (< 200 lines)
├── debugging.md     # Bug solutions
├── architecture.md  # System design
├── patterns.md      # Code conventions
├── commands.md      # Build/test/deploy
└── gotchas.md       # Known issues
```

### MEMORY.md Rules

1. **Index only**: Quick commands, key paths, pointers to topics
2. **No details**: Move explanations to topic files
3. **Line check**: Run `wc -l MEMORY.md` before adding content
4. **Pointers**: Use `→ See debugging.md` format

### Topic File Rules

1. **Categorize**: Put bug fixes in debugging.md, patterns in patterns.md
2. **Format**: Include Context, Problem, Solution for each entry
3. **Cross-reference**: Link related entries across files

### Before Writing to MEMORY.md

```bash
# Check line count
wc -l ~/.claude/projects/*/memory/MEMORY.md
```

If over 180 lines, move content to topic files first.

### Grep Before Reading

```bash
# Search before loading full file
grep -n "search_term" debugging.md
# Read only relevant lines
sed -n '10,20p' debugging.md
```

### When to Save Where

| Content Type | Location |
|--------------|----------|
| Commands | MEMORY.md |
| File paths | MEMORY.md |
| Bug solutions | debugging.md |
| Code patterns | patterns.md |
| Workarounds | gotchas.md |
| Architecture | architecture.md |

### Explicit Commands I Understand

- "Remember that [fact]" → Add to appropriate location
- "Save to debugging.md: [content]" → Add to debugging.md
- "Check memory for [topic]" → Grep and read relevant sections
- "Audit memory" → Check line counts and suggest cleanup
