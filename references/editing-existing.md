# Focused editing of existing Excalidraw drawings

Use this path for edits and diagnosis, not the new-drawing workflow. Follow the
bundle's native CLI contract and recovery rules. Optimize the amount of data
shown to the model, not the safety of saving.

## Why JSON edits still need care

An Obsidian drawing can wrap compressed scene JSON in Markdown. Elements have
frame membership, groups, text containers, bindings, assets, and ordering; the
open view may also contain unsaved changes. Valid JSON alone proves neither a
correct scene nor a readable slide. Use native mutation and save operations;
never rewrite compressed Markdown to bypass their validation.

## Small-edit loop

1. **Resolve scope.** Use the exact known vault and drawing. Identify the target
   frame by current ID/name, not an old slide number. For narrative changes,
   inspect adjacent slide titles and relevant content; for a chart adjustment,
   inspect that chart, not the whole deck. Do not update the source note unless
   requested. Keep rejected or obsolete plans out of projected content.
2. **Check the host once.** Run the required doctor at the start of the editing
   run. Retain its vault, plugin version, and session identity privately. Query
   only relevant command schemas and API/font capabilities. The native wrapper
   already performs discovery before writes; do not duplicate that preflight
   manually before every operation. Refresh assumptions after plugin/session
   changes or capability errors, never reuse stale revisions or view IDs.
3. **Read narrowly, inventory privately.** Start with a current summary: view,
   revision, dirty state, counts. If IDs are unknown, exhaust one complete
   paginated inventory at one revision and retain it outside the vault. Print
   only target text/geometry and a compact frame index, not hundreds of elements,
   compressed payloads, base64 assets, or complete schemas. Use supported `ids`
   filtering for subsequent reads. A selected subset is not a full inventory.
4. **Plan and batch.** Reuse existing elements where their role and bindings fit.
   Prepare one coherent supported `apply` batch within runtime limits. Validate
   update properties against the installed update schema, not the broader create
   skeleton: a property accepted during creation may be rejected on update.
   Use inline requests within the helper's byte limit; use the documented
   request-file path for larger payloads. Retain the request and unique ID.
5. **Guard the write.** Read current target elements and obtain their revision.
   Recheck dirty state and revision before publishing. If unsaved user edits or
   conflicting changes appear, stop and ask rather than saving over them.
   A closed view requires resolving a current view ID. Opening can run drawing
   scripts; use an existing view when possible and disclose necessary opening.
6. **Recover, do not replay.** Missing JSON stdout or a pending receipt is not a
   failed mutation. Query `result` with the original request ID, then inspect
   actual live/disk state before another write. Do independent work while a
   bounded operation completes; avoid tight polling, duplicate writes, or
   resetting/recreating the drawing. Explicit schema rejection with
   `mutation=not-applied` permits a corrected payload with a new request ID.
7. **Verify once, at the right scope.** Check persistence and a clean live view;
   compare saved target content and relationships. Validate the exact output
   requirement, then inspect the changed frame at presentation size using an
   available live view or, if needed, a temporary export. Delete the exact
   task-created image after inspection; keep exports only when explicitly requested.
   Do not refresh every slide or the entire panorama for a single-frame edit
   unless requested or needed to verify cross-frame layout.

## Deterministic checks outside model context

Use an existing helper where suitable; extend a reusable helper rather than
creating several near-identical scripts per edit. Keep full data in private
session files and return a short validation summary:

- Target content, frame membership, groups, bindings, and text containment.
- Unchanged active IDs, frame geometry/names/order, and media outside scope.
- App-state preservation, especially `frameRendering`.
- Arithmetic and proportional geometry: for bars, one zero baseline and one
  pixels-per-unit scale; never inflate short bars for legibility.
- Expected native text remeasurement: an auto-sized width or a centered bound
  label's position may differ from the requested bounding box. Validate the
  resulting bounds and relationships instead of demanding that width literally
  equal the requested value.

Compare semantic element fields separately from `version`, `versionNonce`, and
`updated`. Native saving can refresh this bookkeeping without changing content.
Compare active elements separately from deleted tombstones; do not mistake
tombstone compaction for lost content. Never ignore actual changed text,
coordinates, membership, bindings, assets, or order. Report such differences;
do not automatically restore imperceptible shifts with another script.

Example: changing four bars should produce four checked lengths, visual
inspection of that frame, and an unchanged-outside-scope summary, not another
full-deck audit or a persistent PNG.

## Frames, containers, and presentation behavior

- Geometric containment is not frame membership: check `frameId`.
- A bound text element follows its `containerId`; reuse it with that container
  rather than moving the container elsewhere and treating the text as free.
- Spatial frame arrangement and slideshow navigation order are distinct.
  Preserve both; rename frames only when authorized.
- When frames exist but are invisible, inspect rendering state before repairing
  geometry. `frameRendering.enabled=false` can hide intact frames. Prefer a
  runtime-available built-in display command for an authorized visibility fix;
  verify the saved state afterward. A toggle must be based on known current
  state, not executed blindly.
- Use trusted EA scripts only when the supported native operations cannot
  perform the requested change. Obtain explicit authorization for the exact
  script scope; earlier permission for other IDs is not reusable. Guard against
  a changed scene, await saving, and read back. Script completion alone does not
  prove persistence, even when `ok=true`.

Do not extract and execute decoder code from the plugin's minified bundle.
Prefer native disk reads; if unavailable, report the limitation or use an
already available reviewed pure-data decoder, read-only, without installing a
dependency or rewriting the scene as a shortcut.

## Delivery and cost claims

Report the changed drawing, what was checked, and any remaining limits. Do not
link or register temporary validation images; remove them before delivery.
Distinguish source verification, saved structure, and visual inspection.
Do not claim a token/cost reduction percentage without a measured before/after
comparison. This workflow reduces redundant reads and model-visible JSON;
it does not remove native CLI calls or change wrapper behavior by itself.
Retain recovery records privately and remove only task-created temporary vault
request/script files after verified persistence.
