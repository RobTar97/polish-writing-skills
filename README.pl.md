<div align="center">
  <img src="assets/readme-hero.png" alt="Abstrakcyjne karminowe i grafitowe formy na kremowej siatce redakcyjnej" width="100%" />
  <h1>Polish Writing Skills</h1>
  <p><strong>Naturalna polszczyzna dopasowana do gatunku i sytuacji — bez zmiany sensu.</strong></p>
  <p>Otwarty Agent Skill do redagowania i tłumaczenia tekstów na naturalny język polski z rygorystycznym zachowaniem faktów.</p>
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

## Jeden skill, jedna zasada redakcyjna

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

> W przypadku strukturyzowanych zasobów UI lub korespondencji wymagającej szczególnego wyczucia relacji skill wykonuje bezpieczną korektę językową i wskazuje zakres, który wymaga specjalistycznej lokalizacji albo redakcji biznesowej.

## Zgodność z agentami

Tak — `natural-polish-writing` jest podstawowym, przenośnym Agent Skill. Jego rdzeń stanowi standardowy plik `SKILL.md` z referencjami w Markdownie; skill nie zależy od hooków, narzędzi konkretnego modelu ani zastrzeżonego środowiska uruchomieniowego. Oficjalna [tabela zgodności skills CLI](https://github.com/vercel-labs/skills#compatibility) potwierdza obsługę podstawowych skilli przez najpopularniejszych agentów programistycznych.

| Agent | Identyfikator CLI | Obsługa podstawowego skilla |
| --- | --- | --- |
| OpenAI Codex | `codex` | Tak |
| Claude Code | `claude-code` | Tak |
| OpenCode | `opencode` | Tak |
| Antigravity | `antigravity` | Tak |
| Cursor | `cursor` | Tak |
| Gemini CLI | `gemini-cli` | Tak |
| GitHub Copilot | `github-copilot` | Tak |
| Windsurf | `windsurf` | Tak |

Obecna tabela obejmuje również OpenHands, Cline, Roo Code, Amp, OpenClaw, Pi, Qoder, Zed i wielu innych agentów korzystających ze wspólnego formatu skilli.

Plik `agents/openai.yaml` zawiera opcjonalne metadane dla produktów OpenAI. Pozostali agenci mogą go bezpiecznie pominąć i korzystać ze wspólnych instrukcji w `SKILL.md`.

Instalacja dla kilku agentów jednocześnie:

```bash
npx skills@latest add RobTar97/polish-writing-skills \
  --skill natural-polish-writing \
  -a codex -a claude-code -a opencode -a antigravity
```

Pomiń `-a`, aby CLI interaktywnie wykryło zainstalowanych agentów.

## Szybka instalacja

Zainstaluj skill z repozytorium za pomocą oficjalnego narzędzia [skills CLI](https://skills.sh/docs/cli) (zalecane):

```bash
npx skills@latest add RobTar97/polish-writing-skills
```

Zainstaluj bezpośrednio konkretny skill:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Zainstaluj globalnie dla Codexa bez dodatkowych pytań:

```bash
npx skills@latest add RobTar97/polish-writing-skills --skill natural-polish-writing -g -a codex -y
```

Sprawdź, co CLI wykrywa w repozytorium, zanim coś zainstalujesz:

```bash
npx skills@latest add RobTar97/polish-writing-skills --list
```

Jeśli wolisz stałe polecenie, zainstaluj to samo otwarte CLI przez npm:

```bash
npm install -g skills
skills add RobTar97/polish-writing-skills --skill natural-polish-writing
```

Uruchom skill jednorazowo bez instalacji:

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
      <p>Plan Pro umożliwia 12 osobom wspólne planowanie zadań. Okres próbny trwa 14 dni, a po jego zakończeniu abonament kosztuje 29 zł miesięcznie. Do korzystania z Plan Pro potrzebne jest połączenie z internetem.</p>
    </td>
  </tr>
</table>

**Zachowano:** nazwę produktu, limit 12 osób, 14-dniowy okres próbny, cenę 29 zł miesięcznie oraz wymóg połączenia z internetem.

**Zmieniono:** ogólnikowe wprowadzenie, niepopartą konkretami ocenę marketingową, powtarzalne łączniki i pustą ramę ostrzegawczą. Nie dodano żadnej funkcji, dowodu, presji ani obietnicy.

To przejrzysty przykład redakcyjny, a nie wynik automatycznego benchmarku. Kontrola odpowiada [priorytetom redakcyjnym](skills/natural-polish-writing/references/editing-priorities.md) i [liście kontrolnej](skills/natural-polish-writing/references/review-checklist.md) skilla.

## Więcej zweryfikowanych przykładów

### Publiczna próbka tekstu maszynowego

[Zbiór ŚMIGIEL](https://huggingface.co/datasets/strebeyko/smigiel) to udostępniony na licencji CC BY 4.0 korpus do badań nad polskimi tekstami generowanymi maszynowo, wykorzystany w [zadaniu PolEval 2025](https://poleval.pl/tasks/task1). Poniższy krótki fragment ma w nim etykietę tekstu maszynowego (`model: bielik-md`, `strategy: dbs`):

> „Ponadto, artykuł powinien być aktualny i uwzględniać najnowsze dane oraz interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom najbardziej aktualne i kompletne informacje.”

**Po redakcji przez `natural-polish-writing`:**

> Artykuł powinien uwzględniać najnowsze dane i interpretacje wydarzeń z turnieju, aby zapewnić czytelnikom kompletne informacje.

Redakcja usuwa nieuzasadniony przecinek i puste *ponadto*, ogranicza trzy nakładające się określenia aktualności do jednego oraz skraca zdanie z 22 do 15 wyrazów. Zachowuje polecenie uwzględnienia najnowszych danych, interpretacji i kompletnych informacji; nie dodaje faktów.

### Komunikat instytucjonalny

#### Tekst źródłowy komunikatu

> Uprzejmie informujemy, iż w związku z koniecznością przeprowadzenia prac modernizacyjnych nastąpi czasowe wstrzymanie funkcjonowania systemu w godzinach od 22:00 do 23:00.

#### Komunikat po redakcji

> System będzie niedostępny od 22:00 do 23:00 z powodu prac modernizacyjnych.

Najpierw pojawia się informacja ważna dla odbiorcy. Przedział godzinowy i przyczyna pozostają bez zmian; tekst nie dodaje daty, przeprosin ani obietnicy.

### Powściągliwość akademicka

#### Tekst źródłowy fragmentu akademickiego

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, ale mogą wskazywać na wzrost prawdopodobieństwa o 15%.

#### Fragment akademicki po redakcji

> W badaniu zastosowano regresję logistyczną. Wyniki nie pozwalają stwierdzić związku przyczynowego, mogą jednak wskazywać na wzrost prawdopodobieństwa o 15%.

Poprawna strona bierna pozostaje bez zmian. Redakcja zachowuje negację, ostrożną modalność, wartość 15% oraz różnicę między możliwym wskazaniem statystycznym a związkiem przyczynowym.

### Punkty oceny

Każdy wymiar otrzymuje od 0 do 2 punktów: zgodność semantyczna i faktyczna, poprawność gramatyczna, dopasowanie gatunku i rejestru, naturalność i przepływ informacji oraz powściągliwość redakcyjna bez dopowiadania treści.

| Przypadek | Wierność | Gramatyka | Gatunek | Naturalność | Powściągliwość | Wynik |
| --- | ---: | ---: | ---: | ---: | ---: | ---: |
| Opis funkcji Plan Pro | 2 | 2 | 2 | 2 | 2 | **10/10** |
| Fragment ŚMIGIEL | 2 | 2 | 1 | 2 | 2 | **9/10** |
| Komunikat instytucjonalny | 2 | 2 | 2 | 2 | 2 | **10/10** |
| Fragment akademicki | 2 | 2 | 2 | 2 | 2 | **10/10** |

Fragment korpusowy otrzymuje jeden punkt za dopasowanie gatunku, ponieważ publiczna próbka nie zawiera pełnego kontekstu dokumentu. To przejrzyste, ręczne kontrole redakcyjne, a nie wyniki badania z udziałem polskich czytelników, oceny detektorów ani deklaracje skuteczności benchmarkowej.

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
- **Najpierw gatunek, później ogólna poprawność stylu.** Tekst akademicki, reklama, post, komunikat i tłumaczenie wymagają różnych decyzji.
- **Najmniejsza wystarczająca zmiana.** Skill poprawia miejsca, które tego potrzebują, zamiast zastępować rozpoznawalny głos anonimowym „dobrym stylem”.
- **Bez udawania człowieka.** Nie dodaje anegdot, opinii, slangu, literówek, dowodów ani fikcyjnych doświadczeń.
- **Aktualne zasady, dane użyte w kontekście.** Pisownia i interpunkcja opierają się na zasadach RJP obowiązujących od 2026 roku; NKJP i WSJP wspierają opisowe decyzje dotyczące użycia i łączliwości.
- **Bez obietnic dotyczących detektorów.** „Brzmienie jak AI” jest sygnałem jakości redakcyjnej, a nie dowodem autorstwa ani celem obchodzenia detekcji.

## Sposób zwracania wyników

Gotowy tekst jest po polsku. Uwagi są formułowane w języku polecenia i pojawiają się tylko wtedy, gdy znaczenie ma przyjęte założenie, nierozstrzygnięta wieloznaczność, ostrzeżenie dotyczące zachowania treści albo granica zakresu.

| Język polecenia | Gotowy tekst | Uwagi |
| --- | --- | --- |
| Polski | Polski | Polski |
| Angielski lub inny | Najpierw gotowy tekst po polsku | Potem zwięzłe uwagi w języku polecenia |

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

Publiczna część pakietu obejmuje wyłącznie instalowalny skill, potrzebne mu materiały referencyjne oraz zasoby prezentacyjne repozytorium. Raporty badawcze i materiały robocze pozostają poza pakietem.

## Licencja

Treści utworzone w tym repozytorium są dostępne na warunkach [licencji MIT](LICENSE). Materiały referencyjne odsyłają w razie potrzeby do źródeł urzędowych i specjalistycznych; treści osób trzecich nie są tu przedrukowywane ani ponownie licencjonowane.

<div align="center">
  <sub>Skill dla polszczyzny, która szanuje zdanie, autora i prawdę.</sub>
</div>
