# liu-zhongjing-perspective

A distilled **perspective skill** for LLM agents: analyse history, politics, civilisation, current affairs, and even ordinary life questions the way Liu Zhongjing (刘仲敬, b. 1974) does — translate the question into one about *order being produced or consumed*, about heredity and class position, about genealogical placement — then answer coldly, and withhold reassurance exactly where the reader most wants it.

The skill is written in Chinese, in the first person, as a voice rather than a set of instructions about a voice. It is designed to be dropped into any agent that supports file-based skills, or pasted in as a system prompt.

---

## Repository layout

```
liu-zhongjing-perspective/
├── SKILL.md                        # the core persona — self-contained
├── references/
│   ├── clusters/
│   │   ├── c01-ayi-life-advice.md     # anti-self-help life advice; the "machine off" warm register
│   │   ├── c02-neiya-order.md         # Inner Asia and East Asian order — structure
│   │   ├── c03-wadi-psychology.md     # Chinese collective psychology — pathology
│   │   ├── c04-civilization-theory.md # last man, 守先待后, the Great Flood mechanism
│   │   ├── c05-jingxuan-lectures.md   # 2020s topics, global capitalism, capital flows, family
│   │   ├── c06-interviews.md          # contemporary affairs: how a news item gets absorbed
│   │   ├── c07-figures-written.md     # written character studies: lineage, micro-environment, niche
│   │   ├── c08-figures-lectures.md    # lecture-mode figures: power base, bargain, counterfactuals
│   │   ├── c09-nation-invention.md    # comparative nation-invention: Poland, Russia, 中华民族
│   │   ├── c10-premodern-order.md     # classical & pre-modern constitutions, epigraphy, writing
│   │   ├── c11-minguo-wenyan.md       # Republican chronicle + the classical-Chinese register
│   │   └── c12-class-instinct.md      # class instinct, upbringing, entertainment, fragility
│   ├── frameworks.md               # precise definitions of named frameworks (lookup only)
│   └── voice.md                    # the measured expressive system — load before sustained prose
├── fidelity-ledger/
│   ├── provenance.md               # honesty ledger: element → source → score → gate status;
│   │                                    #   human-facing, never loaded by the host agent
│   └── episodic.md                 # demoted non-expression evidence; disposal notes
├── CHANGELOG.md
├── LICENSE
├── NOTICE.md
└── README.md
```

`SKILL.md` alone is enough for most questions. Load a reference file only when a register needs finer grain — the loading hints are at the bottom of `SKILL.md`.

`frameworks.md` and `voice.md` are the two **standing modules**: what the person thinks with, and how the person sounds. The core carries at most ~20% style by design — enough to *frame* an answer in the voice, not enough to *write* one at length — so **load `voice.md` before writing more than a paragraph or two of sustained prose in this voice.** It holds the favoured constructions, the avoid-list, the trigger→shift modulation rules, the register range across seven settings, and the measured `zh_metrics` baselines the style-match test compares against.

---

## Usage

### As a Claude / Agent Skill

Clone the repository into your skills directory. The repository name already matches the skill name, so `SKILL.md` lands at the root of a correctly named folder:

```bash
git clone https://github.com/ariel-lee-1023/liu-zhongjing-perspective.git \
  ~/.claude/skills/liu-zhongjing-perspective
```

The agent reads the YAML frontmatter in `SKILL.md` to decide when to trigger, then pulls the reference files on demand.

### As a plain system prompt

Paste the body of `SKILL.md` (everything after the frontmatter) as your system prompt. Append one or two reference files when the topic calls for them. Do not paste `fidelity-ledger/provenance.md` or `fidelity-ledger/episodic.md` into the prompt — they are metadata about the distillation, and putting them in context degrades the voice.

---

## Design notes

Three constraints shaped this version, and they are worth knowing before you edit it.

**Frameworks are background, not content.** The named models — 秩序输入/输出, 费拉化, 末人, 瓦房店化, 民族发明学 — live in `references/frameworks.md` and are deliberately kept *out* of the core. The core carries only the concrete judgements those models produce. The main failure mode of earlier versions was reciting definitions at the reader instead of using them.

**Jargon is modulated by register, not sprayed.** Measured density runs ~13 per 10k characters in the life-advice register versus ~35 in theoretical monologue, and back down to ~17 in the written character studies. Flagship terms (瓦房店化, 末人, 编户齐民, 做题家) are near-absent when the subject is a person's life — across all 35 character studies: 瓦房店 0, 末人 0, 做题家 2. Piling up jargon is the most common way an imitation goes wrong.

**The registers are the fingerprint, not the averages.** Measured across 3.21M characters of firsthand material, question marks run 4.6 per 10k in the academic-historical register and 38 in the life-advice Q&A; connectives run 0.7 in the classical-Chinese chronicle and 14 in the Q&A; second-person reference runs 3.6% in written prose and 23% in lectures. Any imitation that hits the means but flattens those gaps is not this voice. The full table is in `references/voice.md`.

**Refusals carry the identity.** The section 我不让步 is the centre of gravity: nine positions the persona holds at a cost — refusing to comfort the bereaved with philosophy, refusing national identity, refusing a way out to someone structurally locked in, refusing to concede that its own system is *correct* rather than merely dominant. A copy that keeps the vocabulary and drops the refusals is not this persona.

**One modulation must survive.** In the face of real grief, the whole analytical machine shuts off: short sentences, plain words, warmth. This is not an inconsistency in the character; it is the single place the character permits.

### Knowledge-base priority & factual cutoff

**the companion knowledge base** https://github.com/ariel-lee-1023/LiuZhongjing-Thoughts (under `content/LZJT/`). Matching material is authoritative and must be used. If nothing matches, the agent stays strictly in character and never admits the gap.

The reasoning posture itself is time-independent. The *facts* are not. Q&A material clusters in 2018–2019; lecture and interview material extends to 2025; the books span 2011–2018. Anything more recent — the last year or two of events, election and conflict outcomes, current policy and market data — is outside the corpus.

Host agents should **retrieve current facts first, then let the persona digest them through its frameworks.** The voice is confident and fond of pronouncement, so this guard matters more here than it would for a neutral assistant.

---

## Provenance and honesty

`fidelity-ledger/provenance.md` is an audit trail rather than documentation: every element in the core is logged with its source cluster, its composite score, and whether it passed the projection and cost gates. It also records what was *demoted* and why. If you fold new material in, extend that ledger — the point of keeping it is that the distillation stays checkable.

Source material was supplied by the commissioning party, who declared the right to use it. The corpus itself is not included in this repository and is excluded by `.gitignore`.

## Contributing

Issues and pull requests are welcome, particularly for: coverage gaps (the female first-person register remains thin), post-2025 fold-ins with fresh source clusters, and translations of the skill into other languages. Please update `CHANGELOG.md` and `fidelity-ledger/provenance.md` alongside any change to `SKILL.md`.

---

## 简介（中文）

这是一个供 LLM 代理加载的**技能**：以刘仲敬的方式分析历史、政治、文明、时事、人物乃至具体人生问题——先把问题翻译成一个关于秩序生产还是消耗、遗传与阶级位置、谱系定位的问题，再冷静给出结论，且在读者最想要安慰、认同、出路的地方偏偏不给。

核心文件是 `SKILL.md`，自足；`references/` 下的参考文件按语域需要加载。命名框架的定义刻意留在 `references/frameworks.md`，不进核心——把定义当讲解复述是上一版最大的失败模式。

**具体事实的覆盖以 2018–2025 语料为界，更新的事实需由宿主代理先行检索。

---

MIT © 2026 Ariel Lee. [See LICENSE](LICENSE).

This license covers the original text in this repository. It does not extend to any referenced source books, which remain the property of their respective copyright holders.
