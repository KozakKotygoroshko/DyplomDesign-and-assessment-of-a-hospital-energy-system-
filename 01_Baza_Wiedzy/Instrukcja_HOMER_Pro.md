# Instrukcja obsługi HOMER Pro — budowa modelu mikrosieci szpitalnej

Dokumentacja krok po kroku, sporządzona podczas budowy modelu testowego
w HOMER Pro x64 3.18.4 (Evaluation Edition) dla obiektu w Szczecinie.

> **Ograniczenia wersji Evaluation:** na wykresach i w tabelach nanoszony jest znak wodny
> „For Evaluation Use". Zapis pliku `.homer` działa poprawnie.
> **Licencja wygasa za 7 dni** (stan na 29.08.2026) — symulacje docelowe należy wykonać
> przed tym terminem lub pozyskać licencję akademicką.

---

## 1. Konfiguracja projektu (DESIGN → Home)

Po uruchomieniu programu widoczny jest panel `REQUIRED CHANGES` wskazujący braki modelu:
`Add a load`, `Add a power source`, `Add a renewable energy source`. Przycisk `Calculate`
pozostaje nieaktywny (szary) dopóki wszystkie wymagania nie zostaną spełnione.

### 1.1. Dane identyfikacyjne

| Pole | Wartość |
|---|---|
| Name | `Scenariusz_2_Hybryda_Siec_Diesel_PV_BESS` |
| Author | Hlieb Snitko |

### 1.2. Lokalizacja

W polu wyszukiwania pod mapą wpisano `Szczecin` i zatwierdzono klawiszem **Enter**.

> **Uwaga:** przycisk `Location Search` bywa zawodny — przy pierwszej próbie mapa
> przeskoczyła na współrzędne 83°24,0'S (Antarktyda). Zatwierdzenie klawiszem Enter
> działa poprawnie.

Wynik: `plac Żołnierza Polskiego 1, 70-413 Szczecin (53°25,7'N, 14°33,2'E)`,
strefa czasowa `(UTC+01:00) Sarajevo, Skopje, Warsaw` ustawiona automatycznie.

### 1.3. Parametry ekonomiczne

| Parametr | Wartość | Uzasadnienie |
|---|---|---|
| Discount rate | 8,00% | wartość domyślna — do korekty wg realiów PL |
| Inflation rate | 2,00% | cel inflacyjny NBP |
| Annual capacity shortage | **0,00%** | wymóg dla obiektu infrastruktury krytycznej |
| Project lifetime | 25 lat | zgodne z żywotnością modułów PV |

---

## 2. Import profilu obciążenia elektrycznego (LOAD → Electric #1)

Ekran `ELECTRIC LOAD SETUP` oferuje trzy metody:

1. `Create a synthetic load from a profile` — profil z biblioteki (Residential, Commercial,
   Industrial, Community, Blank)
2. `Access the Open EI Database` — baza profili USA
3. `Import a load from a time series file` — **metoda zastosowana**

### 2.1. Procedura importu

1. Kliknięto `Import...`
2. W polu `File name` wpisano pełną ścieżkę:
   `D:\Dyplom_ZUT_Microgrid\03_Symulacje_Homer\Profil_obciazenia_elektrycznego_szpital_8760h.csv`
3. Zatwierdzono `Open`
4. W oknie `Imported Data Information` wskazano rok: **2007**

> **Dlaczego rok 2007:** HOMER potrzebuje roku, aby prawidłowo rozłożyć dni robocze
> i weekendy. Profil zbudowano przy założeniu, że 1 stycznia przypada w poniedziałek —
> warunek ten spełniają lata 2007, 2018 i 2024.

### 2.2. Weryfikacja poprawności importu

| Metric | Wartość zaimportowana | Wartość oczekiwana | Zgodność |
|---|---|---|---|
| Average (kWh/day) | 2 739,7 | 2 739,7 | ✔ |
| Average (kW) | 114,16 | 114,16 | ✔ |
| Peak (kW) | 159,76 | 159,76 | ✔ |
| Load factor | 0,71 | 0,715 | ✔ |
| Peak Month | August | sierpień (chłodzenie) | ✔ |

Program automatycznie wyznaczył parametry zmienności: `Day-to-day 3,250%`,
`Timestep 2,407%`.

### 2.3. Dlaczego nie użyto profilu syntetycznego

Test kontrolny z profilem wbudowanym (Industrial, skalowanie do 2 740 kWh/d) dał:

| Metric | Profil syntetyczny | Profil własny |
|---|---|---|
| Peak (kW) | **508,72** | **159,76** |
| Load factor | **0,22** | **0,715** |

Profil syntetyczny zawyża moc szczytową **3,2-krotnie**, co prowadziłoby do
przewymiarowania agregatu, magazynu i przekształtników oraz zafałszowania kosztów.

---

## 3. Dodawanie komponentów (COMPONENTS)

Wstążka zawiera: `Controller, Generator, PV, Wind Turbine, Storage, Converter, Custom,
Boiler, Hydro, Reformer, Electrolyzer, Hydrogen Tank, Hydrokinetic, Grid, Thermal Load Controller`.

### 3.1. Sieć elektroenergetyczna (Grid)

Kliknięcie `Grid` dodaje komponent natychmiast — bez dodatkowego przycisku potwierdzenia.
Otwiera się ekran `ADVANCED GRID` z trybami taryfowymi: `Simple Rates`, `Real Time Rates`,
`Scheduled Rates`, `Grid Extension`.

Przyjęto `Simple Rates`:

| Parametr | Wartość | Uzasadnienie |
|---|---|---|
| Grid Power Price | 0,22 $/kWh | ≈ 0,88 zł/kWh — taryfa biznesowa z dystrybucją |
| Grid Sellback Price | 0,09 $/kWh | ≈ 0,36 zł/kWh — rozliczenie nadwyżek |

> **Uwaga o walucie:** model prowadzono w USD (domyślna waluta HOMER). W wersji
> docelowej należy przełączyć walutę na PLN (`FILE → Settings`) i wprowadzić
> ceny bezpośrednio w złotych.

### 3.2. Agregat prądotwórczy (Generator)

Wybrano `Autosize Genset` — HOMER dobiera moc automatycznie do pokrycia obciążenia.
Konieczne jest kliknięcie przycisku **`Add Generator`** (sam wybór z listy nie dodaje
komponentu).

Parametry domyślne generatora Diesel:

| Parametr | Wartość |
|---|---|
| Fuel curve intercept | 4,96 L/hr |
| Fuel curve slope | 0,236 L/hr/kW |
| Emisje CO | 16,5 g/L paliwa |
| Emisje NOx | 15,5 g/L paliwa |
| Cząstki stałe | 0,1 g/L paliwa |
| Initial Capital | 500 $/kW |
| O&M | 0,030 $/godz. pracy |
| Minimum Load Ratio | **25%** |
| Lifetime | 15 000 godzin |

**Skorygowano:** `Fuel Price` z 1,00 na **1,55 $/L** (≈ 6,20 zł/l — cena oleju napędowego).

> Parametr `Minimum Load Ratio = 25%` jest bezpośrednim odzwierciedleniem zjawiska
> *wet stacking* opisanego w podrozdziale 3.2 pracy — HOMER nie pozwoli agregatowi
> pracować poniżej tego progu.

### 3.3. Instalacja fotowoltaiczna (PV)

Wybrano `Generic flat plate PV`, kliknięto **`Add PV`**.

| Parametr | Domyślnie | Przyjęto | Uzasadnienie |
|---|---|---|---|
| Capital | 2 500 $/kW | **800 $/kW** | realia rynku PL 2026 (~3 200 zł/kWp) |
| Replacement | 2 500 $/kW | **800 $/kW** | jw. |
| O&M | 10 $/kW/rok | 10 $/kW/rok | bez zmian |
| Lifetime | 25 lat | 25 lat | bez zmian |
| Derating Factor | 80% | 80% | straty systemowe |
| Electrical Bus | DC | DC | wymaga przekształtnika |

Po dodaniu PV pojawia się nowy wymóg: `Add a solar GHI resource` oraz `Add converter`.

### 3.4. Magazyn energii (Storage)

Domyślnie proponowany jest `Generic 1kWh Lead Acid`. **Zmieniono na `Generic 100kWh Li-Ion`**
z listy rozwijanej, następnie kliknięto `Add Storage`.

| Parametr | Domyślnie | Przyjęto | Uzasadnienie |
|---|---|---|---|
| Nominal Capacity | 100 kWh | 100 kWh | granulacja modułowa |
| Nominal Voltage | 600 V | 600 V | — |
| Roundtrip efficiency | 90% | 90% | — |
| Capital | 70 000 $ | **30 000 $** | ≈ 300 $/kWh — realia 2026 |
| Replacement | 70 000 $ | **30 000 $** | jw. |
| Lifetime | 15 lat / 300 MWh | bez zmian | — |
| Initial SoC | 100% | 100% | — |
| **Minimum SoC** | 20% | **40%** | **rezerwa dla odbiorów krytycznych** |

> Podniesienie minimalnego SoC do 40% odpowiada praktyce opisanej w podrozdziale 3.4:
> nienaruszalny próg naładowania gwarantujący zasilanie odbiorów klasy 0,5 s,
> podczas gdy pozostała pojemność służy arbitrażowi cenowemu i *peak shavingowi*.

### 3.5. Przekształtnik (Converter)

Kliknięcie `Converter` dodaje `System Converter` automatycznie.

| Parametr | Wartość |
|---|---|
| Capital / Replacement | 300 $/kW |
| Inverter efficiency | 95% |
| Rectifier efficiency | 95% |
| Rectifier relative capacity | 100% |
| Lifetime | 15 lat |
| Parallel with AC Generator | ✔ zaznaczone |

---

## 4. Zasoby (RESOURCES → Solar GHI)

Kliknięto `Solar GHI`, następnie **`Download From Internet...`**.

Dane pobrano z bazy **NASA Prediction of Worldwide Energy Resource (POWER)** —
średnie miesięczne z okresu 42 lat (VII 1983 – VI 2025) dla punktu
53,25°N / 14,75°E.

| Miesiąc | Clearness Index | GHI [kWh/m²/d] |
|---|---|---|
| I | 0,369 | 0,73 |
| II | 0,416 | 1,42 |
| III | 0,425 | 2,44 |
| IV | 0,436 | 3,66 |
| V | 0,471 | **4,96** |
| VI | 0,421 | 4,84 |
| VII | 0,431 | 4,74 |
| VIII | 0,453 | 4,16 |
| IX | 0,422 | 2,80 |
| X | 0,374 | 1,53 |
| XI | 0,332 | 0,76 |
| XII | 0,367 | **0,58** |

**Średnia roczna: 2,72 kWh/m²/dobę** (≈ 993 kWh/m²/rok).

> Stosunek maksimum do minimum wynosi **8,6:1** (maj / grudzień) — skrajna sezonowość
> zasobu w warunkach polskich. Fakt ten należy podkreślić w pracy: instalacja PV nie jest
> w stanie zapewnić autonomii w okresie zimowym, co uzasadnia obecność źródeł
> sterowalnych (agregat, CHP) w architekturze mikrosieci.

Po pobraniu danych panel `REQUIRED CHANGES` znika, a przycisk `Calculate` staje się aktywny.

---

## 5. Obliczenia i wyniki

### 5.1. Uruchomienie

Kliknięto zielony przycisk **`Calculate`** (prawy górny róg). Okno postępu
`HOMER is optimizing for lowest net present cost...`. Czas obliczeń: **ok. 35 sekund**
(8 konfiguracji, 8760 kroków godzinowych).

### 5.2. Odczyt wyników — zakładka `Summary`

Ekran `RESULTS → Summary` prezentuje:

**Winning System Architecture** (konfiguracja optymalna):
- HOMER Cycle Charging (strategia dysponowania)
- Grid
- **PV — 1 043 kW**
- **Converter — 633 kW**

**Base Case Architecture** (wariant odniesienia): Grid + Cycle Charging

**Cost Summary:**

| Wskaźnik | Base Case (sama sieć) | System optymalny | Zmiana |
|---|---|---|---|
| **NPC** | 2,84 mln $ | **2,38 mln $** | −16,2% |
| Initial Capital | 0 $ | 1,02 mln $ | — |
| O&M | 220 000 $/rok | 104 588 $/rok | −52,5% |
| **LCOE** | 0,220 $/kWh | **0,123 $/kWh** | **−44,1%** |

**Economic Metrics:** IRR 10%, ROI 7,3%, Simple Payback **8,5 roku**.

### 5.3. Odczyt wyników — zakładka `Tables`

Pełna tabela `Optimization Results` (8 konfiguracji, sortowanie wg NPC):

| # | PV [kW] | Gen [kW] | BESS [szt.] | Konw. [kW] | Disp. | NPC | LCOE [$/kWh] | CAPEX | Ren. Frac. [%] | Payback [lat] |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 1 043 | — | — | 633 | CC | **2,38 M$** | **0,123** | 1,02 M$ | 59,4 | 8,5 |
| 2 | 1 035 | — | 1 | 618 | LF | 2,40 M$ | 0,127 | 1,04 M$ | 59,7 | 8,6 |
| 3 | 1 043 | 180 | — | 633 | CC | 2,45 M$ | 0,127 | 1,11 M$ | 59,4 | 9,3 |
| 4 | 1 035 | 180 | 1 | 618 | LF | 2,47 M$ | 0,131 | 1,13 M$ | 59,7 | 9,4 |
| 5 | — | — | — | — | CC | 2,84 M$ | 0,220 | 0 $ | 0 | — |
| 6 | — | — | 1 | 5 | LF | 2,90 M$ | 0,224 | 31 500 $ | 0,005 | — |
| 7 | — | 180 | — | — | CC | 2,91 M$ | 0,225 | 90 000 $ | 0 | — |
| 8 | — | 180 | 1 | 5 | LF | 2,97 M$ | 0,230 | 121 500 $ | 0,005 | — |

Produkcja PV w wariancie zwycięskim: **971 601 kWh/rok** (CAPEX PV 834 668 $).

Podwójne kliknięcie wiersza otwiera `Simulation Details` z bilansami godzinowymi.

### 5.4. Eksport

Przyciski `Export...` oraz `Export Details...` (lewy górny róg zakładki `Tables`)
umożliwiają zapis wyników do pliku. Przycisk `Calculation Report` generuje raport zbiorczy.

---

## 6. Wnioski z symulacji testowej — istotne dla pracy

### 6.1. Optymalizator ekonomiczny nie wybiera magazynu ani agregatu

Konfiguracja o najniższym NPC zawiera **wyłącznie PV i przekształtnik**. Dodanie
magazynu BESS podnosi NPC o 20 tys. $, a agregatu — o 70 tys. $.

**Interpretacja:** przy założeniu sieci o nieograniczonej dostępności i braku modelowania
awarii, magazyn i agregat stanowią wyłącznie koszt. Kryterium najniższego NPC jest zatem
**niewystarczające** dla obiektu infrastruktury krytycznej.

**Wniosek metodyczny:** uzasadnia to wprowadzenie **testu przetrwania (Resilience Test)**
jako niezależnego kryterium oceny. Ocena wielokryterialna musi obejmować nie tylko NPC
i LCOE, lecz również czas autonomii w trybie wyspowym.

### 6.2. Optymalizator przekracza fizyczne możliwości dachu

Wynik **PV 1 043 kWp** wymaga ok. **5 000–6 000 m²** powierzchni dachu przy
uwzględnieniu odstępów międzyrzędowych. Zakładana powierzchnia wolna obiektu
referencyjnego wynosi **1 000–1 500 m²**, co odpowiada ok. **200–250 kWp**.

**Wniosek metodyczny:** potwierdza to konieczność wprowadzenia **twardego ograniczenia
górnego (upper bound)** mocy PV, wyznaczonego z analizy CAD rozmieszczenia modułów.
Bez tego ograniczenia wyniki symulacji są fizycznie niewykonalne.

### 6.3. Skala potencjalnych oszczędności

Nawet po ograniczeniu mocy PV kierunek pozostaje jednoznaczny: obniżenie LCOE
z 0,220 do 0,123 $/kWh (−44%) przy udziale OZE 59,4% i okresie zwrotu 8,5 roku.
Wartości te posłużą jako punkt odniesienia dla wariantów z ograniczoną mocą PV.

### 6.4. Sezonowość zasobu słonecznego

Stosunek GHI maj/grudzień = 8,6:1 oznacza, że w grudniu instalacja PV pokrywa
znikomą część zapotrzebowania. Uzasadnia to obecność jednostki CHP w Scenariuszu 3 —
źródła sterowalnego, niezależnego od warunków atmosferycznych.

---

## 7. Napotkane problemy techniczne i obejścia

| Problem | Obejście |
|---|---|
| `Location Search` przenosi mapę na błędne współrzędne | Wpisać nazwę w polu i zatwierdzić klawiszem `Enter` |
| Pole `Scaled Annual Average` nie aktualizuje metryk po `Tab`/`Enter` | Kliknąć w dowolne inne miejsce okna |
| Potrójne kliknięcie w polu liczbowym nie zaznacza całej wartości (powstaje np. `0.0.22`) | Użyć `Ctrl+A`, następnie `Delete`, dopiero potem wpisać wartość |
| Okno nie reaguje na przycisk maksymalizacji | Dwukrotne kliknięcie w pasek tytułu |
| Wybór pozycji z listy nie dodaje komponentu | Kliknąć przycisk `Add [nazwa]` w prawym dolnym rogu panelu |
| Ponowne uruchomienie programu otwiera kolejną instancję | Przełączać się przez pasek zadań, nie przez skrót uruchamiający |

---

## 8. Kolejne kroki

1. Ograniczyć moc PV do wartości wynikającej z analizy CAD (`Sizing → Search Space`
   zamiast `HOMER Optimizer`).
2. Zamodelować przerwy w zasilaniu sieciowym (`Grid → Scheduled Rates` lub
   `Grid Extension`) w celu przeprowadzenia testu autonomii.
3. Dodać szynę cieplną (`LOAD → Thermal #1`) z profilem
   `Profil_obciazenia_cieplnego_szpital_8760h.csv` — wymagane dla Scenariusza 3.
4. Dodać jednostkę CHP (`Generator` z parametrem `CHP Heat Recovery Ratio > 0`)
   oraz kocioł szczytowy (`Boiler`).
5. Przełączyć walutę na PLN i zweryfikować ceny rynkowe komponentów.
