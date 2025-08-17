# MOC System for Obsidian

[![Obsidian](https://img.shields.io/badge/Obsidian-7C3AED?style=flat&logo=obsidian&logoColor=white)](https://obsidian.md)
[![Dataview](https://img.shields.io/badge/Plugin-Dataview-blue)](https://github.com/blacksmithgu/obsidian-dataview)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Self-organizing knowledge management using Maps of Content (MOCs) and automatic aggregation.

## Quick Start

**Requirements:** Obsidian + [Dataview plugin](https://github.com/blacksmithgu/obsidian-dataview)

1. Create `MOCs/` folder in vault root.
    - This is where all MOCs will be stored.
    - You can change this in settings if needed.
2. Create your first MOC and note using the template:
    - Use [MOC template](./Templates/MOC.md) to create a new MOC.
    - Use the [note template](./Templates/Note.md) to create a new note.
    - Ensure the MOC is linked in the note.
3. Link notes: Add `MOCs: [[MOCs/Example MOC|Optional Alias MOC]]` to any note.

## Features

- **Automatic aggregation** - Notes appear in MOCs instantly via Dataview
- **Multi-category support** - Notes can belong to multiple MOCs
- **Zero maintenance** - No manual updating required
- **Native Obsidian** - Uses standard links and Dataview
- **Scalable** - Works with any vault size

## How It Works

1. Notes link to MOCs using standard Obsidian links.
2. MOCs query for backlinks using Dataview.
3. Organization updates automatically without tags, excessively nested folders, or frontmatter.

## Documentation

| Guide | Description |
|-------|-------------|
| [Quick Start](./Docs/Quickstart.md) | Get running in 10 minutes |
| [Migration](./Docs/Migration.md) | Migrate existing notes |
| [Tips](./Docs/Tips.md) | Advanced techniques |
| [Reference](./Docs/Reference.md) | Technical documentation |
| [Philosophy](./Docs/Philosophy.md) | System principles |

## Acknowledgments

- [Nick Milo](https://www.linkingyourthinking.com/) - MOC methodology
- [Michael Brenan](https://github.com/blacksmithgu) - Dataview plugin
- [Obsidian Community]((https://forum.obsidian.md))
