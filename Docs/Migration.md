# Migration Guide

Migrate from folders, tags, or frontmatter to the MOC system.

## Why Migrate

**Problems with traditional systems:**
- Folders force single locations
- Tags become inconsistent
- Frontmatter requires special tools

**MOC advantages:**
- Notes can belong to multiple categories
- Organization emerges from links
- No maintenance overhead

## Pre-Migration

### 1. Back Up Vault
- Copy entire vault folder
- Use version control if available
- Consider testing in duplicate vault

### 2. Install Dataview
- Settings → Community plugins → Browse
- Search and install Dataview
- Enable JavaScript queries in settings

### 3. Analyze Current Structure
Document in a planning note:
- Main folder categories
- Frequently used tags
- Existing index/hub notes
- Notes needing multiple categories

## Phase 1: Plan MOCs

### Identify Categories
Start with broad categories:
- Technology
- Projects
- Learning
- Resources
- Personal

Don't over-categorize - you can split MOCs later when needed.

### Map Content
Create a simple mapping:
```
Current Folder → Target MOC
/Work/Projects → Projects MOC
/Tech/Programming → Technology MOC
/Learning/* → Learning MOC
```

## Phase 2: Create MOCs

### Create Structure
```
MOCs/
├── Technology MOC.md
├── Projects MOC.md
├── Learning MOC.md
└── Resources MOC.md
```

### MOC Template
```markdown
# [Name] MOC

[Description of scope and purpose]

## All notes

\`\`\`dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
\`\`\`
```

### Specialized Sections
For Projects MOC:
```markdown
## Active projects

\`\`\`dataview
LIST
FROM [[]]
WHERE contains(file.content, "#status/active")
SORT file.mtime DESC
\`\`\`

## Completed

\`\`\`dataview
LIST
FROM [[]]
WHERE contains(file.content, "#status/complete")
SORT created DESC
\`\`\`
```

## Phase 3: Migrate Notes

### Add MOC Links
Add to each note:
```markdown
---
MOCs: [[MOCs/Technology MOC|Technology]], [[MOCs/Projects MOC|Projects]]
```

### Batch Processing
For large vaults, use search/replace:
1. Search: `tags: [technology]`
2. Add MOC link after content
3. Consider scripting for thousands of notes

### Flatten Folders (Optional)
After adding MOC links:
1. Create `Notes/` folder
2. Move all notes there
3. Obsidian updates links automatically

## Phase 4: Verify

### Find Orphaned Notes
Create `MOCs/Orphaned Notes.md`:
```markdown
# Orphaned Notes

Notes without MOC links.

\`\`\`dataview
LIST
FROM "Notes"
WHERE !file.outlinks OR 
      !filter(file.outlinks, x => contains(x.path, "MOCs/"))
SORT file.mtime DESC
\`\`\`
```

### Test Queries
- Check each MOC shows expected notes
- Verify multi-MOC notes appear correctly
- Test performance with many notes

## Migration Strategies

### Gradual Migration
- Run MOC and folders in parallel
- Migrate high-value notes first
- Expand coverage over time

### Complete Migration
1. Create all MOCs upfront
2. Bulk-add MOC links
3. Flatten folders
4. Remove obsolete metadata

### Hybrid Approach
- Keep folders for archives/references
- Use MOCs for active knowledge
- Maintain tags during transition

## Post-Migration

### Maintenance
- Weekly: Check orphaned notes
- Monthly: Review MOC structure
- Create templates with MOC sections

### MOC Index
Create overview of all MOCs:
```markdown
# MOC Index

## Knowledge Areas
- [[MOCs/Technology MOC|Technology]]
- [[MOCs/Projects MOC|Projects]]
- [[MOCs/Learning MOC|Learning]]
```

## Timeline

- Small vault (< 500 notes): 2-4 hours
- Medium vault (500-2000): 1-2 days
- Large vault (2000+): 3-5 days

The investment pays off through eliminated maintenance overhead.