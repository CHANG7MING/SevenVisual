---
name: se7en-visual
description: "Create consistent editorial manga-ink explanatory images and reusable illustrations featuring one locked rounded young male protagonist and one locked gray tabby cat, with physically coherent camera viewpoint, object orientation, occlusion, and front/back surface logic. Use for concepts, mechanisms, comparisons, workflows, task scenes, information organization, editorial artwork, serial illustrations, and transparent character assets where stable recurring character identity and a unified visual language are required."
---

# SE7EN-VISUAL

Create raster visuals in one unified manga-ink language. Treat `assets/se7en-character-reference.png` as the mandatory identity reference for every generation. Never introduce a dog.

## Load the required references

Read [references/character-lock.md](references/character-lock.md) before generating any image. Read [references/prompt-patterns.md](references/prompt-patterns.md) when constructing or retrying a prompt. Attach the canonical character image to every image-generation request and identify it as the identity and visual-style reference.

## Choose the output mode

### Mode A — explanatory image

Use when the image itself must explain a concept, mechanism, workflow, comparison, or tradeoff.

- Deliver a complete PNG or WebP on an off-white textured scene.
- Show the relationship through objects, paths, states, or repeated materials.
- Integrate short labels only when they materially improve understanding.
- Keep one focal action and no more than three major visual regions.

### Mode B — reusable illustration

Use when the character scene will be composed into a document, card, slide, hero, or other layout.

- Generate one reusable action with only essential props.
- Use a perfectly uniform chroma-key background that does not occur in the subject.
- Remove the background with the bundled `scripts/cutout.py`.
- Keep generous padding, omit text unless requested, and deliver a transparent PNG.

Choose Mode A when the image must communicate the idea by itself. Choose Mode B when another layout will provide the title and explanatory copy.

For Mode B, generate the source on a perfectly uniform `#00FF00` background; use `#FF00FF` when the subject contains green. Confirm that all four corners are uniform and that no artwork touches the border. Install Pillow in the active Python environment when needed, then run:

```bash
python scripts/cutout.py source.png transparent.png
```

Optional tuning:

```bash
python scripts/cutout.py source.png transparent.png \
  --transparent-threshold 12 \
  --opaque-threshold 220
```

Preserve the opaque source until the transparent output is approved. Validate that the result is RGBA, all four corners have alpha `0`, thin ink details remain intact, internal white and halftone regions are preserved, and no key-color fringe remains.

## Write the visual brief

Define:

```text
viewer_question: what should be understood in 10 seconds?
concrete_claim: one-sentence conclusion
aspect_ratio: requested ratio or default 1:1
real_objects: visible documents, tools, interfaces, or states
relation: comparison, transformation, causality, sequence, hierarchy, feedback, tradeoff, or pipeline
visual_evidence: what remains understandable without labels?
scene: believable setting with 2–4 useful environmental cues
character_action: what the young man does
cat_action: how the same cat naturally accompanies or reacts; choose an awake, observing, walking, sitting, interacting, resting, or sleeping state that fits the scene
semantic_colors: what each accent color means
labels: exact short strings and their evidence surfaces
```

Show input, action or relation, and result. Let poses, expressions, props, and settings change with the supplied content. Keep the recurring identities unchanged.

## Lock viewpoint and physical reality

Before writing the generation prompt, build a simple spatial model of the scene:

```text
camera: where the viewer is
actor: where the character is and what surfaces he can see or touch
object_faces: which front, back, inside, outside, top, or underside faces the camera and actor
display_content_mode: visible-front or hidden-back (choose exactly one for each screen-like object)
directional_objects: every object with a front/back, inside/outside, readable side, opening, hinge, or reflective side
actor_orientation: front-facing when it does not conflict with the scene; use side, rear three-quarter, or over-the-shoulder when that is needed to make the functional face and interaction physically clear
occlusion: which objects must be in front of or behind others
interaction: which hand, gaze, tool, control, or surface participates in the action
```

- Treat every object with meaningful sides as a solid object, not a flat symbol. A visible mark, interface, page, label, button, lens, or opening may appear only on its real supporting face.
- For every monitor, laptop, phone, or tablet, choose exactly one valid display mode before prompting: **visible-front** or **hidden-back**. In visible-front mode, the content-bearing face is genuinely visible to the camera and faces the user; in hidden-back mode, the camera sees only the plain rear casing, hinge, stand, ports, or exterior and no display content is shown. Both modes are correct. Never mix them on one object.
- In visible-front mode, put UI, text, images, and controls only inside the real front display plane. Place the camera and user on the same side of that plane, or use a believable over-the-shoulder/side three-quarter view where the screen plane faces both. In hidden-back mode, if the camera is behind the monitor and looking toward the user, keep the rear casing plain and accept that the screen content is not visible.
- Apply the same rule to laptops, phones, tablets, books, documents, signs, packages, doors, windows, drawers, vehicles, tools, and appliances. Never place front-side content on a visible back, closed interior, underside, or occluded surface.
- Keep gaze, hand reach, keyboard/mouse orientation, chair placement, and object controls consistent with the active surface. Do not mirror only one object or body part.
- Keep the recurring young man front-facing or front three-quarter when that does not make the scene ambiguous. When a screen, book, document, phone, tablet, TV, or other functional face is the focal evidence, prefer a side, rear three-quarter, or over-the-shoulder view like a real operator/viewer would have. Physical clarity outranks showing the character's full face. Never force a front-facing person to look through a solid object or make a readable surface face away from the person.
- Keep `aspect_ratio` at `1:1` unless the user explicitly specifies a ratio or orientation. Resolve wording exactly: `4:3` → 4:3 landscape, `16:9` → 16:9 landscape, `纵向`/`portrait` → 9:16 portrait, `3:4` → 3:4 portrait, and `1:1`/`square` → 1:1. Do not silently substitute a different ratio.
- Prefer an unambiguous composition over displaying extra information. If spatial logic conflicts with showing an interface or label, omit that content or rotate/recompose the whole scene.
- State the selected mode positively and negatively in the prompt. Visible-front example: `camera and user are on the same side; UI appears only inside the front display plane; outer lid is hidden and plain.` Hidden-back example: `camera sees only the plain rear casing; display surface faces the user but is hidden from camera; no UI, chart, text, glow, or screen border on the rear casing.`
- Mentally trace camera -> visible face -> actor before generation. If the action would be impossible in a quick real-world tabletop mock-up, revise the viewpoint.

### Directional-object checklist

Apply the same front/back and inside/outside test to every directional object, not only computers:

| Object | Content-bearing or functional face | Must not appear on |
|---|---|---|
| Book, notebook, paper, card, document | the actually open/readable page or printed face | back cover, reverse page, closed edge, underside |
| Phone, tablet, laptop, monitor, TV | the real glass display plane | rear casing, outer lid, stand, side edge, back panel |
| Window, mirror, picture frame | the visible pane/reflection/image surface | wall behind it, frame thickness, outside when hidden |
| Door, drawer, cabinet, appliance | the visible front, handle, opening, or interior | closed back, side panel, underside, impossible opening |
| Box, package, bottle, vehicle, tool | the labeled/usable exterior face or actual opening | reverse face, sealed interior, underside, disconnected cap |

For books and papers, page order, spine, folds, writing direction, and the hand holding the page must agree. For windows and mirrors, distinguish the pane/reflection from the frame and wall; do not paste scenery or reflections onto the wrong side. For TVs and displays, choose `visible-front` or `hidden-back` exactly as for a laptop. If a directional object's functional face is hidden, leave its content hidden; never invent a second visible front.

### Front-facing person with hidden-back object

This is an explicitly valid default composition when the user wants the object back but the person front:

- Keep the man's face visible from the camera, front-facing or front three-quarter, with his gaze directed toward the hidden functional face.
- Put the monitor/TV/laptop/book/device between camera and person only when its rear/outer surface genuinely faces camera and its functional face genuinely faces the person.
- Show only believable rear details such as casing, stand, hinge, ports, spine, cover, or frame thickness. Hide all front content; it is acceptable that the viewer cannot read it.
- Do not turn the person into a back view merely to expose the object's back. Do not make the person look through the object's solid back.

### Choose actor orientation by focal surface

- **Screen or editing workstation:** prefer side/rear three-quarter or over-the-shoulder when screen content is required; keep the user, screen front, keyboard, and gaze on one coherent side. Use front-facing only when the screen can remain physically clear beside or below the face.
- **Reading or writing:** prefer over-the-shoulder/rear three-quarter when the page content is the evidence; show the open pages from the reader's side, never a mirrored or reverse page. Use front-facing only when the book is turned consistently toward both reader and camera.
- **Sports or full-body action:** choose front, side, or rear three-quarter based on the ball/tool/foot trajectory and the intended action; do not sacrifice believable weight, reach, or contact just to show the face.
- **Simple conversation or portrait action:** use front-facing by default when no directional object creates a conflict.

## Apply the shared visual language

- Draw confident black manga/comic outlines with varied line weight.
- Use restrained circular halftone screentone for gray and shadow areas.
- Use an off-white lightly textured paper environment, not a blank clinical canvas.
- Use black, off-white, and halftone gray as the base.
- Reserve muted orange for the cat collar and add at most two muted semantic colors.
- Prefer blue for input/content, orange for action/warning/cost, purple for process, and green for successful results.
- Keep rounded proportions, professional clarity, and controlled hand-drawn energy.
- Avoid thin stick figures, glasses, dogs, extra animals, 3D, glossy gradients, photorealism, generic card grids, dashboards, clutter, and watermarks.

## Build a Mode A prompt

Use this order:

1. State the concrete claim and task.
2. Describe the real setting and the young man/cat actions.
3. Declare the canvas `aspect_ratio` (default `1:1` or the exact user-requested ratio), camera position, each important object's visible face, its actor-facing face, display-content mode (`visible-front` or `hidden-back`), and required occlusions.
4. Describe evidence objects and their geometry: aligned, nested, connected, split, transformed, repeated, or converging.
5. Repeat all identity invariants from `character-lock.md`.
6. Assign semantic colors.
7. Quote exact labels and specify placements when labels are needed.
8. Append the Mode A style anchor and the physical-consistency block from `prompt-patterns.md`.
9. End with exclusions, including `no dog`, `no thin stick figure`, and scene-specific impossible surfaces.

## Design labels

- Prefer 2–6 labels and use more only when necessary.
- Keep every label short and concrete: role, action, state, or outcome.
- Place each label on or directly beside its evidence surface.
- Use modern Chinese sans-serif typography, medium or bold, large enough to read.
- Do not turn body copy, commands, tables, or long paragraphs into image text.
- Compare generated labels character by character and reject missing, duplicated, invented, or misspelled text.

## Inspect and retry

Inspect the result at original resolution. Reject and retry if:

- The young man's hair, face, clothes, body ratio, or lack of glasses drifts.
- The cat's markings, white muzzle and paws, orange collar, or body shape drifts.
- The cat's eyes or state contradict the requested action, or every unrelated scene repeats the same sleeping pose.
- A dog, additional animal, or duplicate cat appears.
- Repeated scenes depict visibly different people or cats.
- The main relationship is unclear without labels.
- Required labels are missing, duplicated, invented, or misspelled.
- Any interface, text, image, control, opening, or front-face detail appears on an object's back, underside, closed interior, or other impossible surface.
- The camera viewpoint, object orientation, gaze, hands, controls, support, perspective, or occlusion contradict one another.
- The output canvas or composition does not match the selected `aspect_ratio`, or a user-requested ratio was silently replaced with the default square.
- The actor orientation is chosen only to expose the face and causes a screen, book, page, ball, tool, or other focal surface to face the wrong direction or become physically unreadable.
- A screen-like object mixes modes: content is drawn on a rear/outer/closed surface, or a front display is shown while the selected mode says `hidden-back`.
- A `visible-front` screen is physically facing away from both the user and camera, or a `hidden-back` screen contains any UI, text, image, glow, or front bezel detail on its visible rear casing.
- Any book, paper, phone, tablet, TV, window, mirror, door, drawer, package, appliance, or other directional object places its content, reflection, handle, opening, or interaction on the wrong face or through an impossible occlusion.

On retry, attach the canonical reference again and request one targeted correction while repeating every identity invariant. For spatial errors, do not ask to erase only the offending mark: either restore the physically correct face or recompose the camera, actor, and object together using the spatial-consistency retry from `prompt-patterns.md`. Never attempt to repair identity drift after omitting the reference image.

## Handle outputs

- Save approved assets inside the current project or requested output directory.
- Use versioned filenames instead of overwriting approved images.
- Report the output mode, final prompt, reference image, opaque source path for Mode B, final path, and any non-default `cutout.py` options.

## Enforce the quality gate

- Recognize the recurring young man and cat in about three seconds.
- Understand the main action or relation in about ten seconds.
- Preserve both identities when pose, expression, props, and setting change.
- Include exactly one gray tabby cat per depicted moment unless the user explicitly requests a scene without the companion.
- Include zero dogs.
- Keep line work, halftone, paper texture, and semantic accents consistent.
- Pass a physical-plausibility check: all visible faces, contents, interactions, supports, shadows, and occlusions agree with one camera viewpoint.
