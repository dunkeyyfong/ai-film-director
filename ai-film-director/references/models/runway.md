# Runway Gen-4.5 (and Aleph for editing)

Last verified: Oct 2026. Confidence: MEDIUM (Runware docs and invideo notes; limits differ between hosts, so check the UI).

## Limits (verify in UI)
- Image-to-video with a first frame only (no last frame in this mode).
- Prompt 1-1000 characters. Duration 5, 8 or 10 s (Runware); invideo lists 2-10 s. Resolutions: 1280x720, 720x1280, 1104x832, 832x1104, 960x960.
- Gen-4.5 outputs are silent; plan audio in post. Text-to-video is 16:9 only.
- Aleph edits existing video; Motion Brush exists for region-specific motion.

## Prompt rule: describe motion, not the scene
The image already supplies subject, set, light and style. Delete anything visible in the frame. Write two channels:
1. Subject motion: who or what moves, how, how fast.
2. Camera motion: one move, with speed.
Also say what stays still.

## Camera vocabulary
push-in, pull-back, pan, tilt, dolly, orbit, crane. Add pacing words (slow, steady, gentle). Atmospheric motion (steam, dust, drifting fog, fabric) adds life without risking identity. Never contradict the image (do not ask for rain if the frame is dry).

## Template
```
Subject motion: [subject] [one verb phrase with body part and speed]. [Secondary motion: hair, fabric, steam]. Camera: slow [push-in/pan/orbit] [direction]. [What stays still: background static].
```
Example: `The cook lifts the noodle basket slowly with both hands; steam rises and drifts left. Camera: slow push-in toward his face. The counter and background stay still.`

## Editing with Aleph
Describe the change and the preserve rule: `Change the daylight to dusk with warm street lights; keep the character, motion and framing unchanged.` Verify Aleph's current limits (clip length, resolution).

## Retry hints
Image morphs or changes: cut the prompt to motion only and slow the verb. Camera not obeyed: move the camera sentence first and use one move. Subject freezes: add atmospheric motion or a small secondary movement.
