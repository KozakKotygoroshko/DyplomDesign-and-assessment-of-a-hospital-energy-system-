# Profile obciążenia obiektu referencyjnego — dokumentacja danych wejściowych

Pliki wejściowe do symulacji HOMER Pro. Oba profile mają rozdzielczość godzinową
(8760 wartości, krok 60 min) i obowiązują **wspólnie dla wszystkich trzech scenariuszy** —
przedmiotem różnicowania wariantów jest wyłącznie strona wytwórcza, nie strona odbioru.

| Plik | Szyna | Zastosowanie |
|---|---|---|
| `Profil_obciazenia_elektrycznego_szpital_8760h.csv` | elektryczna | Scenariusze 1, 2, 3 |
| `Profil_obciazenia_cieplnego_szpital_8760h.csv` | cieplna | **Scenariusz 3 (CHP)** |

> **Status danych:** profile mają charakter modelowy — zostały wygenerowane na podstawie
> wskaźników literaturowych i typowych krzywych obciążenia obiektów szpitalnych. Po
> ostatecznym wyborze obiektu referencyjnego i pozyskaniu danych rzeczywistych
> (faktury, odczyty licznikowe) profile podlegają weryfikacji i ewentualnej korekcie.

---

## 1. Profil obciążenia elektrycznego

### 1.1. Założenia

| Parametr | Wartość |
|---|---|
| Roczne zużycie energii elektrycznej | **1 000 MWh (1 GWh)** |
| Moc średnia | 114,16 kW |
| Moc szczytowa | 159,76 kW |
| Moc minimalna | 71,41 kW |
| Średnie zużycie dobowe | 2 739,7 kWh/d |
| **Współczynnik obciążenia (load factor)** | **0,715** |

### 1.2. Struktura kształtowania profilu

**Przebieg dobowy** — charakterystyczny dla obiektu pracującego w trybie ciągłym:
płytka dolina nocna (0,74–0,78 wartości średniej w godz. 2:00–4:00), narastanie
obciążenia od godz. 6:00, plateau w godzinach pracy diagnostyki i bloku operacyjnego
(1,18–1,24 wartości średniej w godz. 8:00–15:00), łagodny spadek wieczorny.

**Zmienność tygodniowa** — obniżenie o 7% w soboty i niedziele, wynikające z
ograniczenia zabiegów planowych i pracy poradni przy zachowaniu pełnej obsady
oddziałów łóżkowych.

**Zmienność sezonowa** — dwa maksima: zimowe (styczeń–luty, mnożnik 1,05–1,06;
wentylacja mechaniczna, oświetlenie, pompy obiegowe) oraz letnie (lipiec–sierpień,
mnożnik 1,06–1,07; chłodzenie stref czystych i sal operacyjnych). Minimum przypada
na maj (0,95).

**Zmienność losowa** — nałożony szum gaussowski o odchyleniu standardowym 2,5%,
odwzorowujący stochastyczny charakter załączania aparatury.

### 1.3. Uzasadnienie współczynnika obciążenia

Uzyskana wartość **LF = 0,715** mieści się w przedziale charakterystycznym dla
obiektów szpitalnych (0,6–0,7+). Dla porównania, syntetyczny profil generowany
przez wbudowaną bibliotekę HOMER Pro daje LF = 0,22 — wartość typową dla budynku
mieszkalnego, prowadzącą do zawyżenia mocy szczytowej o ponad 300% i w konsekwencji
do przewymiarowania agregatu, magazynu BESS oraz przekształtników.

---

## 2. Profil obciążenia cieplnego

### 2.1. Założenia

| Parametr | Wartość |
|---|---|
| Roczne zapotrzebowanie na ciepło użytkowe | **1 800 MWh** |
| Moc średnia | 205,48 kW |
| Moc szczytowa | 537,22 kW |
| Moc minimalna | 13,43 kW |
| Średnie zużycie dobowe | 4 931,5 kWh/d |
| Współczynnik obciążenia | 0,382 |

### 2.2. Struktura zapotrzebowania

| Składowa | Udział | Energia [MWh/rok] | Charakter |
|---|---|---|---|
| Centralne ogrzewanie (c.o.) | 63,9% | 1 150 | sezonowy, sterowany stopniodniami |
| Ciepła woda użytkowa (c.w.u.) | 25,0% | 450 | całoroczny, stały rozbiór |
| Sterylizacja i pralnia | 11,1% | 200 | dni robocze, godz. 6:00–18:00 |

**Centralne ogrzewanie** rozdzielono na miesiące proporcjonalnie do liczby
stopniodni grzewczych, wyznaczonych dla temperatury bazowej 15°C i normowych
średnich miesięcznych temperatur zewnętrznych dla Szczecina. Przebieg dobowy
uwzględnia nocne osłabienie oraz poranne dogrzanie budynku.

**C.w.u.** odwzorowano dwoma szczytami rozbioru — porannym (7:00–9:00) i wieczornym
(18:00–20:00), przy zachowaniu niezerowego poboru w godzinach nocnych.

**Sterylizacja i pralnia** ograniczone do dni roboczych, z maksimum w godzinach
8:00–15:00 (cykle autoklawów, pranie technologiczne).

### 2.3. Bilans miesięczny

| Miesiąc | Energia [MWh] | Moc średnia [kW] | Moc szczytowa [kW] |
|---|---|---|---|
| I | 279,4 | 375,5 | 537,2 |
| II | 244,6 | 364,0 | 516,3 |
| III | 221,1 | 297,2 | 433,8 |
| IV | 143,8 | 199,7 | 312,2 |
| V | 77,5 | 104,1 | 191,3 |
| VI | 53,0 | 73,6 | 157,0 |
| VII | 55,0 | 74,0 | 156,8 |
| VIII | 56,0 | 75,2 | 155,4 |
| IX | 64,0 | 88,9 | 176,1 |
| X | 139,2 | 187,1 | 295,7 |
| XI | 206,0 | 286,1 | 415,4 |
| XII | 260,5 | 350,2 | 508,2 |

### 2.4. Znaczenie letniej bazy cieplnej dla doboru CHP

Kluczowy dla ekonomiki układu kogeneracyjnego jest fakt, że zapotrzebowanie na ciepło
**nie zanika poza sezonem grzewczym**. W miesiącach letnich (czerwiec–sierpień)
utrzymuje się na poziomie 73–75 kW mocy średniej, co odpowiada ok. 36% średniej rocznej.
Źródłem tej bazy są c.w.u. oraz procesy technologiczne (sterylizacja, pralnia).

Wartość ta stanowi bezpośrednią przesłankę doboru mocy cieplnej jednostki
kogeneracyjnej: moduł CHP dobrany do letniej bazy cieplnej może pracować w reżimie
ciągłym przez cały rok z wysokim wykorzystaniem mocy, bez konieczności zrzutu ciepła
do otoczenia. Nadwyżkowe zapotrzebowanie w sezonie grzewczym pokrywane jest przez
kocioł szczytowy.

---

## 3. Format plików i import do HOMER Pro

Pliki zapisano jako jedna kolumna wartości mocy w kW, bez nagłówka, separator
dziesiętny — kropka, 8760 wierszy (od 1 stycznia godz. 0:00 do 31 grudnia godz. 23:00).

**Ścieżka importu w HOMER Pro:**

- profil elektryczny: `LOAD → Electric #1 → Import a load from a time series file → Import...`
- profil cieplny: `LOAD → Thermal #1 → Import a load from a time series file → Import...`

Po zaimportowaniu należy zweryfikować zgodność wartości `Average (kWh/day)`
oraz `Peak (kW)` z danymi w tabelach powyżej.
