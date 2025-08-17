```dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/") AND !contains(file.path, "Inbox/") AND !contains(file.path, "Drafts/")
SORT file.mtime DESC
```

## HEADING

```not-dataviewjs
const targetHeading = "HEADING";
const currentFile = dv.current().file;
const pathWithoutMd = currentFile.path.replace('.md', '');

let foundPages = [];

for (const page of dv.pages()) {
    // Skip system folders and current file
    if (page.file.path.includes("_/") ||
        page.file.path.includes("Inbox/") ||
        page.file.path.includes("Drafts/") ||
        page.file.path === currentFile.path) {
        continue;
    }

    // Read actual file content
    const content = await dv.io.load(page.file.path);
    if (content && content.includes(`${pathWithoutMd}#${targetHeading}`)) {
        foundPages.push(page);
    }
}

if (foundPages.length > 0) {
    dv.list(foundPages.sort(p => p.file.mtime, 'desc').map(p => p.file.link));
} else {
    dv.paragraph(`No backlinks to heading "${targetHeading}"`);
}
```

---

MOCs: [[MOCs/Index|Index]]
