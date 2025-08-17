
```dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/") AND !contains(file.path, "Inbox/")
SORT file.mtime DESC
```

---

MOCs: [[MOCs/Index|Index]]
