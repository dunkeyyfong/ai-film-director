# Google Veo 3.1 and Flow

Last verified: Oct 2026. Confidence: HIGH for the formula, audio syntax and features (official Google Cloud prompt guide, 16 Oct 2025); MEDIUM for Flow UI details (third-party); LOW for anything about new tiers. Re-check limits in the Flow UI before writing final prompts.

## Specs (verify in UI)
- Resolution 720p or 1080p; aspect 16:9 or 9:16; clip length 4, 6 or 8 s; native audio (dialogue, SFX, ambience, music).
- Flow model picker (third-party report) lists Lite / Fast / Quality tiers and a Gemini Omni Flash option. Use Fast to test and Quality for finals (Luma-hosted guide gives the same advice for Veo access).
- Features: text-to-video, Ingredients to Video (reference images), first and last frame, add or remove object on existing video (Veo 2 based, no audio), SynthID watermark on outputs.
- The Veo 3 API was shut down on 30 Jun 2026 (third-party). If the user calls the API, check which version is live.
- Flow supports @name references to assets (third-party).

## The formula (official)

`[Cinematography] + [Subject] + [Action] + [Context] + [Style & Ambiance]`

Write each as a clause; add audio as separate sentences at the end.

```
[Cinematography: shot size, angle, camera move]. [Subject: identity block]. [Action: one primary action]. [Context: location, time, weather]. [Style and ambiance: style block, mood, light].
Dialogue: [Speaker label] says, "[line]" in a [tone] voice.
SFX: [specific sounds].
Ambient noise: [bed].
Music: [style, or "no music"].
```

## Audio syntax
- Dialogue in quotes, attributed: `A woman says, "We should go."` Describe tone and voice.
- `SFX: ...` for specific sounds; `Ambient noise: ...` for the bed.
- Luma's guide notes dialogue voice is sometimes robotic: shorten lines; plan a replacement voice in post for key lines.
- Non-English dialogue: not documented here. Test in a short draft first.

## Negatives
Phrase positively: "a desolate landscape with no buildings or roads" works; avoid a bare "no X" list. Put exclusions inside the scene description.

## Timestamp prompting (multi-beat inside one clip)
```
[00:00-00:02] Wide shot, [subject doing A], [camera].
[00:02-00:05] Cut to close-up, [subject doing B].
[00:05-00:08] [subject doing C], [camera].
```
Use sparingly; each segment still follows one action and one camera idea.

## Ingredients to Video (reference images)
Phrase what each image supplies:
```
Using the provided images for [the woman], [the jacket] and [the street setting], create a medium shot of [woman] walking toward the camera on the street at dusk, [camera move]. [Style]. Audio: ...
```
Attach the headshot (face), full body (costume) and plate (set). Keep to the number the UI allows (Luma's access guide says up to 3 reference images; check the current Flow limit).

## First and last frame
Describe the transition between the two frames and the sound; do not re-describe what each frame shows.
```
The camera slowly orbits right as [subject] turns from [state A] to [state B]; [light change]. SFX: ... Ambient noise: ...
```
Make start and end frames share identity, light and framing logic, or the interpolation morphs.

## Gemini prompt enrichment
Google documents using Gemini to expand a short idea into a detailed prompt. Fine for brainstorming; for continuity work, feed Gemini your identity and style blocks and lock the result into the shot card.

## Tips
- Stay inside 8 s; prefer 4-6 s for dialogue shots with one short sentence.
- Name the lens and framing once; describe light direction.
- Use Fast for composition tests; promote only approved prompts to Quality.
- Say "single continuous shot" when you do not want cuts.

## Retry hints
Identity drift: switch to Ingredients with a clean headshot; shorten clip. Wrong audio: re-state SFX and Ambient noise lines explicitly. Unwanted cut: add "single continuous shot, no cuts".
