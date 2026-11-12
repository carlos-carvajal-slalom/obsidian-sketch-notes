# Visual style from the supplied references

Use the images as a visual vocabulary for an original, readable sketchnote—not as
templates to trace or as a source of content. The first square reference is a visual
map: many short handwritten claims, small metaphoric doodles, and connecting marks
are arranged in loose clusters around a common idea. The other references broaden
that language: a large dramatic headline with a left-to-right story; a vertical
live-sketch with people, questions, and gentle color washes; and a wide, modular
feature infographic with compact panels and small diagrams.

The latest CLI onboarding reference sets the target for **visual richness**:
each capability has a recognizable illustration (terminal, document, magnifier,
pencil, image file, gear); each process step pairs a drawing with a short caption;
and a robot-to-app-to-drawing sequence communicates the workflow pictorially.
Pastel fills, dark outlines, colored section borders, and heading highlights unify
the page. Borrow that illustration-led grammar, not its wide aspect ratio: arrange
the same kind of visual units vertically or in readable pairs.

## Shared visual language

- White or warm-white paper-like field; dark, slightly irregular outlines and
  handwritten lettering.
- Use **Comic Shanns** for titles, labels, and body text by default, unless the
  user requests another font. Resolve its name and ID from the running runtime;
  never assume an ID or silently substitute a different font. If unavailable,
  use the installed default and report the limitation.
- A strong title, mixed lettering sizes, selective all-caps emphasis, underlines,
  speech bubbles, labels, and brief annotations.
- Simple hand-drawn metaphors—people, brains, books, tools, charts, symbols—chosen
  to explain a point rather than decorate empty space.
- Arrows and visual connectors show sequence, cause, contrast, or grouping. Keep
  their direction unambiguous and route them around labels.
- Use a small, consistent accent palette: yellow/gold for emphasis, teal/blue for
  structure or key concepts, and red/orange sparingly for warnings or highlights.
  Light color washes or shaded panels may separate clusters without overpowering
  text.
- Allow organic variation and generous negative space. Avoid a rigid corporate
  grid unless the note is a release-note/comparison layout; then use hand-drawn
  panel borders, distinct headings, and a small editable sketch in each panel.

## Composition cues

- Default to a vertical, tabloid-style editorial page, optimized for an Obsidian
  note embed rather than a wide presentation slide. "Tabloid" describes the
  headline, lead, sections, and visual hierarchy, not a fixed physical paper size.
  Adapt the wide references into stacked sections instead of copying their aspect
  ratios.
- Put a prominent headline and short lead at the top, then guide the reader down
  through visual sections to a concluding takeaway or sources. Give each section
  its own heading, short explanatory text, and a relevant diagram or doodle.
- Use one main column. Two compact columns may work for a short comparison or a
  pair of callouts, but avoid three or more columns and long rows of small panels.
  Prefer growing the page vertically over adding side-by-side content.
- For a process or argument, use a top-to-bottom sequence. Short horizontal steps
  can sit inside a section if their labels remain readable at note width.
- For a conceptual map, keep branches compact and arrange related clusters below
  one another; do not let side branches expand the page bounds.
- Use hand-drawn panels, callouts, and whitespace to separate sections without
  making the result feel like a rigid dashboard. Keep intentional outer margins.
- Use a landscape composition only when the user explicitly requests one.

## Illustration-led, not text-led

- Preserve the good explanatory wording. Add visuals that express its meaning
  rather than replacing it with vague captions or merely decorating the margins.
- Before drawing, map every main section and major step/item to a visual. Every
  main explanatory section needs a substantive illustration or diagram; every
  major process step or conceptual list item needs its own pictogram or
  mini-diagram. Source links and short takeaways are exceptions.
- Make illustrations large enough to have a silhouette and a few meaningful
  details: e.g. a terminal with a title bar and prompt, a document with a folded
  corner and text lines, or a robot with a face, antenna, and arms. Use selective
  pastel fills and consistent sketch-like outlines. Do not add detail that becomes
  noise when reduced to note width.
- Colored headings, containers, underlines, numbered badges, generic arrows, and
  punctuation markers are supporting layout elements, not explanatory imagery.
  One lightbulb at the top does not make an otherwise text-only page visual.
- Reserve a substantial area within each section for its visuals. Integrate
  pictures with short labels and captions; avoid a long stack of full-width text
  cards with tiny icons added as an afterthought. Use local image-and-text pairs
  or illustrated steps while retaining the page's vertical reading order.
- Prefer native editable shape/line assemblies and group their parts. A
  recognizable simplified drawing is better than a highly detailed raster icon
  when both communicate the same idea. Use licensed library art only through a
  verified insertion path, retaining provenance and editable parts.

### Example visual mapping for an LLM note

These are options, not a mandatory template or permission to add facts:

| Concept | Meaningful visual |
| --- | --- |
| Training on text | Open books or document stacks feeding a model |
| Input tokens | Segmented word tiles entering a model illustration |
| Next-token probabilities | Labeled candidate tokens with a probability bar chart |
| Sampling | One highlighted candidate selected from several possibilities |
| Append and repeat | Selected tile joining the token ribbon, with a return arrow |
| Hallucination | Speech bubble making a claim beside a contrasting fact-check document |
| Context limit | Bounded window containing tokens, with older tokens outside it |
| Prompt sensitivity | Two slightly different prompt cards branching to different outputs |
| Stochastic outputs | One prompt branching into several candidate answer cards |
| Modalities | Text page, image frame, waveform, and video/play symbol |
| Providers | Several service/server nodes; avoid invented brand logos |
| Token economics | Token stack paired with a coin and clock |
| Reasoning | Short direct route contrasted with a multi-step route |
| Benchmarks | Scorecard or chart with a magnifier and caveat caption |

Use captions to distinguish metaphor from mechanism. For example, a dice metaphor
can express stochastic sampling, but must not imply uniform token probabilities.

### Visual acceptance

Compare the export against the concept-to-visual plan at embed width. Confirm that
the illustrations remain recognizable, explain the nearby text, and cover the
main sections and items. Ignore raw element counts: many rectangles and labels can
still produce a visually sparse result. If the page looks like a formatted outline
rather than an illustrated explanation, revise the visuals and composition while
preserving readable text and vertical flow.

## Design for the embedded size

- Start with a content canvas about 900 units wide, including margins, and let its
  height follow the content. A portrait page is the default, not a rigid aspect
  ratio; do not pad a short note or compress a long one to match a paper size.
- Unless the user specifies another display width, design for a 600 CSS-pixel-wide
  embed. Evaluate text using the complete exported width, including padding and
  any stray objects that expand its bounds.
- Aim for at least 16 displayed pixels for explanatory text and essential diagram
  labels. Calculate `displayed font size = scene font size * embed width / exported
  scene width`. For example, 24-unit text on a 900-unit-wide export displays at
  16 pixels when embedded at 600 pixels. Use larger section headings and a clearly
  dominant title. Increasing PNG export scale improves resolution, not relative
  text size or layout.
- Wrap text and rearrange wide diagrams into vertical steps before reducing font
  size. Keep diagrams and illustration assets within their section's width; an
  oversized off-canvas arrow or doodle can shrink the entire embed.
- Inspect the preview scaled to note width and scroll through it. Do not judge
  readability only from a full-resolution crop or a fit-whole-image thumbnail.
  If the actual Obsidian embed cannot be inspected, use a width-scaled preview and
  state that the in-note rendering remains unverified.

## Keep it legible and editable

Translate long paragraphs into accurate, concise phrases. Preserve the source's
meaning, caveats, and named entities. Use native editable Excalidraw text, shapes,
arrows, and simple line art for the entire structure. A generated/inserted image is
only for an illustration too intricate to draw simply; keep its labels, captions,
connectors, and surrounding layout editable. Never reproduce unrelated wording or
specific artwork from the references.
