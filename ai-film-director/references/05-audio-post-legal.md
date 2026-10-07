# Audio, post-production and legal/disclosure

Contents: 1 Order of operations - 2 Audio layers and mix levels - 3 Dialogue and lip-sync fallbacks - 4 Assembly checklist - 5 Rights and disclosure - 6 Delivery checklist

This file is practical guidance. It is not legal advice; tell the user to check the rules of the platform, festival or client they deliver to.

## 1. Order of operations (practitioner consensus)

1. **Select**: pick the usable seconds of each clip; trim before you spend time upscaling. Typically only a fraction of generated footage survives.
2. **Upscale** (for example Topaz) on ungraded clips. Upscaling graded or heavily compressed footage amplifies artefacts.
3. **Neutral correction**: match exposure and white balance between clips; match skin tone across shots from different tools.
4. **Grade**: one look across the film, applied after correction.
5. **Light blur and grain last**: a little grain over everything glues clips from different models together and hides texture differences.
6. **Audio layers and mix** (section 2).
7. **Titles, subtitles and credits**: add in the editor; do not ask video models for readable text.
8. **Export** at the delivery spec.

## 2. Audio layers and mix levels

Layers: dialogue, SFX, ambience, music. If the clips have native audio, keep what works and replace what does not; native audio often comes back hot and inconsistent between clips, so level each clip first.

Starting levels (peak or short-term, adjust by ear):
- Dialogue: -12 to -6 dB
- SFX: -18 to -10 dB
- Music: -24 to -18 dB
- Duck music 6-8 dB under speech.
- Add a continuous room tone or ambience bed under cuts so audio does not "drop out" between clips.

## 3. Dialogue and lip-sync fallbacks

If a model's dialogue is robotic or wrong for the user's language (Vietnamese support is not documented for the models in this skill), generate the shot silent or with minimal mouth movement, record or synthesise the voice separately, and lip-sync in a dedicated tool or cut on reaction shots and over-the-shoulder angles so synchronisation is less visible. Keep voices consistent: one voice per character for the whole film.

## 4. Assembly checklist

- Shot order matches `shot-list.md`; every shot ID is accounted for.
- Eyeline and screen direction consistent across cuts.
- Continuity: costume, props, time of day.
- Cuts hide generation limits: cut on action and on sound.
- Sound bridges across cuts.
- Frame rate and resolution uniform (convert clips from different tools to one timeline setting).
- Check the loudest and quietest scenes on headphones and a phone speaker.
- Add title card and credits including an AI-use note.

## 5. Rights and disclosure (check each, then tell the user what applies)

- **Copyright (US)**: purely AI-generated material is generally not registrable; works with substantial human authorship (script, selection, arrangement, editing) may be, and AI-generated parts typically must be disclosed. Keep records of human contributions (scripts, storyboards, edit decisions, prompt logs).
- **Tool terms**: check each tool's commercial-use terms and plan tier; some free tiers restrict commercial use or add watermarks. SynthID or similar provenance marks may be embedded by the tool; do not strip them to hide AI use.
- **Likeness and consent**: do not generate a real person's face or voice without written consent. Union and guild rules (for example SAG-AFTRA) may require consent and compensation for digital replicas in covered productions.
- **Third-party IP**: do not reproduce copyrighted characters, logos or brand designs; do not use "in the style of [living artist]" for commercial projects without checking risk.
- **Music and voices**: AI-generated music and voices may have licensing limits; keep proof of licence.
- **Festival and platform disclosure**: many festivals and platforms ask about AI use (examples reported: a Berlinale submission question; the AIFJ requires a list of tools). Read the submission rules and prepare an AI-use statement: which tools, for what (script, images, video, voice), and what was human-made.
- **Platform labels**: major video platforms require labelling of realistic synthetic content; apply the label when uploading.
- **Vietnam**: the Vietnamese AI law of 2025 and Decree 142/2026 (as reported in the sources used) contain obligations about transparency and labelling for AI-generated content. Tell users publishing in Vietnam to read the current text or ask a lawyer, because details and effective dates matter and may have changed.

## 6. Delivery checklist (reply in user's language)

- Master file in the highest quality delivery spec and a social cut (aspect ratio per platform).
- Captions or subtitles in required languages.
- AI-use statement and credits.
- Tool list and licences saved with the project.
- Project folder archived: bible, shot list, approved images, final prompts, QA reports.
