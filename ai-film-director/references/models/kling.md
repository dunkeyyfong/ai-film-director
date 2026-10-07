# Kling 3.0 (Kuaishou)

Last verified: Oct 2026. Confidence: MEDIUM-HIGH for Kling 3.0 prompting (fal guide, 5 Feb 2026; Morphic and aitoolcurator notes); LOW for Kling 4.0 (vendor-reported, not verified).

## Limits (verify in UI)
- Up to 15 s per clip; up to 6 labeled shots in one prompt; native audio.
- Image-to-video: lock the image first, then describe the move.
- Kling 4.0 status: Flash version in early access since 28 Sep (Ultra Yearly subscribers); full model and API announced for Oct 2026 without a date. Claims of 3-30 s, 4K, up to 15 references and stereo lip-sync are vendor-reported and unverified. Do not promise them.

## Multi-shot structure
- Number shots, anchor the subject in Shot 1 (full identity block), then refer back by role.
- Explicit motion for each shot; one action per shot.
- Turbo multi-shot syntax (third-party): `shot 1, 3s, ...; shot 2, 2s, ...` with each shot under about 500 characters.
- Per-shot structure: Camera, Subject, Environment, Lighting and Mood, Texture and Style.

## Dialogue syntax
- Unique label per speaker: `[Character A: Mother, warm low voice]: "Come in."`
- Action first, then dialogue; link with "Immediately,":
  `Mother lifts the lid of the pot. Immediately, [Character A: Mother, warm low voice]: "Come in."`
- Add a tone label (whispered, firm, cracking).
- Keep lines short; split across shots; test non-English dialogue.

## Template
```
Shot 1 (3s): Camera: [shot size, angle, one move]. Subject: [identity block, verbatim] [one action]. Environment: [location block]. Lighting and mood: [light]. Texture and style: [style block].
Shot 2 (2s): Camera: ... Subject: [Role] [action]. Immediately, [Character A: Role, voice]: "line".
Audio: [ambience], [SFX]; music: [yes/no].
```
For image-to-video, drop the contents of the image and keep motion, camera and sound.

## Negative constraints
Use the UI's negative prompt field if present (typical: distortion, extra limbs, text, watermark). If absent, phrase positively.

## Retry hints
Drift between shots: re-anchor with the full identity block in Shot 1 and shorter later shots. Dialogue assigned to the wrong face: check unique labels and put the action sentence immediately before the line. Over-busy motion: slow verbs, drop to 2 shots.
