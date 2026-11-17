# 5. Projekt konfiguracji zasilania szpitala

> **Rozdział w opracowaniu.** Materiał źródłowy jest kompletny: modele `.homer`
> serii V2, opis komponentów oraz szeregi czasowe zdarzeń awaryjnych. Poniżej
> przedstawiono ustalenia, do których odwołują się rozdziały 4 i 7. Do zredagowania
> pozostaje opis przebiegu prac modelowych oraz uzasadnienie doboru komponentów.

## 5.1. Terminologia i siatka analizy

W pracy stosuje się dwa niezależne wymiary opisu, których nie wolno utożsamiać:

| Wymiar | Oznaczenia | Znaczenie |
|---|---|---|
| **Konfiguracja** | K1, K2, K3 | architektura systemu — jakie źródła są zainstalowane |
| **Wariant stanu sieci** | A0, A1, A2 | stan sieci nadrzędnej przyjęty w symulacji |

| Konfiguracja | Architektura |
|---|---|
| **K1 — Baza** | sieć + agregat prądotwórczy |
| **K2 — Hybryda** | sieć + agregat + PV + BESS |
| **K3 — Mikrosieć** | sieć + PV + BESS + CHP gazowy + kocioł |

| Wariant stanu sieci | Zdarzenie | Dopuszczalny niedobór mocy |
|---|---|---|
| **A0** | praca normalna | 0% |
| **A1** | awaria 72 h, 15–17 stycznia | 10% |
| **A2** | pięć przerw, łącznie 21 h | 10% |

Podniesienie dopuszczalnego niedoboru mocy do 10% w wariantach awaryjnych jest
konieczne: przy wartości zerowej optymalizator odrzuca wszystkie konfiguracje jako
niedopuszczalne i nie zwraca wyników, co uniemożliwia pomiar skali niedoboru.
Wielkość ta jest parametrem wejściowym modelu, określającym **górną granicę**
dopuszczalnego niedoboru, i **nie jest tożsama z energią niedostarczoną** — tę
optymalizator podaje w wynikach osobno. W przeprowadzonych symulacjach energia
niedostarczona wyniosła zero we wszystkich konfiguracjach (podrozdział 7.1.2),
a zatem przyjęty limit nie został wykorzystany.

### 5.1.1. Konfiguracje pomocnicze

Jeden przebieg optymalizacyjny zwraca wszystkie kombinacje obecnych komponentów.
Poza K1–K3 w zestawieniach rozdziału 7 występują zatem układy pomocnicze, służące
wyłącznie ocenie wkładu poszczególnych elementów. Nie są one konfiguracjami
w rozumieniu pracy i każdorazowo wymagają pełnej nazwy: *sama sieć* (odniesienie),
*sama PV 124 kWp*, *sama CHP 100 kW*, *CHP bez magazynu*, *PV z agregatem*.

Odrębne znaczenie ma **stan faktycznie istniejący** — dwa agregaty zainstalowane
w obiekcie — omówiony w podrozdziale 7.2.6 oraz w załączniku A. Nie jest on
konfiguracją modelową i nie występuje w wynikach optymalizacji.

## 5.2. Parametry komponentów przyjęte do modelu

| Komponent | Model / parametry | Przestrzeń poszukiwań |
|---|---|---|
| PV | Generic flat plate, 800 $/kW, derating 80% | {0; 50; 75; 100; 110; 115; 124} kWp |
| BESS | Generic 100 kWh Li-Ion, 30 000 $/szt., SoC min. 40% | {0; 1} × 100 kWh |
| Agregat | `Autosize Genset`, paliwo 1,55 $/l | dobór automatyczny |
| CHP | 2G Aura 404, 100 kW, odzysk 57,2%, min. obciążenie 50% | opcjonalny |
| Kocioł | Generic Boiler, sprawność 85%, gaz 0,65 $/m³ | zawsze obecny |
| Przekształtnik | dobór automatyczny | — |
| Sieć | taryfa B22 | zawsze obecna |

Minimalny stan naładowania magazynu (40%) przyjęto jako `[ŹRÓDŁO]` wartość typową
dla ogniw litowo-jonowych eksploatowanych w trybie rezerwowym, ograniczającą degradację
pojemności. Od wartości tej zależy energia użyteczna magazynu (60 kWh) oraz wynikający
z niej czas podtrzymania (ok. 1,3 h przy pełnym obciążeniu).

### 5.2.1. Parametry ekonomiczne

| Parametr | Wartość |
|---|---|
| Stopa dyskontowa | 8,00% |
| Stopa inflacji | 2,00% |
| Okres eksploatacji (horyzont analizy) | 25 lat |
| Cena zakupu energii z sieci | 0,220 $/kWh |
| Cena sprzedaży energii do sieci | 0,090 $/kWh |
| Kurs przyjęty do przeliczeń | 4,00 PLN/$ |

Koszt bieżący netto oznaczany jest w pracy konsekwentnie jako **NPC** (*net present
cost*); określenie „całkowity koszt bieżący systemu" nie jest stosowane.

### 5.2.2. Modelowanie zaopatrzenia w ciepło

Szynę cieplną odwzorowano kotłem gazowym obecnym we wszystkich konfiguracjach,
uzupełnianym odzyskiem ciepła z jednostki kogeneracyjnej w Konfiguracji K3.
**Rozwiązanie to nie odpowiada stanowi faktycznemu** — obiekt zasilany jest ciepłem
z sieci geotermalnej. Niezgodność tę, jej kierunek oraz konsekwencje dla oceny
Konfiguracji K3 omówiono w podrozdziale 4.6.1.

## 5.3. Modelowanie zdarzeń awaryjnych

- **5.3.1.** Wariant A1 — pojedyncze zdarzenie 72 h w okresie zimowym. Termin
  15–17 stycznia przyjęto jako najbardziej niekorzystny: minimum zasobu słonecznego
  przy maksimum zapotrzebowania cieplnego.
- **5.3.2.** Wariant A2 — pięć przerw o łącznym czasie 21 h, rozłożonych w roku
  zgodnie ze statystyką SAIDI/SAIFI polskich sieci dystrybucyjnych `[ŹRÓDŁO]`.
- **5.3.3.** Implementacja w module niezawodności sieci. Konwencja szeregu czasowego:
  **1 = sieć dostępna, 0 = awaria** — odwrotna do intuicyjnej.

### Przyjęcie czasu 72 h jako progu

Czas trwania zdarzenia A1 przyjęto na poziomie 72 godzin jako `[ŹRÓDŁO]` wartość
stosowaną w analizach odporności infrastruktury krytycznej na zdarzenia typu
*black-sky*. Próg ten nie wynika z przepisu prawa krajowego — Rozporządzenie
Ministra Zdrowia nie określa wymaganego czasu pracy źródła rezerwowego, lecz wyłącznie
jego moc (§ 42). Brak wymogu czasowego stanowi jedną z przesłanek pracy.
