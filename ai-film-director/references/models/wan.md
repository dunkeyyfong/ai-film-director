# Wan 3.0 (Alibaba)

Last verified: Oct 2026. Confidence: MEDIUM (Alibaba prompt formulas as relayed by Segmind, 10 Sep 2026; public beta since 6 Aug 2026). Open weights on Hugging Face are still Wan 2.2, so do not tell the user Wan 3.0 is downloadable.

## Limits (verify in host)
- Duration 2-30 s; 480P / 720P / 1080P; audio on by default; `prompt_extend` on by default.
- Segmind pricing (third-party): 0.05 / 0.10 / 0.20 USD per second; latency about 4 min.
- Turn `prompt_extend` OFF for detailed prompts; leave it on only for prompts under about 20 words.

## Formulas (Alibaba)
- Basic: Entity + Scene + Motion.
- Advanced: Basic + Aesthetic control + Stylization.
- Image-to-video: Motion + Camera.
- Sound: lines + emotion + tone + speed + timbre + accent, plus SFX and music.
- Multi-shot: Overall description + shot number + timestamp + content.
- Reference-based: identifier + action + scene + lines + music.

## Template (multi-shot with sound)
```
Overall: [premise in one sentence; style block].
Shot 1 [0-3s]: [shot size] [camera move]. [Subject] [action] in [scene], [light].
Shot 2 [3-6s]: [shot size] [camera move]. [Subject] [action]. [Role] says in a [emotion], [tone], [speed] voice with [timbre] and [accent]: "line".
Sound: [SFX]; ambience: [bed]; music: [style or none].
```

## Notes
- Naming a shot size plus a camera move prevents unwanted automatic cuts.
- Speech budget: about 2.5 s of speech per 5 s clip.
- Audio comes back hot: lower it in post.
- Test the user's dialogue language on a short draft.

## Retry hints
Auto-cuts: name shot size and one camera move. Prompt rewritten too much: disable `prompt_extend`. Dialogue clipped: shorten the line or lengthen the clip.
