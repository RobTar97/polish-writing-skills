<div align="center">
  <img src="assets/readme-hero.png" alt="Abstract carmine and charcoal forms flowing across an ivory editorial grid" width="100%" />
  <h1>Polish Writing Skills</h1>
  <p><strong>Polish that sounds natural, fits the genre, and keeps the meaning intact.</strong></p>
  <p>An open-source Agent Skill for editing and translating natural Polish prose with strict factual fidelity.</p>
  <p>
    <a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent_Skills-compatible-292827?style=flat-square" alt="Agent Skills compatible" /></a>
    <img src="https://img.shields.io/badge/skills-1-b62234?style=flat-square" alt="One skill" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-5b5753?style=flat-square" alt="MIT License" /></a>
  </p>
  <p>
    <a href="#quick-install"><img src="https://img.shields.io/badge/Install_with-skills.sh-b62234?style=for-the-badge" alt="Install with skills.sh" /></a>
    <a href="README.pl.md"><img src="https://img.shields.io/badge/Czytaj_po_polsku-f6f0e6?style=for-the-badge&amp;labelColor=292827" alt="Czytaj po polsku" /></a>
  </p>
</div>

---

## One skill, one editorial contract

The skill improves the Polish without quietly changing what the text says.

<table>
  <tr>
    <td width="100%" valign="top">
      <img src="assets/natural-writing.svg" alt="Natural Polish Writing illustration" width="100%" />
      <h3><a href="skills/natural-polish-writing/SKILL.md">natural-polish-writing</a></h3>
      <p>Natural, contemporary Polish for non-UI prose.</p>
      <p><strong>Best for:</strong> articles, web and marketing prose, messages, notices, social posts, academic prose, and translation into Polish.</p>
    </td>
  </tr>
</table>

> The skill performs a safe language pass on structured UI resources and relationship-sensitive formal correspondence, then flags work that needs specialized localization or business-writing judgment.

## Agent compatibility

Yes—`natural-polish-writing` is a basic, portable Agent Skill. Its core is a standard `SKILL.md` with Markdown references; it does not depend on hooks, model-specific tools, or a proprietary runtime. The official [skills CLI compatibility matrix](https://github.com/vercel-labs/skills#compatibility) marks basic skills as supported across the major coding agents.

| Agent | CLI identifier | Basic skill support |
| --- | --- | --- |
| OpenAI Codex | `codex` | Yes |
| Claude Code | `claude-code` | Yes |
| OpenCode | `opencode` | Yes |
| Antigravity | `antigravity` | Yes |
| Cursor | `cursor` | Yes |
| Gemini CLI | `gemini-cli` | Yes |
| GitHub Copilot | `github-copilot` | Yes |
| Windsurf | `windsurf` | Yes |

The current matrix also covers OpenHands, Cline, Roo Code, Amp, OpenClaw, Pi, Qoder, Zed, and many other agents that consume the shared skill format.

The `agents/openai.yaml` file adds optional OpenAI-facing metadata. Other agents can ignore it safely and use the shared `SKILL.md` instructions.

Install to several agents at once:

```bash
npx skills@latest add RobTar97/polish-writing-skills \
  --skill natural-polish-writing \
  -a codex -a claude-code -a opencode -a antigravity
```

Omit `-a` to let the CLI detect installed agents interactively.

## Quick install

Install from the repository with the official [skills CLI](https://skills.sh/docs/cli) (recommended):

```bash
npx skills@latest add RobTar97/polish-writing-skills
```

Install the skill directly:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Install globally for Codex without prompts:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing -g -a codex -y
```

Inspect what the CLI discovers before installing:

```bash
npx skills@latest add RobTar97/polish-writing-skills --list
```

Prefer a persistent command? Install the same open-source CLI through npm:

```bash
npm install -g skills
skills add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Use the skill once without installing it:

```bash
npx skills@latest use RobTar97/polish-writing-skills@natural-polish-writing
```

## See the technique

This example shows what changes, what stays true, and what the skill refuses to invent.

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>Before</h3>
      <p>W dzisiejszych czasach warto zauważyć, że Plan Pro stanowi kompleksowe rozwiązanie, które pozwala 12 osobom wspólnie planować zadania. Ponadto okres próbny trwa 14 dni, a abonament kosztuje 29 zł miesięcznie. Należy jednak pamiętać, że Plan Pro nie działa bez połączenia z internetem.</p>
    </td>
    <td width="50%" valign="top">
      <h3>After</h3>
      <p>Plan Pro umożliwia 12 osobom wspólne planowanie zadań. Okres próbny trwa 14 dni, a po jego zakończeniu abonament kosztuje 29 zł miesięcznie. Do korzystania z planu Pro potrzebne jest połączenie z internetem.</p>
    </td>
  </tr>
</table>

**Preserved:** the product name, 12-person limit, 14-day trial, 29 zł monthly price, and internet requirement.

**Changed:** generic framing, unsupported promotional evaluation, repetitive connective language, and the empty reminder frame. No capability, proof, urgency, or promise was added.

This is a traceable editing example, not an automated benchmark. The checks map to the skill’s [editing priorities](skills/natural-polish-writing/references/editing-priorities.md) and [review checklist](skills/natural-polish-writing/references/review-checklist.md).

## More verified Polish edits

### Public machine-generated sample

The [ŚMIGIEL dataset](https://huggingface.co/datasets/strebeyko/smigiel) is a CC BY 4.0 corpus created for research on machine-generated Polish and used by the [PolEval 2025 task](https://poleval.pl/tasks/task1). It labels the following short excerpt as machine-generated (`model: bielik-md`, `strategy: dbs`):

> „Ponadto, artykuł powinien być aktualny i uwzględniać najnowsze dane oraz interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom najbardziej aktualne i kompletne informacje.”

**Edited with `natural-polish-writing`:**

> Artykuł powinien uwzględniać najnowsze dane i interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom kompletne informacje.

The edit removes the unjustified comma and empty *ponadto*, reduces three overlapping recency markers to one, and cuts the sentence from 22 to 15 words. It preserves the instruction to include recent data, interpretations, and complete information; it adds no facts.

### Institutional notice

#### Institutional source

> Uprzejmie informujemy, iż w związku z koniecznością przeprowadzenia prac modernizacyjnych nastąpi czasowe wstrzymanie funkcjonowania systemu w godzinach od 22:00 do 23:00.

#### Institutional edit

> System będzie niedostępny od 22:00 do 23:00 z powodu prac modernizacyjnych.

The operational consequence comes first. The time window and cause remain unchanged; no date, apology, or promise is invented.

### Academic restraint

#### Academic source

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, ale mogą wskazywać na wzrost prawdopodobieństwa o 15%.

#### Academic edit

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, mogą jednak wskazywać na wzrost prawdopodobieństwa o 15%.

The valid academic passive stays. The edit preserves negation, cautious modality, the 15% figure, and the distinction between a possible statistical indication and causation.

### Evaluation points

Score each dimension from 0 to 2: semantic and factual fidelity, grammatical correctness, genre/register fit, naturalness and information flow, and edit restraint with no invention.

| Case | Fidelity | Grammar | Genre | Naturalness | Restraint | Total |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Plan Pro feature copy | 2 | 2 | 2 | 2 | 2 | **10/10** |
| ŚMIGIEL excerpt | 2 | 2 | 1 | 2 | 2 | **9/10** |
| Institutional notice | 2 | 2 | 2 | 2 | 2 | **10/10** |
| Academic passage | 2 | 2 | 2 | 2 | 2 | **10/10** |

The corpus excerpt receives one genre point because the public fragment lacks its full document context. These are transparent manual editorial checks, not native-speaker study results, detector scores, or claims of benchmark performance.

## Try it

```text
Use $natural-polish-writing to make this announcement natural and concise in Polish.
Keep every fact, number, condition, and qualification unchanged.
```

```text
Use $natural-polish-writing to translate this article into contemporary Polish.
Preserve its terminology, quotations, uncertainty, and authorial voice.
```

```text
Użyj $natural-polish-writing, aby zredagować ten fragment po polsku.
Zachowaj wszystkie fakty i nie wygładzaj celowo nieformalnego tonu.
```

## How it works

- **Meaning before smoothness.** Facts, conditions, uncertainty, chronology, numbers, names, attribution, quotations, commitments, and consequences stay intact.
- **Genre before generic fluency.** Academic prose, marketing copy, social posts, notices, and translations do not receive the same treatment.
- **Smallest sufficient edit.** The skill fixes the passages that need attention without replacing a recognizable voice with anonymous “good writing.”
- **No simulated humanity.** It does not add anecdotes, opinions, slang, typos, evidence, or fake personal experience.
- **Current rules, contextual evidence.** Orthography and punctuation follow the RJP rules in force since 2026; NKJP and WSJP support descriptive judgments about usage and collocation.
- **No detector promises.** “AI-sounding” is treated as an editorial-quality signal, never proof of authorship or a detector-evasion objective.

## Output behavior

The completed artifact is Polish. Notes follow the language of the request and appear only when an assumption, ambiguity, preservation warning, or scope boundary materially matters.

| Request language | Deliverable | Notes |
| --- | --- | --- |
| Polish | Polish | Polish |
| English or another language | Polish artifact first | Concise request-language notes afterward |

## Evidence and authority

The skill distinguishes normative rules from editorial preferences:

- [Rada Języka Polskiego](https://rjp.pan.pl/zasady-pisowni-i-interpunkcji-polskiej-2/) for current spelling and punctuation.
- [Narodowy Korpus Języka Polskiego](https://nkjp.pl/) for descriptive corpus evidence.
- [Wielki słownik języka polskiego PAN](https://wsjp.pl/) for meanings, grammar, register, and typical connections.
- [Gov.pl plain-language guidance](https://www.gov.pl/web/cyfryzacja/prosty-jezyk) for reader-focused public and instructional prose—not as a universal style mandate.

## Repository layout

```text
assets/
├── natural-writing.svg
└── readme-hero.png
skills/
└── natural-polish-writing/
    ├── agents/
    │   └── openai.yaml
    ├── references/
    └── SKILL.md
```

Only the installable skill, runtime references, and repository presentation assets are public package content. Research drafts and development material remain outside the package.

## License

Repository-authored content is available under the [MIT License](LICENSE). Runtime references link to official and specialist sources where useful; third-party material is not reproduced or relicensed here.

<div align="center">
  <sub>Built for Polish that respects the sentence, the speaker, and the truth.</sub>
</div>
