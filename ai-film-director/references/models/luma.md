# Luma Ray (Ray3 / Ray3.14 / Ray3.2)

Last verified: Oct 2026. Confidence: HIGH for prompt rules (Luma field guide, 27 Feb 2026); MEDIUM for model specs (change often; check the UI).

## Limits (verify in UI)
- Ray3.14: no character reference (Ray3 has it), no native audio, text-to-video 5 or 10 s, image-to-video 5 s, six aspect ratios including 21:9, HDR and EXR output.
- Ray3.2: 16 keyframes, 20 s video-to-video.
- Luma also hosts other models (Veo access with up to 3 reference images, 1080p at all durations, 4K upscaling). Check which model the user selects.

## Template (official)
`Create a video of [SUBJECT] [MID-ACTION VERB] in [SETTING], [SECONDARY MOTION], [CAMERA], [LIGHTING/MOOD].`

## Rules
- Positive-only wording: describe what is there, not what is absent.
- Use mid-action verbs ("is lifting", "turns"), not "begins to".
- Add secondary consequences (steam, fabric, dust, reflections).
- About 100 words; present tense.
- Avoid the words vibrant, whimsical, hyper-realistic, beautiful, stunning.
- With keyframes, describe only what changes between them.

## Modify (video-to-video)
Describe the end state; no commands ("make", "change"), no temporal language ("then", "after"); positive only.
`The street is wet at dusk with warm lamp light reflecting on the pavement; the walker, framing and camera path remain as in the original.`

## Example
`Create a video of a cook in a white apron lifting a wire noodle basket from boiling water in a narrow ramen bar, steam rolling across his forearms, slow push-in at eye level, warm tungsten key with cool blue street spill.`

## Retry hints
Style drifts: remove praise words and name one lens or film stock. Motion stalls: replace "begins to" with a mid-action verb. Keyframe morph: shorten the prompt to the change only.
