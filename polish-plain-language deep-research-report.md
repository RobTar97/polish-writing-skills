# Polish Plain Language: Research-Based Specification for `polish-plain-language`

> **Implementation status:** This research has been converted into the installable [`polish-plain-language`](skills/polish-plain-language/SKILL.md) skill. See the concise [`polish-plain-language` implementation report](polish-plain-language.md) for the final architecture, boundaries, and validation model. This document remains the full research record.

## Executive conclusion

Robert, the central design decision is this:

**`polish-plain-language` should not be a “make this sound natural” skill.** It should be a **task-oriented information transformation skill** whose success criterion is whether the intended Polish reader can **find, understand, and correctly use** the information.

That distinction is not cosmetic. The Polish Ministry of Digital Affairs explicitly describes *prosty język* as a **communication standard**, not simply an attractive writing style. Its guidance starts with the reader's perspective, recommends putting the most important information first, using direct forms, explaining abbreviations and difficult terms, organizing information logically, and using headings, paragraphs, lists, and tables. citeturn24view0 The government's digital-accessibility guidance goes further: understandable content, instructions, warnings, form labels, error messages, and correction guidance are treated as part of digital accessibility. citeturn24view1

The international plain-language definition points in the same direction: wording, structure, and design should enable intended readers to **find what they need, understand it, and use it**. Audience and purpose, structure, design, expression, and evaluation are all part of plain language. citeturn26view2

So I would give the skill this core contract:

> **Transform Polish functional content so that its intended reader can quickly determine what matters, what applies to them, what they need to decide or do, when and how to do it, and what happens next — while preserving all material meaning, conditions, rights, obligations, numbers, warnings, and necessary terminology.**

That is substantially stronger than:

> “Make this simpler.”

And much stronger than:

> “Make this sound human.”

Those are different jobs.

I would therefore keep your future architecture separated:

| Skill | Primary optimization |
|---|---|
| `polish-perfect-writing` | Native-feeling Polish, natural rhythm, stylistic quality, removal of LLM artifacts |
| `polish-plain-language` | Findability, comprehension, task completion, accessibility |
| `polish-easy-to-read` | Dedicated ETR adaptation for readers with substantial comprehension difficulties |
| optional domain skills | Legal, healthcare, finance, administration terminology and semantic safeguards |

This separation matters because some anti-AI techniques actively **conflict** with plain language. For example, stylistic synonym variation may make prose feel less repetitive, yet Polish government guidance specifically advises against unnecessary synonyms, and ETR guidance is stricter still about using the same term for the same concept. citeturn24view0turn23view2

A good pipeline could eventually be:

```text
source
  ↓
domain / semantic preservation
  ↓
polish-plain-language
  ↓
polish-perfect-writing
     with a constraint:
     "do not undo terminology consistency,
      task structure, warnings, conditions,
      or information hierarchy"
```

Not the reverse. Otherwise the stylistic agent cheerfully “improves” a carefully standardized instruction by introducing four elegant synonyms for one government service. Very literary. Very useless.

## What Polish plain language actually requires

### Reader purpose comes before sentence simplification

The strongest recurring finding across Polish government material and international plain-language guidance is that simplification begins **before editing individual sentences**.

The Polish European Funds guidance tells writers to determine who the reader is, what the reader already knows, whether they regularly encounter official documents, which information matters to them, and crucially: **what the recipient should do after reading the document**. It then recommends organizing information either by importance or chronologically and testing whether readers can actually locate information and perform tasks. citeturn25view0

This means the skill should first reconstruct an implicit communication model:

```text
WHO is reading?
WHY are they reading?
WHAT decision are they trying to make?
WHAT action may they need to take?
WHAT do they need before taking it?
WHEN must they act?
WHAT happens if they do or do not act?
WHERE / HOW do they act?
WHAT terminology must they understand?
```

Only then should it rewrite sentences.

Consider a synthetic administrative example:

**Source**

> W związku z przeprowadzoną weryfikacją kompletności dokumentacji złożonej w ramach postępowania informujemy o stwierdzeniu braku załącznika nr 3, którego niedostarczenie w terminie 7 dni od dnia otrzymania niniejszego wezwania skutkować będzie pozostawieniem wniosku bez rozpoznania.

A conventional “simplifier” might merely split it:

> Zweryfikowaliśmy dokumentację. Brakuje załącznika nr 3. Należy go dostarczyć w ciągu 7 dni. W przeciwnym razie wniosek zostanie pozostawiony bez rozpoznania.

Better, but still written from the institution's perspective.

A task-oriented plain-language version is:

> **Doślij załącznik nr 3 w ciągu 7 dni od otrzymania tego wezwania.**  
> W Twoim wniosku brakuje tego załącznika.  
> Jeśli nie dostarczysz go w terminie, pozostawimy wniosek bez rozpoznania.

The improvement is primarily **information architecture**, not shorter words.

That directly reflects Polish government advice to begin with information most important to the recipient and to adopt the recipient's perspective. citeturn24view0

### Plain language is an information-design problem

The Ministry of Digital Affairs recommends logical ordering, headings, paragraphs, lists, and tables, while government accessibility guidance requires logical content structures and stresses that headings and lists should not be merely visual when content is digital. citeturn24view0turn24view1

Accordingly, the skill should be allowed to change:

- information order;
- paragraph boundaries;
- headings;
- list structure;
- instruction sequence;
- placement of explanations;
- placement of legal bases;
- warning prominence.

But it should **not** be allowed to invent or eliminate substantive content.

This is especially important for an agent skill. Merely rewriting sentences in their existing order preserves the very administrative architecture plain language is supposed to fix.

### Polish-specific simplification cannot be imported mechanically from English

The University of Wrocław's Plain Polish Lab notes that readability methods developed for other languages, particularly English, cannot simply be transferred to Polish because of systemic differences including Polish's rich inflection. citeturn25view1

There is another subtle Polish-specific issue that I would explicitly encode into the skill.

The Ministry's introductory guidance says to use a “natural” order and summarizes it rather crudely as putting the noun before the verb. citeturn24view0 That is acceptable as beginner-facing government advice, but **it is too crude for an agent instruction**. Research on Polish word-order variation specifically analyzes the interaction between information structure and constituent ordering; Polish order cannot responsibly be reduced to “always use subject–verb–object.” citeturn27view1

Therefore do **not** hard-code:

```text
ALWAYS use SVO.
```

Instead use something like:

```text
Prefer unmarked, easy-to-process word order in informational prose.
Keep the actor and finite verb reasonably close.
Do not move constituents merely to satisfy an SVO template.
Preserve information structure when fronting expresses a meaningful
condition, contrast, topic, or emphasis.
```

For example:

> Jeśli nie masz Profilu Zaufanego, wybierz „Potwierdź tożsamość w urzędzie”.

is naturally useful despite beginning with a subordinate condition.

Forcing:

> Ty wybierz „Potwierdź tożsamość w urzędzie”, jeśli nie masz Profilu Zaufanego.

does not make it more Polish, clearer, or more plain.

## Recommended transformation contract

I would formalize the skill around **semantic invariants, reader-task reconstruction, transformation rules, and validation**, rather than a loose collection of style tips.

### Proposed skill-level contract

```yaml
name: polish-plain-language

purpose: >
  Transform functional Polish content so the intended reader can
  quickly find, understand, and use the information while preserving
  all material meaning.

default_mode:
  language: Polish
  audience: intended non-expert reader inferred from context
  adaptation: plain_language
  easy_to_read: false
  preserve_register: true

primary_goals:
  - identify the reader's task, decision, or information need
  - put decision-critical and action-critical information first
  - make conditions, actions, deadlines, consequences, and next steps explicit
  - explain necessary terminology and abbreviations
  - make structure easy to scan
  - reduce unnecessary linguistic and bureaucratic complexity
  - preserve factual, legal, medical, financial, and procedural meaning

must_not:
  - invent missing facts
  - silently resolve substantive ambiguity
  - change rights, obligations, conditions, exceptions, thresholds, or deadlines
  - change numbers, units, amounts, rates, doses, dates, or references
  - weaken warnings
  - replace legally or technically necessary terms with inaccurate approximations
  - remove information merely to shorten the text
  - treat a sentence-length score as proof of comprehension
  - label ordinary simplification as Easy-to-Read
```

This prioritization follows the reader-centered model in Polish government guidance and the international plain-language model of finding, understanding, and using information. citeturn25view0turn26view2

### The transformation hierarchy

The skill needs explicit priorities so that one rule does not accidentally destroy a more important one.

I recommend:

| Priority | Objective | Meaning for the agent |
|---|---|---|
| **P0** | Semantic fidelity | Never make the message materially wrong |
| **P1** | Reader task | Make the required decision/action unmistakable |
| **P2** | Findability | Put information where readers expect and can scan it |
| **P3** | Comprehension | Simplify syntax, vocabulary, terminology and references |
| **P4** | Accessibility | Improve headings, instructions, warnings, errors and structure |
| **P5** | Natural Polish | Avoid bureaucratic or machine-like formulations |
| **P6** | Concision | Remove genuine redundancy, not necessary content |

The order is deliberate.

A legally accurate 24-word sentence is preferable to an elegant 12-word sentence that changes a condition.

ISO's legal plain-language standard explicitly recognizes that legal communication must remain capable of dealing with legally required structures, complex and nuanced legal concepts, multiple audiences, and processes through which readers exercise rights and obligations. citeturn28view0

### Reader-task extraction

Before rewriting, the agent should internally identify at least:

| Question | Example answer |
|---|---|
| Who is the reader? | customer whose payment failed |
| Why are they reading? | to understand whether the order exists |
| Main decision/action | retry payment |
| Prerequisites | verify card details |
| Deadline | none |
| Consequence | order will not be placed until payment succeeds |
| Important exception | do not retry if account was already charged |
| Next step | contact support if charge exists |
| Necessary terminology | authorization, payment card |

This analysis should normally be **internal**, not dumped into the customer-facing rewrite.

If the skill cannot determine the task reliably, it should preserve the uncertainty instead of manufacturing one.

### Information order

For transactional and instructional text, a useful default hierarchy is:

```text
OUTCOME / STATUS
↓
ACTION
↓
DEADLINE OR CONDITION
↓
WHAT THE READER NEEDS
↓
CONSEQUENCE / EXPECTED RESULT
↓
EXCEPTIONS
↓
EXPLANATION
↓
LEGAL / TECHNICAL BASIS
↓
CONTACT / HELP
```

But this is a **default, not a universal template**. Procedures may work better chronologically, exactly as Polish government material recommends. citeturn25view0

Example:

**Before**

> W celu dokonania zmiany danych adresowych konieczne jest uprzednie zalogowanie się do systemu, a następnie przejście do zakładki „Dane osobowe”, w której możliwe jest dokonanie stosownej aktualizacji.

**After**

> **Jak zmienić adres**
>
> 1. Zaloguj się do systemu.
> 2. Otwórz **Dane osobowe**.
> 3. Zmień adres i zapisz dane.

There is no intellectual prize for preserving “w celu dokonania”, “konieczne jest” and “możliwe jest dokonanie stosownej aktualizacji.” The reader came to change an address, not to admire the institution's collection of nominalizations.

## Polish-specific language and structure rules

### Prefer actions and actors over nominalizations and institutional fog

Official Polish guidance recommends direct forms, discourages passive constructions and deverbal nouns, and replaces constructions such as *dokonywać zakupów* with *kupić*. citeturn24view0 The University of Wrocław's work on plain Polish likewise treats text organization, sentence processing and interpersonal relationships as central parts of the standard, not merely vocabulary replacement. citeturn25view1

The skill should aggressively inspect constructions such as:

| Bureaucratic pattern | Prefer when meaning permits |
|---|---|
| dokonać wpłaty | wpłacić |
| dokonać zgłoszenia | zgłosić |
| dokonać wyboru | wybrać |
| przeprowadzić weryfikację | sprawdzić / zweryfikować |
| nastąpi realizacja | zrealizujemy / rozpocznie się |
| w celu uzyskania | aby uzyskać |
| istnieje możliwość | możesz / można |
| zachodzi konieczność | musisz / trzeba |
| dokonano zmiany | zmieniliśmy / urząd zmienił |
| zostało przeprowadzone badanie | przeprowadziliśmy badanie / badanie przeprowadzono, if actor irrelevant |

But this must not become a primitive search-and-replace list.

Compare:

> Dokonano kontroli urządzenia.

Who did it?

Sometimes that omission is bad:

> **Serwisant sprawdził urządzenie.**

Sometimes the actor genuinely does not matter:

> **Urządzenie sprawdzono przed wysyłką.**

The skill should optimize **reader-relevant agency**, not wage ideological war against every impersonal construction.

### Keep conditions attached to consequences

For procedural Polish, conditional information is often clearer when the condition appears before the action it controls:

> **Jeśli** zmienił się Twój adres, zaktualizuj dane.

rather than:

> Zaktualizuj dane w przypadku zaistnienia zmiany adresu.

This also reduces nominalization and makes branching logic easier to scan. Polish plain-language materials recommend organizing information around user needs and procedures, while international plain-language guidance treats logical sequencing as part of structure rather than mere sentence style. citeturn24view0turn26view2

For agents, I would explicitly model conditional structures as:

```text
IF condition
THEN action
BY deadline
OTHERWISE consequence
```

Then realize that logic naturally in Polish.

Example:

> Jeśli otrzymasz wezwanie do uzupełnienia dokumentów, wyślij brakujące dokumenty w terminie podanym w wezwaniu. Jeśli tego nie zrobisz, urząd może zakończyć sprawę bez rozpatrzenia wniosku.

The important thing is not that every sentence is short. It is that the branching logic is visible.

### Explain terminology rather than blindly deleting it

The Ministry recommends familiar words and requires difficult terminology to be explained; abbreviations should be expanded on first use. citeturn24view0 Digital-accessibility guidance repeats the same requirement for new concepts and abbreviations. citeturn24view1

The correct transformation is therefore often:

```text
technical/legal term + plain explanation
```

not:

```text
technical/legal term → approximate casual synonym
```

Example:

**Risky rewrite**

> Możesz poprosić urząd, żeby jeszcze raz spojrzał na decyzję.

**Better when the legal mechanism is actually an appeal**

> Możesz złożyć **odwołanie**, czyli formalnie zakwestionować decyzję.

The exact procedural term stays discoverable and legally useful; the reader also learns what it means.

The same principle is valuable in healthcare:

**Too technical**

> Lek jest przeciwwskazany u pacjentów z ciężką niewydolnością nerek.

**Potential plain-language structure**

> **Nie stosuj leku, jeśli masz ciężką niewydolność nerek.**  
> Niewydolność nerek oznacza, że nerki nie działają prawidłowo.

Whether that precise wording is medically valid depends on the source material; a plain-language agent must **not invent the clinical threshold or broaden the contraindication**. Plain-language adaptation has been applied to Polish healthcare materials such as informed-consent documents, while ISO's newer legal-communication standard explicitly includes health-sector legal communication. citeturn25view1turn28view0

### Expand abbreviations intelligently

The baseline rule should be:

> Expand an abbreviation or initialism on first meaningful use unless the full form would be less useful to the intended audience and the abbreviation is already the actual user-facing name.

Official Polish guidance gives the pattern:

```text
Kancelaria Prezesa Rady Ministrów (KPRM)
```

on first use. citeturn24view0

For an agent, I would add one important nuance.

Do not blindly produce absurd expansions every time:

> Zakład Ubezpieczeń Społecznych (ZUS)

is appropriate in a formal informational page.

But a button probably should remain:

> Zaloguj się do ZUS

if that is the exact product/interface terminology.

The skill must distinguish **prose explanation** from **literal UI labels**.

### Do not introduce synonym variation merely for style

This is one of the places where `polish-perfect-writing` and `polish-plain-language` diverge.

Suppose a source discusses *wniosek*.

A “humanizer” may generate:

> wniosek → dokument → formularz → zgłoszenie → podanie

because repetitive vocabulary looks machine-generated.

That is disastrous when those terms carry different meanings.

The Ministry explicitly advises writers not to introduce synonyms simply for variation outside literary writing. citeturn24view0

For functional content:

> **one concept → one stable label**

should usually beat lexical variety.

### Sentence length is a warning signal, not a law

The Ministry's public guidance suggests roughly **15–20 words per sentence**. citeturn24view0 International plain-language guidance similarly describes 15–20 words as an average rather than requiring every sentence to hit the same target. citeturn26view2

More importantly, Tomasz Piekot's 2026 review of readability research reports a lack of conclusive evidence that simply improving readability-formula scores improves comprehension and notes that the ISO plain-language approach favors user testing over relying on readability formulas. citeturn26view1

Therefore this would be a bad skill rule:

```text
MUST: Every Polish sentence <= 20 words.
```

It encourages pathological output like:

> Bank może odmówić wypłaty.  
> Są pewne sytuacje.  
> Wynikają one z umowy.  
> Umowa jest zawarta z klientem.  
> Dotyczy ona rachunku.

The sentences are short. The text is dreadful.

Use instead:

```text
SHOULD:
- keep most informational sentences relatively short;
- flag unusually long or deeply embedded sentences for review;
- split only where semantic relations remain clear;
- prefer one dominant proposition per sentence;
- allow longer sentences when splitting would obscure a condition,
  contrast, exception, or legal relationship.
```

A useful diagnostic system would flag:

- long sentences;
- multiple nested subordinate clauses;
- multiple parentheticals;
- long noun chains;
- several nominalizations;
- distant subject/verb relationships;
- stacked conditions;
- ambiguous pronoun references.

Then the agent decides whether rewriting actually helps.

### Keep references explicit when ambiguity would result

Functional Polish often contains:

> powyższy  
> przedmiotowy  
> ww.  
> wskazany wyżej  
> rzeczony  
> niniejszy

Many can be replaced with the actual object:

> ten wniosek  
> umowa  
> decyzja  
> załącznik nr 2

Example:

**Before**

> W przypadku braku podpisu na ww. dokumencie należy dokonać jego ponownego przedłożenia.

**After**

> Jeśli formularz nie jest podpisany, podpisz go i wyślij ponownie.

But again, repeat the exact noun if a pronoun would create ambiguity:

> Do wniosku dołącz umowę i zaświadczenie. **Zaświadczenie** musi być wystawione nie wcześniej niż 30 dni przed złożeniem wniosku.

Not:

> Do wniosku dołącz umowę i zaświadczenie. **Dokument** musi…

Which document? Wonderful little comprehension lottery.

### Headings should answer reader questions

Government guidance explicitly recommends headings because they help users understand where they are and what a section contains. citeturn24view0

Prefer headings such as:

> **Kto może złożyć wniosek**  
> **Co musisz przygotować**  
> **Jak złożyć wniosek**  
> **Ile zapłacisz**  
> **Ile będziesz czekać**  
> **Co zrobić, jeśli urząd odmówi**

over:

> **Informacje ogólne**  
> **Warunki**  
> **Procedura**  
> **Pozostałe informacje**

The latter technically label sections while forcing the reader to investigate what the section is actually useful for.

### Lists need a semantic reason

Use lists for sequences, requirements, options, comparisons, or genuinely parallel elements.

Do not convert every paragraph into bullets merely because “plain language likes bullet points.”

Good:

> Przygotuj:
>
> - dowód osobisty,
> - numer rachunku,
> - potwierdzenie dochodu.

Less useful:

> Ważne informacje:
>
> - decyzja została wydana,
> - decyzja dotyczy Twojego wniosku,
> - urząd wysłał ją wczoraj,
> - możesz ją przeczytać online.

That is just prose wearing a bullet costume.

### Warnings should expose risk and action

Government accessibility guidance explicitly calls for understandable feedback, warnings, error messages, and correction instructions. citeturn24view1

I would give the skill a warning schema:

```text
WARNING LABEL, if appropriate
→ what can go wrong
→ when / under what condition
→ consequence
→ what the reader should do
```

Example:

**Before**

> Należy mieć na uwadze, iż opuszczenie strony przed zapisaniem zmian może skutkować brakiem możliwości zachowania wprowadzonych informacji.

**After**

> **Uwaga: zapisz zmiany przed zamknięciem strony.**  
> Jeśli zamkniesz stronę wcześniej, stracisz wpisane dane.

Much less ceremonial. Significantly more useful.

## Domain behavior for administrative, financial, healthcare, instructional, and service content

Plain-language rules should remain common across domains, but **what must be protected during rewriting changes by domain**.

### Administrative content

Administrative communication should usually lead with the reader's status, required action, deadline, and consequence before institutional background. Polish public-sector plain-language work has explicitly covered official forms, citizen services, Gov.pl and administrative decisions. citeturn25view1

Recommended structure:

```text
WHAT happened / what you can do
WHAT you must do
BY WHEN
WHAT to submit
HOW / WHERE
WHAT happens afterward
WHAT happens if you do nothing
exceptions
legal basis
contact
```

**Source-style version**

> Na podstawie art. X ustawy Y, w związku ze stwierdzeniem braków formalnych w złożonym przez Pana wniosku, wzywa się do ich uzupełnienia poprzez przedłożenie kopii dokumentu Z w terminie 7 dni od dnia doręczenia niniejszego wezwania.

**Plain-language architecture**

> **Doślij kopię dokumentu Z w ciągu 7 dni od otrzymania tego wezwania.**
>
> Dokumentu brakuje w Twoim wniosku.
>
> **Podstawa prawna:** art. X ustawy Y.

Whether `Ty`, `Pan/Pani`, or a more neutral construction is appropriate must depend on the institution's chosen register. The skill should **not automatically convert every formal Polish text into second-person singular**.

### Financial content

Financial plain-language transformations need unusually strict numeric and conditional fidelity.

The skill should preserve exactly:

- amounts;
- percentages;
- currencies;
- fees;
- interest rates;
- calculation bases;
- repayment periods;
- payment dates;
- eligibility criteria;
- exclusions;
- consequences of late payment;
- whether a figure is illustrative or guaranteed.

The Polish Accessibility Act includes retail banking among covered services and requires, among other accessibility requirements, understandability of specified banking methods and communication in Polish or, with consumer consent, another language at CEFR B2 level. citeturn20view1turn21view0

Example:

**Before**

> W przypadku wystąpienia opóźnienia w regulowaniu zobowiązania Bank uprawniony jest do naliczania odsetek za opóźnienie według stopy określonej w Tabeli Opłat i Prowizji.

**Safer plain-language pattern**

> **Jeśli spóźnisz się ze spłatą, bank może naliczyć odsetki za opóźnienie.**
>
> Ich wysokość określa Tabela Opłat i Prowizji.

But if the source provides the actual percentage, the rewrite should show it rather than forcing the reader to hunt for it:

> Odsetki wynoszą **X% rocznie**.

The skill must never “simplify”:

> 7,20% w skali roku

into:

> około 7%

unless the source explicitly authorizes approximation.

### Healthcare content

Healthcare text creates a different danger: oversimplification can erase clinically significant distinctions.

The skill should protect:

- medicine names;
- active ingredients;
- doses;
- units;
- routes of administration;
- frequency;
- duration;
- age or weight thresholds;
- contraindications;
- symptoms requiring urgent action;
- test values;
- timing relative to meals or other medication;
- exceptions and uncertainty;
- instructions to contact a clinician.

The University of Wrocław research inventory includes work adapting Polish anaesthesia informed-consent material to plain-language standards, showing that plain-language methodology is relevant to healthcare rather than being confined to office correspondence. citeturn25view1 ISO 24495-2:2025 likewise states that its legal-communication guidance applies in health-sector contexts where readers must understand rights, obligations, processes, and nuanced concepts. citeturn28view0

A correct healthcare transformation often uses a layered explanation:

> **Hipoglikemia** oznacza zbyt niski poziom cukru we krwi.

rather than deleting the technical term completely.

That allows the reader to recognize the same term later in a leaflet, laboratory system, or conversation with a clinician.

### Instructional content

Instructions should normally be transformed into **observable actions in execution order**.

Poor:

> W celu rozpoczęcia procesu aktywacji należy dokonać wyboru znajdującej się poniżej opcji aktywacyjnej, po czym możliwe będzie przejście do kolejnego etapu procesu.

Better:

> **Aby rozpocząć aktywację:**
>
> 1. Wybierz **Aktywuj**.
> 2. Potwierdź swój adres e-mail.
> 3. Wpisz kod, który Ci wyślemy.

For procedures, chronological order is specifically identified as a useful organizational approach in both Polish government and international plain-language guidance. citeturn25view0turn26view2

The skill should also preserve literal labels:

> wybierz **Ustawienia konta**

not:

> przejdź do ustawień profilu

when the button actually says `Ustawienia konta`.

### Customer-service and interface content

Customer-service writing should optimize for four immediate questions:

```text
What happened?
What does it mean for me?
What can I do now?
What happens next?
```

The Polish government's accessibility guidance explicitly stresses understandable feedback, labels, error messages, and guidance for correcting errors. citeturn24view1

**Bad**

> Wystąpił błąd podczas realizacji operacji. Prosimy spróbować ponownie w późniejszym terminie.

**Better when the system actually knows the problem**

> **Nie udało się zapisać płatności.**
>
> Twoja karta nie została obciążona. Spróbuj ponownie.
>
> Jeśli problem się powtórzy, skontaktuj się z obsługą.

But there is an important anti-hallucination rule:

If the system **does not know** whether the card was charged, the agent must not manufacture reassurance.

Use:

> **Nie udało się potwierdzić płatności.**
>
> Sprawdź historię płatności przed ponowną próbą.

A plain-language model that confidently invents a reassuring explanation is worse than the bureaucratic original.

### Plain-language rewriting cannot by itself guarantee digital accessibility

This boundary should be explicit in the skill documentation.

The government guidance requires not merely visually apparent headings/lists but logical structures interpretable by assistive technologies, along with appropriate labels and other interface semantics. citeturn24view1

Therefore:

```text
polish-plain-language can:
✓ produce better heading text
✓ produce logical Markdown/HTML-friendly structure
✓ improve labels, instructions, warnings and errors
✓ recommend lists/tables

polish-plain-language alone cannot:
✗ guarantee semantic HTML
✗ guarantee keyboard accessibility
✗ guarantee contrast
✗ guarantee ARIA correctness
✗ guarantee WCAG conformance
```

Do not let an agent claim “accessible” merely because it changed *niniejszym informujemy* to *informujemy*. Accessibility has annoyingly refused to be solved by deleting *niniejszy*.

## Plain language versus Easy-to-Read

This deserves a **hard mode boundary**, because Polish government-backed guidance now distinguishes the two very explicitly.

A 2026 Polish publication on *tekst łatwy do czytania i zrozumienia* defines ETR as communication intended for people with low reading/writing ability or limited language proficiency and identifies potential audiences including people with intellectual disabilities, dyslexia and other reading difficulties, dementia, autism, aphasia, attention difficulties, children, older people, and learners of Polish. citeturn22view0

Most importantly, the Polish ETR recommendations directly state that plain language and ETR are different: plain language seeks clarity without such radical simplification, retains the full substantive value of relevant information, and is intended for a broad readership, whereas ETR is designed specifically around people with major comprehension difficulties. citeturn22view1turn23view0

The comparison in the official 2026 recommendations is particularly useful for your skill architecture. It distinguishes the approaches in vocabulary, sentence complexity, amount of information, punctuation, white space, typography, and visual support. citeturn23view1

| Dimension | Plain Polish | Easy-to-Read Polish |
|---|---|---|
| Audience | Broad intended readership | Readers with substantial reading/comprehension barriers |
| Content | Preserve all relevant substantive information | Focus more aggressively on essential information |
| Vocabulary | Familiar vocabulary; explain necessary specialist terms | Very simple vocabulary; stricter terminology control |
| Sentences | Generally short and clear | Much stricter simplification |
| Syntax | Natural, low-complexity Polish | Strong preference for very simple structures |
| Terminology | Can retain necessary legal/technical terms with explanations | Avoid wherever possible; explain when unavoidable |
| Repetition | Consistency preferred | Extremely strong consistency; avoid synonym substitution |
| Typography | Normal accessible document design | More specialized layout and larger visual spacing/font |
| Images | Optional when useful | More commonly used as communication support |
| Validation | Reader/user testing strongly desirable | Target-user consultation is part of the methodology |

The distinction becomes even clearer in the ETR checklist. It includes rules such as using the same terms rather than synonyms, simple sentence construction, straightforward word order, and a **10-word sentence limit** as an ETR-specific checklist criterion. citeturn23view2

That provides a useful warning for your implementation:

> **Never copy the ETR 10-word rule into `polish-plain-language`.**

Doing so would make ordinary public Polish choppy, unnatural, and sometimes less comprehensible.

There is an even more important point for AI systems. The 2026 Polish ETR recommendations define an ETR text as one that follows ETR standards **and has undergone at least one ETR consultation**, and describe consultation with an actual target user as an inseparable part of the process. citeturn22view0

Therefore an autonomous LLM should not honestly claim:

```text
"This is certified / validated ETR."
```

It can produce:

```text
ETR draft
```

or:

```text
draft adapted according to ETR linguistic principles;
target-user consultation still required
```

That should be a separate skill or explicit `mode`, not something silently triggered because the source looks complicated.

My stronger recommendation is separate skills:

```text
polish-plain-language
polish-easy-to-read
```

rather than:

```text
polish-plain-language --simplify-more
```

The methodological difference is too large for the latter design.

## Evaluation and comprehension testing

The other major trap is turning Polish plain language into a scoreboard.

A text with:

```text
average sentence length: 14.7
passive voice: 0
Jasnopis: "easy"
FOG: low
```

is **not automatically understandable**.

Polish government guidance recommends analytical tools such as Jasnopis and Logios, but it also explicitly recommends usability testing: give readers a task, measure whether they find the required information correctly and how long it takes, and test whether they remember key information. citeturn25view0

The 2026 review of readability research by Tomasz Piekot is even more consequential for an agent skill: it reports that the research does not provide conclusive evidence that improving readability-formula results necessarily improves comprehension, and says the ISO plain-language approach recommends user testing instead of relying on formulas as the final criterion. citeturn26view1

So evaluation should have **three layers**.

### Semantic validation

This should be the hard gate.

For every transformation, compare source and output for:

| Check | Failure example |
|---|---|
| Facts preserved | “may” becomes “will” |
| Actor preserved | bank obligation becomes customer obligation |
| Conditions preserved | exception disappears |
| Negation preserved | “nie przysługuje” becomes “przysługuje” |
| Numbers preserved | 30 days becomes 30 working days |
| Units preserved | mg becomes ml |
| Dates preserved | 15 May becomes end of May |
| Amounts preserved | 1,500 zł becomes ~1,500 zł |
| Legal effect preserved | appeal becomes informal complaint |
| Warning severity preserved | “do not use” becomes “avoid” |
| Uncertainty preserved | “może” becomes “na pewno” |
| Scope preserved | “some customers” becomes “customers” |

For an agent, this layer matters more than every readability metric combined.

### Plain-language diagnostics

These should trigger review rather than automatic failure.

Suggested signals:

```text
- mean sentence length
- longest sentence
- clause depth
- parenthetical depth
- nominalization density
- passive / impersonal density
- undefined abbreviations
- specialist terms without explanation
- long noun/genitive chains
- ambiguous pronouns
- multiple actions inside one instruction
- action appearing late in a paragraph
- legal basis appearing before reader-relevant outcome
- inconsistent terminology
- unexplained condition / exception
- non-descriptive headings
- warning without corrective action
```

For example:

```text
Sentence length:
15–20 words average → desirable tendency, not hard requirement

Sentence >25–30 words:
flag for inspection

Sentence >40 words:
strong inspection signal

Result:
never split solely because threshold was exceeded
```

The exact numeric cutoffs above should be treated as an implementation heuristic, not a scientific definition of understandable Polish; official Polish guidance itself gives 15–20 words as practical advice, while contemporary readability research cautions against mechanical use of such metrics. citeturn24view0turn26view1

### Behavioral comprehension checks

This is where the evaluation should ultimately land.

For common functional messages, generate questions such as:

```text
Can the reader identify:
- why they received this message?
- what has happened?
- whether they need to act?
- exactly what they need to do?
- by when?
- where / how?
- what documents or information they need?
- how much it costs?
- what happens if they do nothing?
- what important exceptions apply?
- where to get help?
```

Then evaluate whether the answers are **explicitly and quickly recoverable from the output**.

For a payment notification:

```text
Q: Was the payment successful?
Q: Was the customer charged?
Q: Does the customer need to retry?
Q: What should they do if they see a charge?
```

For a medical instruction:

```text
Q: What should the patient take?
Q: How much?
Q: When?
Q: For how long?
Q: Under what condition should they stop / seek help?
```

For an administrative notice:

```text
Q: What does the office need?
Q: What is the deadline?
Q: How is the deadline calculated?
Q: Where should the reader send the document?
Q: What happens if they do not send it?
Q: Can they challenge the decision?
```

This approach operationalizes the Polish government's own recommendation to test whether readers can locate and correctly use information. citeturn25view0

A useful final rubric would be:

| Dimension | Pass criterion |
|---|---|
| **Fidelity** | No material meaning changed |
| **Task visibility** | Main reader task is immediately identifiable |
| **Findability** | Critical facts are easy to locate |
| **Comprehension** | Necessary concepts are stated or explained clearly |
| **Actionability** | Reader knows what to do, how and when |
| **Condition clarity** | If/then relations and exceptions are explicit |
| **Terminology** | One concept uses stable wording |
| **Navigation** | Headings/lists reflect information structure |
| **Warnings** | Risk, consequence and corrective action are clear |
| **Register** | Respectful and appropriate to context |
| **Natural Polish** | No avoidable bureaucratic constructions or awkward calques |
| **Metric sanity** | Readability statistics are used diagnostically, not as proof |

## Recommended implementation blueprint for the skill

The research supports a substantially more precise specification than “rewrite in simple Polish.”

I would make the skill reason through the following internal sequence.

### Analyze before rewriting

```text
1. Identify domain:
   administrative | instructional | financial |
   healthcare | customer_service | other

2. Identify intended reader:
   expertise
   relationship to sender
   likely context
   relevant accessibility needs if explicitly supplied

3. Identify communication purpose:
   inform | request action | instruct | warn |
   explain decision | collect information |
   resolve problem | obtain consent

4. Extract semantic units:
   status
   action
   prerequisite
   condition
   deadline
   consequence
   exception
   amount
   definition
   warning
   contact
   legal/technical basis

5. Mark protected information.

6. Detect ambiguity or missing dependencies.

7. Rebuild information architecture.

8. Rewrite at sentence/word level.

9. Validate source ↔ output semantics.

10. Run plain-language diagnostics.

11. Check reader-task questions.
```

This sequence reflects the reader-first and evaluation-oriented model found in Polish government guidance and in the broader plain-language standard. citeturn25view0turn26view2

### Protected-information model

For high-stakes content I would explicitly mark tokens/spans before rewriting:

```text
PROTECT:
- names
- organizations
- product names
- legal act names
- article/paragraph references
- medical terminology where clinically relevant
- medicine names
- numbers
- dates
- time periods
- monetary amounts
- currencies
- percentages
- units
- URLs / identifiers
- UI labels
- quoted contract language when required
```

Then allow the skill to **explain around those elements** rather than casually paraphrasing them.

Example:

```text
SOURCE:
Odwołanie wnosi się w terminie 14 dni od dnia doręczenia decyzji.

BAD:
Masz około dwóch tygodni, żeby poprosić o zmianę decyzji.

GOOD:
Masz 14 dni od dnia doręczenia decyzji, aby złożyć odwołanie.
```

The second rewrite preserves:

```text
14 days ≠ approximately two weeks
od doręczenia ≠ from date of issue
odwołanie ≠ generic request
```

That is precisely the sort of semantic discipline an agent needs in legal and administrative communication, where plain-language simplification still has to preserve rights and obligations. citeturn28view0

### Register should be a controlled variable

Do not encode:

```text
Plain Polish = always use "Ty"
```

Instead:

```yaml
register:
  preserve_source: default
  options:
    - ty
    - pan_pani
    - plural_you
    - neutral
    - institutional_formal
```

Then simplify inside that register.

Compare:

**Direct consumer service**

> Sprawdź dane i wybierz **Wyślij**.

**Formal correspondence**

> Prosimy sprawdzić dane i przesłać formularz.

**Neutral instruction**

> Sprawdź dane przed wysłaniem formularza.

All can be plain Polish. Plainness and interpersonal register are related but not identical.

### The skill should detect “institution-first” openings

Common target pattern:

> Informujemy, że…  
> Uprzejmie informujemy, iż…  
> Niniejszym zawiadamiamy…  
> W odpowiedzi na…  
> W związku z…  
> Mając na uwadze…  
> Na podstawie…

These openings are not automatically incorrect. But the agent should ask:

> **Does the reader need this before the actual result or action?**

Example:

**Before**

> Uprzejmie informujemy, że w wyniku przeprowadzonej weryfikacji Państwa zgłoszenia stwierdzono jego prawidłowość.

**After**

> **Twoje zgłoszenie jest prawidłowe. Nie musisz nic robić.**

That second sentence — *Nie musisz nic robić* — is particularly valuable because it answers the reader's latent task.

### It should detect fake simplification

Several transformations should explicitly fail review.

**Shorter but less precise**

> Wniosek należy złożyć nie później niż w terminie 30 dni od dnia powstania obowiązku.

becoming:

> Złóż wniosek w ciągu miesiąca.

Fail: `30 dni` is not necessarily `miesiąc`.

**Friendlier but legally altered**

> Organ może odmówić…

becoming:

> Organ odmówi…

Fail: possibility became certainty.

**More “natural” but inconsistent**

> reklamacja

becoming alternately:

> reklamacja / zgłoszenie / skarga / prośba

Fail: terminology drift.

**Short sentences but broken logic**

> Jeśli masz mniej niż 18 lat i składasz wniosek samodzielnie, potrzebujesz zgody opiekuna.

becoming:

> Masz mniej niż 18 lat.  
> Składasz wniosek samodzielnie.  
> Potrzebujesz zgody opiekuna.

Fail: the conjunction between the two conditions has effectively disappeared.

**Simplified warning**

> Nie stosować w przypadku ciężkiej reakcji alergicznej na substancję X.

becoming:

> Lepiej nie stosować, jeśli masz alergię.

Fail spectacularly.

### Recommended final skill doctrine

The final core instructions can eventually be condensed to something close to this:

```text
Write for the reader's task, not for the institution's process.

Preserve meaning before simplifying form.

Put the outcome, required action, deadline, condition,
or warning where the reader will find it first.

Prefer explicit actors and verbs when the actor matters.

Prefer familiar Polish words, but retain necessary legal,
medical, financial, technical, and interface terminology.
Explain such terms instead of replacing them inaccurately.

Expand unfamiliar abbreviations on first use.

Use one stable term for one concept.
Do not introduce synonyms merely to avoid repetition.

Use short, structurally simple sentences where this improves
understanding, but never enforce a mechanical word limit.

Keep conditions, exceptions, causes, and consequences visibly connected.

Use headings that tell readers what information they will find.
Use lists for genuine sequences, requirements, options, and comparisons.

Write instructions as actions in execution order.
State prerequisites before the step they control.

Write warnings so readers can identify the risk,
the triggering condition, the consequence, and the safe action.

For errors, tell readers what happened and how to recover
whenever that information is actually known.

Do not invent reassurance, explanations, causes, deadlines,
eligibility, consequences, or procedural rights.

Preserve exact numbers, amounts, dates, units, percentages,
thresholds, deadlines, conditions, exceptions, legal effects,
medical instructions, and warning strength.

Treat readability scores and sentence lengths as diagnostics.
Judge success primarily by semantic fidelity and whether
the intended reader can find, understand, and use the information.

Plain language is not Easy-to-Read.
Do not apply ETR-specific restrictions unless ETR is explicitly requested.
Do not claim that an AI-only ETR draft has been user-validated.
```

That contract is much closer to how Polish plain language is actually treated by public-sector guidance, Polish plain-language research, accessibility guidance, and contemporary international standards: **a communication system centered on reader success rather than an exercise in replacing long words with short ones.** citeturn24view0turn24view1turn25view1turn26view2

The most important architectural decision is therefore to keep `polish-plain-language` narrowly disciplined. Let `polish-perfect-writing` worry about whether a passage sounds elegantly native and non-AI. Let this skill worry about whether a person receiving a tax letter, bank message, medical instruction, failed-payment notice, government form, or setup procedure can look at it and reliably answer:

> **Co się stało? Co to oznacza dla mnie? Co mam zrobić? Do kiedy? Jak? Co będzie potem?**

If the rewritten Polish cannot answer those questions substantially better than the source without changing the source's meaning, the skill has not succeeded.
