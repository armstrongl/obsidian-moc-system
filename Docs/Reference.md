# Technical Reference

Complete MOC system documentation.

## System Components

### MOC Structure
```markdown
# [Name] MOC

[Description]

\`\`\`dataview
[Query]
\`\`\`
```

### Note Structure
```markdown
# Note Title

[Content]

---
MOCs: [[MOCs/Primary MOC|Primary]], [[MOCs/Secondary MOC|Secondary]]
```

### Link Formats
```markdown
[[Technology MOC]]                           # Basic
[[MOCs/Technology MOC]]                      # Full path
[[MOCs/Technology MOC|Technology]]           # Aliased (recommended)
[[MOCs/Technology MOC#Web Development]]      # Section-specific
```

## Dataview Queries

### Basic Backlink Query
```dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
```

### Table View
```dataview
TABLE file.mtime as "Modified", file.size as "Size"
FROM [[]]
SORT file.mtime DESC
```

### Filtered Query
```dataview
LIST
FROM [[]]
WHERE contains(file.content, "#status/active")
  AND file.mtime >= date(today) - dur(7d)
SORT file.mtime DESC
```

### JavaScript Queries

**Group by month:**
```dataviewjs
const pages = dv.pages([[]]);
const groups = {};

for (const page of pages) {
    const month = page.file.mtime.toFormat("yyyy-MM");
    if (!groups[month]) groups[month] = [];
    groups[month].push(page);
}

for (const [month, monthPages] of Object.entries(groups).sort().reverse()) {
    dv.header(3, month);
    dv.list(monthPages.map(p => p.file.link));
}
```

**Find shared MOCs:**
```dataviewjs
const targetMOCs = ["MOCs/Technology MOC", "MOCs/Projects MOC"];
const pages = dv.pages("")
    .where(p => {
        const links = p.file.outlinks.map(l => l.path);
        return targetMOCs.every(moc => links.includes(moc + ".md"));
    });

dv.list(pages.map(p => p.file.link));
```

**Section-specific backlinks:**
```dataviewjs
const targetHeading = "Python";
const currentFile = dv.current().file;
const pathWithoutMd = currentFile.path.replace('.md', '');

let foundPages = [];
for (const page of dv.pages()) {
    const content = await dv.io.load(page.file.path);
    if (content && content.includes(`${pathWithoutMd}#${targetHeading}`)) {
        foundPages.push(page);
    }
}

dv.list(foundPages.map(p => p.file.link));
```

## Query Operators

### FROM Clause
```dataview
FROM [[]]                    # Backlinks
FROM outgoing([[]])          # Outgoing links
FROM "Folder"                # Specific folder
FROM #tag                    # Tagged notes
FROM [[]] AND "Folder"       # Combined
```

### WHERE Operators
```dataview
WHERE contains(file.name, "Project")
WHERE file.size > 1000
WHERE file.mtime >= date(today) - dur(7d)
WHERE length(file.outlinks) > 5
WHERE !contains(file.path, "Archive")
```

### SORT Options
```dataview
SORT file.mtime DESC         # Modified (newest)
SORT file.ctime ASC          # Created (oldest)
SORT file.name               # Alphabetical
SORT length(file.outlinks)   # Link count
```

### Display Formats
```dataview
LIST                         # Bullet list
TABLE col1, col2             # Table view
TASK                         # Extract tasks
CALENDAR file.mtime          # Calendar view
```

## Folder Structure

### Required
- `MOCs/` - Contains all MOCs

### Optional
- `Notes/` - Flat note storage
- `Inbox/` - Uncategorized captures
- `Archive/` - Completed notes
- `Templates/` - Note templates
- `_System/` - Configuration

## Troubleshooting

### Notes Not Appearing

1. **Check link format** - Path and capitalization must be exact
2. **Review WHERE clause** - May be filtering out notes
3. **Verify Dataview** - Plugin enabled, JavaScript enabled

### Performance Issues

1. **Limit scope:** `FROM [[]] AND "Notes"`
2. **Add limits:** `LIMIT 20`
3. **Use simple queries** when possible
4. **Split large MOCs** into smaller ones

### Orphaned Notes Query
```dataview
LIST
FROM "Notes"
WHERE !file.outlinks OR 
      !filter(file.outlinks, x => contains(x.path, "MOCs/"))
SORT file.mtime DESC
```

## DataviewJS API

### Core Objects
- `dv` - Main API object
- `dv.current()` - Current file
- `dv.pages(source)` - Query pages
- `dv.page(path)` - Get specific page

### Query Methods
- `pages.where(predicate)` - Filter
- `pages.sort(field, order)` - Sort
- `pages.limit(n)` - Limit
- `pages.map(transform)` - Transform

### Display Methods
- `dv.list(items)` - Render list
- `dv.table(headers, rows)` - Render table
- `dv.paragraph(text)` - Render text
- `dv.header(level, text)` - Render header

### File Operations
- `dv.io.load(path)` - Read file
- `await dv.io.load(path)` - Async read

### Utilities
- `dv.date(string)` - Parse dates
- `dv.duration(string)` - Parse durations
- `dv.compare(a, b)` - Compare values