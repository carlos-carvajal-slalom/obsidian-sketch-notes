---
name: obsidian-sketch-notes
description: "Create or edit editable Obsidian Excalidraw drawings, sketchnotes, diagrams, and frame-based presentations. Use for Spanish or English requests to create visual study notes with automatic section frames and source-note embeds, modify existing slides or charts, or diagnose missing frames in a specified vault."
argument-hint: "Paste the note or give its path, and specify the Obsidian vault and output path."
user-invocable: true
---

# Obsidian sketchnotes

Turn user-provided notes into clear, hand-drawn-looking Excalidraw drawings saved
inside the specified Obsidian vault. Keep text, shapes, connectors, and simple
icons editable. Use an inserted image only for an illustration that would be
unreasonably complex to construct natively.

Default to a **portrait, vertically scrolling tabloid-style composition** designed
to remain readable when embedded in an Obsidian note. Grow downwards rather than
widening the drawing or shrinking its text. This is an editorial layout preference,
not a requirement to use physical tabloid paper dimensions.

Make an **illustrated explainer, not a formatted text outline**. Preserve useful
wording, but let recognizable illustrations and diagrams carry the explanation.
Boxes, numbered circles, arrows, colored headings, and punctuation alone do not
satisfy the visual requirement.

When creating a study drawing from an existing Markdown note in the same vault,
complete the workflow by default: create named frames for its visual sections
and insert clipped-frame embeds into the corresponding parts of the source note.
Follow [frames and source-note embeds](./references/frames-and-embeds.md).
An explicit request for a drawing only, no frames, or no source-note edits
overrides the relevant defaults. Pasted text without a source path does not
authorize creating or modifying a source note.

## Choose creation or editing first

For an existing drawing, use the [focused editing workflow](./references/editing-existing.md)
instead of repeating the creation workflow below. A request to change a slide
authorizes that bounded edit, not recreation, source-note updates, global
restyling, or unrelated preview replacement. Reuse the known vault and exact
drawing path; do not ask for a source note when the drawing itself is the source.
For inspection-only requests, diagnose before proposing or applying changes.

Existing presentations keep their frame sizes, spatial layout, media, fonts,
and presentation order unless the user requests changes. Do not apply the portrait
sketchnote defaults to existing landscape slides.

## Required inputs for new drawings

Get these from the request or the current workspace; ask only for missing details:

- The note text or an exact source-note path.
- The exact Obsidian vault name/ID.
- The exact vault-relative output path ending in `.excalidraw.md`. If the user
  supplies only an output folder, derive the filename from the source note's
  basename using the filename rules below.

Do not create persistent PNG/image previews by default, for either creation or
editing. Prefer inspecting the live drawing when supported. If an image export
is needed for visual verification, treat it as temporary: use a unique unused
path, inspect it, then delete that exact task-created file before delivery.
If the native exporter requires a vault-relative path, export there temporarily
and clean it up afterward; do not change plugin auto-export settings silently.
Never delete pre-existing images, embedded assets, or user-requested exports.
Keep an image only when the user explicitly requests it as a deliverable.

For new study drawings from an existing Markdown note, source-note edits are
limited to inserting the verified frame embeds described above. Preserve all
original content; other source-note edits require an explicit request. Editing an
existing drawing does not authorize source-note changes. Never replace an
existing drawing/export without explicit permission. If the drawing output path
already exists when creating, stop and ask for a different path or explicit
overwrite permission.

When deriving an output basename from a note title, preserve the original title in
the drawing but replace characters that are invalid or rejected in Obsidian paths
(including `?`, `:`, `*`, `"`, `<`, `>`, `|`, backslashes, and control characters)
with a readable separator such as ` - `. Keep the requested output folder unchanged.
Before creating anything, validate the final vault-relative drawing path and derived
preview path against the native CLI's visible-path requirements, then check those
exact paths for existing files. Do not silently rewrite an explicitly requested
full output path; if it is invalid, ask the user for a valid path or permission to
use a clearly stated safe filename.

## Visual direction

Read [the visual style reference](./references/visual-style.md) before composing.
Treat the supplied images as style and structure guidance, not content to reproduce.
Keep the drawing self-contained, readable, and faithful to the source note:

1. Extract the main idea, key supporting points, relationships, and any source links.
   Preserve important qualifications and do not invent facts.
2. Select a layout that fits the material within a narrow portrait canvas:
   top-to-bottom for a process, compact branches for a mental model, paired panels
   for short comparisons, or vertically stacked editorial sections for independent
   topics. Use one main column; at most two local columns when both remain readable.
   Do not spread an entire note across a wide horizontal diagram.
3. Use a prominent hand-drawn title and a clear visual reading order. Break dense
   material into a few clusters with short labels, annotations, arrows, callouts,
   and substantial relevant illustrations. Give every main explanatory section a
   meaningful visual; give each major process step or conceptual list item its own
   recognizable pictogram or mini-diagram. References and brief closing takeaways
   need not have an illustration each. Keep meaningful whitespace; do not cram the
   original prose onto the canvas.
4. Prefer a light background, dark sketch-like strokes, and a restrained palette
   such as black/charcoal plus teal/blue, warm yellow, and a sparing red accent.
   Vary lettering hierarchy and use **Comic Shanns** for titles, labels, and body
   text by default, unless the user requests another font. Confirm the font
   against the running Excalidraw runtime before using it.
5. Make the content native and editable by default: text elements for all labels,
   native shapes/lines/arrows for diagrams, and simple editable component shapes for
   icons. Keep generated or other raster art limited to the complex illustration
   itself; never flatten the complete infographic into one image.
6. Design visuals before placing text: map each key concept to an illustration,
   diagram, or metaphor and reserve space for it. Use pictorial shapes with enough
   detail to be recognizable at embed width, not emoji, generic dots, or an
   isolated "!" / "?" as substitutes. Pair illustrations with the text they explain;
   do not put one decorative doodle in the header and leave the rest text-only.

## Workflow

The complete portable native-CLI bundle is at
`./tools/obsidian-excalidraw-cli/`. Follow its [agent
instructions](./tools/obsidian-excalidraw-cli/SKILL.md) and read the relevant
references there, especially `docs/getting-started.md`,
`docs/native-cli-workflow.md`, `docs/authoring.md`, and `docs/troubleshooting.md`.
The bundled helper is based on
[zsviczian/obsidian-excalidraw-cli](https://github.com/zsviczian/obsidian-excalidraw-cli);
preserve its included license and attribution when redistributing it.
The companion ExcalidrawAutomate authoring references are in
`./references/ea-script-template/`; use them to inform drawing style and API choices,
not as permission to execute a script.

1. **Discover and verify the host.** Use the exact vault name/ID. Run the bundle's
   read-only doctor (`node <bundle>/scripts/doctor.mjs --vault "<vault>"`) and
   confirm the returned vault and `ready` status. Query the installed `create`
   schema and relevant EA/Lib methods from the running plugin before relying on
   optional features or font IDs. Do not infer capabilities from repository source
   code alone.
2. **Inspect targets.** List the exact output folder and check that the new
   `.excalidraw.md` path and any temporary export path are unused. Verify every
   intended deliverable at its exact path before linking or reporting it; prior
   session summaries and remembered previews are not evidence that a file exists.
   Do not create a persistent PNG unless the user requests one. If the note is
   already in the workspace, read it directly; do not search unrelated folders.
   For source-note integration, retain its original content and inspect existing
   embeds so the eventual patch is additive and duplicate-free.
3. **Plan before authoring.** Briefly map the note into a title, 3–7 visual clusters,
   relationships, and a canvas layout. Include a concept-to-visual mapping for
   every main section and major step/item, using the examples in the visual style
   reference. Keep wording concise but accurate. Use a
   portrait tabloid-style layout by default: a prominent headline, a short lead,
   stacked visual sections, and a concluding takeaway or references. Start around
   900 canvas units wide and add height as needed; do not enforce a fixed page
   height. Plan for an approximately 600 CSS-pixel-wide note embed. Follow the
   display-size and typography checks in the visual style reference. Use landscape
   only when explicitly requested; a locally horizontal process must still fit
   within the portrait layout.
   Plan one named frame per coherent visual section and map each to an insertion
   location in the source note, following the frames-and-embeds reference. Frames
   delimit the existing portrait composition; they do not turn it into slides.
4. **Build a native scene.** Use the installed plugin's native `create` command and
   validated skeletons. The repository helper `scripts/native.mjs` provides
   `invokeNative`, `discover`, and `readAll`; use it rather than constructing shell
   commands with interpolated JSON. Use a unique request ID and an absolute,
   per-vault private `stateDirectory` outside the vault/source control. Keep request
   records private because they contain note text. For large payloads, follow the
   bundle's vault-relative request-file workflow and retain the payload/receipt
   until the save is verified.
   Build recognizable illustrations from native component shapes and lines, with
   selective pastel fills, consistent outlines, and small meaningful details.
   Group each multi-part illustration using the installed supported operation so
   it can be moved as a unit while its components remain editable. For complex
   symbols, consult `docs/library-reuse.md` and use a verified library insertion
   path that preserves editability and provenance; do not execute library data.
   Use runtime-supported native frame creation and membership operations. Save
   actual frame IDs for embeds, not temporary skeleton IDs or frame names.
5. **Use runtime-confirmed typography.** Query available fonts/methods and resolve
   **Comic Shanns** by name as the default for all text, including titles and
   bound labels, unless the user requests another font. Never guess or hard-code
   a numeric font ID, reuse an ID from a previous session, or silently substitute
   Excalifont, Virgil, or another font. If the requested font is unavailable, use
   the installed default and explicitly mention the limitation. Verify the saved
   text elements use the runtime-resolved font and recheck wrapping and bounds.
6. **Use complex art selectively.** If a complex illustration materially improves
   comprehension, use an available image-generation capability for that isolated
   illustration and insert its local asset through a supported native operation.
   If no image-generation capability is available, represent the idea with a
   simplified editable sketch or explain the limitation; do not silently flatten or
   fake an image asset. Never use an external service for private note content
   without the user's authorization.
7. **Create and verify.** Create only at the exact unused drawing path. Check
   `ok`, `status`, `mutation`, and `persistence`; then read the complete saved scene
   back from disk, following every page at one revision. Verify that key text,
   groups/relationships, connectors, and expected element counts are present.
   Visually inspect the saved drawing through an available live view or, when
   needed, a temporary PNG export at an unused path. Inspect the image/view both at full size and scaled to the
   intended note width (600 CSS pixels by default), scrolling vertically rather
   than fitting the whole tall image into one screen. Inspect text-heavy regions;
   fix clipping, collisions, illegible text, awkward arrows, and imbalance before
   finishing. If labels are too small at embed width, reflow sections, shorten
   wording, or increase height and font sizes; do not widen the canvas or rely on
   zooming to make the embedded result readable. Report if embed-width inspection
   could not be performed.
   Also audit visual coverage: every main explanatory section and major step/item
   must have its planned meaningful illustration or diagram. Check that icons are
   recognizable at embed width, not merely technically present. If the result
   still reads like stacked text boxes or a bullet list with colored headings,
   revise the composition before delivery. Do not equate element count with
   visual richness. Delete any task-created temporary image after inspection,
   including intermediate exports superseded by later fixes. Track exact paths;
   never use wildcard or directory-wide image deletion. If cleanup fails, report
   the remaining path explicitly rather than claiming no image was left behind.
8. **Recover safely.** On timeout, missing/unparseable JSON, unknown/pending
   receipt, stale revision, or unsaved state, follow the bundle's recovery procedure
   and inspect disk/live state before any new write. A zero exit code does not prove
   that a structured receipt was returned, and a missing receipt does not prove the
   mutation failed. Reuse the original request ID to query `result`; if that is
   unknown or pending, read the exact target back from disk and inspect it before
   deciding what to do. Never blindly retry a write, delete/recreate a drawing, or
   claim success based only on a zero exit code. If a script changes a live scene
   but the disk read does not reflect it, treat persistence as unverified even if
   the script says it saved. Do not rerun it blindly or issue a no-op mutation to
   force a save; use a runtime-supported save path and verify the complete disk
   scene. If no supported path is available, stop before source-note embeds and
   ask the user to save or authorize a specific recovery method.
9. **Embed verified frames in the source note.** After the drawing is saved and
   verified, follow the frames-and-embeds reference to insert
   `![[<vault-relative drawing path>#^clippedframe=<saved frame ID>|100%]]`
   at the planned locations. Re-read the source before applying a narrow patch,
   preserve its prose and existing embeds, and verify every inserted link against
   the saved scene. Do not insert links to unsaved or unverified frames. Skip
   source edits when the user opted out or there is no eligible source file.

Opening a drawing can run configured drawing scripts. Prefer disk reads/exports
unless a live view is needed; if opening is necessary, note this behavior and use
the explicit view ID returned by the runtime.

## Delivery

Report a link to the `.excalidraw.md` drawing, summarize the visual
structure, and state what was actually verified. Distinguish structural/save
verification from visual inspection. When source-note integration applies, also
link the source note, report the frames and embeds added or reused, and distinguish
link/ID validation from actual Obsidian embed rendering. Explicitly report any
incomplete frame creation or source-note integration; a saved drawing alone does
not complete that workflow. Mention any unavailable font/image capability
or remaining limitation. Link an image only if the user requested keeping it and
it exists and has been verified. Temporary validation images are not deliverables;
do not register them as artifacts or link deleted previews.
