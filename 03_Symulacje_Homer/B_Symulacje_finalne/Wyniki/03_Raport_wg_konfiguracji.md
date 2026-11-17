# Analiza trzech konfiguracji systemu zasilania — Szpital Powiatowy w Pyrzycach

Raport uporządkowany **według konfiguracji**: dla każdej omówiono kolejno pracę normalną
oraz oba badane typy awarii. Wnioski zestawiono na końcu.

Wersja do druku: `RAPORT_Analiza_trzech_konfiguracji.docx` (16 stron, wykresy i tabele).

---

## Dane wejściowe

| Parametr | Wartość | Źródło |
|---|---|---|
| Zużycie energii elektrycznej | 355 MWh/rok | dokumentacja przetargowa |
| Moc średnia / szczytowa | 40,53 / 56,72 kW | profil godzinowy |
| Współczynnik obciążenia | 0,715 | — |
| Odbiory krytyczne (30% P.szcz.) | 17,0 kW | § 42 Rozp. MZ |
| Powierzchnia dachu | 2 110,43 m² | Geoportal — pomiar własny |
| Graniczna moc PV | 110 kWp | oszacowanie z powierzchni |
| Zasób słoneczny (GHI) | 2,72 kWh/m²/d | NASA POWER, 42 lata |

| Wariant | Zdarzenie | Zapotrzebowanie |
|---|---|---|
| **A0** | praca normalna | 355 MWh/rok |
| **A1** | black-sky 72 h (15–17 stycznia) | 3 111 kWh |
| **A2** | seria pięciu przerw, łącznie 21 h | 895 kWh |

---

## 1. Konfiguracja K1 — układ bazowy (sieć + agregat 63 kW)

### 1.1. A0 — praca normalna

| Wskaźnik | Odniesienie | K1 | Różnica |
|---|---|---|---|
| NPC | 1,71 M$ | 1,73 M$ | +20 000 $ |
| LCOE | 0,220 | 0,225 | +0,005 |
| CAPEX | 0 $ | 31 500 $ | +31 500 $ |
| **Czas pracy agregatu** | — | **0 h** | — |

Agregat nie zostaje uruchomiony ani razu. Stanowi wyłącznie obciążenie kapitałowe.

### 1.2. A1 — black-sky 72 h

| Wskaźnik | Wartość |
|---|---|
| Czas pracy agregatu | **72,0 h** |
| Energia wyprodukowana | **3 111 kWh** |
| Pokrycie zapotrzebowania | **100%** |
| **Zużycie paliwa** | **944 l ON** |
| NPC / LCOE | 1,20 M$ / 0,109 |

| Zbiornik | Czas pracy | Pokrycie 72 h | Margines |
|---|---|---|---|
| 500 l | 38,1 h | **NIE — 53%** | — |
| **1 000 l (typowa)** | 76,3 h | TAK | **56 l (6%)** |
| 1 500 l | 114,4 h | TAK | 556 l (59%) |
| 2 000 l | 152,5 h | TAK | 1 056 l (112%) |

Margines 6% oznacza, że warunek pokrycia spełniony jest wyłącznie przy zbiorniku
całkowicie napełnionym w chwili zdarzenia.

### 1.3. A2 — seria przerw krótkotrwałych

| Wskaźnik | Wartość |
|---|---|
| Czas pracy agregatu | **21,0 h** |
| Energia wyprodukowana | 895 kWh |
| Pokrycie | **100%** |
| Zużycie paliwa | 272 l |

Zapas typowego zbiornika pokrywa to zapotrzebowanie z trzykrotnym marginesem.

---

## 2. Konfiguracja K2 — układ hybrydowy (+ PV + BESS)

### 2.1. A0 — praca normalna

| Wskaźnik | K2 | Odniesienie |
|---|---|---|
| NPC | 1,65 M$ | 1,71 M$ |
| LCOE | **0,207** | 0,220 |
| CAPEX | 110 638 $ | 0 $ |
| IRR / zwrot | 9,2% / 9,3 lat | — |
| Udział OZE | 8,63% | 0% |
| **Czas pracy agregatu** | **0 h** | — |

Wariant najtańszy w A0 to **sama PV 110 kWp**: LCOE 0,190, zwrot 6,0 lat, IRR 16% —
przy zerowej autonomii.

### 2.2. A1 — black-sky 72 h

| Wskaźnik | Wartość |
|---|---|
| Czas pracy agregatu | 72,0 h |
| Energia z agregatu | 2 834 kWh |
| Wkład PV | 277 kWh |
| Pokrycie | **100%** |
| Zużycie paliwa | **879 l (−65 l, −6,9%)** |

Wkład PV niewielki — napromieniowanie styczniowe 0,73 kWh/m²/d (15% wartości majowej).
Ograniczenie zbiornika pozostaje aktualne.

### 2.3. A2 — seria przerw

| Wskaźnik | K2 | K1 | Różnica |
|---|---|---|---|
| Czas pracy | 21,0 h | 21,0 h | — |
| Energia z agregatu | 596 kWh | 895 kWh | −299 kWh |
| Pokrycie | 100% | 100% | — |
| **Zużycie paliwa** | **202 l** | 272 l | **−70 l (−26%)** |

Tu magazyn ujawnia właściwą funkcję — przejmuje część przerw w całości.

---

## 3. Konfiguracja K3 — mikrosieć (PV + CHP gazowy 100 kW)

### 3.1. A0 — praca normalna

| Wskaźnik | K3 (PV+CHP) | K3 (CHP bez PV) | Odniesienie |
|---|---|---|---|
| NPC | 2,02 M$ | 2,13 M$ | 1,71 M$ |
| LCOE | 0,281 | 0,312 | 0,220 |
| CAPEX | 557 350 $ | 450 000 $ | 0 $ |
| **Czas pracy CHP** | **125 h** | 753 h | — |

Przewymiarowanie ok. 2,5-krotne (100 kW wobec 40,53 kW mocy średniej). Test z obniżeniem
minimalnego obciążenia 50% → 30% nie zmienił wyniku.

### 3.2. A1 — black-sky 72 h

| Wskaźnik | Wartość |
|---|---|
| Czas pracy CHP | **72,0 h** |
| Energia wyprodukowana | 2 905 kWh |
| Wkład PV | 206 kWh |
| Pokrycie | **100%** |
| Zużycie paliwa | **1 060 m³ gazu** |
| Dostawa paliwa | **sieć gazowa — bez transportu drogowego** |

### 3.3. A2 — seria przerw

| Wskaźnik | Wartość |
|---|---|
| Czas pracy CHP | 21,0 h |
| Energia | 850 kWh |
| Pokrycie | **100%** |
| Zużycie paliwa | 310 m³ |

Dla zdarzeń krótkotrwałych przewaga logistyczna nie ujawnia się.

---

## 4. Zestawienie zbiorcze

| Wskaźnik | K1 | K2 | K3 |
|---|---|---|---|
| CAPEX | 31 500 $ | 110 638 $ | 499 138 $ |
| NPC (A0) | 1,73 M$ | 1,65 M$ | 2,02 M$ |
| LCOE (A0) | 0,225 | 0,207 | 0,281 |
| NPC (A1) | 1,20 M$ | 1,26 M$ | 1,60 M$ |
| **Pokrycie A1** | **100%** | **100%** | **100%** |
| **Pokrycie A2** | **100%** | **100%** | **100%** |
| Paliwo A1 | 944 l ON | 879 l ON | 1 060 m³ gazu |
| Paliwo A2 | 272 l ON | 202 l ON | 310 m³ gazu |
| Czas pracy (A0) | 0 h | 0 h | 125 h |
| Udział OZE | 0% | 8,63% | 8,65% |
| **Zależność od transportu** | wysoka | wysoka | **brak** |

Wykresy: `../Grafika/F1_CAPEX_porownanie.png`, `F2_LCOE_warianty.png`,
`F3_Zbiornik_paliwa.png`, `F4_Godziny_A0.png`, `F5_Paliwo.png`.

---

## 5. Wnioski

**5.1.** Wszystkie trzy konfiguracje pokrywają oba typy awarii w 100%. Czas pracy źródła
sterowalnego odpowiada dokładnie czasowi trwania zdarzenia (72,0 h / 21,0 h), co
potwierdza poprawność modelu.

**5.2. Kryterium ekonomiczne → K1.** Pełne pokrycie awarii za 31 500 $ wobec 499 138 $
dla kogeneracji — stosunek **1 : 14,3**. Dla obiektu 355 MWh/rok kogeneracja gazowa nie
znajduje uzasadnienia ekonomicznego.

**5.3. Kryterium logistyczne → K3.** 944 litry przy zbiorniku 1 000 l dają margines 6%.
Gaz ziemny doprowadzany jest siecią podziemną — czas pracy ograniczony wyłącznie
ciągłością dostaw, nie zapasem na terenie obiektu.

**5.4. Wniosek zasadniczy — warunkowy.**
Jeżeli kryterium stanowi koszt, a zdarzenia mają charakter krótkotrwały — optymalna
pozostaje **K1**. Jeżeli kryterium stanowi odporność na zdarzenia black-sky —
rozstrzyga **niezależność od transportu drogowego**, której agregat nie posiada.

**5.5. Magazyn bateryjny** nie jest źródłem autonomii (60 kWh użytecznych ≈ 1,4 h pracy),
lecz elementem ograniczającym pracę agregatu — redukcja paliwa o 26% w wariancie A2 oraz
podtrzymanie odbiorów klasy 0,5 s.

**5.6. Instalacja PV** obniża LCOE o 13,6% przy zwrocie 6,0 lat, lecz w warunkach
awaryjnych jej wkład wynosi 7–9%. Nie może stanowić podstawy zasilania awaryjnego
w warunkach polskich.

---

## 6. Zadania dalsze

| Zadanie | Uzasadnienie |
|---|---|
| Ustalenie pojemności zbiornika agregatu | Wartość rozstrzygająca dla oceny K1 |
| Dane CHP 30–40 kW od producenta | Katalog HOMER nie zawiera jednostek < 100 kW |
| Weryfikacja zapotrzebowania cieplnego | 700 MWh to oszacowanie — wniosek o audyt złożony |
| Rozmieszczenie modułów PV w CAD | Potwierdzenie granicy 110 kWp |
| Praca wyspowa na odbiorach krytycznych (17,0 kW) | Znaczące wydłużenie autonomii |
