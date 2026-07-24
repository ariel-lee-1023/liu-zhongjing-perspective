# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Knowledge-base priority retrieval rule: host agents must first search https://github.com/ariel-lee-1023/LiuZhongjing-Thought (content/LZJT/) before answering. Matching content is treated as authoritative; absence of a match must never break character or be admitted.

### Changed
- On-demand reference loading paths corrected to match the actual flat repository layout (files live at repo root, not under `references/clusters/`).

### Known gaps
- Female first-person register remains thin; the source corpus frames questions from a predominantly male viewpoint.
- Specific facts from roughly the last one to two years are outside the corpus. Host agents must retrieve current facts before the persona reasons over them.

---

## [4.1.0] - 2026-07-23

First public release. Packaged for GitHub with license, changelog, and repository conventions.

### Added
- `interviews.md` cluster listed in the on-demand loading hints in `SKILL.md`; the file shipped with the reference set but was not previously referenced from the core.
- `README.md`, `LICENSE` (MIT), `.gitignore`, and this changelog.

### Changed
- Skill frontmatter `name` set to `liu-zhongjing-perspective` to match the repository and skill directory name (previously `liu-zhongjing-persona-v4`).
- Reference files reorganised into `references/` with cluster files under `references/clusters/`, matching the paths already cited in `SKILL.md`.

---

## [4.1.0-fold.2] - Batch 2 fold-in

Folded in 23 lectures plus 5 topical talks from 《刘仲敬访谈精选》 (2020–2025), narrowing the post-2019 factual gap. Scoring weights unchanged; new material scored on the same scale as existing elements.

### Added
- **Anti-\"new\" recognition move** promoted into the core (composite 0.62): a thing presented as unprecedented is first identified as which recurrence of an old state it is. This is the engine that keeps the persona from fumbling 2020s topics.
- New domains in `jingxuan-lectures.md`: global capitalism and financial empire, cognitive warfare, knowledge and nihilism, ideological genealogy, family and fertility as order structure.

### Changed
- **Capital-flow / global-capitalism placement** promoted from `references/` back into the core (composite 0.61). It had been demoted for overlapping with order input/output; batch 2 supplied independent multi-cluster evidence.
- Post-2019 factual coverage reclassified from \"weak\" to \"partially filled\".

### Fixed
- Off-home-turf projection score upgraded from an estimate of ~0.6 to a measured 0.75, clearing the 0.70 robustness line. The one miss (t19, on the \"useless class\") is what prompted the anti-\"new\" rule to enter the core.

---

## [4.0.0] - Rewrite from v3

A full re-distillation, not an edit. Four failure modes in v3 were targeted directly.

### Changed
- Named frameworks moved out of the core into `references/frameworks.md`. The core now carries only the concrete judgements those frameworks produce, with an explicit instruction not to recite definitions. v3 front-loaded the entire framework set as expository content.
- Jargon rewritten as a register-modulated voice rule backed by measured density (~13 per 10k characters in conversational and life registers, ~35 in theoretical monologue), replacing v3's large glossary, which invited pile-up. Flagship terms now near-absent from the core.
- The core rewritten entirely in the first person and inside the voice. v3 was largely meta-instruction *about* imitating the subject.

### Added
- **Cost-refusal made the highest-priority pass.** Seven positions held at a cost were extracted and made the centre of gravity of the core (`我不让步`), replacing v3's success criteria, which measured only surface style — catchphrases, sentence length, proper-noun density, term frequency.
- The grief modulation: the analytical machine shuts off in the face of real bereavement, with short, plain, warm sentences.
- The recoverable-versus-locked distinction governing \"what should I do\" answers.
- `references/provenance.md` as an honesty ledger, and `references/episodic.md` for measured style figures and demoted evidence.

### Removed
- v3's demonstration answers. They were model-written simulations rather than genuine source material and are excluded from the evidence base; they may serve as application examples but must not be quoted as the subject's own words.

[Unreleased]: https://github.com/ariel-lee-1023/liu-zhongjing/compare/v4.1.0...HEAD
[4.1.0]: https://github.com/ariel-lee-1023/liu-zhongjing/releases/tag/v4.1.0
