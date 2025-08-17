# MOC System for Obsidian

[![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat&logo=obsidian&logoColor=white)](https://obsidian.md)
[![Dataview](https://img.shields.io/badge/Plugin-Dataview-blue)](https://github.com/blacksmithgu/obsidian-dataview)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Self-organizing knowledge management using Maps of Content (MOCs) and automatic aggregation.

## Quick Start

**Requirements:** Obsidian + [Dataview plugin](https://github.com/blacksmithgu/obsidian-dataview)

1. Create `MOCs/` folder in vault root
2. Create your first MOC using the template below
3. Link notes: Add `MOCs: [[MOCs/Your MOC|Your MOC]]` to any note
4. Watch notes appear automatically in MOCs

### MOC Template

```markdown
# Technology MOC

Technology-related notes.

## All Notes

\`\`\`dataview
LIST
FROM [[]]
WHERE !contains(file.path, "_/")
SORT file.mtime DESC
\`\`\`
```

### Note Template

```markdown
# Note Title

Content here...

---
MOCs: [[MOCs/Technology MOC|Technology]], [[MOCs/Projects MOC|Projects]]
```

## Features

- **Automatic aggregation** - Notes appear in MOCs instantly via Dataview
- **Multi-category support** - Notes can belong to multiple MOCs
- **Zero maintenance** - No manual updating required
- **Native Obsidian** - Uses standard links and Dataview
- **Scalable** - Works with any vault size

## How It Works

1. Notes link to MOCs using standard Obsidian links
2. MOCs query for backlinks using Dataview
3. Organization updates automatically

## Documentation

| Guide | Description |
|-------|-------------|
| [Quick Start](./Docs/Quickstart.md) | Get running in 10 minutes |
| [Migration](./Docs/Migration.md) | Migrate existing notes |
| [Tips](./Docs/Tips.md) | Advanced techniques |
| [Reference](./Docs/Reference.md) | Technical documentation |
| [Philosophy](./Docs/Philosophy.md) | System principles |

## Examples

### Finding Orphaned Notes

```markdown
# Orphaned Notes

Notes without MOC links.

\`\`\`dataview
LIST
FROM "Notes"
WHERE !contains(file.content, "MOCs:")
SORT file.mtime DESC
\`\`\`
```

### Multiple Views

```markdown
# Projects MOC

## Active Projects

\`\`\`dataview
LIST
FROM [[]]
WHERE contains(file.content, "#status/active")
SORT file.mtime DESC
\`\`\`

## All Projects

\`\`\`dataview
TABLE file.mtime as "Modified"
FROM [[]]
SORT file.mtime DESC
\`\`\`
```

## Support

- [Documentation](./Docs/)
- [GitHub Issues](https://github.com/yourusername/obsidian-moc-system/issues)
- [Obsidian Forum](https://forum.obsidian.md)
- [Discord](https://discord.gg/obsidianmd)

## License

MIT License - see [LICENSE](LICENSE) file.

## Acknowledgments

- [Nick Milo](https://www.linkingyourthinking.com/) - MOC methodology
- [Michael Brenan](https://github.com/blacksmithgu) - Dataview plugin
- Obsidian Community

---

**[Get Started →](./Docs/Quickstart.md)**