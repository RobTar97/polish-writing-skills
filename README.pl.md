<div align="center">
  <img src="assets/readme-hero.png" alt="Abstrakcyjne karminowe i grafitowe formy na kremowej siatce redakcyjnej" width="100%" />
  <h1>Polish Writing Skills</h1>
  <p><strong>Naturalna polszczyzna dopasowana do gatunku i sytuacji — bez zmiany sensu.</strong></p>
  <p>Otwarty skill dla agentów AI, który redaguje i tłumaczy teksty na współczesną polszczyznę, ściśle zachowując fakty.</p>
  <p>
    <a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent_Skills-compatible-292827?style=flat-square" alt="Zgodność z Agent Skills" /></a>
    <img src="https://img.shields.io/badge/skills-1-b62234?style=flat-square" alt="Jeden skill" />
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-5b5753?style=flat-square" alt="Licencja MIT" /></a>
  </p>
  <p>
    <a href="#szybka-instalacja"><img src="https://img.shields.io/badge/Zainstaluj_przez_skills.sh-b62234?style=for-the-badge" alt="Zainstaluj przez skills.sh" /></a>
    <a href="README.md"><img src="https://img.shields.io/badge/Read_in_English-f6f0e6?style=for-the-badge&amp;labelColor=292827" alt="Read in English" /></a>
  </p>
</div>

---

## Jeden skill, jedna umowa redakcyjna

Skill poprawia polszczyznę, ale nie zmienia po cichu tego, co mówi tekst.

<table>
  <tr>
    <td width="100%" valign="top">
      <img src="assets/natural-writing.svg" alt="Ilustracja Natural Polish Writing" width="100%" />
      <h3><a href="skills/natural-polish-writing/SKILL.md">natural-polish-writing</a></h3>
      <p>Naturalna, współczesna polszczyzna dla tekstów poza interfejsem użytkownika.</p>
      <p><strong>Najlepszy wybór do:</strong> artykułów, treści internetowych i marketingowych, wiadomości, ogłoszeń, postów społecznościowych, tekstów akademickich oraz tłumaczeń na język polski.</p>
    </td>
  </tr>
</table>

> W przypadku strukturyzowanych zasobów interfejsu lub korespondencji wymagającej szczególnego wyczucia relacji skill ogranicza się do bezpiecznej korekty językowej. Wskazuje też elementy, które wymagają specjalistycznej lokalizacji albo redakcji biznesowej.

## Zgodność z agentami

Tak. `natural-polish-writing` to przenośny skill zgodny z podstawowym formatem Agent Skills. Jego rdzeniem jest standardowy plik `SKILL.md` oraz materiały referencyjne w Markdownie. Nie wymaga hooków, narzędzi właściwych dla konkretnego modelu ani zamkniętego środowiska uruchomieniowego. Oficjalna [tabela zgodności skills CLI](https://github.com/vercel-labs/skills#compatibility) potwierdza obsługę tego formatu przez najpopularniejszych agentów programistycznych.

| Agent | Identyfikator CLI | Obsługa skilla |
| --- | --- | --- |
| OpenAI Codex | `codex` | Tak |
| Claude Code | `claude-code` | Tak |
| OpenCode | `opencode` | Tak |
| Antigravity | `antigravity` | Tak |
| Cursor | `cursor` | Tak |
| Gemini CLI | `gemini-cli` | Tak |
| GitHub Copilot | `github-copilot` | Tak |
| Windsurf | `windsurf` | Tak |

Lista obejmuje również OpenHands, Cline, Roo Code, Amp, OpenClaw, Pi, Qoder, Zed i wielu innych agentów obsługujących ten sam format.

Plik `agents/openai.yaml` zawiera opcjonalne metadane dla produktów OpenAI. Inni agenci mogą go pominąć i korzystać ze wspólnych instrukcji zapisanych w `SKILL.md`.

Instalacja dla kilku agentów jednocześnie:

```bash
npx skills@latest add RobTar97/polish-writing-skills \
  --skill natural-polish-writing \
  -a codex -a claude-code -a opencode -a antigravity
```

Pomiń opcję `-a`, aby CLI wykryło zainstalowanych agentów i pozwoliło wybrać ich interaktywnie.

## Szybka instalacja

Zainstaluj skill z repozytorium za pomocą oficjalnego narzędzia [skills CLI](https://skills.sh/docs/cli):

```bash
npx skills@latest add RobTar97/polish-writing-skills
```

Zainstaluj tylko `natural-polish-writing`:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Zainstaluj go globalnie dla Codexa, bez dodatkowych pytań:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing -g -a codex -y
```

Sprawdź przed instalacją, jakie skille CLI wykrywa w repozytorium:

```bash
npx skills@latest add RobTar97/polish-writing-skills --list
```

Jeśli chcesz korzystać z polecenia bez `npx`, zainstaluj to samo otwarte narzędzie przez npm:

```bash
npm install -g skills
skills add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Użyj skilla jednorazowo, bez instalowania go:

```bash
npx skills@latest use RobTar97/polish-writing-skills@natural-polish-writing
```

## Zobacz, jak działa

Ten przykład pokazuje, co się zmienia, co pozostaje bez zmian i czego skill nie dopowiada.

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>Przed</h3>
      <p>W dzisiejszych czasach warto zauważyć, że Plan Pro stanowi kompleksowe rozwiązanie, które pozwala 12 osobom wspólnie planować zadania. Ponadto okres próbny trwa 14 dni, a abonament kosztuje 29 zł miesięcznie. Należy jednak pamiętać, że Plan Pro nie działa bez połączenia z internetem.</p>
    </td>
    <td width="50%" valign="top">
      <h3>Po</h3>
      <p>Plan Pro umożliwia 12 osobom wspólne planowanie zadań. Okres próbny trwa 14 dni, a po jego zakończeniu abonament kosztuje 29 zł miesięcznie. Do korzystania z planu Pro potrzebne jest połączenie z internetem.</p>
    </td>
  </tr>
</table>

**Zachowano:** nazwę produktu, limit 12 osób, 14-dniowy okres próbny, cenę 29 zł miesięcznie oraz wymóg połączenia z internetem.

**Zmieniono:** usunięto ogólnikowe wprowadzenie, niepopartą konkretami ocenę marketingową, powtarzalne łączniki i pustą formułę ostrzegawczą. Nie dodano żadnej funkcji, dowodu, presji ani obietnicy.

To przejrzysty przykład redakcyjny, a nie wynik automatycznego benchmarku. Kontrola odpowiada [priorytetom redakcyjnym](skills/natural-polish-writing/references/editing-priorities.md) i [liście kontrolnej](skills/natural-polish-writing/references/review-checklist.md) skilla.

## Więcej zweryfikowanych przykładów

### Publiczna próbka tekstu maszynowego

[Zbiór ŚMIGIEL](https://huggingface.co/datasets/strebeyko/smigiel) to udostępniony na licencji CC BY 4.0 korpus do badań nad polskimi tekstami generowanymi maszynowo. Wykorzystano go w [zadaniu PolEval 2025](https://poleval.pl/tasks/task1). Poniższy krótki fragment oznaczono w zbiorze jako tekst maszynowy (`model: bielik-md`, `strategy: dbs`):

> „Ponadto, artykuł powinien być aktualny i uwzględniać najnowsze dane oraz interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom najbardziej aktualne i kompletne informacje.”

**Po redakcji przez `natural-polish-writing`:**

> Artykuł powinien uwzględniać najnowsze dane i interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom kompletne informacje.

Redakcja usuwa nieuzasadniony przecinek i zbędne *ponadto*, pozostawia tylko jedno z trzech nakładających się określeń aktualności oraz skraca zdanie z 22 do 15 wyrazów. Zachowuje wymóg uwzględnienia najnowszych danych, interpretacji i kompletnych informacji. Nie dodaje żadnych faktów.

### Komunikat instytucjonalny

#### Komunikat przed redakcją

> Uprzejmie informujemy, iż w związku z koniecznością przeprowadzenia prac modernizacyjnych nastąpi czasowe wstrzymanie funkcjonowania systemu w godzinach od 22:00 do 23:00.

#### Komunikat po redakcji

> System będzie niedostępny od 22:00 do 23:00 z powodu prac modernizacyjnych.

Najważniejsza dla odbiorcy informacja pojawia się na początku. Przedział godzinowy i przyczyna pozostają bez zmian. Tekst nie dodaje daty, przeprosin ani obietnicy.

### Powściągliwość akademicka

#### Fragment przed redakcją

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, ale mogą wskazywać na wzrost prawdopodobieństwa o 15%.

#### Fragment po redakcji

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, mogą jednak wskazywać na wzrost prawdopodobieństwa o 15%.

Poprawna konstrukcja bezosobowa pozostaje bez zmian. Redakcja zachowuje negację, ostrożną modalność, wartość 15% oraz rozróżnienie między możliwym wzrostem prawdopodobieństwa a związkiem przyczynowym.

### Punkty oceny

Każdy z pięciu wymiarów oceniamy w skali od 0 do 2 punktów: wierność znaczeniu i faktom, poprawność gramatyczną, dopasowanie do gatunku i rejestru, naturalność i przepływ informacji oraz powściągliwość redakcyjną — bez dopowiadania treści.

| Przypadek | Wierność | Gramatyka | Gatunek | Naturalność | Powściągliwość | Razem |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Opis funkcji Plan Pro | 2 | 2 | 2 | 2 | 2 | **10/10** |
| Fragment ŚMIGIEL | 2 | 2 | 1 | 2 | 2 | **9/10** |
| Komunikat instytucjonalny | 2 | 2 | 2 | 2 | 2 | **10/10** |
| Fragment akademicki | 2 | 2 | 2 | 2 | 2 | **10/10** |

Fragment korpusowy otrzymuje jeden punkt za dopasowanie do gatunku, ponieważ publiczna próbka nie zawiera pełnego kontekstu dokumentu. Są to jawne oceny redakcyjne wykonane ręcznie, a nie wyniki badania z udziałem polskich czytelników, wskazania detektorów czy deklaracje skuteczności w benchmarkach.

## Wypróbuj

```text
Użyj $natural-polish-writing, aby ten komunikat brzmiał naturalnie i zwięźle po polsku.
Zachowaj wszystkie fakty, liczby, warunki i zastrzeżenia.
```

```text
Użyj $natural-polish-writing, aby przetłumaczyć ten artykuł na współczesny język polski.
Zachowaj terminologię, cytaty, stopień pewności i głos autora.
```

```text
Użyj $natural-polish-writing, aby zredagować ten fragment po polsku.
Zachowaj wszystkie fakty i nie wygładzaj celowo nieformalnego tonu.
```

## Jak podejmuje decyzje

- **Najpierw sens, później płynność.** Fakty, warunki, stopień pewności, chronologia, liczby, nazwy, atrybucja, cytaty, zobowiązania i konsekwencje pozostają bez zmian.
- **Najpierw gatunek, później ogólne reguły stylu.** Tekst akademicki, reklama, post, komunikat i tłumaczenie wymagają różnych decyzji.
- **Najmniejsza wystarczająca zmiana.** Skill poprawia miejsca, które tego potrzebują, zamiast zastępować rozpoznawalny głos anonimowym „dobrym stylem”.
- **Bez udawania człowieka.** Nie dodaje anegdot, opinii, slangu, literówek, dowodów ani fikcyjnych doświadczeń.
- **Aktualne zasady i dane odczytywane w kontekście.** Pisownia i interpunkcja opierają się na zasadach RJP obowiązujących od 2026 roku; NKJP i WSJP wspierają decyzje dotyczące użycia języka i łączliwości wyrazów.
- **Bez obietnic dotyczących detektorów.** „Brzmienie jak AI” jest sygnałem jakości redakcyjnej, a nie dowodem autorstwa ani celem obchodzenia detekcji.

## Sposób zwracania wyników

Gotowy tekst jest zawsze po polsku. Ewentualne uwagi są formułowane w języku polecenia i pojawiają się tylko wtedy, gdy trzeba wskazać istotne założenie, nierozstrzygniętą wieloznaczność, ryzyko zmiany sensu albo granicę zakresu.

| Język polecenia | Gotowy tekst | Uwagi |
| --- | --- | --- |
| Polski | Polski | Polski |
| Angielski lub inny | Najpierw tekst po polsku | Następnie zwięzłe uwagi w języku polecenia |

## Źródła i hierarchia autorytetu

Skill odróżnia normy językowe od preferencji redakcyjnych:

- [Rada Języka Polskiego](https://rjp.pan.pl/zasady-pisowni-i-interpunkcji-polskiej-2/) — aktualna pisownia i interpunkcja.
- [Narodowy Korpus Języka Polskiego](https://nkjp.pl/) — opisowe dane korpusowe.
- [Wielki słownik języka polskiego PAN](https://wsjp.pl/) — znaczenia, gramatyka, kwalifikatory stylistyczne i typowe połączenia.
- [Zasady prostego języka na Gov.pl](https://www.gov.pl/web/cyfryzacja/prosty-jezyk) — wskazówki dla tekstów publicznych i instruktażowych, a nie uniwersalny wzorzec stylu.

## Struktura repozytorium

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

Publiczna część pakietu obejmuje wyłącznie instalowalny skill, jego materiały referencyjne oraz zasoby prezentacyjne repozytorium. Raporty badawcze i materiały robocze nie wchodzą w skład pakietu.

## Licencja

Treści opracowane w tym repozytorium są dostępne na warunkach [licencji MIT](LICENSE). Materiały referencyjne odsyłają w razie potrzeby do źródeł urzędowych i specjalistycznych. Treści osób trzecich nie są tu przedrukowywane ani obejmowane nową licencją.

<div align="center">
  <sub>Dla polszczyzny, która szanuje sens, głos autora i fakty.</sub>
</div>
