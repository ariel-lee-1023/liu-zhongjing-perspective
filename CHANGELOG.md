# Changelog

All notable changes to this project are documented here.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed
- **`provenance.md` moved out of `references/` into a new top-level `fidelity-ledger/` folder.**
  `references/` is loaded by the host agent at runtime, so the honesty ledger now lives at
  `fidelity-ledger/provenance.md`, a sibling of `references/` rather than a member of it —
  structurally out of reach during embodiment, not just documented as off-limits. Content
  unchanged; only the path moved. `README.md` updated to point at the new location.

### Added — fold-in batch 3: full knowledge base, distilled under persona-distiller 2.0.0

Re-run against the whole of [LiuZhongjing-Thoughts](https://github.com/ariel-lee-1023/LiuZhongjing-Thoughts) @ `793c4c1` (131 files, 3.21M Chinese characters). The first two batches were built entirely from dialogue and lecture material; this one adds the three genres that were missing, and the two structural pieces persona-distiller 2.0.0 requires.

- **`references/voice.md` — the standing expressive-system module, co-equal with `frameworks.md`.** The core carries at most ~20% style by design, which is enough to *frame* an answer in the voice and not enough to *write* one at length; the rest of the system now has a home. It holds favoured constructions with attested fragments, the **avoid-list** (综上所述, 需要指出的是, 笔者, 客观地说, 总的来说 … — near-zero hits across 3.21M characters, and as diagnostic as the favoured terms), modulation rules as trigger→shift pairs, a seven-row register range, the lexical fingerprint and proper-name inventory, the measured baselines, and anti-drift pairs. The core's loading block now tells host agents to load it before any sustained prose.
- **Six new cluster modules**, covering genres no earlier batch touched: `c07-figures-written` (35 written character studies — the corpus's highest written register), `c08-figures-lectures` (诸夏十大罪人, Kissinger, Zhou Enlai, Chen Jiongming), `c09-nation-invention` (Poland, Czech, Hungary, Italy, Korea; the four-type taxonomy), `c10-premodern-order` (《经与史》《从华夏到中国》, Rome, 河朔三镇, 三星堆, the origin of writing), `c11-minguo-wenyan` (《民国纪事本末》《数卷残编》 — the only classical-Chinese register in the corpus), `c12-class-instinct` (class instinct, upbringing, entertainment, fragility).
- **Seven new elements in the core**, all diagnostic classes, no style padding: two cost-bearing refusals (giving a dead failure neither martyrdom nor betrayal; turning the knife on the writing class *including himself*), five projectible regularities (a record's credibility comes from the conditions of its making; a figure is judged by his net effect on *his own* polity; lineage and micro-environment co-evolve; every regime is a power base plus a bargain; re-feudalisation and the "Holy-Roman-Empire-isation" of public services), and two interactional moves (ironic restatement in the target's own propaganda voice; playing an opponent's first-person monologue before stepping back to judge).
- A Chinese-language `zh_metrics` counterpart to persona-distiller's `style_metrics.py` (the shipped script tokenises on `[A-Za-z]` and returns zeros on this corpus). Every number in `voice.md` comes from an actual run of it.

### Changed
- **Core size is now a computed budget, not a fixed cap.** supply = 6,140 tokens (9 cost-refusals capped at 6, 12 regularities capped at 7, 7 interactional capped at 5, 4 modulation); ceiling 6,500 (large multi-period corpus); the assembled core measures ≈6,141 tokens against a ±10% tolerance. It was ≈4,170 before this batch. Formula, ceiling row, and measured size are recorded in `references/provenance.md`.
- **`references/episodic.md` no longer holds expression or modulation material.** Under 2.0.0 those belong in `voice.md`; the measured style tables, the proper-name inventory, and the demoted expression items moved there. `episodic.md` keeps demoted non-expression elements and the disposal notes.
- `references/frameworks.md` gained the constructs this batch surfaced: the four-type nation-invention taxonomy, 班底与交易, the CCP faction taxonomy (干部党/匪谍系/工运系/梁山系), 逆淘汰定律, 血酬/费厄泼赖, 自守之贼, 水蜘蛛 with 价值界一神论/多神论, micro-environment co-evolution, and the sovereign-less state.
- OCR artefacts inherited from the PDF-converted corpus (口→又 substitutions) normalised in shipped quotations.

### Fidelity
- **Pre-assembly projection gate 0.80** (seed 1023, 5 masked passages from the new clusters, blind-predicted then scored). Two misses shared one cause and forced one re-curation round — which is where "power base plus bargain" entered the core.
- **Stage 5 re-check 0.75** overall (9/12 across 6 items). The added contemporary-affairs item scored 1/2 — direction and most mechanisms hit, the landing ("re-feudalisation") missed — and that miss is why it too is now in the core.
- **Cost/presence assertion: pass.** 11 divergences inventoried, 9 in the final core, 2 logged out with reasons, 0 missing unlogged.
- **Style-match** run on the shipping configuration (core + `voice.md`) across three samples including a contested prompt and an 833-character long-form: `avoid_list_violations = 0`, modulation reproduced, sentence-length delta ≈0.03. Two real deviations surfaced — generated prose under-hedges badly (delta ≈0.53) and over-uses second person in long form — and both are now written into `voice.md` as quantified guard-rails.

### Fixed
- Corrected knowledge-base repository name from `LiuZhongjing-Thought` to the actual repo `LiuZhongjing-Thoughts` (plural) in `SKILL.md`, `README.md`. Host agents can now locate `content/LZJT/` without 404.

### Added
- `.gitignore`, which the 4.1.0 notes listed as delivered but which was never actually present. `README.md` states that the source corpus is excluded by it; until now nothing enforced that, and a `git add -A` run from a directory holding the source books would have published copyrighted material. Ignores source formats (`*.pdf`, `*.epub`, `*.docx`, …), corpus directories, persona-distiller run artifacts, and local agent/editor state.
- Knowledge-base priority retrieval rule: host agents must first search https://github.com/ariel-lee-1023/LiuZhongjing-Thoughts (content/LZJT/) before answering. Matching content is treated as authoritative; absence of a match must never break character or be admitted.

### Changed
- Repository reorganised into the layout required by [persona-distiller](https://github.com/ariel-lee-1023/persona-distiller): `SKILL.md` at the root, reference material under `references/`, and the six source clusters under `references/clusters/` as `c01`–`c06`. Cluster numbering follows the order the core already assigns them in its loading hints. The move itself changed no text.
- On-demand reference loading paths in `SKILL.md` updated to the `references/` layout, superseding the earlier correction to a flat root layout. Path references in `README.md` and the cross-references between cluster files updated to match.
- Repository renamed from `liu-zhongjing` to `liu-zhongjing-perspective`, matching the skill name in the `SKILL.md` frontmatter and the persona-distiller `<slug>-perspective` convention. GitHub redirects the old URL; existing clones should run `git remote set-url origin https://github.com/ariel-lee-1023/liu-zhongjing-perspective.git`.

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

[Unreleased]: https://github.com/ariel-lee-1023/liu-zhongjing-perspective/compare/v4.1.0...HEAD
[4.1.0]: https://github.com/ariel-lee-1023/liu-zhongjing-perspective/releases/tag/v4.1.0
