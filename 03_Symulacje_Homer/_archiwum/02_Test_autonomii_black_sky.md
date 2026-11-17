# Test przetrwania (Resilience Test) — awaria typu *black-sky*

Symulacja przeprowadzona w HOMER Pro x64 3.18.4 dla obiektu modelowego w Szczecinie.
Celem testu było wyznaczenie zdolności obiektu do pracy w trybie wyspowym w warunkach
długotrwałej awarii sieci nadrzędnej.

---

## 1. Definicja zdarzenia awaryjnego

| Parametr | Wartość | Uzasadnienie doboru |
|---|---|---|
| Czas trwania | **72 godziny** | Górna granica przedziału przyjętego w metodyce (24–72 h) |
| Termin | **15–17 stycznia** | Miesiąc o minimalnym zasobie słonecznym (GHI 0,73 kWh/m²/d) |
| Charakter | Całkowity zanik zasilania sieciowego | Scenariusz *black-sky hazard* / HILP |
| Dopuszczalny niedobór mocy | podniesiony z 0% na 10% | Warunek konieczny — przy 0% optymalizator odrzuca wszystkie warianty jako niedopuszczalne, uniemożliwiając pomiar skali niedoboru |

Zdarzenie zamodelowano poprzez import szeregu czasowego (8760 wartości) do modułu
`Grid → Scheduled Rates → Reliability → Import from a time series data file`.

Plik: `Awaria_blacksky_72h_styczen.csv`

> **Konwencja zapisu w HOMER (ustalona doświadczalnie):** wartość **1 = sieć dostępna**,
> **0 = awaria**. Konwencja jest odwrotna do intuicyjnej — przy pierwszej próbie importu
> pliku z zapisem odwrotnym program zinterpretował dane jako awarię trwającą cały rok
> z wyjątkiem 72 godzin.

Wybór okresu zimowego stanowi celowe przyjęcie **przypadku najbardziej niekorzystnego**:
w styczniu produkcja fotowoltaiczna osiąga minimum roczne, wskutek czego wsparcie ze
strony instalacji PV jest pomijalne, a obciążenie cieplne — maksymalne.

---

## 2. Wyniki — zestawienie porównawcze

Poniższa tabela zestawia wszystkie osiem konfiguracji obliczonych przez optymalizator
przy zdefiniowanej awarii 72-godzinnej.

| # | PV [kW] | Agregat [kW] | BESS [szt.] | NPC | LCOE [$/kWh] | CAPEX | Godziny pracy agregatu | Produkcja agregatu [kWh] | Zużycie paliwa [L] |
|---|---|---|---|---|---|---|---|---|---|
| 1 | — | — | — | **3,08 M$** | **0,100** | 0 $ | — | — | — |
| 2 | 150 | — | — | 3,10 M$ | 0,101 | 147 000 $ | — | — | — |
| 3 | — | — | 2 | 3,19 M$ | 0,108 | 61 500 $ | — | — | — |
| 4 | 150 | — | 2 | 3,20 M$ | 0,109 | 207 000 $ | — | — | — |
| 5 | — | 180 | — | 3,30 M$ | 0,116 | 216 000 $ | **72,0** | 8 762 | 2 425 |
| 6 | 150 | 180 | — | 3,31 M$ | 0,117 | 363 000 $ | **72,0** | 8 075 | 2 263 |
| 7 | — | 180 | 2 | 3,41 M$ | 0,124 | 277 500 $ | **72,0** | 8 654 | 2 399 |
| 8 | 150 | 180 | 2 | 3,42 M$ | 0,125 | 422 000 $ | **72,0** | 7 966 | 2 237 |

**Obserwacja podstawowa:** we wszystkich konfiguracjach wyposażonych w agregat czas jego
pracy wynosi dokładnie **72,0 godziny** — wartość identyczną z czasem trwania awarii.
Potwierdza to poprawność zamodelowania zdarzenia: jednostka uruchamiana jest wyłącznie
w okresie braku zasilania sieciowego.

---

## 3. Energia niedostarczona (EENS) — pomiar zasadniczy

### 3.1. Wariant bez źródeł rezerwowych (sama sieć)

![[Grafika/Autonomia_05_Podsumowanie_zuzycia.png]]

| Wskaźnik | Wartość |
|---|---|
| Zakup energii z sieci | 991 238 kWh/rok |
| Obciążenie pokryte | 991 238 kWh/rok |
| **Energia niedostarczona (Unmet Electric Load)** | **8 762 kWh (0,876%)** |
| **Niedobór mocy (Capacity Shortage)** | **9 639 kWh (0,964%)** |
| Udział OZE | 0% |

Interpretacja: przy braku jakiegokolwiek źródła rezerwowego obiekt pozostaje **całkowicie
pozbawiony zasilania przez pełne 72 godziny**. Wartość 8 762 kWh odpowiada energii, której
szpital nie otrzymał — w praktyce oznacza to unieruchomienie bloku operacyjnego, oddziału
intensywnej terapii oraz utratę zawartości chłodni krwi i szczepionek.

### 3.2. Wariant PV 150 kW + BESS 200 kWh (bez agregatu)

![[Grafika/Autonomia_07_Engineering_BESS.png]]

| Wskaźnik | Wartość |
|---|---|
| Produkcja PV | 139 687 kWh/rok (13,9%) |
| Zakup z sieci | 865 010 kWh/rok (86,1%) |
| **Energia niedostarczona** | **7 966 kWh (0,797%)** |
| Niedobór mocy | 9 393 kWh (0,939%) |
| Udział OZE | 4,50% |

**Kluczowy wynik pracy:** układ PV + BESS pokrywa jedynie **796 kWh z 8 762 kWh deficytu,
co odpowiada 9,1%** zapotrzebowania w czasie awarii. Pozostałe 91% energii pozostaje
niedostarczone.

### 3.3. Warianty z agregatem prądotwórczym

| Konfiguracja | Produkcja agregatu | Paliwo | Energia niedostarczona |
|---|---|---|---|
| Agregat 180 kW | 8 762 kWh | 2 425 L | **0 kWh** |
| PV 150 + agregat 180 kW | 8 075 kWh | 2 263 L | **0 kWh** |
| PV 150 + agregat + BESS 200 kWh | 7 966 kWh | 2 237 L | **0 kWh** |

Wszystkie warianty wyposażone w agregat zapewniają pełne pokrycie obciążenia.

---

## 4. Analiza wyników

### 4.1. Dlaczego PV i BESS nie zapewniają autonomii zimą

Uzyskany wynik (pokrycie 9,1% deficytu) wynika z dwóch niezależnych ograniczeń
występujących jednocześnie:

**Ograniczenie zasobu.** W styczniu napromieniowanie wynosi 0,73 kWh/m²/dobę wobec
4,96 kWh/m²/dobę w maju — stosunek **1:6,8**. Instalacja 150 kWp wytwarza w tym okresie
kilkanaście procent mocy nominalnej, przy czym wyłącznie w godzinach 9:00–15:00.

**Ograniczenie pojemności.** Magazyn 200 kWh przy minimalnym stanie naładowania 40%
udostępnia 120 kWh energii użytecznej. Przy średnim obciążeniu styczniowym rzędu 120 kW
odpowiada to **około jednej godzinie pracy autonomicznej** — wobec wymaganych 72 godzin.

Zestawienie tych dwóch faktów prowadzi do wniosku, że **magazyn bateryjny w rozpatrywanej
skali nie stanowi źródła autonomii długoterminowej**, lecz wyłącznie element pomostowy
zapewniający ciągłość zasilania w klasie 0,5 s do czasu uruchomienia źródła sterowalnego.
Wniosek ten jest zgodny z rolą przypisaną magazynom w podrozdziale 3.4.

### 4.2. Konflikt kryterium ekonomicznego z wymogiem bezpieczeństwa

Konfiguracją o najniższym NPC (3,08 mln $) pozostaje **wariant pozbawiony jakiegokolwiek
źródła rezerwowego** — ten sam, który generuje 8 762 kWh energii niedostarczonej.
Optymalizator, minimalizując koszt bieżący netto, uznaje **niedostarczenie energii do
szpitala za rozwiązanie tańsze** niż zakup agregatu za 216 000 $.

Wynik ten stanowi ilościowy dowód tezy metodycznej pracy: **kryterium najniższego NPC jest
niewystarczające dla obiektów infrastruktury krytycznej**. Ocena wielokryterialna musi
obejmować energię niedostarczoną jako parametr o charakterze ograniczenia twardego,
nie zaś jako składnik funkcji celu.

Koszt zapewnienia pełnego pokrycia wynosi w analizowanym przypadku:

```
ΔNPC = 3,30 M$ − 3,08 M$ = 220 000 $
ΔLCOE = 0,116 − 0,100 = 0,016 $/kWh (wzrost o 16%)
```

Jest to wymierna cena bezpieczeństwa energetycznego obiektu.

### 4.3. Zależność od łańcucha dostaw paliwa

Pokrycie 72-godzinnej awarii wymaga **2 425 litrów oleju napędowego**. Przy typowej
pojemności zbiornika przyagregatowego rzędu 1 000–1 500 l oznacza to konieczność
uzupełnienia paliwa w trakcie trwania zdarzenia — w warunkach, w których transport
drogowy może być niemożliwy.

Zależność ta stanowi bezpośrednie potwierdzenie ograniczenia opisanego w podrozdziale 3.2:
autonomia układu klasycznego nie jest determinowana przez parametry elektryczne, lecz
przez **logistykę zaopatrzenia w paliwo**.

---

## 5. Materiał ilustracyjny

### Bilans elektryczny — produkcja miesięczna

![[Grafika/Autonomia_06_Engineering_PV.png]]

### Współpraca z siecią elektroenergetyczną

![[Grafika/Autonomia_08_Engineering_Siec.png]]

### Przekształtnik i kocioł szczytowy

![[Grafika/Autonomia_09_Engineering_Konwerter_Kociol.png]]

### Przepływy pieniężne w cyklu życia

![[Grafika/Autonomia_10_Cashflow.png]]

---

## 6. Wnioski

1. **Układ bez źródła rezerwowego** traci zasilanie na pełne 72 godziny; energia
   niedostarczona wynosi 8 762 kWh. Wariant niedopuszczalny dla obiektu szpitalnego.

2. **Układ PV + BESS** w warunkach zimowych pokrywa 9,1% zapotrzebowania podczas awarii.
   Magazyn zapewnia autonomię rzędu jednej godziny — pełni funkcję pomostową, nie zaś
   źródła podtrzymania długoterminowego.

3. **Układ z agregatem** zapewnia pełne pokrycie obciążenia kosztem 2 425 l paliwa oraz
   wzrostu LCOE o 16%. Autonomia ograniczona jest pojemnością zbiornika paliwa.

4. **Kryterium NPC prowadzi do rozwiązania niedopuszczalnego** — optymalizator wybiera
   wariant generujący niedobór energii. Konieczne jest wprowadzenie ograniczenia twardego
   `Unmet Load = 0` lub oceny wielokryterialnej z wagą dla wskaźnika niezawodności.

---

## 7. Zadania otwarte

| Zadanie | Uzasadnienie |
|---|---|
| Dobór **gazowej** jednostki CHP z katalogu HOMER | Obecny `Autosize Genset` pracuje wyłącznie na oleju napędowym, przez co kogeneracja nie jest dysponowana; zasilanie gazem sieciowym eliminuje ponadto zależność od transportu paliwa |
| Powtórzenie testu dla okresu **letniego** | Weryfikacja hipotezy o istotnie wyższym udziale PV poza sezonem zimowym |
| Symulacja **serii przerw krótkotrwałych** wg statystyki SAIDI/SAIFI | Wyznaczenie rocznych wskaźników niezawodności |
| Zwiększenie pojemności BESS w przestrzeni poszukiwań | Określenie pojemności granicznej zapewniającej autonomię 60 min dla odbiorów klasy 0,5 s |
| Ograniczenie testu do **obciążeń krytycznych** (30% mocy szczytowej) | Odwzorowanie rzeczywistego trybu awaryjnego z odrzuceniem obciążeń nieistotnych |

---

## Pliki źródłowe

- Model: `Scenariusz_3_TEST_AUTONOMII_blacksky_72h` (plik `.homer`)
- Szereg czasowy awarii: `Awaria_blacksky_72h_styczen.csv`
- Raport pełny HOMER: `Raport_HOMER_Test_autonomii_blacksky_72h.docx` (14 stron)
- Grafika: folder `Grafika/`
