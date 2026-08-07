<div align="center">
  <img src="assets/readme-hero.png" alt="Abstract carmine and charcoal forms flowing across an ivory editorial grid" width="100%" />
  <h1>Polish Writing Skills</h1>
  <p><strong>Polish that sounds natural, fits the genre, and keeps the meaning intact.</strong></p>
  <p>An open-source Agent Skill for editing and translating natural Polish prose with strict factual fidelity.</p>
  <p>
    <a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent_Skills-compatible-292827?style=flat-square" alt="Agent Skills compatible" /></a>
    <img src="https://img.shields.io/badge/skills-1-b62234?style=flat-square" alt="One skill" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-5b5753?style=flat-square" alt="MIT License" /></a>
    <a href="https://skills.sh/RobTar97/polish-writing-skills"><img src="https://skills.sh/b/RobTar97/polish-writing-skills" alt="skills.sh installs" /></a>
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
      <p>Plan Pro umożliwia 12 osobom wspólne planowanie zadań. Okres próbny trwa 14 dni, a po jego zakończeniu abonament kosztuje 29 zł miesięcznie. Do korzystania z Plan Pro potrzebne jest połączenie z internetem.</p>
    </td>
  </tr>
</table>

**Preserved:** the product name, 12-person limit, 14-day trial, 29 zł monthly price, and internet requirement.

**Changed:** generic framing, unsupported promotional evaluation, repetitive connective language, and the empty reminder frame. No capability, proof, urgency, or promise was added.

This is a traceable editing example, not an automated benchmark. The checks map to the skill’s [editing priorities](skills/natural-polish-writing/references/editing-priorities.md) and [review checklist](skills/natural-polish-writing/references/review-checklist.md).

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
