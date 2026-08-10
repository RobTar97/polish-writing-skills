---
name: polish-plain-language
description: Rewrite or structure functional Polish content so its intended reader can quickly find, understand, and use the information without changing material meaning. Use for administrative letters, public information, financial or healthcare explanations, procedures, instructions, forms, customer-service messages, warnings, errors, notices, or requests for prosty język, prosta polszczyzna, zrozumiały tekst, clearer Polish, reader-centered Polish, or actionable Polish. Preserve rights, obligations, conditions, exceptions, numbers, deadlines, terminology, warnings, and register. Do not present ordinary plain-language work as Easy-to-Read (ETR) or as proof of accessibility compliance.
---

# Polish Plain Language

## Establish the reader's task

1. Identify the intended reader, domain, relationship, channel, purpose, and requested format.
2. Determine what the reader needs to find, decide, understand, or do after reading.
3. Extract the status or outcome, required action, prerequisites, conditions, deadline, consequence, exceptions, help path, and necessary terminology.
4. Infer missing context conservatively. Ask only when a missing choice would materially change meaning, responsibility, register, or the required action.
5. Default to contemporary `pl-PL`, the current RJP 2026 rules, the source register, and ordinary plain language—not Easy-to-Read.

For the complete analysis sequence and transformation hierarchy, read [transformation contract](references/transformation-contract.md).

## Protect material meaning

Build a semantic lock before changing the information architecture. Preserve:

- people, organizations, products, legal acts, article references, identifiers, URLs, quotations, and literal UI labels;
- numbers, dates, periods, amounts, currencies, percentages, rates, thresholds, units, doses, and calculation bases;
- negation, possibility, certainty, recommendation, obligation, permission, prohibition, conditions, and exceptions;
- rights, legal effects, medical instructions, warning strength, responsibility, chronology, causality, and scope;
- stable domain terminology and the distinction between a formal mechanism and an ordinary-language approximation.

Never invent a cause, reassurance, deadline, remedy, right, eligibility rule, consequence, contact route, recovery step, or missing procedure. Preserve unresolved substantive ambiguity and flag it briefly when it prevents a safe rewrite.

For administrative, financial, healthcare, instructional, and service content, read [domain safeguards](references/domain-safeguards.md).

## Rebuild the information architecture

Write for the reader's task, not the institution's process.

For transactional or instructional content, consider this default order:

1. outcome or status;
2. reader action;
3. deadline or controlling condition;
4. prerequisites and required materials;
5. consequence or expected result;
6. exceptions;
7. explanation or legal and technical basis;
8. contact or help.

Use chronological order when it better matches the task. Keep a condition visibly attached to the action or consequence it controls. Place decision-critical facts where readers can find them without reconstructing the institution's reasoning.

Create headings that answer reader questions. Use lists only for genuine sequences, requirements, options, or comparisons. Make warnings expose the risk, triggering condition, consequence, and safe action. For detailed Polish patterns and diagnostics, read [plain-language diagnostics](references/plain-language-diagnostics.md).

## Rewrite in plain Polish

- Prefer explicit actions and reader-relevant actors over nominalizations and institutional fog.
- Prefer familiar words, but retain necessary legal, medical, financial, technical, and interface terms. Explain them instead of replacing them inaccurately.
- Expand an unfamiliar abbreviation on first meaningful use when the expansion helps the reader. Preserve established user-facing names and literal controls.
- Use one stable term for one concept. Do not introduce synonyms merely for stylistic variety.
- Prefer structurally simple sentences and keep related elements close. Treat sentence length as a diagnostic, never a rule.
- Use unmarked, easy-to-process word order without imposing an SVO template on Polish.
- Replace vague back-references with the precise noun when a pronoun or generic label would be ambiguous.
- Preserve the source's respectful register unless the request authorizes a change. Plain Polish does not require `Ty`.
- Remove genuine redundancy, ceremonial framing, and avoidable bureaucratic constructions only after protecting meaning.

## Respect boundaries

Plain language is not Easy-to-Read Polish. Do not apply ETR-specific sentence, vocabulary, layout, illustration, or content-selection rules unless the user explicitly asks for ETR. Do not call an AI-only adaptation validated or certified ETR; target-user consultation is separate work.

Language rewriting alone does not guarantee digital accessibility, legal sufficiency, medical safety, financial compliance, semantic HTML, ARIA correctness, contrast, or WCAG conformance. Improve the language and structure that are in scope, then state any material specialist or implementation review still required.

For structured UI resources, preserve every key, placeholder, tag, escape sequence, and runtime branch. Improve only language that can be changed safely from the available context and note when product-localization QA remains necessary.

## Validate and deliver

1. Compare the output with the semantic lock; reject any fluent candidate that changes protected meaning.
2. Check whether the reader can quickly answer: What happened? Does this apply to me? What must or may I do? By when? How? What happens next? What exceptions or risks matter?
3. Review terminology, references, conditions, headings, instructions, warnings, and recovery paths.
4. Treat readability formulas and word counts as review signals, not evidence of comprehension.
5. Apply the [review checklist](references/review-checklist.md).

Return the finished Polish artifact first. Add only material assumptions, unresolved ambiguity, preservation warnings, or scope limitations by default. Provide an analysis, reader-task map, or edit log only when requested.
