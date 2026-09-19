# Wyniki symulacji finalnych — Szpital Powiatowy w Pyrzycach

Seria obliczeniowa wykonana na **danych rzeczywistych** obiektu.
Data wykonania: 19 września 2026. Środowisko: HOMER Pro x64 3.18.4.

---

## 1. Parametry modelu

| Pozycja | Wartość | Źródło |
|---|---|---|
| Lokalizacja | plac Wolności 2, 74-200 Pyrzyce | Geoportal |
| Współrzędne siatki NASA | 53,25°N / 14,75°E | pobrane automatycznie |
| **Zasób słoneczny (GHI)** | **2,72 kWh/m²/d** | NASA POWER, 42 lata |
| Zapotrzebowanie elektryczne | 355 MWh/rok (972,6 kWh/d) | dokumentacja przetargowa |
| Moc szczytowa | 56,72 kW | profil własny |
| Zapotrzebowanie cieplne | 700 MWh/rok (1 917,8 kWh/d) | oszacowanie |
| Moc cieplna szczytowa | 208,92 kW | profil własny |

### Komponenty

| Komponent | Model | Parametry | Przestrzeń poszukiwań |
|---|---|---|---|
| PV | Generic flat plate | 800 $/kW, derating 80% | {0; 50; 75; 100; 110} kWp |
| BESS | Generic 100 kWh Li-Ion | 30 000 $/szt., SoC min 40% | {0; 1; 2; 3} × 100 kWh |
| **CHP** | **2G Aura 404** | **100 kW, gaz ziemny, odzysk 57,2%** | opcjonalny |
| Kocioł | Generic Boiler | η 85%, gaz 0,65 $/m³ | zawsze obecny |
| Sieć | — | 0,220 / 0,090 $/kWh | zawsze obecna |

---

## 2. Wariant A0 — praca normalna (bez awarii)

| # | PV [kW] | CHP | BESS | Przeksz. [kW] | NPC | LCOE | CAPEX | IRR | Zwrot | Godz. CHP |
|---|---|---|---|---|---|---|---|---|---|---|
| **1** | **110** | — | — | **64,5** | **1,59 M$** | **0,190** | 107 350 $ | **16%** | **6,0 lat** | — |
| 2 | 110 | — | 1 | 52,0 | 1,63 M$ | 0,202 | 133 588 $ | 12% | 7,5 | — |
| 3 | — | — | — | — | 1,71 M$ | 0,220 | 0 $ | — | — | — |
| 4 | — | — | 1 | 2,15 | 1,76 M$ | 0,232 | 30 645 $ | — | — | — |
| 5 | 110 | 100 | — | 64,5 | 2,02 M$ | 0,281 | 557 350 $ | — | — | **125** |
| 6 | 110 | 100 | 1 | 52,0 | 2,06 M$ | 0,295 | 583 588 $ | — | — | 103 |
| 7 | — | 100 | — | — | 2,13 M$ | 0,312 | 450 000 $ | — | — | 750 |
| 8 | — | 100 | 1 | 2,15 | 2,19 M$ | 0,324 | 480 645 $ | — | — | 749 |

**Konfiguracja optymalna:** PV 110 kWp + przekształtnik 64,5 kW.
Produkcja PV **101 758 kWh/rok** (925 kWh/kWp). Udział OZE 8,65%.
Redukcja LCOE z 0,220 na **0,190 $/kWh** (−13,6%), okres zwrotu **6,0 lat**, IRR 16%.

> **Komunikat HOMER:** `PV search space may be insufficient` — optymalizator osiągnął
> górną granicę zbioru (110 kWp). Ograniczeniem jest powierzchnia dachu, nie ekonomia.

---

## 3. Wariant A1 — awaria black-sky, 72 h (15–17 stycznia)

Energia wymagana w czasie awarii: **3 111 kWh** (obciążenie średnie 43,2 kW).

| # | PV [kW] | CHP | BESS | NPC | LCOE | CAPEX | **Godz. CHP** | **Produkcja CHP** | Paliwo |
|---|---|---|---|---|---|---|---|---|---|
| 1 | — | — | — | 1,16 M$ | 0,100 | 0 $ | — | — | — |
| 2 | 50 | — | — | 1,16 M$ | 0,101 | 49 138 $ | — | — | — |
| 3 | — | — | 1 | 1,21 M$ | 0,112 | 30 538 $ | — | — | — |
| 4 | 50 | — | 1 | 1,21 M$ | 0,113 | 79 138 $ | — | — | — |
| **5** | — | **100** | — | 1,60 M$ | 0,195 | 450 000 $ | **72,0** | **3 111 kWh** | 1 109 m³ |
| 6 | 50 | 100 | — | 1,60 M$ | 0,196 | 499 138 $ | **72,0** | 2 905 kWh | 1 060 m³ |
| 7 | — | 100 | 1 | 1,65 M$ | 0,207 | 480 645 $ | **72,0** | 3 111 kWh | 1 109 m³ |
| 8 | 50 | 100 | 1 | 1,65 M$ | 0,208 | 529 675 $ | **72,0** | 2 905 kWh | 1 060 m³ |

### Wynik zasadniczy

Jednostka kogeneracyjna pracuje **dokładnie 72,0 godziny** — czas identyczny z czasem
trwania awarii — wytwarzając **3 111 kWh**, tj. **dokładnie tyle, ile wynosi
zapotrzebowanie obiektu w tym okresie**. Zgodność z obliczeniem analitycznym
przeprowadzonym niezależnie (3 111 kWh) potwierdza poprawność modelu.

Zużycie gazu: **1 109 m³** na pokrycie pełnej awarii 72-godzinnej.

W wariantach z PV produkcja CHP spada do 2 905 kWh — różnicę 206 kWh pokrywa
instalacja fotowoltaiczna w godzinach dziennych.

---

## 4. Wariant A2 — seria pięciu przerw krótkotrwałych (łącznie 21 h)

| # | PV [kW] | CHP | BESS | NPC | LCOE | **Godz. CHP** | **Produkcja CHP** | Paliwo |
|---|---|---|---|---|---|---|---|---|
| 1 | — | — | — | 1,16 M$ | 0,100 | — | — | — |
| 2 | 50 | — | — | 1,16 M$ | 0,101 | — | — | — |
| **5** | — | **100** | — | 1,59 M$ | 0,194 | **21,0** | **895 kWh** | 320 m³ |
| 6 | 50 | 100 | — | 1,60 M$ | 0,195 | **21,0** | 850 kWh | 310 m³ |
| 7 | — | 100 | 1 | 1,65 M$ | 0,206 | **21,0** | 882 kWh | 317 m³ |
| 8 | 50 | 100 | 1 | 1,65 M$ | 0,207 | **21,0** | 789 kWh | 296 m³ |

Kogeneracja pracuje **dokładnie 21,0 godziny** — czas równy sumie pięciu przerw.
Produkcja 895 kWh, zużycie gazu 320 m³.

---

## 5. Wnioski

### 5.1. Instalacja fotowoltaiczna ograniczona wyłącznie powierzchnią dachu

Optymalizator wybiera maksymalną dopuszczoną moc (110 kWp) w wariancie bez awarii,
sygnalizując przy tym niewystarczający zakres przestrzeni poszukiwań. Oznacza to, że
**ekonomicznie uzasadniona jest instalacja większa niż fizycznie możliwa do
zainstalowania** na dostępnej powierzchni 2 110 m².

Uzysk jednostkowy 925 kWh/kWp odpowiada wartościom typowym dla Polski północno-zachodniej.

### 5.2. Kogeneracja pokrywa awarie w sposób precyzyjny

Zgodność czasu pracy jednostki z czasem trwania awarii (72,0 h oraz 21,0 h) oraz
zgodność produkcji energii z zapotrzebowaniem (3 111 kWh) potwierdzają, że model
odwzorowuje zdarzenia awaryjne poprawnie, a kogeneracja gazowa zapewnia **pełne
pokrycie obciążenia w obu badanych typach awarii**.

### 5.3. Problem doboru mocy jednostki kogeneracyjnej

W wariancie bez awarii jednostka pracuje jedynie **125 godzin rocznie** (1,4% czasu)
przy współpracy z PV, oraz 750 godzin bez PV. Dla porównania — w symulacjach testowych
(obiekt o zapotrzebowaniu 1 GWh) analogiczna jednostka pracowała **7 112 godzin**.

**Przyczyna:** jednostka 2G Aura 404 o mocy 100 kW jest dla obiektu o mocy średniej
40,5 kW **przewymiarowana około 2,5-krotnie**. Przy minimalnym obciążeniu roboczym
50% (50 kW) jednostka nie może pracować bez wytwarzania nadwyżek przekraczających
zapotrzebowanie obiektu.

Przeprowadzono test kontrolny z obniżeniem minimalnego obciążenia do 30% — czas pracy
nie uległ istotnej zmianie (125 h). Oznacza to, że ograniczeniem nie jest wyłącznie
reżim pracy silnika, lecz **relacja nakładów inwestycyjnych do skali obiektu**:
450 000 $ za jednostkę stanowi 26% całkowitego NPC wariantu bazowego (1,71 mln $).

**Wniosek:** dla szpitala powiatowego o zapotrzebowaniu 355 MWh/rok kogeneracja
uzasadniona jest **wyłącznie jako źródło zasilania awaryjnego**, nie zaś jako źródło
pracujące w podstawie obciążenia. Dobór jednostki powinien obejmować moc rzędu
**30–40 kW**, niedostępną w katalogu HOMER Pro — wymaga to pozyskania danych
bezpośrednio od producenta.

### 5.4. Konflikt kryterium ekonomicznego z wymogiem bezpieczeństwa — potwierdzony

Podobnie jak w symulacjach testowych, konfiguracją o najniższym NPC w wariantach
awaryjnych pozostaje układ **pozbawiony źródła rezerwowego** (1,16 mln $ wobec
1,60 mln $ dla wariantu z CHP). Koszt zapewnienia pełnego pokrycia awarii wynosi:

```
ΔNPC = 1,60 − 1,16 = 440 000 $
ΔLCOE = 0,195 − 0,100 = 0,095 $/kWh (wzrost o 95%)
```

Wzrost LCOE jest znacznie wyższy niż w symulacjach testowych (16%), co wynika
z przewymiarowania jednostki kogeneracyjnej względem skali obiektu.

---

## 6. Pliki modeli

| Plik | Wariant |
|---|---|
| `FINAL_Pyrzyce_A0_bez_awarii.homer` | A0 — praca normalna |
| `FINAL_Pyrzyce_A1_blacksky_72h.homer` | A1 — awaria 72 h |
| `FINAL_Pyrzyce_A2_serie_krotkich.homer` | A2 — seria przerw |

---

## 7. Zadania otwarte

| Zadanie | Uzasadnienie |
|---|---|
| Pozyskanie danych jednostki CHP 30–40 kW od producenta | Katalog HOMER nie zawiera jednostek gazowych poniżej 100 kW |
| Weryfikacja zapotrzebowania cieplnego | Wartość 700 MWh jest oszacowaniem — wniosek o audyt złożony |
| Analiza rozmieszczenia modułów w PV\*SOL | Potwierdzenie granicy 110 kWp |
| Rozszerzenie przestrzeni poszukiwań PV powyżej 110 kWp | Sprawdzenie, gdzie leży optimum ekonomiczne (wyłącznie dla porównania) |
| Ustalenie pojemności zbiornika istniejącego agregatu | Porównanie autonomii CHP z rozwiązaniem istniejącym |
