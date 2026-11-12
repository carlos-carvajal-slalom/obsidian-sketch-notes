# Section frames and source-note embeds

## Scope and defaults

For a new study drawing based on an existing Markdown note in the same Obsidian
vault, create named section frames and embed them in that source note by default.
The output remains one editable `.excalidraw.md` drawing, not one file per frame.
Do not generate persistent image previews as a substitute for these embeds.

Respect explicit opt-outs. With "do not modify the source", still create frames
unless declined, but return the embed snippets without inserting them. With
"no frames", skip clipped-frame integration and do not silently insert a whole
drawing embed instead. With pasted text or a source outside the vault, create the
drawing and its frames, but do not invent, copy, or modify a source note.
Existing-drawing edits use the focused editing workflow; adding or updating
source embeds during those edits requires an explicit request.

## Plan frames around meaning

Read the source and map each visual section to:

- A short descriptive frame name in the requested drawing language.
- Its complete set of native content elements.
- A source location identified by heading and surrounding text, not line number
  alone; distinguish repeated headings using their parent section.

Use one frame per coherent explanatory cluster, typically the 3-7 planned visual
sections. Do not create a frame for every paragraph, list item, or heading without
visual content. Include a title/overview frame when it carries a useful visual.
A substantial demo can have multiple frames inserted around its relevant steps.
Keep the portrait layout, reading order, typography, and existing whitespace.

Place the overview after the introductory paragraph, before the first main
heading. Place a section's frame after the paragraph or complete block it
illustrates, before the next heading. Use an existing local embed placement
convention when clear. Never split frontmatter, fenced code, tables, lists,
callouts, or other Markdown blocks to insert an embed.

Example mapping for a graph-pattern note: overview after the introduction;
edge behavior after the concept summary; checkpoints after the motivation;
moderation flow after the demo introduction; parallel fan-out after the stretch
exercise. This is illustrative, not a fixed five-frame template.

## Create and verify actual frames

Inspect the installed native `create`/`apply` schemas and relevant frame API
documentation before authoring. Use supported frame elements and membership
operations; a rectangle, group, frame name, or bounding box is not a frame.
API documentation lookup is not permission or a mechanism to execute EA methods.
If native commands cannot create frames or assign membership, report that
limitation and ask before using a reviewed trusted script for the exact scope.
Do not rewrite compressed drawing Markdown or insert fabricated IDs as a fallback.

Enclose each section with enough padding to avoid clipping text, arrowheads, and
illustrations. Assign all its constituent shapes, bound text, icon components,
and internal connectors to that frame. Check actual `frameId` membership, not just
geometric containment. Prefer non-overlapping frames and avoid cross-frame
connectors that would disappear in an isolated clipped embed.

After saving, read the complete persisted scene at one revision. Resolve actual
IDs from the native receipt's `data.idMap` where available, then confirm each ID
exists as a non-deleted frame in the saved scene. Never use a skeleton-local ID,
a guessed ID, a frame name, or an ID copied from another drawing.
Verify membership, bounds, and preservation of groups and bindings. Inspect each
frame at note width when supported; whole-canvas inspection alone does not prove
that a clipped frame is complete and legible. Preserve frame-rendering settings
unless changing them is necessary and authorized; do not toggle them blindly.

For a trusted script that edits a live view, compare the live and disk scenes
before proceeding: a script's success message is not proof of persistence. If
disk is stale, do not rerun the script or issue a no-op native mutation as a save
bridge. Use a documented, runtime-supported save operation and verify the full
saved scene; if none is available, stop before editing the source note and ask
the user to save or authorize a concrete recovery path. Likewise, if native CLI
output is unparseable, recover the original request receipt and read the exact
target back before considering any retry.

Retain a compact mapping of source location, frame name, and verified saved ID
privately until source-note verification is complete.

## Insert Obsidian embeds safely

Use the full vault-relative drawing path with its `.excalidraw.md` extension,
forward slashes, and literal spaces. Use Obsidian wikilink syntax, not a file URI,
an absolute filesystem path, or a URL-encoded path:

```markdown
![[<vault-relative drawing path>.excalidraw.md#^clippedframe=<saved frame ID>|100%]]
```

The angle-bracket fields above are placeholders, not literal link content. For
example, a saved frame with ID `abc12345` could produce:

```markdown
![[Cursos/Example/_attachments/excalidraw/Graph.excalidraw.md#^clippedframe=abc12345|100%]]
```

Use the actual path and saved ID; the example ID must never be copied into a
real note. Keep the source language, wording, headings, frontmatter, code, links,
and existing embeds unchanged. An English drawing request does not authorize
translating a Spanish source. Insert only standalone embed lines and the blank
lines needed to separate them from adjacent Markdown blocks.

Before editing, re-read the source and compare it with the inspected version.
If it changed, re-evaluate insertion anchors; stop and ask if changes conflict.
If the note is open with unsaved edits, use a supported editor-aware operation
or ask for it to be saved first rather than overwriting the disk copy.
Use a narrow additive patch, not a rewrite or wholesale replacement.

Before inserting each embed, inspect existing links throughout the note:

- If the same drawing/frame is already embedded, reuse it without duplicating
  or moving it. Recognize links resolving to the same file even when their path
  form or display width differs.
- Preserve manual frames, embeds, and other drawings' links. Do not replace an
  existing embed just because its placement differs from the planned location.
- If an existing embed for the intended section points to a missing frame or
  conflicts with the new mapping, report it and ask before replacing it.

Do not bypass the existing-output guard to regenerate a drawing on a repeated
run. Reusing an existing drawing for explicitly requested integration follows
the focused editing workflow and reads its current frames first.

## Verify the complete outcome

After the patch, read the source back from disk and check:

1. Every planned embed is present exactly once or intentionally reuses an existing
   equivalent embed. Every inserted embed resolves to the intended drawing and a
   verified non-deleted frame ID in its saved scene.
2. Each embed occupies its planned Markdown location without splitting a block.
3. Removing only the newly inserted lines and their added separators reproduces
   the original source exactly. All pre-existing content and embeds are intact.
4. The drawing remains saved and verified. When an Obsidian reading view is
   available, inspect the source's actual embeds for correct clipping and
   readability; do not claim rendering verification from link syntax alone.

If source integration is blocked, leave the verified drawing intact, report
the specific blocker, and supply its verified embed snippets for manual use.
Do not report the complete workflow as finished. On retry after an uncertain
note write, read the source first to avoid duplicate insertion.
