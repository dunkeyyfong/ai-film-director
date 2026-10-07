# Muse (Meta Muse Video and Muse Image)

Last verified: 7 Oct 2026. Confidence: HIGH for status facts (Meta announcement, 7 Jul 2026); MEDIUM for Muse Image prompting (Runware and ComfyUI docs for the Meta Model API); LOW for every Muse Video prompting rule, which is inferred (see "Where the rules come from"). Read this whole file before writing a Muse prompt.

Contents: 1 Identify the product - 2 Status and specs - 3 Where the rules come from - 4 Muse Video prompt structure - 5 Templates - 6 Worked examples - 7 Audio and dialogue - 8 Image-to-video and references - 9 Muse Image for keyframes - 10 Pre-flight checklist - 11 Retry ladder

## 1. Identify the product first

"Muse" covers several different things. Ask the user for the app name or URL before writing anything.

| What the user has | What it is | What to do |
|---|---|---|
| Meta AI app / meta.ai, "Muse Video" option | Meta Superintelligence Labs video model | Use this file. |
| Meta AI app / meta.ai / fal / Runware / ComfyUI, "Muse Image" | Meta image model (released) | Use section 9 for references and keyframes. |
| musevideo.ai, musevideo.dev, musevideos.io, muse-video.app and similar | Third-party wrapper sites. At least one (musevideo.ai) states it is "not an official Meta product or API endpoint" and offers Wan, Kling and Grok Imagine models | Ask which model the dropdown shows. If it is Wan or Kling, use `wan.md` or `kling.md`, not this file. |
| muse.ai | Video hosting and search platform | Not a generator. Pick another tool. |
| "Muse" personal agent in Meta AI (Connect 2026) | Meta's assistant product; video chat with avatars announced "coming soon" | Not a filmmaking video model. |
| Microsoft Muse | Gameplay world model for game ideation | Not a prompt-to-video film tool. |

## 2. Status and specs (verify in the UI)

- **Announced:** 7 Jul 2026 with Muse Image, as an "early preview". Meta's wording: Muse Video is "coming soon to creators and Meta AI".
- **Release:** As of 7 Oct 2026 no public release date, no API, no price, no published clip length, resolution, frame rate or aspect ratios. Meta Connect 2026 (23-24 Sep) focused on the Muse agent and did not launch Muse Video. If the user can generate with it, they are in an early-access group or the rollout has started since this file was written. Ask them to read the controls off the screen: duration, aspect ratio, resolution, image input, audio toggle, number of takes.
- **Meta's stated strengths:** prompt adherence, visual fidelity, temporal consistency, native audio generated in the same pass as the picture. Preview clips showed room tone, diegetic foley and voiceover in ad-style pieces.
- **Meta's stated gaps:** audio-video synchronisation and physically accurate fast motion.
- **Arena:** #3 text-to-video by human-preference Elo (5 Jul 2026).
- **Provenance:** Muse Image outputs carry Meta's invisible "Content Seal" watermark. Meta said Content Seal is coming to Muse Video. Disclose AI use anyway (see `../05-audio-post-legal.md`).
- **Ignore unsourced specs.** Some blogs quote 30 s clips, 4K, 28 voice languages or "prompts under 15 words". None of these come from Meta and they contradict its preview-only status. Do not plan around them.

## 3. Where the rules come from

There is no official Muse Video prompt guide yet. The rules below combine three things, in this order of weight:

1. **Meta's own statements** (section 2): lean on adherence, fidelity, consistency and ambient/foley/voiceover audio; design around fast motion and lip-sync.
2. **Muse Image's documented behaviour.** Muse Video is built on the same pretraining base. Muse Image reads a prompt as a full specification (a "brief"), plans the layout before rendering, has no negative-prompt field, and resolves contradictions silently. Hosted guides tell you to write a production brief in full sentences, state counts and positions exactly, name lens and light direction, repeat identity wording verbatim, and change one clause per iteration. It is reasonable, but **not verified**, that the video model reads prompts the same way.
3. **The universal discipline** in `../04-video-prompt-universal.md`: one action, one camera move, short clips.

Label every Muse Video prompt "Muse: unverified" in the shot card. Run one test clip before batching (see section 10). When Meta publishes a guide, replace sections 4-8 with it and update `../sources.md`.

## 4. Muse Video prompt structure

Write the prompt as a short **production brief** in full sentences, not a keyword list. Keep this order. It mirrors the order hosted Muse Image guides recommend (deliverable, subject, setting, light, camera, focus, style), with motion and sound added for video:

1. **Deliverable and duration:** what the clip is and how long it runs. ("A five-second single continuous shot for a short drama.")
2. **Camera:** shot size, angle, lens, one camera move with speed. ("Medium close-up at eye level, 50mm lens, slow push-in.")
3. **Subject:** the identity block, verbatim from the bible.
4. **Action:** one primary action, present tense, with body part, direction and speed. Add a sentence for what stays still.
5. **Setting and layout:** the location block, verbatim, plus exact positions ("the counter runs out of frame to the right; two stools on the left").
6. **Light:** source, direction, quality, colour temperature, time of day.
7. **Focus and depth of field:** what is sharp, what falls off.
8. **Style:** the style block, verbatim (medium, film stock or grade, palette, texture).
9. **Sound:** ambience bed, two or three specific SFX, music or "no music", then any dialogue or voiceover (section 7).
10. **Continuity guard:** a positive closing line ("Single continuous shot; her face, hair and costume stay exactly as described; the background stays still.")

Rules:
- **Be specific and countable.** "Three paper lanterns, the largest in the centre" holds across takes; "some lanterns" changes every take.
- **No contradictions.** The model will pick one side without telling you. Check that the camera, light and action sentences agree with the start frame.
- **Positive wording only.** Assume there is no negative-prompt field. Write "an empty street at dawn", not "no people".
- **Slow, continuous motion.** Avoid running, fights, sports, fast pans, whip pans, quick hand work and object hand-offs. Split fast beats into a slow shot and an implied cut.
- **One idea per clip.** If the UI offers longer durations, still use one action per 4-6 s. Do not stack shots inside one Muse prompt until multi-shot behaviour is documented.
- **Length:** a full brief of about 80-180 words is a good starting range for this style of model (an inference, not a documented limit). If the UI shows a character limit, respect it and cut the style details first, never the identity block.
- **Verbatim blocks.** A paraphrased identity block reads as a different person. Copy it character for character.
- **No readable text** in frame (signs, labels, subtitles); add text in post.

## 5. Templates

### Text-to-video (full brief)
```
A [N]-second single continuous shot for [deliverable: short film scene / product ad / music video].
Camera: [shot size], [angle], [lens]mm lens, [one camera move] at a [slow/steady] pace.
Subject: [IDENTITY BLOCK, verbatim].
Action: [subject] [one physical action with body part, direction and speed]. [What stays still].
Setting: [LOCATION BLOCK, verbatim]. [Exact positions of key objects relative to frame].
Light: [source] from the [direction], [hard/soft], [colour temperature], [time of day]; [shadow detail].
Focus: [what is sharp]; [what falls out of focus].
Style: [STYLE BLOCK, verbatim].
Sound: ambience of [bed]; [SFX 1], [SFX 2]; [music description / no music]. [Dialogue or voiceover line, see audio rules].
Continuity: single continuous shot, [subject]'s face, hair and costume stay exactly as described, steady natural motion.
```

### Image-to-video (only if the UI accepts a start image)
The image already sets identity, set, light and framing. Describe motion, camera and sound only, and do not contradict the image.
```
Animate the provided image as a [N]-second single continuous shot.
Camera: [one camera move] at a [slow/steady] pace; framing stays [shot size].
Motion: [subject role] [one slow action]; [secondary natural motion: hair, steam, fabric, leaves]; [what stays still].
Sound: ambience of [bed]; [SFX]; [music / no music].
Keep the face, costume, lighting and composition of the image unchanged.
```

### Voiceover shot (preferred over on-screen dialogue)
```
[Full brief as above, with the subject's mouth closed or face turned away from camera]
Sound: [ambience]; [SFX]. A [gender-neutral or specified] narrator's voice, [tone, pace], says in [language]: "[one short sentence]". [Music / no music].
```

## 6. Worked examples

All three use invented characters. Replace the blocks with the project bible's.

**A. Quiet drama beat (text-to-video, no dialogue)**
```
A five-second single continuous shot for a short drama.
Camera: medium close-up at eye level, 50mm lens, slow push-in toward the subject's face.
Subject: Mia, a woman in her late twenties with a straight black bob cut at the jaw, a small mole under her left eye, wearing a faded mustard-yellow apron over a white linen shirt with rolled sleeves.
Action: Mia slowly lifts her eyes from the steaming bowl in front of her and looks toward the door on the right of frame, her hands resting still on the counter.
Setting: a narrow late-night ramen counter with dark walnut wood, three paper lanterns hanging above, the largest in the centre; rain-streaked glass door on the right edge of frame.
Light: warm tungsten light from the lanterns above, soft and low; cool blue streetlight leaks through the door on the right; gentle shadows under her cheekbones.
Focus: Mia's eyes are sharp; the lanterns and the door fall into soft bokeh.
Style: photoreal 35mm film look, soft halation around highlights, fine grain, muted teal and amber palette.
Sound: ambience of steady rain on glass and a low refrigerator hum; a faint ceramic clink as the spoon settles in the bowl; no music.
Continuity: single continuous shot, Mia's face, hair and apron stay exactly as described, steam rises slowly, the background stays still.
```

**B. Product reveal (text-to-video, music only)**
```
A six-second single continuous shot for a product ad.
Camera: low-angle close-up, 85mm lens, slow orbit from left to right around the product, a quarter turn in total.
Subject: a matte sage-green ceramic coffee dripper with a thin gold rim, sitting on a round glass carafe.
Action: hot water pours in a thin, steady stream from a gooseneck kettle entering from the top of frame; coffee drips slowly into the carafe.
Setting: a pale oak counter; one folded linen cloth on the left; a plain warm-grey wall behind.
Light: morning daylight from a tall window on the right, soft and diffused, casting a long soft shadow to the left.
Focus: the dripper rim and the water stream are sharp; the wall falls into soft blur.
Style: clean commercial product cinematography, warm neutral palette, gentle contrast.
Sound: soft pouring water and slow drips; a quiet room tone; gentle acoustic guitar music at low volume.
Continuity: single continuous shot, the dripper's shape, colour and gold rim stay unchanged, the stream stays smooth and continuous.
```

**C. Atmospheric establishing shot (image-to-video)**
```
Animate the provided image as a five-second single continuous shot.
Camera: slow, steady crane up from street level, ending slightly above the rooftops; framing stays wide.
Motion: light rain falls; neon reflections ripple gently in the puddles; a single cyclist in the far distance rides slowly from left to right; the buildings stay still.
Sound: ambience of soft rain and distant city traffic; one faint bicycle bell far away; low ambient synth pad.
Keep the architecture, colours, lighting and composition of the image unchanged.
```

## 7. Audio and dialogue

Meta flags audio-video sync as a weak point. Plan around it:
- **Prefer ambience, foley and voiceover.** These worked in Meta's preview clips and do not need lip-sync.
- **On-screen dialogue:** at most one short sentence (about 2-2.5 s) per clip, one speaker, face at medium close-up or wider, slow head movement. Attribute it clearly: `Mia says quietly in Vietnamese: "Anh về rồi à?"`. Name the language.
- **Hide the mouth when you can:** back to camera, profile, a hand near the face, or a cutaway. Then the voice can be replaced in post with no visible mismatch.
- **Non-English dialogue,** including Vietnamese, is not documented. Test one clip first. Keep a fallback: generate the shot with ambience only and record or synthesise the voice separately, then lip-sync in post.
- Describe sounds as concrete sources ("a ceramic spoon settling in a bowl"), not moods ("tense audio").
- Always say "no music" when you do not want a score. Generators tend to add one.

## 8. Image-to-video and references

- Meta has not confirmed image-to-video or reference images for Muse Video. Muse Image supports 1-10 references, so a reference feature is plausible. Use what the UI shows.
- If a start image is accepted, attach the approved keyframe from Phase 4 and use the image-to-video template. Remove everything the image already shows from the prompt.
- If reference images (not a start frame) are accepted, bind each image to a role in words, as Muse Image does: "the woman from the first image, wearing the apron from the second image, in the ramen bar from the third image". Use ordinal references unless the UI shows a different syntax (some hosts use `@Image1`, `@Image2`).
- If neither is supported, text-to-video depends entirely on the verbatim identity block. Keep shots closer, shorter and fewer per character. Consider generating that character's key shots in a tool with reference support (Veo Ingredients, Seedance, Kling) and using Muse for establishing shots, inserts and atmosphere.

## 9. Muse Image for references and keyframes

Muse Image is released (Meta AI app, meta.ai, Instagram Stories in the US, WhatsApp in some countries; developer access via the Meta Model API on fal since 1 Sep 2026, plus Runware and ComfyUI partner nodes). It suits Phase 3 keyframes and sheets well:
- Write a full brief in this order: deliverable, subject and action, setting and props with positions, lighting, camera and framing, depth of field, style and palette. A long prompt is fine; the hosted API accepts very long prompts.
- No negative prompt and no seed. Generate several takes and pick one; you cannot reproduce a take later, so save approved images immediately.
- Multi-reference: 1-10 images. Bind roles in words ("the woman from the first image ... the coat from the second image"). Give a character and a location as separate references and repeat the identity block verbatim in every call. Hosted guides note that "a paraphrase between calls reads to the model as a change".
- Editing: send one image with one scoped instruction. The rest of the frame is meant to stay unchanged, which fits FIX verdicts from Image QA.
- The API offers a "thinking" level (high by default; low for simple single subjects) and a fixed set of output sizes. Each size gives a different composition, not a crop, so pick the size that matches the video aspect ratio before generating keyframes.
- QA Muse Image outputs with `../03-image-qa.md` exactly as for other tools.

## 10. Pre-flight checklist (run before every Muse Video batch)

1. The user has confirmed it is Meta Muse Video, not a wrapper running another model (section 1).
2. The UI controls are written into the shot card: duration, aspect, resolution, image input yes/no, audio yes/no.
3. The prompt follows section 4 order, has one action and one slow camera move, and contains no fast motion.
4. The identity, location and style blocks are pasted verbatim.
5. There are no contradictions with the start frame, if one is used.
6. The audio plan uses voiceover or ambience, or else at most one short attributed line.
7. Test one clip, check identity, motion and audio, then lock the template and batch.

## 11. Retry ladder (Muse-specific; then continue with the universal ladder)

1. **Motion smeared or physically wrong:** slow every verb, shorten duration, remove the second moving element, make the camera static.
2. **Identity drift:** re-paste the identity block verbatim, move to a closer framing, shorten the clip; if the UI accepts an image, switch to image-to-video with the approved keyframe.
3. **Lips out of sync:** turn the line into voiceover, hide the mouth, or generate without dialogue and add the voice in post.
4. **Wrong or busy audio:** list the exact ambience and two SFX, and add "no music" explicitly.
5. **Layout ignored:** state positions relative to frame edges ("on the left third", "out of frame to the right") and give exact counts.
6. **Still failing after three tries:** move the shot to a documented tool (Veo, Kling, Seedance) and keep Muse for shots it handles well.
