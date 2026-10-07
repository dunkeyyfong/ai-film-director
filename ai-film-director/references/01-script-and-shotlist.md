# Script and shot list for AI video

Contents: 1 Principles - 2 Script structure - 3 Writing rules - 4 Dialogue budget - 5 Shot list fields - 6 Runtime and budget - 7 Worked mini-example

## 1. Principles

Generative video models fail in predictable ways: they drift on identity over time, they invent cuts and details you did not specify, and they struggle with long continuous action. A script written for them is therefore a *production document*, not literature. Three consequences:

- Anything the audience must see has to be a visible, physical action. "Maria feels conflicted" gives the model nothing to render; "Maria stops with her hand on the door handle, lets go, and looks back at the table" does.
- Short units are reliable units. Practitioner guides converge on 3-5 second shots for dependable results and scenes under about 15 seconds before quality or consistency slips. Most models cap a single clip between 5 and 15 seconds (some go to 30); treat the cap as a budget, not a target.
- The script is also the generation input. Ambiguity at script level becomes randomness at video level, and randomness costs credits.

## 2. Script structure

Deliver in this order:

1. **Logline** - one sentence: who, wants what, against what.
2. **Premise and tone** - 2-3 lines, plus the one-line "feel" reference (not a copyrighted title; describe the feel).
3. **Beat sheet** - 5-12 beats for a short; each beat one sentence of *what changes*.
4. **Scene breakdown** - 8-15 scenes for a 1-3 minute film. For each scene: location, time of day, characters present, purpose, emotion, target duration.
5. **Shots inside each scene** - 2-5 shots, each one visual idea.
6. **Dialogue and sound notes** per shot (see section 4).

If the film is an ad, MV or explainer, replace beats with the structure that fits (hook / proof / payoff; verse / chorus / bridge; problem / demo / result) but keep the same scene and shot discipline.

## 3. Writing rules for AI-renderable scripts

- Present tense, concrete verbs, one primary movement per shot. Name the body part and the degree: "slowly lifts the bowl with both hands" beats "picks up the bowl".
- Show emotion as behavior: shoulders drop, a held breath, a faint smile - not adjectives.
- Slow, continuous motion renders better than sprinting, large jumps or violent action. If the story needs action, break it into several short shots and cut on the impact.
- Keep the number of simultaneous subjects low. Two characters per shot is comfortable; crowds should be background texture, not performers. Scenes where several people interact physically (handshakes, embraces, fights) are the most failure-prone; plan extra generations or plan to cheat with cuts and reaction shots.
- Avoid text that must be readable in frame (signs, screens, subtitles) unless the user accepts retries or will add it in post.
- Each character needs a **stable, visually distinct silhouette**: one signature costume element and one signature prop or feature help both the model and the viewer.
- Do not rely on a model remembering a character between clips. Every shot must be re-anchored with references (see the bible and image plan).
- Prefer cuts to continuous camera moves across space. Cutting is how you hide generation limits, exactly as in live action.
- Write every scene so it can be shot as several independent 3-8 second clips, then assembled.

## 4. Dialogue budget

- Speech takes real time. A working heuristic from Wan 3 tests is about 2.5 seconds of speech per 5-second clip - roughly two short sentences - because models spend the first moment establishing the shot and leave a beat at the end. Treat this as a starting point and verify on the user's tool.
- Split long lines across shots. Use reaction shots between lines.
- Name who speaks in every line, in multi-character shots. Several models need an explicit speaker label with a unique role name and a voice description (see `models/kling.md`).
- Decide dialogue language now. Support differs by model (English and Chinese are strongest on most; some list Japanese, Korean, Spanish and others; Vietnamese support is not documented in the sources used here and must be tested). If a model handles the user's language poorly, plan to record dialogue separately with a voice tool and lip-sync in post (see `05-audio-post-legal.md`).
- Native audio is generated in the same pass by Veo, Kling, Seedance, Wan and others, so ambience, SFX and music cues belong in the shot notes now, not later.

## 5. Shot list fields

Maintain `shot-list.md` as a table. One row per shot:

| ID | Scene | Duration (s) | Purpose / emotion | Framing and camera | Action (visible) | Start frame ref | End frame ref | Characters | Location | Dialogue / SFX / music | Notes and risks |
|---|---|---|---|---|---|---|---|---|---|---|---|

Rules: IDs are stable (S03-SH02) and never reused; every shot names which approved image(s) it starts from; "Risks" lists anything known to fail (hands on props, multiple characters touching, readable text, fast motion).

## 6. Runtime and budget

- Script to a runtime *band*, not a lock. Documented AI productions finish shorter than scripted because the edit decides what survives.
- Plan raw generation at about 4x the finished runtime in clip-seconds, and about 3 generations per usable shot. These ratios are vendor-reported (invideo case studies) - use them for planning, then replace them with the user's own measured ratio after the first day.
- Reported finished costs ranged from roughly 315 to 750 USD per finished minute on subscription/credit platforms for narrative work, with higher figures for complex or feature-style work. Do not quote these as guarantees; they depend on tool, resolution and retry discipline.
- Iterate composition, casting and style in images, not video. Resolve as much as possible at image cost.

## 7. Worked mini-example (format only)

Logline: A night-shift ramen cook discovers the last customer of the night is the daughter he has not seen in ten years.

Scene 2, SH01 (5s) - Purpose: establish routine. Medium close-up, static camera. The cook lifts a wire noodle basket from boiling water and snaps it down twice, steam rising. Ambience: rolling boil, faint street noise. No dialogue.

Scene 2, SH02 (5s) - Purpose: first sign of recognition. Close-up on his face, slow push-in. He glances at the door chime, stills, and his hands stop mid-motion. SFX: door chime, then silence.

Notice: one idea per shot, visible behavior instead of stated feelings, sound planned from the start.
