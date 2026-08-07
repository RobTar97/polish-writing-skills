---
name: natural-polish-writing
description: Edit, rewrite, or translate non-UI text into natural, contemporary Polish while preserving facts, intent, uncertainty, terminology, and voice. Use for articles, web or marketing prose, ordinary messages and notices, social posts, academic prose, translations into Polish, or requests to make Polish sound natural, native, less mechanical, mniej sztucznie, bardziej naturalnie, or poprawić styl without detector evasion. For structured locale resources or relationship-sensitive formal correspondence, perform only a safe language pass and flag the specialized work still required.
---

# Natural Polish Writing

## Establish the assignment

1. Determine the task, reader, genre, channel, register, voice, format, and permitted degree of change from the request and source.
2. Infer missing context conservatively. Ask only when a choice would materially alter the result; otherwise state a consequential assumption briefly.
3. Default to contemporary `pl-PL`, the current RJP 2026 rules, and the smallest edit that solves the problem.
4. Preserve an explicit house style or glossary unless it conflicts with the user's request or a factual requirement.

For structured locale files, placeholders, message syntax, or in-product interaction design, preserve every technical token and limit the work to a safe language pass. For high-stakes or relationship-sensitive formal correspondence, improve the Polish without inventing protocol, commitments, apologies, authority, or organizational policy. Briefly identify the need for specialized localization or business-writing work.

## Protect meaning

Create a semantic lock before editing. Record substantive claims, certainty, conditions, negation, causality, chronology, numbers, units, dates, times, names, attribution, quotation content, citations, URLs, protected terms, commitments, and the writer's actual position or experience. Distinguish these from content-free framing and unsupported promotional evaluation; do not lock an adjective as a fact merely because it appears in the source.

Never invent facts, examples, evidence, mechanisms, testimonials, lived experience, opinions, urgency, permissions, apologies, promises, or precision. Never strengthen *może* into certainty, remove a limitation, change who did something, or replace stable terminology merely for variety.

For a non-Polish source, translate all relevant meaning faithfully before polishing its Polish expression. Preserve ambiguity when the source does not resolve it.

Read [editing priorities](references/editing-priorities.md) for the decision order, semantic-lock method, and translation safeguards.

## Edit for natural Polish

Treat “AI-sounding” as an editorial-quality description, never as proof of authorship or a detector-evasion target. Diagnose patterns by their density, context, and effect: generic framing, empty evaluation, repetitive connectives, semantic restatement, terminology drift, translation-like collocations, overloaded syntax, register mismatch, mechanical rhythm, and faulty punctuation or typography. Do not ban a word, structure, passive, nominalization, dash, list, or sentence length in isolation.

In ordinary and marketing prose, remove generic promotional judgments such as *kluczowy*, *kompleksowy*, *innowacyjny*, or *niezwykle intuicyjny* when the source supplies no evidence and the user has not explicitly marked them as approved claims or required wording. A request to preserve facts does not protect those judgments. Remove empty frames such as *warto zauważyć, że*, *należy podkreślić, że*, or *trzeba pamiętać, że* while preserving the substantive statement, warning, or limitation that follows.

Edit in this order:

1. Fix information order and remove content-free framing or repetition.
2. Match the reader, genre, channel, register, and communicative purpose.
3. Repair terminology, collocations, calques, reference, and lexical precision.
4. Repair syntax, agency, word order, agreement, government, aspect, and rhythm.
5. Normalize spelling, punctuation, quotation marks, dashes, capitalization, and spacing.
6. Compare the result with the semantic lock and revert any unsupported change.

Prefer a local correction over a wholesale rewrite. Preserve deliberate irregularity, humor, emphasis, informality, technical density, academic caution, and established voice when they serve the text.

Read [naturalness diagnostics](references/naturalness-diagnostics.md) when identifying Polish-specific problems. Read [genres and boundaries](references/genres-and-boundaries.md) when register, medium, translation, UI, or formal-business scope matters.

## Deliver

- Return the finished Polish text first.
- Use the language of the user's request for any notes: Polish for a Polish request and concise English for an English or other-language request.
- Add only material assumptions, unresolved ambiguity, preservation warnings, or scope limitations by default. Provide a detailed edit log only when requested.
- Reframe detector-evasion requests as work on naturalness, clarity, correctness, voice, and genre fit. Do not promise a detector result or claim that the text is human-authored.

Before sending, apply the [review checklist](references/review-checklist.md).
