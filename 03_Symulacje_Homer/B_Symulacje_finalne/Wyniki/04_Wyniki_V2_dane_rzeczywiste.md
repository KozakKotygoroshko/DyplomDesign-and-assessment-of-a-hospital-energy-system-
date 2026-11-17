# Wyniki symulacji — seria V2 na danych rzeczywistych szpitala

Data wykonania: **21 września 2026**. Środowisko: HOMER Pro x64 3.18.4.
Podstawa danych: odpowiedź Szpitala Powiatowego w Pyrzycach z 21.09.2026
(`02_Rozdzialy/04_Zalozenia_projektowe/04_Odpowiedz_szpitala_dane_rzeczywiste.md`).

> Seria V2 **zastępuje** wyniki serii z 19.09.2026, wykonanej na wartościach szacowanych.

---

## 1. Zmiany parametrów wejściowych wobec serii poprzedniej

| Parametr | Seria I (szacunek) | **Seria V2 (dane rzeczywiste)** | Zmiana |
|---|---|---|---|
| Zużycie elektryczne | 355,0 MWh/rok | **384,44 MWh/rok** | +8,3% |
| Obciążenie średnie | 40,53 kW | **43,89 kW** | +8,3% |
| Moc szczytowa | 56,72 kW | **61,42 kW** | +8,3% |
| Zapotrzebowanie cieplne | 700 MWh/rok | **810,8 MWh/rok** | +15,8% |
| Moc cieplna szczytowa | 208,92 kW | **242,0 kW** | +15,8% |
| Górna granica PV | 110 kWp | **124 kWp** | +12,7% |
| Min. obciążenie CHP | 30% | **50%** | wartość producenta |

Pliki modeli: `V2_Pyrzyce_A0_bez_awarii_dane_rzeczywiste.homer`,
`V2_Pyrzyce_A1_blacksky_72h_dane_rzeczywiste.homer`,
`V2_Pyrzyce_A2_serie_krotkich_dane_rzeczywiste.homer`.

---

## 2. Wariant A0 — praca normalna

| Architektura | NPC | LCOE | CAPEX | Udział OZE | IRR | Zwrot | Czas pracy |
|---|---|---|---|---|---|---|---|
| **PV 124 kWp** *(optimum ogólne)* | **1,77 M$** | **0,188** | 121 869 $ | 8,67% | **16%** | **6,0 lat** | — |
| PV 124 + agregat | 1,80 M$ | 0,193 | 155 869 $ | 8,67% | 12% | 7,7 | agregat **0 h** |
| PV 124 + BESS | 1,81 M$ | 0,200 | 146 638 $ | 8,50% | 12% | 7,4 | — |
| **K2** — PV 124 + agregat + BESS | 1,84 M$ | 0,205 | 180 638 $ | 8,50% | 9,5% | 9,1 | agregat **0 h** |
| *Odniesienie — sama sieć* | 1,91 M$ | 0,220 | 0 $ | 0% | — | — | — |
| **K1** — sam agregat 68 kW | 1,93 M$ | 0,225 | 34 000 $ | 0% | — | — | agregat **0 h** |
| **K3** — PV 124 + BESS + CHP 100 kW | **2,24 M$** | **0,285** | **596 638 $** | 8,50% | — | — | CHP **476 h** |
| PV 124 + CHP (bez BESS) | 2,20 M$ | 0,270 | 571 869 $ | 8,66% | 0,01% | 25 | CHP 504 h |
| CHP 100 kW bez PV i BESS | 2,31 M$ | 0,301 | 450 000 $ | 0% | — | — | CHP **1 976 h** |

> **Uwaga redakcyjna.** Zgodnie z definicją przyjętą w [[02_Zasady_symulacji_HOMER]]
> Konfigurację **K3 stanowi układ pełny: sieć + PV + BESS + CHP + kocioł**. Wiersze
> z samą kogeneracją lub z kogeneracją bez magazynu stanowią materiał uzupełniający,
> przydatny do oceny wkładu poszczególnych komponentów — nie są natomiast Konfiguracją K3.

### Obserwacje

**Czas pracy kogeneracji wzrósł czterokrotnie.** Wobec serii poprzedniej: 125 → **504 h**
przy współpracy z PV oraz 753 → **1 976 h** bez PV. Przyczyną jest wyższe rzeczywiste
zapotrzebowanie cieplne (810,8 zamiast 700 MWh), mimo równoczesnego podniesienia
minimalnego obciążenia roboczego z 30% na 50%. Jednostka pozostaje przewymiarowana,
lecz w stopniu mniejszym niż wskazywały szacunki.

**Optymalizator ponownie osiągnął górną granicę mocy PV.** Przy zbiorze rozszerzonym
testowo do 150 kWp optymalizator wybrał 150 kWp (LCOE 0,180, zwrot 6,3 lat),
sygnalizując przy tym niewystarczający zakres poszukiwań. Ograniczeniem pozostaje
**powierzchnia dachu, nie ekonomia** — wniosek serii poprzedniej zachowuje ważność.

**Agregat prądotwórczy nie pracuje ani godziny.** Wynik niezmieniony.

---

## 3. Wariant A1 — awaria black-sky, 72 h

Zapotrzebowanie obiektu w okresie awarii: **3 369 kWh** (obciążenie średnie 46,79 kW).

| Architektura | NPC | LCOE | CAPEX | Czas pracy | Produkcja | **Paliwo** |
|---|---|---|---|---|---|---|
| *Odniesienie — sama sieć* | 1,30 M$ | 0,100 | 0 $ | — | — | brak pokrycia |
| **K1** — agregat 68 kW | 1,35 M$ | 0,109 | 34 000 $ | **72,0 h** | 3 369 kWh | **1 013 l ON** |
| PV 50 + agregat | 1,36 M$ | 0,110 | 83 300 $ | 72,0 h | 3 147 kWh | 961 l ON |
| agregat + BESS | 1,41 M$ | 0,120 | 64 581 $ | 72,0 h | 3 315 kWh | 1 000 l ON |
| **K2** — PV 50 + agregat + BESS | 1,41 M$ | 0,120 | 113 300 $ | **72,0 h** | 3 093 kWh | **948 l ON** |
| sama CHP 100 kW | 1,75 M$ | 0,188 | 450 000 $ | 72,0 h | 3 763 kWh | 1 263 m³ gazu |
| PV 50 + CHP | 1,75 M$ | 0,189 | 499 300 $ | 72,0 h | 3 661 kWh | 1 239 m³ gazu |
| CHP + BESS | 1,80 M$ | 0,199 | 480 698 $ | 72,0 h | 3 763 kWh | 1 263 m³ gazu |
| **K3** — PV 50 + BESS + CHP | **1,80 M$** | **0,199** | **529 300 $** | **72,0 h** | 3 661 kWh | **1 239 m³ gazu** |

### Ustalenie rozstrzygające

**Konfiguracja K1 przekracza pojemność istniejącego zbiornika.**

```
Zapotrzebowanie na paliwo (K1, agregat 68 kW):   1 013 l
Pojemność zbiornika (GO 356 BDLS, dane szpitala): 1 000 l
DEFICYT:                                             13 l
```

W serii poprzedniej, opartej na zaniżonym zapotrzebowaniu, wynik wynosił 944 l — zapas
6%. Po podstawieniu danych rzeczywistych zapas **zmienia znak**. Agregat dobrany
optymalnie przez HOMER nie pokrywa pełnej awarii 72-godzinnej ze zbiornika obiektu.

Jednostka faktycznie zainstalowana (326 kVA ≈ 261 kW) pracuje przy obciążeniu 16,5%
mocy znamionowej, wskutek czego jednostkowe zużycie paliwa jest wyższe. Oszacowanie
własne: 15–16 l/h, tj. **ok. 1 116 l** na 72 h — deficyt rzędu **116 l (7,5 h pracy)**.
Wartość wymaga potwierdzenia dokumentacją techniczno-ruchową (pismo z 21.09.2026).

**Dodanie PV i magazynu poprawia bilans, lecz nie rozwiązuje problemu.** Konfiguracja K2
zużywa 948 l — mieści się w zbiorniku z zapasem 5,2%, czyli na granicy. Warunek pokrycia
spełniony jest wyłącznie przy zbiorniku napełnionym całkowicie w chwili zdarzenia.

**Kogeneracja gazowa nie podlega temu ograniczeniu.** Zużycie 1 263 m³ gazu ziemnego
pobierane jest z sieci podziemnej, niezależnej od transportu drogowego.

---

## 4. Wariant A2 — seria pięciu przerw krótkotrwałych (21 h)

| Architektura | NPC | LCOE | CAPEX | Czas pracy | Produkcja | **Paliwo** |
|---|---|---|---|---|---|---|
| *Odniesienie* | 1,31 M$ | 0,100 | 0 $ | — | — | brak pokrycia |
| **K1** — agregat 68 kW | 1,34 M$ | 0,106 | 34 000 $ | **21,0 h** | 969 kWh | **292 l ON** |
| PV 50 + agregat | 1,34 M$ | 0,107 | 83 300 $ | 21,0 h | 924 kWh | 282 l ON |
| agregat + BESS | 1,39 M$ | 0,117 | 64 581 $ | 21,0 h | 928 kWh | 283 l ON |
| **K2** — PV 50 + agregat + BESS | 1,40 M$ | 0,118 | 113 300 $ | **21,0 h** | 667 kWh | **221 l ON** |
| sama CHP 100 kW | 1,74 M$ | 0,187 | 450 000 $ | 21,0 h | 1 068 kWh | 361 m³ gazu |
| PV 50 + CHP | 1,75 M$ | 0,188 | 499 300 $ | 21,0 h | 1 057 kWh | 359 m³ gazu |
| CHP + BESS | 1,80 M$ | 0,198 | 480 698 $ | 21,0 h | 1 060 kWh | 359 m³ gazu |
| **K3** — PV 50 + BESS + CHP | **1,80 M$** | **0,199** | **529 300 $** | **21,0 h** | 1 052 kWh | **358 m³ gazu** |

### Obserwacja

Magazyn bateryjny ogranicza zużycie paliwa o **24,3%** (292 → 221 l), przejmując część
przerw w całości i redukując liczbę rozruchów agregatu. Dla zdarzeń krótkotrwałych
zapas zbiornika jest wystarczający z ponad trzykrotnym marginesem w każdej konfiguracji.

---

## 5. Zestawienie zbiorcze — seria V2

| Wskaźnik | K1 — Baza | K2 — Hybryda | K3 — Mikrosieć |
|---|---|---|---|
| Architektura | agregat 68 kW | PV + agregat + BESS | PV + BESS + CHP 100 kW |
| CAPEX (A0) | 34 000 $ | 180 638 $ | **596 638 $** |
| NPC (A0) | 1,93 M$ | **1,84 M$** | 2,24 M$ |
| LCOE (A0) | 0,225 | **0,205** | 0,285 |
| Udział OZE | 0% | 8,50% | 8,50% |
| Czas pracy źródła (A0) | 0 h | 0 h | 476 h |
| **Pokrycie A1 (72 h)** | **100%** | **100%** | **100%** |
| Paliwo A1 | **1 013 l — przekracza zbiornik** | **948 l — przekracza zbiornik** | 1 239 m³ gazu |
| **Pokrycie A2 (21 h)** | **100%** | **100%** | **100%** |
| Paliwo A2 | 292 l | **221 l (−24,3%)** | 358 m³ gazu |
| Zależność od transportu paliwa | wysoka | wysoka | **brak** |

**Stosunek nakładów inwestycyjnych:** K2/K1 = 5,3× · **K3/K1 = 17,5×**

> **Pojemność użyteczna zbiornika wynosi 900 l** ([[05_Agregat_GRUPEL_dane_z_tabliczki]]).
> Zapotrzebowanie Konfiguracji K1 (1 013 l) oraz K2 (948 l) przekracza tę wartość.
> Wyczerpanie zapasu następuje odpowiednio w **64,0** oraz **68,4 godzinie** awarii.

---

## 6. Wnioski serii V2

**6.1.** Wszystkie trzy konfiguracje pokrywają oba typy awarii w 100%. Czas pracy źródła
sterowalnego odpowiada dokładnie czasowi trwania zdarzenia (72,0 h oraz 21,0 h),
a produkcja energii — zapotrzebowaniu obliczonemu analitycznie (3 369 kWh). Model
odwzorowuje zdarzenia awaryjne poprawnie.

**6.2. Wniosek zmieniony wobec serii poprzedniej.** Podstawienie danych rzeczywistych
oraz uwzględnienie ograniczenia napełnienia zbiornika do 90% (pojemność użyteczna
**900 l**) odwróciło ocenę obu konfiguracji opartych na agregacie:

| Konfiguracja | Zapotrzebowanie | Zbiornik | Wyczerpanie |
|---|---|---|---|
| K1 — agregat | 1 013 l | 900 l | **64,0 h** |
| K2 — + PV + BESS | 948 l | 900 l | **68,4 h** |

Konfiguracja K1, najtańsza inwestycyjnie i zgodna z wymogiem § 42 Rozporządzenia
Ministra Zdrowia, **nie zapewnia przetrwania zdarzenia 72-godzinnego**. Dodanie
instalacji fotowoltaicznej i magazynu (K2) przesuwa moment wyczerpania o 4,4 godziny,
co również nie wystarcza. **Jedyną konfiguracją pokrywającą zdarzenie w pełni
pozostaje K3** — jako niepodlegająca ograniczeniu zapasu zgromadzonego na obiekcie.

**6.3.** Kryterium ekonomiczne w warunkach normalnych wskazuje instalację
fotowoltaiczną (LCOE 0,188, zwrot 6,0 lat), nie zaś którąkolwiek z konfiguracji
zapewniających autonomię. Konflikt kryterium kosztowego z wymogiem bezpieczeństwa
pozostaje w mocy.

**6.4.** Magazyn bateryjny nie stanowi źródła autonomii, lecz ogranicza pracę źródła
sterowalnego — redukcja zużycia paliwa o 24,3% w wariancie serii przerw.

**6.5.** Kogeneracja gazowa pozostaje najdroższa (CAPEX **17,5×** wyższy od K1), lecz
jako jedyna nie podlega ograniczeniu pojemności zbiornika. Przy zapotrzebowaniu
cieplnym 810,8 MWh czas pracy jednostki w warunkach normalnych wyniósł 476 h rocznie
w układzie pełnym (K3), a 1 976 h w układzie bez PV i magazynu — w obu przypadkach
poniżej progu opłacalności.

> **Uwaga.** Obiekt zasilany jest ciepłem z sieci geotermalnej. Kogeneracja gazowa nie
> zastępuje zatem kotła kopalnego, lecz konkuruje ze źródłem odnawialnym. Ocena
> środowiskowa Konfiguracji K3 wymaga uwzględnienia tego faktu.

---

## 7. Zadania otwarte

| Zadanie | Wpływ na wynik |
|---|---|
| DTR agregatu GO 356 BDLS — krzywa zużycia paliwa | **Rozstrzyga o skali deficytu paliwa** |
| Zakres odbiorów każdego z agregatów | Umożliwia analizę pracy na odbiorach krytycznych (18,4 kW) |
| Zasilanie rezerwowe ciepłowni geotermalnej | Rozstrzyga o wartości odzysku ciepła z CHP w awarii |
| Profil godzinowy z licznika (OSD) | Zastąpienie profilu syntetycznego |
| Dane CHP 30–40 kW od producenta | Katalog HOMER nie zawiera jednostek gazowych < 100 kW |

---

## 8. Powiązane

**Dane wejściowe:**

- [[04_Odpowiedz_szpitala_dane_rzeczywiste]] — zużycie energii, geometria, źródło ciepła
- [[05_Agregat_GRUPEL_dane_z_tabliczki]] — **pojemność użyteczna 900 l**
- [[04_Zalozenia_projektowe_TEKST]] — profile obciążenia, graniczna moc PV

**Zasady obliczeń:** [[02_Zasady_symulacji_HOMER]] — terminologia K1/K2/K3 oraz A0/A1/A2,
lista kontrolna przed uruchomieniem

**Serie poprzedzające:**

- [[01_Wyniki_symulacji_finalnych]] — seria I na danych szacowanych (**nieaktualna**)
- [[00_SYMULACJE_TESTOWE_raport_zbiorczy]] — seria weryfikacyjna, wnioski metodyczne

**Opracowania na podstawie tych wyników:**

- [[03_Raport_wg_konfiguracji]] — raport wg konfiguracji (**wymaga przeliczenia na V2**)
- [[00_INDEKS_RYSUNKOW]] — materiał graficzny

**Nawigacja:** [[00_PRZEWODNIK_po_folderze]] · [[00_STAN_PRAC]]
