# Transformation contract

## Decision order

Resolve conflicts in this order:

1. **Semantic fidelity:** preserve material meaning.
2. **Reader task:** expose the required decision, action, or information.
3. **Findability:** place critical information where readers expect it.
4. **Comprehension:** simplify structure, vocabulary, terminology, and reference.
5. **Actionability:** make prerequisites, steps, timing, consequences, and help explicit.
6. **Natural Polish:** remove avoidable bureaucratic or translation-shaped language.
7. **Concision:** remove only genuine redundancy.

A precise longer sentence is better than a shorter sentence that changes a condition, exception, legal effect, or warning.

## Reader-task model

Determine internally:

| Question | Extract |
| --- | --- |
| Who is reading? | expertise, role, relationship, likely context |
| Why are they reading? | decision, action, explanation, warning, consent |
| What happened? | status, result, change, problem |
| What applies to them? | eligibility, condition, exception, scope |
| What must or may they do? | action and responsible actor |
| When and how? | deadline basis, channel, steps, prerequisites |
| What happens next? | result, consequence, recovery, help |
| Which terms must remain? | legal, medical, financial, technical, UI terms |

Do not print this map unless the user asks for it.

## Semantic units

Extract before rewriting:

- status or outcome;
- action and actor;
- prerequisite;
- condition and branch;
- deadline and how it is calculated;
- consequence and warning;
- exception or exclusion;
- amount, definition, legal or technical basis;
- contact, escalation, or recovery route.

Keep combined conditions combined. For example, do not split `jeśli masz mniej niż 18 lat i składasz wniosek samodzielnie` into independent statements that erase the logical `and`.

## Information structures

Use the smallest structure that fits the task:

- **Status message:** outcome → action → consequence → help.
- **Procedure:** prerequisite → numbered actions → expected result → recovery.
- **Notice or request:** required action → deadline → reason → consequence → basis → contact.
- **Explanation:** answer → essential context → definitions → exceptions → source or basis.
- **Warning:** risk → condition → consequence → safe action.
- **Comparison:** reader-relevant criteria in a table or parallel list.

Do not force every document into one template. Preserve a necessary narrative, evidentiary, contractual, or argumentative relationship.

## Register control

Preserve the source register by default. Suitable realizations may include:

- direct `Ty` for established consumer communication;
- `Pan/Pani/Państwo` for relationship-sensitive communication;
- plural address for a known collective audience;
- neutral imperatives or impersonal instructions;
- institutional formality where roles or protocol require it.

Do not treat directness as permission to become casual, patronizing, or legally overconfident.

## Evaluation model

Use three layers:

1. **Semantic validation:** hard gate; no protected meaning may change.
2. **Plain-language diagnostics:** signals for editorial review, not automatic failure.
3. **Reader-task check:** verify that the intended reader can recover the necessary answers quickly and explicitly.

Readability scores, average sentence length, and passive counts cannot establish comprehension. Prefer task-based testing with representative readers when the stakes justify it.

## Sources

- [Gov.pl: Prosty język](https://www.gov.pl/web/cyfryzacja/prosty-jezyk) — Polish public-sector principles for reader-focused, understandable communication.
- [Gov.pl: Najważniejsze zasady prostego języka](https://www.gov.pl/web/redakcyjne-abc/najwazniejsze-zasady-prostego-jezyka) — audience, task, structure, and practical editing guidance.
- [ISO 24495-1:2023](https://www.iso.org/standard/78907.html) — governing principles and guidelines for plain-language documents.
- [Rada Języka Polskiego: Zasady pisowni i interpunkcji polskiej](https://rjp.pan.pl/zasady-pisowni-i-interpunkcji-polskiej-2/) — normative Polish orthography and punctuation in force from 2026.
