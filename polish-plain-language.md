# `polish-plain-language`: implementation report

## Outcome

The research has been converted into an installable Agent Skill at [`skills/polish-plain-language/`](skills/polish-plain-language/).

The skill does not treat plain language as a cosmetic request to shorten Polish sentences. Its operational objective is to help an intended reader **find, understand, and use** functional information while preserving every material fact, condition, right, obligation, warning, number, deadline, and necessary term.

## Product boundary

| Skill | Primary job |
| --- | --- |
| `natural-polish-writing` | Improve naturalness, genre fit, rhythm, and Polish expression without changing meaning |
| `polish-plain-language` | Rebuild functional information around the reader's task, comprehension, and action |
| Future `polish-easy-to-read` | Produce ETR drafts under stricter linguistic and design rules, with target-user consultation still required |

The boundary prevents stylistic variety from damaging functional consistency. In plain-language content, one concept should normally retain one stable label even when repetition would be edited out of literary or promotional prose.

## Core contract

> Transform functional Polish content so the intended reader can quickly determine what happened, what applies to them, what they need to decide or do, when and how to do it, what happens next, and which exceptions or risks matter—without changing material meaning.

The skill follows this priority order:

1. semantic fidelity;
2. reader task;
3. findability;
4. comprehension;
5. actionability and accessibility of the language structure;
6. natural Polish;
7. concision.

The ordering is deliberate. A precise longer sentence is preferable to a short sentence that changes a condition, exception, deadline, legal effect, or warning.

## Runtime architecture

```text
skills/polish-plain-language/
├── agents/
│   └── openai.yaml
├── references/
│   ├── domain-safeguards.md
│   ├── plain-language-diagnostics.md
│   ├── review-checklist.md
│   └── transformation-contract.md
└── SKILL.md
```

The main skill file contains the essential workflow. Detailed decisions are loaded only when relevant:

- `transformation-contract.md` defines priorities, task extraction, information structures, register, and evaluation;
- `plain-language-diagnostics.md` covers Polish-specific bureaucratic patterns, conditions, reference, terminology, sentences, headings, lists, warnings, and accessibility boundaries;
- `domain-safeguards.md` protects administrative, financial, healthcare, instructional, customer-service, interface, legal, and regulated meaning;
- `review-checklist.md` provides the final semantic and reader-task gate.

## Transformation model

Before rewriting, the skill identifies:

- intended reader and relationship;
- communication purpose;
- status or outcome;
- action and responsible actor;
- prerequisite;
- condition and exception;
- deadline and its calculation basis;
- consequence or expected result;
- warning and recovery path;
- necessary terminology and protected values.

It then chooses an information structure appropriate to the task. A transactional notice may lead with the outcome and action; a procedure usually follows execution order; a warning exposes risk, condition, consequence, and safe action.

## Semantic safeguards

The skill protects:

- names, organizations, products, legal references, identifiers, URLs, quotations, and literal interface labels;
- dates, periods, amounts, rates, percentages, thresholds, units, doses, and calculation bases;
- negation, modality, conditions, exceptions, responsibility, chronology, causality, and scope;
- rights, obligations, legal effects, medical instructions, financial distinctions, and warning strength;
- stable terminology and formal procedural mechanisms.

It must not invent causes, reassurance, deadlines, remedies, rights, eligibility rules, consequences, contact routes, recovery steps, or system states.

## Polish-specific decisions

The implementation intentionally avoids several mechanical rules:

- It does not require subject–verb–object order; Polish information structure remains contextual.
- It does not require every sentence to contain 20 words or fewer.
- It does not ban passive or impersonal constructions when the actor is irrelevant or unknown.
- It does not replace necessary specialist terms with approximate everyday synonyms.
- It does not use synonym variation merely to make functional prose look less repetitive.
- It does not automatically convert every institutional register to `Ty`.

Instead, it prefers reader-relevant actors, finite verbs, stable terms, explicit conditions, descriptive headings, meaningful lists, executable instructions, and precise references.

## Domain behavior

| Domain | Additional protected information |
| --- | --- |
| Administrative | authority, formal mechanism, deadline basis, attachments, delivery method, consequence, appeal route |
| Financial | amounts, currencies, rates, fees, calculation bases, periods, guarantees, exclusions |
| Healthcare | medicine, dose, unit, route, frequency, duration, thresholds, contraindications, urgency |
| Instructional | prerequisites, execution order, literal controls, commands, files, branches, expected result |
| Customer service | transaction state, charges, account or delivery status, retry consequence, support path |

High-stakes language can be reorganized and explained, but specialist review remains necessary when legal interpretation, medical safety, financial compliance, or organizational authority is material.

## Plain language is not ETR

The skill maintains a hard distinction between ordinary Polish plain language and *tekst łatwy do czytania i zrozumienia* (ETR).

It does not silently apply ETR-specific restrictions on sentence length, vocabulary, layout, illustration, or content selection. It also does not claim that an AI-only adaptation is validated or certified ETR. The Polish ETR methodology is aimed at readers with substantial comprehension barriers and includes target-user consultation.

## Accessibility boundary

The skill can improve understandable headings, labels, instructions, warnings, errors, and recovery guidance. Language editing alone cannot guarantee semantic HTML, keyboard operation, contrast, ARIA correctness, assistive-technology compatibility, or WCAG conformance.

## Evaluation

Every result passes three layers:

1. **Semantic validation:** verify that protected meaning did not change.
2. **Plain-language diagnostics:** inspect information order, syntax, terminology, references, headings, instructions, and warnings.
3. **Reader-task questions:** verify that the reader can quickly recover what happened, whether they must act, what to do, by when, how, what happens next, and which exceptions or risks matter.

Readability formulas and sentence counts are diagnostic signals only. They are not evidence that a reader understands or can act on the text.

## Principal sources

- [Rada Języka Polskiego: Zasady pisowni i interpunkcji polskiej](https://rjp.pan.pl/zasady-pisowni-i-interpunkcji-polskiej-2/)
- [Gov.pl: Prosty język](https://www.gov.pl/web/cyfryzacja/prosty-jezyk)
- [Gov.pl: Najważniejsze zasady prostego języka](https://www.gov.pl/web/redakcyjne-abc/najwazniejsze-zasady-prostego-jezyka)
- [Gov.pl: Cztery zasady dostępności cyfrowej](https://www.gov.pl/web/dostepnosc-cyfrowa/cztery-zasady-dostepnosci-cyfrowej)
- [ISO 24495-1:2023: Plain language](https://www.iso.org/standard/78907.html)
- [ISO 24495-2:2025: Legal communication](https://www.iso.org/standard/85774.html)
- [Polish government publication of the 2026 ETR recommendations](https://niepelnosprawni.gov.pl/publikacja-opracowania-standardow-tekstu-latwego-do-czytania-i-zrozumienia-etr/)

The full evidence review remains in [`polish-plain-language deep-research-report.md`](polish-plain-language%20deep-research-report.md). This report records the implementation decisions; it does not duplicate the full research narrative in the installable skill.
