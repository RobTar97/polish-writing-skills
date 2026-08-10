<div align="center">
  <img src="assets/readme-hero.png" alt="Abstract carmine and charcoal forms flowing across an ivory editorial grid" width="100%" />
  <h1>Polish Writing Skills</h1>
  <p><strong>Polish that sounds natural—and functional Polish that readers can act on.</strong></p>
  <p>Two open-source Agent Skills for faithful Polish editing, translation, and reader-centered plain language.</p>
  <p>
    <a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent_Skills-compatible-292827?style=flat-square" alt="Agent Skills compatible" /></a>
    <img src="https://img.shields.io/badge/skills-2-b62234?style=flat-square" alt="Two skills" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-5b5753?style=flat-square" alt="MIT License" /></a>
  </p>
  <p>
    <a href="#quick-install"><img src="https://img.shields.io/badge/Install_with-skills.sh-b62234?style=for-the-badge" alt="Install with skills.sh" /></a>
    <a href="README.pl.md"><img src="https://img.shields.io/badge/Czytaj_po_polsku-f6f0e6?style=for-the-badge&amp;labelColor=292827" alt="Czytaj po polsku" /></a>
  </p>
</div>

---

## Two skills, two editorial contracts

Each skill has one primary job. Both preserve material meaning.

<table>
  <tr>
    <td width="100%" valign="top">
      <img src="assets/natural-writing.svg" alt="Natural Polish Writing illustration" width="100%" />
      <h3><a href="skills/natural-polish-writing/SKILL.md">natural-polish-writing</a></h3>
      <p>Natural, contemporary Polish for non-UI prose.</p>
      <p><strong>Best for:</strong> articles, web and marketing prose, messages, notices, social posts, academic prose, and translation into Polish.</p>
    </td>
  </tr>
  <tr>
    <td width="100%" valign="top">
      <img src="assets/plain-language.svg" alt="Polish Plain Language illustration" width="100%" />
      <h3><a href="skills/polish-plain-language/SKILL.md">polish-plain-language</a></h3>
      <p>Task-focused Polish that readers can find, understand, and use.</p>
      <p><strong>Best for:</strong> administrative and public information, procedures, financial or healthcare explanations, instructions, forms, customer-service messages, warnings, and errors.</p>
    </td>
  </tr>
</table>

> `natural-polish-writing` optimizes expression and genre fit. `polish-plain-language` can rebuild information order around the reader's task. Neither silently changes facts, conditions, rights, obligations, warnings, or deadlines.

## Agent compatibility

Yes—both skills use the basic, portable Agent Skills format. Their cores are standard `SKILL.md` files with Markdown references; neither depends on hooks, model-specific tools, or a proprietary runtime. The official [skills CLI compatibility matrix](https://github.com/vercel-labs/skills#compatibility) marks basic skills as supported across the major coding agents.

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
  --skill natural-polish-writing polish-plain-language \
  -a codex -a claude-code -a opencode -a antigravity
```

Omit `-a` to let the CLI detect installed agents interactively.

## Quick install

Install from the repository with the official [skills CLI](https://skills.sh/docs/cli) (recommended):

```bash
npx skills@latest add RobTar97/polish-writing-skills
```

Install one skill directly:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing
```

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill polish-plain-language
```

Install both globally for Codex without prompts:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing polish-plain-language -g -a codex -y
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

```bash
npx skills@latest use RobTar97/polish-writing-skills@polish-plain-language
```

## See the technique

### Natural Polish writing

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

### Polish plain language

The plain-language skill changes the information architecture before polishing individual sentences.

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>Before</h3>
      <p>W związku z przeprowadzoną weryfikacją kompletności dokumentacji informujemy o stwierdzeniu braku załącznika nr 3, którego niedostarczenie w terminie 7 dni od dnia otrzymania niniejszego wezwania skutkować będzie pozostawieniem wniosku bez rozpoznania.</p>
    </td>
    <td width="50%" valign="top">
      <h3>After</h3>
      <p><strong>Doślij załącznik nr 3 w ciągu 7 dni od otrzymania tego wezwania.</strong><br />W Twoim wniosku brakuje tego załącznika.<br />Jeśli nie dostarczysz go w terminie, pozostawimy wniosek bez rozpoznania.</p>
    </td>
  </tr>
</table>

**Preserved:** attachment number, seven-day deadline and its calculation basis, missing-document status, required action, and procedural consequence.

**Changed:** the reader's action and deadline now come first; the institution-first opening and nominalized structure are removed. No submission channel, legal basis, or appeal right was invented.

The validation maps to the skill's [transformation contract](skills/polish-plain-language/references/transformation-contract.md) and [review checklist](skills/polish-plain-language/references/review-checklist.md).

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

```text
Use $polish-plain-language to rewrite this notice around the reader's task.
Keep every deadline, condition, consequence, right, and required term unchanged.
```

```text
Użyj $polish-plain-language, aby odbiorca szybko znalazł decyzję, wymagane działanie,
termin i konsekwencje. Nie zmieniaj podstawy prawnej ani warunków.
```

## How it works

- **Separate objectives.** Natural writing optimizes expression and genre fit; plain language optimizes findability, comprehension, and action.
- **Meaning before improvement.** Facts, conditions, uncertainty, chronology, numbers, names, rights, obligations, warnings, commitments, and consequences stay intact.
- **Reader task before sentence length.** Plain-language work identifies what readers need to know or do, then chooses an appropriate information structure.
- **Genre and domain safeguards.** Academic, administrative, financial, healthcare, service, and instructional texts do not receive the same treatment.
- **Smallest sufficient intervention.** Natural writing prefers local corrections; plain language changes structure only when reader success requires it.
- **Stable functional terminology.** Plain-language work does not introduce synonyms merely to avoid repetition.
- **No simulated humanity.** It does not add anecdotes, opinions, slang, typos, evidence, or fake personal experience.
- **Current rules, contextual evidence.** Orthography and punctuation follow the RJP rules in force since 2026; NKJP and WSJP support descriptive judgments about usage and collocation.
- **Plain language is not ETR.** The skill does not apply Easy-to-Read rules or claim ETR validation without the required target-user process.
- **No detector promises.** “AI-sounding” is treated as an editorial-quality signal, never proof of authorship or a detector-evasion objective.

## Output behavior

The completed artifact is Polish. Both skills return the finished text first. Notes follow the language of the request and appear only when an assumption, ambiguity, preservation warning, or scope boundary materially matters.

| Request language | Deliverable | Notes |
| --- | --- | --- |
| Polish | Polish | Polish |
| English or another language | Polish artifact first | Concise request-language notes afterward |

## Evidence and authority

The skills distinguish normative rules from editorial preferences and plain-language methods:

- [Rada Języka Polskiego](https://rjp.pan.pl/zasady-pisowni-i-interpunkcji-polskiej-2/) for current spelling and punctuation.
- [Narodowy Korpus Języka Polskiego](https://nkjp.pl/) for descriptive corpus evidence.
- [Wielki słownik języka polskiego PAN](https://wsjp.pl/) for meanings, grammar, register, and typical connections.
- [Gov.pl plain-language guidance](https://www.gov.pl/web/cyfryzacja/prosty-jezyk) for reader-focused public and instructional prose—not as a universal style mandate.
- [Gov.pl digital-accessibility guidance](https://www.gov.pl/web/dostepnosc-cyfrowa/cztery-zasady-dostepnosci-cyfrowej) for understandable labels, instructions, warnings, and error recovery.
- [ISO 24495-1:2023](https://www.iso.org/standard/78907.html) for the governing plain-language principles.
- [ISO 24495-2:2025](https://www.iso.org/standard/85774.html) for plain legal communication and preservation of rights and obligations.

## Repository layout

```text
assets/
├── natural-writing.svg
├── plain-language.svg
└── readme-hero.png
skills/
├── natural-polish-writing/
│   ├── agents/
│   │   └── openai.yaml
│   ├── references/
│   └── SKILL.md
└── polish-plain-language/
    ├── agents/
    │   └── openai.yaml
    ├── references/
    └── SKILL.md
```

The installable skills contain only runtime instructions and focused references. The repository root also retains the [plain-language implementation report](polish-plain-language.md) and its [deep research report](polish-plain-language%20deep-research-report.md) for transparent development history.

## License

Repository-authored content is available under the [MIT License](LICENSE). Runtime references link to official and specialist sources where useful; third-party material is not reproduced or relicensed here.

<div align="center">
  <sub>Built for Polish that respects the sentence, the reader, and the truth.</sub>
</div>
