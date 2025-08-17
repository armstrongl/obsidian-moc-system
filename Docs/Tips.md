# Tips and Best Practices

Advanced techniques for the MOC system.

## MOC Design Patterns

### Hierarchical MOCs
Parent-child relationships without rigid constraints:

```markdown
# Programming MOC

Part of [[MOCs/Technology MOC|Technology MOC]].

## Language MOCs
- [[MOCs/Python MOC|Python]]
- [[MOCs/JavaScript MOC|JavaScript]]

## All notes
\`\`\`dataview
LIST FROM [[]]
\`\`\`
```

### Cross-Referenced MOCs
Acknowledge intersecting domains:

```markdown
## Related MOCs
- [[MOCs/Skills MOC|Skills]] - Skills from projects
- [[MOCs/Learning MOC|Learning]] - Learning outcomes
- [[MOCs/Resources MOC|Resources]] - Tools used
```

### Specialized MOCs
Dynamic dashboards for specific workflows:

```markdown
# Daily Review MOC

## Today's work
\`\`\`dataview
LIST
FROM ""
WHERE file.mtime >= date(today)
SORT file.mtime DESC
\`\`\`
```

## Query Optimization

### Performance Tips
```dataview
LIST
FROM [[]] AND "Notes"    # Limit scope
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
LIMIT 20                  # Limit results
```

### Advanced Filtering
```dataviewjs
const pages = dv.pages([[]])
    .where(p => {
        const content = p.file.content || "";
        return content.includes("#status/active") &&
               p.file.mtime >= dv.date("2024-01-01");
    });
dv.list(pages.map(p => p.file.link));
```

### Custom Sorting
```dataviewjs
const pages = dv.pages([[]])
    .sort(p => {
        const priority = p.priority || 999;
        return [priority, -p.file.mtime.ts];
    });
dv.table(["Note", "Priority", "Modified"],
    pages.map(p => [
        p.file.link,
        p.priority || "—",
        p.file.mtime.toFormat("yyyy-MM-dd")
    ])
);
```

## Workflow Enhancements

### Templates
Use Templater for automatic MOC links:

```markdown
---
MOCs: <% tp.file.folder() == "Projects" ? 
       "[[MOCs/Projects MOC|Projects]]" : 
       "[[MOCs/Notes MOC|Notes]]" %>
```

### Quick Capture
Inbox for uncategorized notes:

```markdown
# Inbox MOC

\`\`\`dataview
LIST FROM "Inbox"
SORT file.ctime DESC
\`\`\`
```

### Review Process
Weekly template:
```markdown
# Weekly Review
- [ ] Check orphaned notes
- [ ] Review new notes for MOCs
- [ ] Update project status
- [ ] Archive completed items
```

## Common Pitfalls

### Over-Categorization
Start with fewer, broader MOCs. Split only when unwieldy (100+ notes).

### Under-Linking
Find notes without MOCs:
```dataview
LIST
FROM "Notes"
WHERE !contains(file.content, "MOCs:")
LIMIT 20
```

### Inconsistent Format
Standard format (recommended):
```markdown
MOCs: [[MOCs/Technology MOC|Technology]], [[MOCs/Learning MOC|Learning]]
```

## Advanced Techniques

### Dynamic MOCs
Auto-updating based on conditions:

```dataviewjs
const currentSprint = "sprint-2024-Q1";
const pages = dv.pages("")
    .where(p => p.file.content?.includes(currentSprint));
dv.header(2, `Sprint: ${currentSprint}`);
dv.list(pages.map(p => p.file.link));
```

### Computed Relationships
Find notes sharing MOCs:

```dataviewjs
const currentMOCs = dv.current().file.outlinks
    .filter(l => l.path.includes("MOCs/"))
    .map(l => l.path);

const related = dv.pages("")
    .where(p => {
        const pageMOCs = p.file.outlinks
            .filter(l => l.path.includes("MOCs/"))
            .map(l => l.path);
        return pageMOCs.some(m => currentMOCs.includes(m)) && 
               p.file.path !== dv.current().file.path;
    })
    .limit(10);

dv.header(3, "Related notes");
dv.list(related.map(p => p.file.link));
```

### Section-Specific Links
Link to MOC sections:

```markdown
MOCs: [[MOCs/Programming MOC#Python]]
```

Query for section links:
```dataviewjs
const targetHeading = "Python";
const currentPath = dv.current().file.path.replace('.md', '');

let found = [];
for (const page of dv.pages()) {
    const content = await dv.io.load(page.file.path);
    if (content?.includes(`${currentPath}#${targetHeading}`)) {
        found.push(page);
    }
}
dv.list(found.map(p => p.file.link));
```

## Key Takeaways

1. Start simple, evolve gradually
2. Use templates for consistency
3. Regular reviews prevent drift
4. Optimize queries for large vaults
5. Balance organization with flexibility

The MOC system grows with your knowledge. Begin with basics, add advanced features as needed.