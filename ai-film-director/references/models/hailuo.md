# Hailuo / MiniMax

Last verified: Oct 2026. Confidence: HIGH for camera command syntax and API limits (official MiniMax API docs); LOW for MiniMax H3 (newer; Luma's "MiniMax H3 Prompting Guide" dated 30 Jul 2026 was not read - search for it before writing H3 prompts and mark the result unverified until checked).

## Limits (API docs; verify in UI)
- Prompt 1-2000 characters; duration 6 or 10 s; resolution 768P or 1080P (Hailuo-02 also 512P).
- Prompt optimiser toggle: turn it off when you wrote a detailed prompt; leave on for very short prompts.
- First and last frame supported on Hailuo-02.

## Camera commands (square brackets)
Truck left / Truck right, Pan left / Pan right, Push in / Pull out, Pedestal up / Pedestal down, Tilt up / Tilt down, Zoom in / Zoom out, Shake, Tracking shot, Static shot.
- Simultaneous moves inside one bracket separated by commas, maximum 3 recommended: `[Pan left, Pedestal up]`.
- Sequential moves with "then": `[Push in], then [Pull out]`.
- Prefer one command; chain only for a deliberate reveal.

## Template
```
[Camera command]. [Subject: identity block] [one action, slow]. [Scene and light]. [Style]. [Atmosphere].
```
Example: `[Push in] A woman in an olive canvas jacket slowly lifts a teacup and exhales; steam curls past her face. Rain-lit alley at night, warm lantern key, cool blue spill. 35mm anamorphic look, fine grain.`

## Notes
- Place the camera command first.
- For image-to-video, describe motion and camera only.
- Dialogue and audio support differs by model version: check the UI before writing audio lines.

## Retry hints
Camera ignored: use only one command in brackets and put it first. Face drift: shorten to 6 s and use a closer shot. Too static: add a second motion (hair, steam) rather than a second camera move.
