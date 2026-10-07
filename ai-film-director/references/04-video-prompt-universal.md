# Universal video brief, model selection, translation and retry ladder

Contents: 1 The universal brief - 2 Choosing a model per shot - 3 Translating the brief into a tool prompt - 4 Shot-writing rules that hold everywhere - 5 Reference handling - 6 Audio in the prompt - 7 Retry ladder - 8 Test before batch

## 1. The universal brief

Write this first for every shot, in plain English, before any tool-specific prompt. It is the single source for all model prompts, so you can switch tools without rewriting the idea. Fill every field; write "none" rather than leaving blank.

```
SHOT ID: S02-SH01          DURATION: 5 s          ASPECT: 16:9
START FRAME: S02-SH01-start-v3.png     END FRAME: none
REFERENCES: CHAR-mia-headshot.png (face), CHAR-mia-full.png (body and costume), LOC-noodle-bar-plate-v1.png (set)
SUBJECT: [identity block, verbatim]
ACTION (one primary action, physical, present tense): ...
CAMERA (one move, with speed): ...
SCENE / LOCATION: [location block, verbatim]
LIGHT AND COLOUR: ...
STYLE: [style block, verbatim]
AUDIO: dialogue [speaker, language, line] / SFX / ambience / music (or "no music")
CONSTRAINTS (positive wording): no on-screen text, no logos or watermarks, no cuts inside the clip, keep identity and costume unchanged
RISKS: [hands on props, two characters touching, readable text, fast motion]
```

## 2. Choosing a model per shot

Facts are dated and carry confidence labels in each model file. Treat this matrix as a starting heuristic and verify limits in the tool's UI, because products change monthly.

| Need | Good first choice | Why (see model file) |
|---|---|---|
| Native dialogue with SFX and ambience, cinematic feel | Veo 3.1 in Flow; Kling 3.0; Seedance 2.0 | All generate audio in the same pass |
| Many references (faces, outfits, set, audio) in one prompt | Seedance 2.0 | 9 images, 3 videos, 3 audios per prompt |
| Multi-shot sequence in a single generation | Kling 3.0, Seedance 2.0, Wan 3.0 | Labeled shots in one prompt |
| Tight control of first and last frame | Veo 3.1 first/last frame; Hailuo-02; Luma keyframes | Frame-to-frame transitions |
| Camera moves driven by explicit commands | Hailuo/MiniMax | Bracket camera commands |
| Animate a still with pure motion direction | Runway Gen-4.5 | First-frame image, motion-only prompt |
| Editing an existing clip | Runway Aleph; Seedance edit phrasing; Luma Modify | Video-to-video |
| Cheap draft or test pass before final | Veo Fast, Seedance Fast/Mini, Kling standard tiers | Spend little to test the idea |
| Atmosphere, inserts, voiceover shots with native ambience (if the user has access) | Muse Video (Meta, early preview) | Unverified; avoid fast motion and on-screen lip-sync |
| Long single clip | Wan 3.0 (2-30 s, vendor); Seedance 2.5 (30 s, vendor) | Verify availability |

Mixed-tool films are normal: choose per shot, but keep identity blocks, style block and approved references identical across tools. Expect each model to render the same face slightly differently, so grade and cut with that in mind, and keep one tool per scene when possible.

## 3. Translating the brief into a tool prompt

1. Open the model file for the tool; copy its template.
2. Map fields: subject, action, camera, scene, light, style, audio, constraints.
3. Apply the tool's grammar (labeled shots, bracket commands, @references, dialogue syntax).
4. Respect the character limit and duration limits.
5. If a start frame is supplied, remove everything the frame already shows and keep motion, camera and sound only (Runway, Kling, Wan I2V, Luma keyframes). Where the tool takes references instead of a first frame (Seedance, Veo ingredients), keep the subject sentence but say what each reference controls.
6. Output a code block per tool, with a one-line "use this when" and the settings to choose (model tier, duration, resolution, aspect ratio, audio on/off, prompt optimiser on/off).

## 4. Shot-writing rules that hold everywhere

- One primary action and one camera move per shot. A second idea belongs in a second shot.
- Mid-action verbs in present tense, with a body part and a degree of speed ("slowly turns her head to the left and lifts her chin").
- Describe emotion as behaviour.
- Camera speed words: slow, steady, gentle, subtle. Slow continuous motion renders best.
- Name the framing (close-up, medium, wide) and the angle (eye-level, low, high) once.
- Say what stays still ("the background stays static") when the model tends to add motion.
- Use positive wording for exclusions ("empty street" instead of "no people"), except where the model's own guide shows a negative-constraint syntax (Seedance closing constraints, Kling negative prompt fields). The model file says which.
- Avoid empty praise words; they add noise.
- Do not contradict the start frame: no new clothing, new location or new lighting in the prompt.
- Keep the same identity block word for word across shots.
- Avoid readable text in frame; add text in post.

## 5. Reference handling

- Attach the approved images only; never attach rejected ones.
- Say what each reference controls: face, costume, set, style, camera movement, voice, motion.
- A clean headshot plus a clean full-body image works better than a multi-view sheet for several models (Seedance reads a sheet as several people).
- Keep the reference count modest (4-5 for Seedance) even where the limit is higher: more references means more conflicts.
- Keep a `reference-map` table in the shot card: file, role, which tool slot it goes in (@Image 1, Ingredient 2, image input).

## 6. Audio in the prompt

For tools that generate audio, write audio direction with the same discipline as the picture: who speaks, in what language, what tone; the two or three sounds that matter; the ambient bed; music yes or no. Keep speech short (about 2.5 s per 5 s clip) and name the speaker. For tools without audio (Runway Gen-4.5, Luma Ray3.14), say "silent" in the card and plan the sound in post.

## 7. Retry ladder (change one thing at a time, in this order)

1. **Read the clip, name the failure**: identity drift, motion wrong, camera wrong, extra cut, artefact, audio wrong, text appeared.
2. **Prompt too long or contradicting itself**: cut to the one action and one camera move; delete anything the start frame shows.
3. **Identity drift**: swap the reference (clean headshot), repeat the identity block verbatim, shorten the shot, move to a shot with a closer framing.
4. **Motion too big or chaotic**: slow the verb ("slowly", "gently"), shorten the duration, break the action into two shots.
5. **Unwanted cut inside the clip**: name the shot size and the single camera move; add "single continuous shot".
6. **Camera ignored**: move the camera sentence to the beginning, use the tool's own camera vocabulary.
7. **Artefacts on hands or props**: re-frame to hide or simplify the hand action; use an end frame.
8. **Dialogue wrong or robotic**: shorten the line, label the speaker, mark the language; if it still fails, generate silent and replace voice in post.
9. **Still failing after three tries**: change the tool for this shot, or change the shot (different angle, different blocking). Do not re-roll the same prompt more than twice.

Log each attempt in the shot card (prompt version, change, result) so the user and other agents do not repeat tries.

## 8. Test before batch

Pick the hardest shot of the scene, run it on the cheapest tier first, check identity and motion, then lock the prompt template and batch the rest. Upgrade to the high-quality tier only for approved prompts.
