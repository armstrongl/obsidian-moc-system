# Quick Start Guide

Get the MOC system running in under 10 minutes.

## Prerequisites

- **Obsidian** - Any recent version
- **Dataview plugin** - Install from Community Plugins
  - Enable JavaScript queries in settings

## Step 1: Create First MOC

1. Create `MOCs/` folder in vault root
2. Create `MOCs/Technology MOC.md`:

```markdown
# Technology MOC

Technology-related notes, auto-updating via backlinks.

## All technology notes

\`\`\`dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/") AND !contains(file.path, "Inbox/")
SORT file.mtime DESC
\`\`\`
```

**Query breakdown:**
- `FROM [[]]` - Finds backlinks to this MOC
- `WHERE` - Filters out system folders
- `SORT` - Shows recent notes first

## Step 2: Link Notes to MOCs

Create `Docker basics.md`:

```markdown
# Docker basics

Docker is a containerization platform that packages applications with dependencies.

## Key concepts

Containers are lightweight packages. Images are container blueprints.

---
MOCs: [[MOCs/Technology MOC|Technology MOC]]
```

The MOC link at the bottom makes this note appear in Technology MOC automatically.

## Step 3: View Results

Open Technology MOC in reading mode - your Docker note appears instantly. No manual updates needed.

## Step 4: Multiple MOCs

Create `MOCs/Learning MOC.md`:

```markdown
# Learning MOC

Learning and education notes.

## Recent (10)

\`\`\`dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
LIMIT 10
\`\`\`

## All learning notes

\`\`\`dataview
TABLE file.mtime as "Modified"
FROM [[]]
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
\`\`\`
```

## Step 5: Multi-Category Notes

Update Docker basics to link both MOCs:

```markdown
---
MOCs: [[MOCs/Technology MOC|Technology MOC]], [[MOCs/Learning MOC|Learning MOC]]
```

The note now appears in both MOCs without duplication.

## Next Steps

- **Create MOCs** for your main areas (Projects, Reading, Research)
- **Add templates** with MOC sections for consistent linking
- **Link existing notes** to bring them into the system

## Resources

- [Migration Guide](./Migration.md) - Organize existing notes
- [Tips & Best Practices](./Tips.md) - Advanced techniques
- [Reference Guide](./Reference.md) - Technical details
- [Philosophy](./Philosophy.md) - System principles

## Success Indicators

✓ Notes appear in MOCs immediately after linking
✓ Find notes through multiple organizational lenses
✓ Zero folder maintenance required
✓ Knowledge network grows organically