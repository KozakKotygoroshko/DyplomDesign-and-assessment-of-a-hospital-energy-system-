# Porównanie trzech konfiguracji — wyniki kompletne

Seria uzupełniona o **agregat prądotwórczy**, pominięty w pierwszym podejściu.
Dopiero teraz możliwe jest porównanie wszystkich trzech konfiguracji zgodnie
ze szkieletem pracy.

Data: 19 września 2026. Obiekt: Szpital Powiatowy w Pyrzycach (355 MWh/rok).

---

## 1. Konfiguracje zidentyfikowane w tabeli wyników

Optymalizator dobrał moc agregatu automatycznie: **63,0 kW** (`Autosize Genset`),
co odpowiada 111% mocy szczytowej obiektu (56,72 kW).

| Oznaczenie | Architektura | Wiersz w tabeli HOMER |
|---|---|---|
| **odniesienie** | sama sieć | brak źródeł rezerwowych |
| **K1 — Baza** | sieć + agregat 63 kW | Gen 63,0 |
| **K2 — Hybryda** | sieć + agregat + PV 50 kW + BESS 100 kWh | PV 50 · Gen 63,0 · 100LI 1 |
| **K3 — Mikrosieć** | sieć + PV 50 kW + CHP 100 kW | PV 50 · Au404 100 |

---

## 2. Wariant A0 — praca normalna (bez awarii)

| Konfiguracja | NPC | LCOE | CAPEX | IRR | Zwrot | **Czas pracy źródła** |
|---|---|---|---|---|---|---|
| **PV 110 kW** (optimum) | **1,59 M$** | **0,190** | 107 350 $ | **16%** | **6,0 lat** | — |
| K2 — PV 110 + agregat | 1,62 M$ | 0,195 | 138 850 $ | 12% | 7,7 | **0 h** |
| PV 110 + BESS | 1,63 M$ | 0,202 | 133 588 $ | 12% | 7,5 | — |
| **K2 — PV 110 + agregat + BESS** | **1,65 M$** | **0,207** | 165 088 $ | 9,2% | 9,3 | **0 h** |
| odniesienie (sama sieć) | 1,71 M$ | 0,220 | 0 $ | — | — | — |
| **K1 — agregat 63 kW** | **1,73 M$** | **0,225** | **31 500 $** | — | — | **0 h** |
| **K3 — PV 110 + CHP 100 kW** | **2,02 M$** | **0,281** | 557 350 $ | — | — | **125 h** |
| K3 — CHP bez PV | 2,13 M$ | 0,312 | 450 000 $ | — | — | 753 h |

### Obserwacja zasadnicza

**Agregat prądotwórczy pracuje zero godzin w roku.** Przy nieprzerwanej dostępności
sieci nie zostaje uruchomiony ani razu, stanowiąc wyłącznie obciążenie kapitałowe:

```
K1 wobec odniesienia:  NPC +20 000 $  ·  LCOE +0,005 $/kWh  ·  0 kWh wyprodukowanych
```

Jest to ilościowe potwierdzenie tezy z podrozdziału 3.2 o pasywnym charakterze
klasycznego zasilania rezerwowego.

**Jednostka kogeneracyjna** pracuje 125 godzin (przy współpracy z PV) lub 753 godziny
(bez PV) — w obu przypadkach znikomo wobec 8 760 godzin roku. Przyczyną jest
przewymiarowanie 2,5-krotne względem obciążenia obiektu.

**Konfiguracją optymalną w warunkach normalnych** jest układ z samą instalacją PV
o mocy 110 kWp: LCOE 0,190 $/kWh (−13,6% wobec odniesienia), okres zwrotu 6,0 lat,
IRR 16%. Układ ten nie zapewnia jednak żadnej autonomii w razie awarii.

---

## 3. Wariant A1 — awaria black-sky, 72 godziny

Zapotrzebowanie obiektu w czasie awarii: **3 111 kWh**.

| Konfiguracja | NPC | LCOE | CAPEX | Czas pracy źródła | Produkcja | Paliwo |
|---|---|---|---|---|---|---|
| odniesienie (sama sieć) | 1,16 M$ | 0,100 | 0 $ | — | — | — |
| **K1 — agregat 63 kW** | **1,20 M$** | **0,109** | **31 500 $** | **72,0 h** | **3 111 kWh** | **944 l ON** |
| K1 + PV 50 kW | 1,20 M$ | 0,110 | 80 638 $ | 72,0 h | 2 889 kWh | 891 l |
| **K2 — agregat + PV + BESS** | **1,26 M$** | **0,121** | **110 638 $** | **72,0 h** | **2 834 kWh** | **879 l** |
| **K3 — CHP 100 kW + PV** | **1,60 M$** | **0,196** | **499 138 $** | **72,0 h** | **2 905 kWh** | **1 060 m³ gazu** |

### Obserwacja zasadnicza

**Wszystkie trzy konfiguracje pokrywają awarię w całości.** Czas pracy źródła
sterowalnego wynosi w każdym przypadku dokładnie 72,0 godziny, a suma produkcji
odpowiada zapotrzebowaniu obiektu.

Różnica dotyczy **kosztu** i **rodzaju paliwa**:

```
K1 (agregat)  :  31 500 $ CAPEX  ·  944 litry oleju napędowego
K3 (CHP)      : 499 138 $ CAPEX  ·  1 060 m³ gazu sieciowego

Stosunek nakładów: 1 : 15,8
```

---

## 4. Wariant A2 — seria pięciu przerw (łącznie 21 h)

Zapotrzebowanie: **895 kWh**.

| Konfiguracja | NPC | LCOE | CAPEX | Czas pracy | Produkcja | Paliwo |
|---|---|---|---|---|---|---|
| odniesienie | 1,16 M$ | 0,100 | 0 $ | — | — | — |
| **K1 — agregat 63 kW** | **1,19 M$** | **0,106** | **31 500 $** | **21,0 h** | **895 kWh** | **272 l ON** |
| K1 + PV 50 kW | 1,19 M$ | 0,107 | 80 638 $ | 21,0 h | 850 kWh | 262 l |
| **K2 — agregat + PV + BESS** | **1,24 M$** | **0,119** | **110 638 $** | **21,0 h** | **596 kWh** | **202 l** |
| **K3 — CHP 100 kW + PV** | **1,60 M$** | **0,195** | **499 138 $** | **21,0 h** | **850 kWh** | **310 m³ gazu** |

W wariancie A2 konfiguracja K2 wykazuje najniższe zużycie paliwa (202 l wobec 272 l
w K1) — magazyn bateryjny przejmuje część krótkich przerw, ograniczając liczbę
uruchomień agregatu.

---

## 5. Wnioski — rewizja wcześniejszych ustaleń

### 5.1. Pod względem ekonomicznym agregat prądotwórczy wygrywa jednoznacznie

Wprowadzenie agregatu do modelu **zmienia wnioski sformułowane wcześniej**.
Przy nakładach 31 500 $ zapewnia on pełne pokrycie obu badanych typów awarii —
przy kosztach niższych o **rząd wielkości** niż jednostka kogeneracyjna.

| Kryterium ekonomiczne | K1 | K3 | Stosunek |
|---|---|---|---|
| CAPEX | 31 500 $ | 450 000 $ | **1 : 14,3** |
| NPC (A1) | 1,20 M$ | 1,60 M$ | 1 : 1,33 |
| LCOE (A1) | 0,109 | 0,195 | 1 : 1,79 |

**Dla szpitala o zapotrzebowaniu 355 MWh/rok kogeneracja nie znajduje uzasadnienia
ekonomicznego jako źródło zasilania awaryjnego.** Jest to wniosek przeciwny do
uzyskanego w symulacjach testowych, gdzie obiekt o zapotrzebowaniu 1 GWh/rok
pozwalał jednostce CHP pracować 7 112 godzin rocznie i generować oszczędności.

### 5.2. Rozstrzygające pozostaje kryterium logistyczne, nie ekonomiczne

Pokrycie awarii 72-godzinnej wymaga **944 litrów oleju napędowego**.

| Pojemność zbiornika | Pokrycie 72 h | Margines |
|---|---|---|
| 500 l | **NIE** — 38 h | — |
| **1 000 l** | **TAK** — 76 h | **56 litrów (6%)** |
| 1 500 l | TAK — 114 h | 556 l |
| 2 000 l | TAK — 152 h | 1 056 l |

Przy typowej pojemności 1 000 litrów margines wynosi zaledwie **6%**. Oznacza to,
że pokrycie pełnej awarii black-sky jest możliwe **wyłącznie przy założeniu zbiornika
całkowicie napełnionego w chwili wystąpienia zdarzenia**. Każde wcześniejsze użycie
agregatu — choćby na próbę okresową — narusza ten warunek.

Kogeneracja gazowa nie podlega temu ograniczeniu: paliwo dostarczane jest siecią
podziemną, niezależną od transportu drogowego, a czas pracy ograniczony jest wyłącznie
ciągłością dostaw gazu.

### 5.3. Właściwe sformułowanie wniosku dla pracy

Zestawienie wyników prowadzi do wniosku o charakterze warunkowym:

> **Jeżeli** kryterium oceny stanowi koszt, konfiguracja K1 (sieć + agregat) jest
> rozwiązaniem optymalnym dla obiektu tej skali.
>
> **Jeżeli** kryterium stanowi odporność na zdarzenia typu *black-sky*, w których
> dostawa paliwa płynnego może okazać się niemożliwa, rozstrzygająca staje się
> niezależność od transportu drogowego — cecha, której agregat nie posiada.

Wniosek ten jest **mocniejszy** od pierwotnego, ponieważ nie pomija najtańszej
alternatywy, lecz wskazuje warunki, w których droższe rozwiązanie znajduje
uzasadnienie.

### 5.4. Rola magazynu bateryjnego — potwierdzona

W wariancie A2 konfiguracja z BESS zużywa **202 litry zamiast 272** (−26%).
Magazyn przejmuje krótkie przerwy, ograniczając liczbę uruchomień agregatu.
Potwierdza to rolę przypisaną magazynom w podrozdziale 3.4 — element pomostowy
ograniczający pracę niskoobciążeniową źródła sterowalnego.

---

## 6. Zestawienie zbiorcze

| Wskaźnik | odniesienie | K1 Baza | K2 Hybryda | K3 Mikrosieć |
|---|---|---|---|---|
| **CAPEX** | 0 $ | **31 500 $** | 110 638 $ | 499 138 $ |
| **NPC (A1)** | 1,16 M$ | **1,20 M$** | 1,26 M$ | 1,60 M$ |
| **LCOE (A1)** | 0,100 | **0,109** | 0,121 | 0,196 |
| **Pokrycie awarii A1** | 0% | **100%** | **100%** | **100%** |
| **Pokrycie awarii A2** | 0% | **100%** | **100%** | **100%** |
| Paliwo (A1) | — | 944 l ON | 879 l ON | 1 060 m³ gazu |
| Paliwo (A2) | — | 272 l ON | **202 l ON** | 310 m³ gazu |
| Zależność od transportu | — | **wysoka** | **wysoka** | **brak** |
| **Praca w warunkach normalnych (A0)** | — | **0 h/rok** | **0 h/rok** | **125 h/rok**¹ |
| Udział OZE | 0% | 0% | 4,0% | 4,0% |

¹ Wartość dla konfiguracji z PV. Bez PV jednostka pracuje 753 h/rok. W obu przypadkach
znikomo wobec 8 760 godzin roku — przyczyną jest przewymiarowanie 2,5-krotne.

---

## 7. Pliki modeli

| Plik | Wariant | Zawiera agregat |
|---|---|---|
| `FINAL_Pyrzyce_A0_bez_awarii.homer` | A0 | ✅ tak |
| `FINAL_Pyrzyce_A1_blacksky_72h.homer` | A1 | ✅ tak |
| `FINAL_Pyrzyce_A2_serie_krotkich.homer` | A2 | ✅ tak |

---

## 8. Zadania otwarte

| Zadanie | Uzasadnienie |
|---|---|
| Pozyskanie danych jednostki CHP 30–40 kW od producenta | Katalog HOMER nie zawiera jednostek gazowych poniżej 100 kW |
| Ustalenie rzeczywistej pojemności zbiornika agregatu | Wartość rozstrzygająca dla oceny konfiguracji K1 |
| Weryfikacja zapotrzebowania cieplnego | 700 MWh jest oszacowaniem — wniosek o audyt złożony |
| Wygenerowanie raportów HOMER w formacie DOCX | Licencja Evaluation wygasa 26.09.2026 |
| Analiza rozmieszczenia modułów w PV\*SOL | Potwierdzenie granicy 110 kWp |
