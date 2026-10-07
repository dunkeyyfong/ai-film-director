# Seedance 2.0 (ByteDance) - notes from Runway's guide

Last verified: Oct 2026. Confidence: HIGH for prompt structure (Runway official guide, 24 Sep 2026); MEDIUM for limits (check the host UI, because limits differ by platform); LOW for Seedance 2.5 (vendor-reported).

## Limits (verify in host UI)
- Duration 5-15 s per clip; aspect ratios from 21:9 to 9:16; 480p / 720p / 1080p. Fast and Mini variants cap at 720p.
- Per prompt: up to 9 images, 3 videos and 3 audios. Total reference video + audio is 15 s; reference video at 720p or below.
- Public figures are moderated: use original characters.
- Seedance 2.5 (vendor-reported): up to 30 s, up to 50 references, timestamped editing. Confirm availability before promising it.

## The eight elements
Subject, action, scene, lighting and colour, camera movement, style, image quality, constraints. Write them as connected sentences, not a keyword list.

## Structure
- Label shots in event order: `Shot 1: ... Shot 2: ...`.
- Inside each shot, order the sentence as: camera, then subject action, then spatial change, then audio.
- Let the model pace the shots; do not force fixed durations per shot unless required.
- One camera move per shot; slow continuous motion; emotion as physical behaviour.

## References
- Define the subject before you reference it: `Define the woman in the linen apron in @Image 1 as the ceramicist.` Then use "the ceramicist" in the prompt.
- Label every reference with what it governs, for example `@Image 1 is the sole authority on the ceramicist's face and costume. @Image 2 is the sole authority on the studio layout. @Video 1 is the sole authority on camera movement. @Audio 1 provides the music mood.`
- Use 4-5 assets even though the limit is higher. A clean headshot plus a clean full-body image beats a multi-view sheet (a sheet can be read as several different people).

## Symbols for sound and text
- `{dialogue}` in braces for spoken lines, `(music)` in parentheses, `<sfx>` in angle brackets, corner brackets for subtitles.
- If dialogue is not in English or Chinese, mark the language explicitly (`{Vietnamese: "..."}` style, and test; support for Vietnamese is not documented in the sources used here).

## Closing line
End with image quality plus constraints: `Cinematic, sharp, natural skin texture. Keep it subtitle-free, do not generate a logo or watermark.`

## Template
```
Define [the role] in @Image 1 as [role name]. @Image 1 is the sole authority on [face and costume]. @Image 2 is the sole authority on [setting].
Shot 1: [camera move and framing], [role name] [one primary action with body part and speed] in [setting], [light and colour]; [spatial change]. {Role name says: "line"} <sfx: ...> (music: ... or none)
Shot 2: [camera], [action]...
[Style]. [Image quality]. Keep it subtitle-free, do not generate a logo or watermark; keep [role name]'s face and costume unchanged.
```

## Editing existing video
`Remove [object] from @Video 1, keeping the rest unchanged.` Same pattern for replace or add: name what changes, then state what stays.

## Retry hints
Faces differ between shots: re-label the references as sole authority and reduce to headshot + full body. Camera ignored: attach a reference video for movement. Extra cuts: reduce to one shot per prompt and name the camera move.
