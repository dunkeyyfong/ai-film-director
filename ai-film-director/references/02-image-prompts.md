# Image prompts: character sheets, plates, keyframes, edits

Contents: 1 Why images first - 2 Tool notes (Nano Banana, GPT Image) - 3 Style block - 4 Character sheet - 5 Location plate - 6 Props - 7 Keyframes - 8 Storyboard contact sheet - 9 Edit prompts - 10 Naming and delivery

## 1. Why images first

Consistency in AI film is decided before the first video generation. Practitioners lock multi-angle character sheets, approved still frames and a style block, attach them to every clip, and iterate in images because they cost far less than video. Video models also behave better when they start from a good first frame: image-to-video fixes subject, composition, palette and light, so the video prompt only has to direct motion.

Generate 3-4 options for each asset, pick one, and lock it. Expect around five generations to lock one character.

## 2. Tool notes

**Nano Banana / Gemini image models (Nano Banana 2, Nano Banana Pro)**
- Google's own guidance for the Pro model: it is a "thinking" model, so write natural-language descriptions, not comma-tag lists like "cool car, neon, city, night, 8k".
- Supports many reference images (Google's guide cites up to 14, with about 6 held at high fidelity - verify in the tool). Say what each reference is for ("Image 1 is the identity reference for the face; Image 2 is the costume reference") so the model does not guess.
- For edits use the pattern "change only X; keep everything else exactly the same", and repeat the preserve list each iteration.
- Practitioners found Pro adheres to identity details more strongly for character sheets but can look stock-photo clean; generate on both Pro and the faster model and pick the look that fits.

**GPT Image models**
- Structure helps. A reliable skeleton: type of image, subject, identity lock, materials, pose, environment, lighting, camera, grade, text (if any), constraints. Labeled sections beat one long paragraph.
- Edits: separate what changes from what must be preserved. Write "change only X" then an explicit preserve list (face, hairstyle, clothing, pose, background, lighting, framing) and finish with "make no other changes". A longer, more specific preserve list means less drift.
- Repeated edits still move details you asked to keep: check the whole image each time, not only the edited part.
- In the API, an input-fidelity setting exists to preserve distinctive features of the input image; if the user works through the API, mention it.
- Keep in-image text short; polish text in an editor if exactness matters.

**Muse Image (Meta AI, fal, Runware, ComfyUI):** see section 9 of `models/muse.md` for brief order, multi-reference role binding and scoped edits.

**Other tools (Midjourney, Flux, Seedream):** use the same assets and the same discipline. Translate the skeleton to the tool's syntax and ask the user for the tool's reference-image method (for Midjourney: character and style reference parameters). Mark any tool-specific detail you cannot verify as unverified.

## 3. Style block

Write one paragraph, stored in the bible, pasted into every image and video prompt. Include: medium and era (digital cinema, 35mm anamorphic, 16mm, hand-painted animation), lens and depth of field, key light character, colour palette in plain words or hex values, grain and texture, mood in one phrase, and exclusions in positive form. Example shape (replace with the project's own):

```
STYLE: Shot on 35mm anamorphic, shallow depth of field, soft tungsten key light with cool blue street spill, muted teal and amber palette, fine photochemical grain, calm and melancholic mood, natural skin texture with visible pores.
```

Avoid empty praise words ("stunning", "masterpiece", "8k"); they add noise, not control. For Luma Ray models, avoid "vibrant", "whimsical" and "hyper-realistic" in the downstream video prompt as well.

## 4. Character sheet

Build in two passes when realism matters: (a) a face/headshot pass for identity, then (b) a multi-angle turnaround that uses the locked headshot as reference.

Rules learned from practitioners:
- Hands empty. Props in hands cause drift between angles; make the prop its own sheet.
- Neutral, plain background; consistent lighting across panels; full body visible in the body panels; character centered.
- Panels: front, three-quarter, side (true profile), back, plus a face close-up and a mid-shot. Add close-up panels for scars, jewelry and accessories - wide-only sheets make video models hallucinate the missing detail.
- A separate sheet per beat if costume, injury or accessories change.
- For models that struggle with multi-view sheets (Seedance can read a multi-view sheet as several different people), also export one clean close-up headshot and one clean full-body image as separate files.

Template (fill brackets from the bible identity block):

```
Create a professional character reference sheet of ONE character, strictly following the reference image(s) provided.
IDENTITY: [age, ethnicity or species, build, height impression, face shape, eyes, hair colour/length/style, skin details, 2-3 unique marks].
WARDROBE: [each garment with colour, material, fit; footwear; accessories].
LAYOUT: six panels on a plain neutral studio background - front, three-quarter, true side profile, back, a face close-up, and a waist-up mid-shot. Hands empty, relaxed arms. Same character, same outfit, same lighting in every panel.
STYLE: [style block].
Maintain exact identity consistency across all panels. No text, no logos, no extra characters.
```

Aspect ratio 16:9 or 3:2 for the sheet; highest resolution available.

## 5. Location plate

Generate the empty location first (no characters), from the main camera angle and one reverse angle. Include time of day, weather, light sources and their colour, three to five anchoring props, and the style block.

```
Establishing plate of [location], [time of day], [weather]. [Layout: foreground / midground / background]. Light: [source 1 and colour], [source 2 and colour]. Key set pieces: [3-5 items]. No people. [style block]. Aspect ratio [x:y].
```

Keep a reverse-angle plate for dialogue scenes so shot/reverse-shot stays geometrically consistent.

## 6. Props

One sheet per important prop: isolated on neutral background, front/side/top, with a size reference (for example "held in an adult hand, drawn separately"). If a prop must appear in a hand in the film, make a keyframe that shows it in the hand and treat that keyframe as the reference.

## 7. Keyframes (start and end frames)

One start frame per shot; add an end frame for shots where the video model should travel between two defined states (a camera orbit, a transformation, a reveal).

```
[Shot ID] start frame. [Framing and angle], [lens]. [Character identity block, verbatim], [pose and expression], in [location identity block, verbatim]. Light: [as in plate]. [style block]. Aspect ratio [target]. Leave natural room in the frame for the motion that follows: [e.g. space ahead of the walker / headroom for a push-in].
Use Image 1 as the identity reference and Image 2 as the location reference. Keep identity, costume and light identical to the references.
```

Keyframe design rules for image-to-video:
- Only animate what the frame can support. A head-and-shoulders portrait cannot stand up and walk; the model has no body to animate. Generate a wider frame first.
- Match the frame's aspect ratio to the video setting to avoid stretching or bars.
- Do not put readable text in the frame unless you accept retries.
- Keep poses mid-action rather than frozen, so motion has a natural direction.

## 8. Storyboard contact sheet

For fast approval, generate a grid (for example 3x2 panels) of the scene's start frames in one image, with panel numbers matching shot IDs. Use it to approve composition and pacing, then regenerate each approved panel as a full-resolution keyframe with the identity and location references attached.

## 9. Edit prompts (fixing, not regenerating)

Pattern:

```
Edit Image 1. Change only: [the one problem, stated physically]. Preserve exactly: face, hairstyle, skin tone, expression, outfit, pose, background, lighting direction, framing, colour grade. Make no other changes.
```

Use one change per edit. If three things are wrong, either run three edits in sequence (checking the whole image each time) or regenerate with a corrected prompt.

## 10. Naming and delivery

Ask the user to name files with the shot or asset ID (`CHAR-mia-sheet-v2.png`, `LOC-noodle-bar-plate-v1.png`, `S02-SH01-start-v3.png`) so QA can map every image without guessing. Keep every locked reference in one folder; that folder is what gets attached to video prompts.
