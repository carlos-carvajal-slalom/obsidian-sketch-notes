# Obsidian sketch notes

An agent skill for creating and editing visual, editable Obsidian Excalidraw
sketchnotes, diagrams, and presentations from study notes.

## Install

Copy this folder into your Copilot skills directory:

```sh
cp -R obsidian-sketch-notes ~/.copilot/skills/
```

The included Excalidraw CLI helper is in
[`tools/obsidian-excalidraw-cli`](tools/obsidian-excalidraw-cli). See its
README for requirements and usage. Its AGPL-3.0-only license is included in
that folder.

## Upstream project and license

The bundled helper is based on
[zsviczian/obsidian-excalidraw-cli](https://github.com/zsviczian/obsidian-excalidraw-cli).
Its upstream documentation and original `LICENSE` are preserved in
[`tools/obsidian-excalidraw-cli`](tools/obsidian-excalidraw-cli); retain them
when copying or redistributing that bundle. The separate
[Excalidraw CLI](https://github.com/excalidraw/cli) mentioned in the helper's
README is a different project.
