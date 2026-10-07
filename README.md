# 🎬 AI Film Director

**An Agent Skill for making AI films from idea to finished cut.** It writes the script, plans reference images, checks the images you generate for consistency, and writes detailed video prompts for each tool (Veo/Flow, Seedance, Kling, Runway, Hailuo, Luma, Wan, Muse).

> An [Agent Skills](https://agentskills.io) package that turns an AI agent into a director, script supervisor and prompt engineer for AI filmmaking. The agent talks to you in the language you write in (Vietnamese by default) and writes all image and video prompts in English.

---

## Why this skill exists

AI video is cheap per clip but expensive per **mistake**. A usable shot often takes about 3 generations, and only about 1 clip in 4 survives the edit (vendor-reported figures). You fix this before you generate any video: lock the story, lock the look, lock the characters in still images, check those images carefully, and only then spend video credits. This skill makes the agent follow that order.

## The 7-phase workflow (each phase ends with a gate you approve)

| Phase | What the agent does | Gate to move on |
|---|---|---|
| 0. Intake | Asks for the brief (at most 4 questions, each with a default answer) | You confirm the brief |
| 1. Script | Logline, beats, scenes, dialogue, a timed shot list | You approve the script |
| 2. Project Bible | Style block plus identity blocks for characters, locations and props (copied word for word into every prompt) | You approve the bible |
| 3. Image plan | Image prompts for Nano Banana / Gemini, GPT Image or Muse Image: character sheets, location plates, keyframes | You generate the images |
| 4. Image QA | Scores the images you send back, lists what changed or drifted, and gives a PASS / FIX / REDO verdict | Every needed image is PASS |
| 5. Video prompts | Shot cards: one universal brief plus a prompt for each tool | You generate the clips |
| 6. Post & delivery | Post-production order, audio levels, copyright and AI-disclosure checklist | Film delivered |

### Highlight: image QA (Phase 4)

When you send generated images, the agent:
- identifies each image (character sheet, location, or which shot's keyframe) and compares it with the approved originals and the bible;
- scores 9 criteria: character identity, costume, anatomy/hands, style, lighting, composition, location, artefacts, and how well the image will animate;
- builds a **diff table** showing which details changed, drifted, went missing or were added;
- gives a verdict: PASS, FIX (with a prompt that changes exactly one thing) or REDO (with a rewritten prompt);
- checks whether the **whole set** looks like one film, and lists the approved images to use as video references;
- says plainly what it cannot see clearly (hands, small text) and asks for a crop instead of passing the image to please you.

## Supported tools

| Tool | File | Confidence (Oct 2026) |
|---|---|---|
| Google Veo 3.1 / Flow | `references/models/veo-flow.md` | High (official Google Cloud guide) |
| Seedance 2.0 | `references/models/seedance.md` | High for prompt structure (Runway guide); check limits on your platform |
| Kling 3.0 | `references/models/kling.md` | Medium–high (third-party guide); Kling 4.0 unverified |
| Runway Gen-4.5 / Aleph | `references/models/runway.md` | Medium |
| Hailuo / MiniMax | `references/models/hailuo.md` | High for camera syntax; MiniMax H3 unverified |
| Luma Ray | `references/models/luma.md` | High for prompt rules |
| Wan 3.0 | `references/models/wan.md` | Medium (Alibaba formulas via Segmind) |
| Meta Muse Video / Muse Image | `references/models/muse.md` | High for status; medium for Muse Image prompting; **low (unverified) for Muse Video prompting** (see note below) |
| Images: Nano Banana / Gemini, GPT Image | `references/02-image-prompts.md` | Based on vendor guidance |

If you use a tool that has no file yet, the agent searches the web for its official guide, uses the universal prompt format in the meantime, and labels the result "unverified".

> ⚠️ **About Muse**: "Muse" can mean several products. **Meta Muse Video** was announced on 7 Jul 2026 as an early preview ("coming soon to creators and Meta AI"). As of Oct 2026 it has no public release, API, published specs or official prompt guide. `muse.md` therefore combines Meta's stated strengths (prompt adherence, fidelity, native ambience, foley and voiceover) and weak spots (lip-sync, fast motion) with the documented prompting style of its sister model **Muse Image**. It includes a full brief template, image-to-video and voiceover variants, three worked examples, a pre-flight checklist and a Muse-specific retry ladder. Sites such as musevideo.ai are third-party wrappers that run other models (Wan, Kling and others), and muse.ai is a video hosting platform. Tell the agent the exact app or URL you use so it applies the right guide.

> ⚠️ Tool limits and prices change every month. Each model file has a date and a confidence label, and the agent is told to check the tool's real UI before writing final prompts.

## Installation

The skill follows the open Agent Skills standard: one `ai-film-director/` folder containing `SKILL.md`, `references/` and `assets/`.

**Claude Code**

```bash
# For all projects
git clone <your-repo-url> ai-film-director-repo
cp -r ai-film-director-repo/ai-film-director ~/.claude/skills/

# Or for a single project
cp -r ai-film-director-repo/ai-film-director <your-project>/.claude/skills/
```

**Claude.ai / Claude Desktop**: zip the `ai-film-director/` folder (or use the `.skill` file from Releases, if available) and upload it under Settings → Capabilities → Skills.

**Other agents that support Agent Skills**: copy the `ai-film-director/` folder into that agent's skills directory. See the agent's documentation for the exact path.

## Usage

Just describe what you want, for example:

- "I want to make a 90-second AI short film about a night-shift ramen chef."
- "Here are the character images I just generated. Check whether anything drifted." (attach the images, named as shown below)
- "Write Veo and Kling prompts for shot S02-SH01."

**Name your image files** so the agent can match them exactly: `CHAR-mia-sheet-v2.png`, `LOC-noodle-bar-plate-v1.png`, `S02-SH01-start-v3.png`.

The agent keeps project state in files (`project-bible.md`, `shot-list.md`, `image-qa/round-n.md`), so work can continue across sessions or between agents.

## Folder structure

```
ai-film-director/
├── SKILL.md                         # main workflow and rules
├── references/
│   ├── 01-script-and-shotlist.md    # writing scripts for AI, shot lists, budgeting
│   ├── 02-image-prompts.md          # character sheets, locations, keyframes, edit prompts
│   ├── 03-image-qa.md               # rubric, diff table, verdict rules, report template
│   ├── 04-video-prompt-universal.md # universal brief, model choice, retry ladder
│   ├── 05-audio-post-legal.md       # audio, post-production, copyright, AI disclosure
│   ├── sources.md                   # sources and trust levels
│   └── models/                      # veo-flow, seedance, kling, runway, hailuo, luma, wan, muse
└── assets/                          # bible, shot card and QA report templates
```

## Sources and confidence

Every rule traces back to a source in [`references/sources.md`](ai-film-director/references/sources.md), labelled **Official** (vendor documentation), **Vendor-reported** (marketing or case studies), **Third-party** or **Unverified**. The cost figures (about 4x footage, about 3 generations per shot, 315–750 USD per minute) are vendor-reported and are only meant for planning.

## Known limitations

- No source confirms that video models handle **Vietnamese** dialogue (or other non-English dialogue) well. Test a short clip first, or record the voice separately and lip-sync in post.
- Muse Video prompting rules are inferred until Meta publishes an official guide; run a test clip before batching.
- The skill had not been tested on a real production when this README was written.
- The legal and AI-disclosure section (US copyright rules, SAG-AFTRA, film festivals, Vietnam's 2025 AI law and Decree 142/2026, as described in the sources read) is practical guidance only, **not legal advice**.
- The agent will not write prompts depicting real people without their consent, or copyrighted characters and brands.

## Contributing

When a tool changes, update its model file with the date you checked and add the source to `sources.md`. Prefer official documentation. Issues and pull requests are welcome.

## License

Released under the [MIT License](LICENSE). You may use, copy, modify and redistribute this skill, including commercially, as long as you keep the copyright and license notice.

The license covers this repository's text and templates only. It grants no rights to the third-party tools, models or trademarks it mentions (Google, Meta, OpenAI, Runway, Kuaishou, ByteDance, MiniMax, Luma, Alibaba and others), and it does not cover the films, images or prompts you create with the skill. Each tool's own terms of service apply to its outputs.
