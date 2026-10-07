# Image QA: judging the images the user sends back

Contents: 1 Goal - 2 Before you look - 3 Rubric - 4 Diff table - 5 Verdict rules - 6 Set-level check - 7 Fix patterns - 8 Honesty rules - 9 Report template (Vietnamese)

## 1. Goal

Decide, image by image and as a set, whether the stills are safe to feed into video generation. A video model amplifies whatever is in the start frame: a wrong sleeve colour becomes a wrong sleeve colour in every frame of every clip. The QA step exists so the user finds that out in a cheap image, not in an expensive clip.

## 2. Before you look

1. Identify each image from its filename or the user's message: reference sheet, location plate, prop sheet, keyframe (which shot), or storyboard contact sheet. If you cannot tell, ask.
2. Load the sources of truth: the identity block, location block, prop block and style block from `project-bible.md`; the already-approved references; the shot-list row for keyframes (framing, action, characters, light).
3. Treat the first approved sheet of a character as the master. Every later image is compared with the master, not with your memory of the previous image (drift compounds when you compare only neighbours).

## 3. Rubric (score each 0-2: 0 = fail, 1 = minor issue, 2 = good)

| # | Criterion | What to check |
|---|---|---|
| 1 | Identity | Face shape, eye colour and shape, hair colour/length/style, age impression, build, skin marks vs the master |
| 2 | Costume and props | Each garment, colour, material, fit, accessories, number of items (extra or missing buttons, straps, rings) |
| 3 | Anatomy | Hands and finger count, limbs, joints, neck, teeth, eyes aligned, no merged bodies; check hands holding anything |
| 4 | Style match | Lens feel, light character, palette, grain, medium vs the style block |
| 5 | Light and colour | Light direction and colour consistent with the plate and with other keyframes of the same scene |
| 6 | Composition vs shot list | Framing, angle, subject placement, headroom or room for the planned motion, aspect ratio |
| 7 | Location match | Layout, key set pieces, time of day, weather vs the plate |
| 8 | Clean frame | No stray text, watermarks, logos, duplicated objects, artefacts, extra people |
| 9 | Animatability | Can the planned motion happen from this frame? (body visible enough, pose mid-action, no tangents or hidden limbs that will melt) |

Reference sheets are scored on 1, 2, 3, 4, 8 and on layout (all requested panels present, same character in every panel, hands empty, plain background). Location plates are scored on 4, 5, 7, 8. Keyframes use all nine.

Any **0 on Identity or Anatomy** forces REDO or FIX regardless of the total.

## 4. Diff table: what changed or drifted

This is the part the user asked for explicitly: "has anything changed". Fill one table per image, comparing to the master or to the spec. Only list rows where you compared something; mark "cannot judge" honestly.

| Element | Spec / master says | This image shows | Status |
|---|---|---|---|
| Hair | Black, shoulder length, centre part | Black, shoulder length, side part | CHANGED (minor) |
| Jacket | Olive canvas, two chest pockets | Olive canvas, one chest pocket | DRIFT (fix) |
| Scar | Left eyebrow | Not visible (face turned) | CANNOT JUDGE |
| Light | Warm key from camera left | Warm key from camera left | OK |

Status vocabulary: OK, CHANGED (minor), DRIFT (must fix), MISSING, EXTRA, CANNOT JUDGE. Order rows so the DRIFT and MISSING rows come first.

## 5. Verdict rules

- **PASS**: no 0s; no DRIFT rows on identity, costume or anatomy; total at least 80 percent of the maximum. Minor CHANGED rows are listed and accepted explicitly, and the bible is updated if the accepted change becomes the new canon.
- **FIX**: one or two localised problems, the rest is good. Give an edit prompt (section 7) that changes only the broken thing. Never recommend FIX when the problem is the face identity of a hero character after two failed fixes; go to REDO.
- **REDO**: identity wrong, multiple problems, wrong composition, or a failed fix. Give a rewritten prompt that adds the missing constraint, plus the references to attach.
- After **two failed FIX rounds** on the same image, switch to REDO with a changed approach (different reference, different tool, simpler pose), not a third identical fix.

Be specific about the reason in one line per verdict, with the strongest evidence first.

## 6. Set-level check (do this after every image has a verdict)

Answer these and give the set a verdict: CONSISTENT / MOSTLY CONSISTENT (list fixes) / NOT YET.

- Does every image of the same character read as the same person at thumbnail size? Place the faces side by side mentally; compare hairline, jaw, eye spacing.
- Is costume identical across the images of the same beat?
- Is the colour grade and light logic consistent inside a scene, and does the palette hold across scenes unless the bible changes it deliberately?
- Do locations keep the same layout and key set pieces when seen from different angles?
- Does the lens and depth of field feel the same across the set (no switching between wide-angle phone look and cinema look)?
- Is the aspect ratio uniform?
- Which shots are still missing a start frame or end frame?
- Which images are the **approved set** to attach to video prompts? Output this as a list of filenames. Mark everything not on the list as rejected.

## 7. Fix patterns

Edit prompt (for FIX), one change at a time:

```
Edit Image 1. Change only: [physical description of the single problem, e.g. "add the second chest pocket on the left side of the jacket, matching the right pocket"]. Preserve exactly: face, hairstyle, skin tone, expression, outfit (except the change), pose, background, lighting direction, framing, colour grade. Make no other changes.
```

Common problems and the usual remedy:

| Problem | First remedy | If it fails |
|---|---|---|
| Face drifted from master | Regenerate with master headshot attached as identity reference, "same person as Image 1" | New headshot pass; reduce style words that change faces (heavy filters, extreme lighting) |
| Hands wrong | Crop, ask for a zoomed edit "Change only: the right hand, five fingers resting on the table" | Re-pose so hands are hidden or simple (in pocket, behind object) |
| Costume detail missing | Add the detail to the prompt verbatim from the identity block | Create a costume close-up reference and attach it |
| Style drift | Paste the style block verbatim at the end of the prompt | Attach an approved image as the style reference |
| Light direction mismatch | State the light direction and colour explicitly and attach the plate | Regenerate the plate with a clear lighting diagram in words |
| Unwanted text or logo | Edit: "Change only: remove the text on the sign, leave the sign blank" | Inpaint in an editor |
| Wrong aspect ratio | Regenerate; do not crop if the framing then breaks | Outpaint carefully, then re-check |
| Extra people | Edit "Change only: remove the person on the right" | Regenerate the plate without people |
| Pose cannot animate | Generate a wider frame; mid-action pose | Pick a different start frame; use the end-frame feature instead |

Remember that each edit can move other things. After every FIX, re-check the whole image against the diff table, not only the edited area.

## 8. Honesty rules

- Say what you cannot see. Small hands, jewellery, text on props and eye details are often too small to judge in a downscaled upload; ask for a crop or the full-resolution file.
- If a comparison depends on an image the user has not sent (the master), say so and ask for it. Do not fill the gap with the bible text alone and call it verified.
- Do not praise in order to be pleasant. A PASS is a claim that the image is safe to spend credits on.
- Do not invent flaws either. If the image is good, say PASS and say why in one line.
- If the user disagrees with a verdict, restate the evidence once; if they still prefer the image, record it as an accepted change in the bible and move on.

## 9. Report template (reply in the user's language, default Vietnamese)

```
# Image QA - [project] - [date] - round [n]

## Tổng quan
Đã xem [n] ảnh. PASS: [n] · FIX: [n] · REDO: [n]. Bộ ảnh: [CONSISTENT / MOSTLY CONSISTENT / NOT YET].
Việc quan trọng nhất cần làm tiếp: [one line]

## Ảnh 1 - [filename] ([what it is])
Điểm: Identity [0-2] · Costume [0-2] · Anatomy [0-2] · Style [0-2] · Light [0-2] · Composition [0-2] · Location [0-2] · Clean [0-2] · Animatable [0-2]
Verdict: PASS / FIX / REDO - [one-line reason]
Bảng thay đổi (diff):
| Element | Spec / master | Ảnh này | Trạng thái |
|---|---|---|---|
Prompt sửa (nếu FIX/REDO):
[code block]
Cần xem kỹ hơn: [crops requested, if any]

(repeat per image)

## Kiểm tra cả bộ
[bullets from section 6]

## Bộ ảnh đã duyệt (dùng làm reference cho video)
- [filenames]

## Bước tiếp theo
[what to regenerate, in order; or "sẵn sàng sang Phase 5"]
```

Save the report to `image-qa/round-[n].md` (template in `assets/image-qa-report-template.md`).
