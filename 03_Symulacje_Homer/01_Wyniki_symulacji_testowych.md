# Wyniki symulacji testowych — trzy scenariusze zasilania

Symulacje przeprowadzono w HOMER Pro x64 3.18.4 dla obiektu modelowego
zlokalizowanego w Szczecinie (53°25,7'N, 14°33,2'E).

> **Status:** wyniki mają charakter **testowy i weryfikacyjny**. Obiekt referencyjny
> nie został jeszcze wybrany, a profile obciążenia są modelowe. Celem tej serii było
> sprawdzenie poprawności metodyki, identyfikacja pułapek modelowych oraz rozpoznanie
> dostępnych form prezentacji wyników.

---

## 1. Wspólne dane wejściowe

| Parametr | Wartość |
|---|---|
| Lokalizacja | Szczecin (53,25°N / 14,75°E — punkt siatki NASA) |
| Zasób słoneczny (GHI) | 2,72 kWh/m²/d (≈ 993 kWh/m²/rok) |
| Temperatura średnia roczna | 8,32 °C (I: −1,68 °C, VII: 18,75 °C) |
| Zapotrzebowanie elektryczne | 1 000 MWh/rok, szczyt 159,76 kW, LF = 0,715 |
| Zapotrzebowanie cieplne | 1 800 MWh/rok, szczyt 537,22 kW, LF = 0,382 |
| Cena energii z sieci | 0,22 $/kWh |
| Cena odsprzedaży | 0,09 $/kWh |
| Stopa dyskontowa / inflacja | 8% / 2% |
| Okres analizy | 25 lat |
| Dopuszczalny niedobór mocy | **0%** |

### Parametry komponentów

| Komponent | CAPEX | Uwagi |
|---|---|---|
| PV (flat plate) | 800 $/kW | derating 80%, żywotność 25 lat |
| BESS Li-Ion 100 kWh | 30 000 $/szt. | SoC min **40%**, sprawność 90% |
| Przekształtnik | 300 $/kW | sprawność 95% |
| Agregat / CHP | 500 → 1 200 $/kW | min. obciążenie 25%, odzysk ciepła 50% |
| Kocioł szczytowy | — | sprawność 85%, gaz ziemny 0,65 $/m³ |
| Olej napędowy | 1,55 $/L | ≈ 6,20 zł/l |

**Ograniczenie przestrzenne:** moc PV ograniczono do zbioru {0; 100; 150; 200; 250} kW,
zgodnie z szacowaną powierzchnią dachu 1 000–1 500 m². Pojemność BESS: {0; 1; 2; 4; 6}
modułów po 100 kWh.

---

## 2. Scenariusz 1 — Baza (Sieć + Agregat)

Architektura: sieć elektroenergetyczna + agregat prądotwórczy (rezerwa).

| Konfiguracja | NPC | LCOE [$/kWh] | Koszt operacyjny [$/rok] | CAPEX | Godziny pracy agregatu |
|---|---|---|---|---|---|
| **Sama sieć** | **2,84 M$** | **0,220** | 220 000 | 0 $ | — |
| Sieć + agregat 180 kW | 2,91 M$ | 0,225 | 218 374 | 90 000 $ | **0** |

Energia zakupiona z sieci: **1 000 000 kWh/rok** (100% pokrycia).

### Wniosek

Agregat prądotwórczy pracuje **zero godzin w roku**. Przy nieprzerwanej dostępności sieci
stanowi wyłącznie obciążenie kapitałowe (+90 000 $ CAPEX) podnoszące NPC o 2,5% oraz LCOE
o 0,005 $/kWh, bez jakiegokolwiek udziału w produkcji energii.

Wynik ten stanowi ilościowe potwierdzenie tezy postawionej w podrozdziale 3.2: w układzie
klasycznym agregat pozostaje **pasywnym centrum kosztowym**, nieuczestniczącym w bieżącej
optymalizacji kosztów zakupu energii.

---

## 3. Scenariusz 2 — Hybryda (Sieć + Agregat + PV + BESS)

| # | PV [kW] | Agregat [kW] | BESS [szt.] | Przeksz. [kW] | Strategia | NPC | LCOE | CAPEX | Ren. Frac. | IRR | Zwrot |
|---|---|---|---|---|---|---|---|---|---|---|---|
| **1** | **250** | — | — | **150** | CC | **2,54 M$** | **0,196** | 245 000 $ | 21,0% | **17%** | **5,7 lat** |
| 2 | 250 | — | 1 | 145 | LF | 2,58 M$ | 0,199 | 273 500 $ | 21,4% | 15% | 6,3 |
| 3 | 250 | 180 | — | 150 | CC | 2,61 M$ | 0,201 | 335 000 $ | 21,0% | 12% | 7,7 |
| 4 | 250 | 180 | 1 | 145 | LF | 2,65 M$ | 0,205 | 363 500 $ | 21,4% | 11% | 8,4 |
| 5 | — | — | — | — | CC | 2,84 M$ | 0,220 | 0 $ | 0 | — | — |

Produkcja PV: **232 811 kWh/rok** przy 250 kWp → **931 kWh/kWp/rok** (wartość typowa dla PL).

### Wnioski

**Redukcja LCOE o 10,9%** względem wariantu bazowego (0,220 → 0,196 $/kWh) przy okresie
zwrotu 5,7 roku i IRR 17%.

**Porównanie z wariantem nieograniczonym:** w pierwszej symulacji bez ograniczenia
przestrzennego optymalizator wskazał PV 1 043 kW (LCOE 0,123 $/kWh, zwrot 8,5 roku).
Konfiguracja ta wymagałaby 5 000–6 000 m² dachu — pięciokrotnie więcej niż dostępne.
Ograniczenie do 250 kWp obniża efekt ekonomiczny, **lecz jednocześnie skraca okres zwrotu**
(5,7 vs 8,5 roku), ponieważ cała wyprodukowana energia jest konsumowana lokalnie
po pełnej stawce taryfowej, bez odsprzedaży nadwyżek po cenie 0,09 $/kWh.

---

## 4. Scenariusz 3 — Zaawansowana mikrosieć (Sieć + PV + BESS + CHP + kocioł)

Model rozszerzony o **szynę cieplną**: zapotrzebowanie 1 800 MWh/rok pokrywane przez
kocioł szczytowy oraz odzysk ciepła z jednostki kogeneracyjnej.

| # | PV [kW] | CHP [kW] | BESS [szt.] | Przeksz. [kW] | Strategia | NPC | LCOE | CAPEX | Zwrot |
|---|---|---|---|---|---|---|---|---|---|
| **1** | **250** | — | — | **150** | CC | **4,35 M$** | **0,196** | 245 000 $ | **5,7 lat** |
| 2 | 250 | — | 2 | 140 | LF | 4,43 M$ | 0,203 | 302 000 $ | 7,0 |
| 3 | 250 | 180 | — | 150 | CC | 4,51 M$ | 0,208 | 461 000 $ | 11 |
| 4 | 250 | 180 | 2 | 140 | LF | 4,59 M$ | 0,216 | 518 000 $ | 12 |
| 5 | — | — | — | — | CC | 4,65 M$ | 0,220 | 0 $ | — |

### 4.1. Struktura kosztów wariantu optymalnego (NPC)

| Komponent | Kapitał | Wymiana | O&M | Paliwo | Wartość rezydualna | **Razem** |
|---|---|---|---|---|---|---|
| Kocioł gazowy | 0 $ | 0 $ | 0 $ | **1 801 959 $** | 0 $ | **1 801 959 $** |
| Instalacja PV | 200 000 $ | 0 $ | 32 319 $ | 0 $ | 0 $ | 232 319 $ |
| Sieć | 0 $ | 0 $ | 2 251 540 $ | 0 $ | 0 $ | 2 251 540 $ |
| Przekształtnik | 45 000 $ | 19 092 $ | 0 $ | 0 $ | −3 593 $ | 60 499 $ |
| **System** | **245 000 $** | **19 092 $** | **2 283 859 $** | **1 801 959 $** | **−3 593 $** | **4 346 317 $** |

### 4.2. Bilans elektryczny

| Produkcja | kWh/rok | % |
|---|---|---|
| Instalacja PV | 232 811 | 22,7 |
| Zakup z sieci | 793 875 | 77,3 |
| **Razem** | **1 026 686** | **100** |

| Zużycie | kWh/rok | % |
|---|---|---|
| Obciążenie AC | 1 000 000 | 99,5 |
| Sprzedaż do sieci | 5 400 | 0,54 |

| Wskaźnik | Wartość |
|---|---|
| Energia nadmiarowa | 10 153 kWh/rok (0,99%) |
| **Niepokryte obciążenie** | **0 kWh** |
| **Niedobór mocy** | **0 kWh** |
| Udział OZE | 7,50% |
| Maks. penetracja OZE | 167% |

**Autokonsumpcja PV: 97,7%** — z 232 811 kWh wyprodukowanych lokalnie jedynie 5 400 kWh
(2,3%) trafiło do sieci. Wynik ten stanowi bezpośrednie potwierdzenie tezy z podrozdziału
3.3 o niemal pełnej autokonsumpcji energii fotowoltaicznej w obiektach szpitalnych,
wynikającej z wysokiego obciążenia podstawowego.

### 4.3. Bilans cieplny

| Pozycja | kWh/rok | % |
|---|---|---|
| Produkcja — kocioł gazowy | 1 800 000 | 100 |
| Zużycie — obciążenie cieplne | 1 800 000 | 100 |
| Ciepło nadmiarowe | 0 | 0 |

### 4.4. Emisje (wariant optymalny)

| Substancja | kg/rok |
|---|---|
| **Dwutlenek węgla (CO₂)** | **914 504** |
| Dwutlenek siarki (SO₂) | 2 160 |
| Tlenki azotu (NOₓ) | 1 057 |
| CO, węglowodory, cząstki stałe | 0 |

---

## 5. Wnioski krytyczne — do uwzględnienia w metodyce

### 5.1. Jednostka CHP nie została wybrana — przyczyna i sposób naprawy

W Scenariuszu 3 optymalizator **nie wybrał jednostki kogeneracyjnej** (0 godzin pracy).
Przyczyną jest paliwo: wykorzystany komponent `Autosize Genset` pracuje wyłącznie na
oleju napędowym (1,55 $/L), co czyni wytwarzanie energii w kogeneracji droższym niż
zakup z sieci połączony z produkcją ciepła w kotle gazowym (0,65 $/m³).

**Działanie naprawcze:** w modelu docelowym należy dobrać z katalogu HOMER konkretną
**gazową jednostkę kogeneracyjną** (silnik tłokowy zasilany gazem ziemnym), a nie
generyczny `Autosize Genset`. Dopiero wówczas relacja kosztów paliwa umożliwi
ekonomiczne dysponowanie modułem CHP.

### 5.2. Kryterium NPC nie promuje magazynu energii

We wszystkich trzech scenariuszach konfiguracja o najniższym NPC **nie zawiera BESS**.
Magazyn podnosi NPC o 60–80 tys. $ nie wnosząc korzyści ekonomicznej, ponieważ model
zakłada nieprzerwaną dostępność sieci.

**Działanie naprawcze:** wprowadzenie **testu przetrwania (Resilience Test)** jako
niezależnego kryterium — modelowanie przerw w zasilaniu sieciowym i pomiar czasu
autonomii. Bez tego rozszerzenia ocena wielokryterialna sprowadza się do analizy
ekonomicznej, co jest nieadekwatne dla obiektu infrastruktury krytycznej.

### 5.3. Ograniczenie przestrzenne jest niezbędne

Optymalizator bez ograniczeń wskazał PV 1 043 kW — moc fizycznie niemożliwą do
zainstalowania na dachu obiektu. Wprowadzenie zbioru dopuszczalnych mocy
(`Sizing → Search Space`) na podstawie analizy CAD jest warunkiem wiarygodności wyników.

HOMER sygnalizuje osiągnięcie granicy zbioru komunikatem `PV search space may be
insufficient` — w tym przypadku komunikat jest oczekiwany i **nie stanowi błędu**,
lecz potwierdza, że ograniczeniem jest powierzchnia dachu, a nie ekonomia.

---

## 6. Dostępne formy prezentacji wyników (materiał na rozdział 6)

Okno `Simulation Results` (dwukrotne kliknięcie wiersza w zakładce `Tables`) zawiera
zakładki stanowiące gotowy materiał ilustracyjny:

| Zakładka | Zawartość | Zastosowanie w pracy |
|---|---|---|
| **Cost Summary** | Wykres słupkowy NPC wg komponentów + tabela (kapitał, wymiana, O&M, paliwo, wartość rezydualna) | Podrozdział 6.2 — analiza ekonomiczna |
| **Cash Flow** | Przepływy pieniężne w cyklu życia | Podrozdział 6.2 |
| **Compare Economics** | Porównanie wariantu z przypadkiem bazowym, wykres skumulowanego przepływu | Podrozdział 6.4 |
| **Electrical** | Bilans produkcji i zużycia + **wykres miesięcznej produkcji** (słupki skumulowane PV/sieć) | Podrozdział 6.1 |
| **Thermal** | Bilans cieplny + wykres miesięcznej produkcji ciepła | Podrozdział 6.1 |
| **Renewable Penetration** | Udział OZE w czasie | Podrozdział 6.1 |
| **Generic flat plate PV** | Uzysk, godziny pracy, wykres produkcji | Podrozdział 6.1 |
| **Grid** | Zakup/sprzedaż energii, szczyty poboru | Podrozdział 6.2 |
| **Emissions** | Tabela emisji: CO₂, CO, HC, PM, SO₂, NOₓ | Podrozdział 6.3 — analiza ekologiczna |
| **Time Series Plot** | **Przebiegi godzinowe dowolnych zmiennych** (moc, SoC, przepływy) | Podrozdział 6.1 — kluczowe dla testu autonomii |

Przycisk `Calculation Report` generuje zbiorczy raport, `Export...` / `Export Details...`
umożliwiają eksport danych do dalszej obróbki.

> **Uwaga:** zakładka `Graphs` w oknie głównym służy wyłącznie analizie wrażliwości
> i pozostaje pusta (`There are not enough sensitivity variables`) dopóki nie zdefiniuje
> się zmiennych wrażliwości (np. cena energii, stopa dyskontowa). Wykresy wyników
> znajdują się w oknie `Simulation Results`.

---

## 7. Zestawienie porównawcze trzech scenariuszy

| Wskaźnik | Scen. 1 (Baza) | Scen. 2 (Hybryda) | Scen. 3 (Mikrosieć + ciepło) |
|---|---|---|---|
| NPC | 2,84 M$ | **2,54 M$** | 4,35 M$ |
| LCOE [$/kWh] | 0,220 | **0,196** | 0,196 |
| CAPEX | 0 $ | 245 000 $ | 245 000 $ |
| Koszt operacyjny [$/rok] | 220 000 | **177 865** | 317 255 |
| Udział OZE | 0% | 21,0% | 7,5%¹ |
| Okres zwrotu | — | **5,7 lat** | 5,7 lat |
| Niepokryte obciążenie | 0 | 0 | 0 |

¹ Niższy udział OZE w Scenariuszu 3 wynika z uwzględnienia energii cieplnej w bilansie
całkowitym — ta sama produkcja PV odnoszona jest do sumy zapotrzebowania elektrycznego
i cieplnego (2 800 MWh zamiast 1 000 MWh).

> **Zastrzeżenie:** bezpośrednie porównanie NPC Scenariusza 3 z pozostałymi jest
> nieuprawnione — model obejmuje dodatkowo koszt paliwa gazowego dla pokrycia
> zapotrzebowania cieplnego (1,80 mln $ NPC). Porównanie wielokryterialne w rozdziale 6
> musi uwzględniać ten sam zakres bilansu energetycznego dla wszystkich wariantów,
> tzn. szynę cieplną należy wprowadzić również do Scenariuszy 1 i 2.
