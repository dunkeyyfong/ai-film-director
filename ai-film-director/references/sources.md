# Sources and trust levels

Research date: Oct 2026 (as of 7 Oct 2026). Trust labels: **Official** = vendor documentation; **Vendor-reported** = vendor marketing or case study; **Third-party** = hosting platform, blog or reseller; **Unverified** = not read or contradictory.

Product facts change monthly. Treat the dates below as the last time each fact was seen and re-check limits in the tool's UI.

| Topic | Source | Date | Trust |
|---|---|---|---|
| Veo 3.1 prompt formula, audio syntax, timestamp prompting, ingredients, first/last frame | Google Cloud Vertex AI guide to Veo 3.1 prompting | 16 Oct 2025 | Official |
| Veo via Luma: reference images, 1080p, Fast vs Quality, robotic dialogue note | Luma guide | 2026 | Vendor-reported |
| Flow @name references, picker tiers, Veo 3 API shutdown (30 Jun 2026) | Third-party Flow coverage | 2026 | Third-party |
| Seedance 2.0 eight elements, labeled shots, reference authority, symbols, limits | Runway Seedance 2.0 prompting guide | 24 Sep 2026 | Official (host vendor) |
| Seedance 2.5 (30 s, 50 refs, timestamped editing) | Vendor announcements | 2026 | Vendor-reported |
| Kling 3.0 multi-shot, dialogue labels, image-to-video | fal Kling 3.0 prompting guide | 5 Feb 2026 | Third-party (API host) |
| Kling turbo syntax, per-shot structure | Morphic; aitoolcurator | 2026 | Third-party |
| Kling 4.0 Flash early access, claimed specs | Kuaishou announcements | 28 Sep 2026 | Vendor-reported / unverified |
| Runway Gen-4.5 limits | Runware docs; invideo | 2026 | Third-party |
| Runway prompt style (motion-only, two channels) | Runway documentation and practitioner guides | 2026 | Official / third-party |
| Hailuo/MiniMax camera commands, prompt and duration limits | MiniMax API docs | 2026 | Official |
| MiniMax H3 prompting | Luma "MiniMax H3 Prompting Guide" | 30 Jul 2026 | Unverified (not read) |
| Luma Ray template and rules, Ray3.14 / Ray3.2 specs, Modify | Luma field guide | 27 Feb 2026 | Official |
| Wan 3.0 formulas, params, pricing | Segmind relaying Alibaba formulas | 10 Sep 2026 | Third-party |
| Muse Video status (early preview, "coming soon to creators and Meta AI"), stated strengths and gaps, Arena rank, Content Seal | Meta, "Introducing Muse Image and Muse Video" (ai.meta.com) | 7 Jul 2026 | Official announcement; no prompt guide published |
| Muse Video still unreleased after Connect 2026; no specs, API or price | pexo.ai explainer (updated 10 Sep 2026); kie.ai deep dive; Meta Connect 2026 newsroom; Latent Space Connect recap | Sep 2026 | Third-party / Official (absence of launch) |
| Muse Image prompting: brief order, no negative prompt, no seed, specificity, thinking levels, sizes | Runware Muse Image prompting guide | 2026 | Third-party (API host of Meta Model API) |
| Muse Image multi-reference (1-10 refs, ordinal role binding, verbatim identity) and scoped editing | Runware guides; ComfyUI Meta partner node docs (@Image1 syntax) | 2026 | Third-party (API hosts) |
| Muse Image on fal (Meta Model API) | fal launch coverage | 1 Sep 2026 | Vendor-reported |
| "Muse Video" wrapper sites (musevideo.ai and similar) are not Meta; route to Wan, Kling, Grok Imagine | musevideo.ai footer | Oct 2026 | Official (site's own disclaimer) |
| Unsourced Muse Video specs (30 s, 4K, 28 languages, "under 15 words") | digen.ai blog | 2026 | Unverified; contradicts Meta's preview status; do not use |
| muse.ai | Site itself: video hosting and search platform | 2026 | Official (not a generator) |
| Nano Banana Pro prompting (thinking model, natural language, refs) | Google guidance | 2026 | Official |
| GPT Image edit and structure advice, input fidelity | OpenAI guidance and practitioner posts | 2026 | Official / third-party |
| Workflow ratios (4x footage, 3 generations per shot, 315-750 USD per minute) | invideo case studies | 2026 | Vendor-reported |
| Post order, mix levels | Practitioner consensus | 2026 | Third-party |
| US human-authorship rule, SAG-AFTRA consent, festival disclosure, Vietnam AI law 2025 and Decree 142/2026 | Public reports | 2026 | Third-party; not legal advice |
| Agent Skills open standard | agentskills.io specification | 2026 | Official |

## Conflicts resolved

- Veo guide favours structured, detailed prompts; Luma's guide favours concise prompts. Resolution: follow each model's own guide; keep the shot to one action either way.
- Runway duration: 5/8/10 s (Runware) vs 2-10 s (invideo). Resolution: verify in the user's UI.
- Muse Video prompting: no official guide. Resolution: `models/muse.md` combines Meta's stated strengths and gaps with Muse Image's documented brief style; every rule is labelled unverified until Meta publishes a guide.
- Dialogue: Kling and Wan guides want speaker labels, Seedance uses braces, Veo uses quotes with attribution. Resolution: follow each model file.

## Keeping this skill current

When a user reports that a tool changed, update the matching model file and the date, and add the new source here. Prefer official documentation; mark everything else with its trust label.
