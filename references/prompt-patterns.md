# Prompt patterns

## Mode A style anchor

```text
Professional friendly editorial manga/comic ink illustration. Preserve the exact recurring rounded young man and gray tabby cat from the attached identity reference. Use clean confident black outlines with varied line weights, expressive but controlled. Use classic circular halftone screentone for gray and shadow areas. Use an off-white lightly textured real environment with only useful props. Color is restrained: black, off-white, halftone gray, muted orange only for the cat collar, plus at most two muted semantic accent colors. Choose the cat's eye state and pose to match the scene: open attentive eyes for observing or interacting, closed eyes only for genuine sleep or rest. Do not make the cat sleep by default. No dog, no glasses, no thin stick figure, no extra animal, no 3D, no glossy gradient, no photorealism, no generic card grid, no dashboard, no clutter, and no watermark.
```

## Aspect-ratio block

```text
Canvas aspect ratio: <1:1, 4:3, 16:9, 9:16, or 3:4>. Use the exact requested canvas ratio and compose the full scene to fill that shape naturally. Default to 1:1 when no ratio or orientation is specified. Map wording exactly: 4:3 = landscape, 16:9 = wide landscape, 纵向/portrait = 9:16, 3:4 = portrait, 1:1/square = square. Do not crop a square composition into another ratio or silently substitute a different ratio.
```

## Exact-label block

```text
Text (verbatim): Render these exact labels as part of the bitmap illustration:
"<label 1>", "<label 2>", "<label 3>".
Use each phrase exactly once. Do not translate, paraphrase, misspell, repeat, or add other text. Use modern Chinese sans-serif medium/bold typography, large and readable. Place every label on or directly beside its evidence surface.
```

## Physical-consistency block

```text
Use one coherent real-world camera viewpoint and treat every prop as a solid object with distinct front, back, inside, outside, top, and underside surfaces. Put interfaces, text, images, controls, openings, and labels only on the physical face that actually supports them. Keep the character's gaze, hands, reach, keyboard/mouse direction, chair position, supports, perspective, shadows, and occlusion consistent with that viewpoint. If the camera sees the rear of a monitor, laptop lid, phone, tablet, book, sign, package, door, appliance, or vehicle, show a believable plain rear/exterior surface and no front-side content. If front content is essential, rotate or recompose the entire scene so that content-bearing face is genuinely visible. Never mirror a single object or body part in isolation. Prefer omitting hidden information over violating physical reality.
```

Use this directional-object audit for every prop with a meaningful side:

```text
Directional-object audit: For each book, page, document, phone, tablet, laptop, monitor, TV, window, mirror, picture frame, door, drawer, cabinet, package, bottle, vehicle, tool, or appliance, name the camera-visible face and the actor-facing/functional face. Put readable content, controls, reflections, handles, openings, hinges, and interactions only on their real supporting face. Keep page order, spine, folds, pane/frame boundaries, glass reflections, lid/hinge, object thickness, supports, shadows, and occlusion physically connected. If the functional face is hidden, omit its content. Never paste a front surface onto a back, side, underside, closed interior, wall behind a window, or disconnected object.
```

Actor-orientation selection:

```text
Keep the recurring young man front-facing or front three-quarter when that does not conflict with the focal object. If a screen, book, document, phone, tablet, TV, or tool is the evidence, prefer a physically clear side, rear three-quarter, or over-the-shoulder view like a real operator/viewer. Keep user, functional face, hands, gaze, and supports on one coherent side. Do not force a full face if doing so makes the focal surface face away from the user or camera, and do not turn the person solely to hide an object error.
```

Scene-angle selection:

```text
For screen editing, use side/rear three-quarter or over-the-shoulder when screen content is essential. For reading/writing, use over-the-shoulder/rear three-quarter when page content is essential. For sports, choose the angle that keeps ball/tool contact, weight, reach, and foot trajectory believable. Use a front-facing portrait only when no focal directional surface conflicts with it.
```

Choose exactly one display-content mode for each screen-like object; both are valid, but do not mix them:

```text
Display mode: <visible-front OR hidden-back>.
Visible-front means the real content-bearing display plane faces the user and is genuinely visible to the camera; put all UI, text, images, and controls only inside that front plane, and keep the outer lid/back separate and plain. Hidden-back means the camera sees only a believable plain rear casing/exterior while the display faces the user but is hidden; omit all UI, text, images, glow, screen border, and front-face details from the visible rear. If content is not physically visible, omit it instead of inventing a second-facing surface.
```

## Monitor viewpoint examples

```text
Hidden-back composition: The seated man looks at the display. The camera is behind and slightly beside the monitor, looking toward the man. The display surface faces the man and is hidden from the camera. The camera sees only the plain rear casing, rear edge, and stand. No UI, chart, text, glow, screen bezel, or content panel appears on the rear casing.

Visible-front composition: Use an over-the-shoulder or side three-quarter camera angle with the user and camera on the same side of the display. The display plane visibly faces the seated man and is also obliquely visible to the camera. Put UI content only inside that front display plane. The rear casing remains separate and plain.
```

## Identity retry

```text
Keep the scene, composition, actions, props, correct labels, and colors unchanged. Using the attached canonical reference, change only the recurring character identity: restore the same rounded young man with no glasses and the same single gray tabby cat with white muzzle, white paws, three forehead stripes, and orange collar. Remove every dog and additional animal. Do not alter anything else.
```

## Text retry

```text
Keep the scene, composition, characters, objects, colors, and all correct labels unchanged. Change only the incorrect text "<wrong>" to the exact text "<right>". Do not add, remove, translate, or repeat any other text.
```

## Spatial-consistency retry

```text
Correct the scene's physical viewpoint and object orientation as one coherent composition. The camera is <camera position>. The character is <actor position> and interacts with <actor-facing surface>. The camera must see <camera-visible face>; it must not see <hidden face or content>. Move or rotate the whole object and any dependent hands, gaze, controls, supports, shadows, and occlusions together. Put no interface, text, image, button, opening, or front-face detail on the wrong side. Preserve the recurring character identities, intended action, style, and all unrelated correct elements.
```

## Display-mode retry

```text
Keep the scene and identities unchanged. Set the screen-like object to exactly one mode: <visible-front OR hidden-back>. If visible-front, rotate/recompose the whole camera, user, object, hands, gaze, keyboard, hinge, and shadows so the real front display plane faces both user and camera; place content only inside that plane. If hidden-back, keep the visible rear casing plain and remove all UI, text, images, glow, border, and front-face details from it; the user may continue looking toward the hidden display. Do not mirror a single surface or preserve an impossible hybrid.
```

## Directional-object retry

```text
Keep the scene, identities, style, and unrelated correct objects unchanged. Correct the directional-object logic for <object>. The camera sees <visible face>; the actor uses/sees <functional face>. Move or rotate the whole object and all dependent hands, gaze, page order, hinge, frame, reflections, supports, shadows, and occlusions together. Restore content, controls, handles, openings, or reflections only to their real face. Remove any such detail from the back, side, underside, closed interior, wall behind a window, or disconnected surface. If the functional face is hidden, leave it hidden rather than inventing a second front.
```

## Front-actor / hidden-back recipe

```text
Keep the person front-facing or front three-quarter. Show the back/outer surface of <object> to the camera while its functional face genuinely faces the person. The person's face remains visible, with gaze, hands, body position, and support consistent with interacting with the hidden face. Show only believable rear details on the object and no front content, UI, writing, reflection, opening, or control on that rear surface. It is correct for the viewer not to see the object's content. Do not rotate the person into a back view or make the person look through the solid object.
```
