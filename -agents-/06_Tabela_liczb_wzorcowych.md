# Tabela liczb wzorcowych

> **Dokument rozstrzygający.** Każda liczba występująca w tekście pracy, w tabelach,
> na rysunkach i w załącznikach musi być zgodna z niniejszym zestawieniem.
> W razie rozbieżności obowiązuje wartość stąd. Dokument powstał w wykonaniu
> kroku 1 planu korekty recenzyjnej z 13.11.2026.

---

## 0. Rozstrzygnięcia pojęciowe

| Pojęcie | Definicja obowiązująca |
|---|---|
| **Stan istniejący** | Grupel G0356 (258 kW PRP) + ZPW 100 DTDEO (≈68 kW); zbiornik użyteczny 900 + 108 = **1 008 l**; CAPEX **0 $**. Punkt odniesienia **testu przetrwania** |
| **K1 — Baza** | model: sieć + `Autosize Genset` **68 kW**; CAPEX **34 000 $**. Punkt odniesienia **analizy ekonomicznej** |
| **K2 — Hybryda** | sieć + agregat 68 kW + PV + BESS 100 kWh |
| **K3 — Mikrosieć** | sieć + PV + **BESS** + CHP 100 kW + kocioł — **wariant z magazynem jest obowiązujący** |
| **A0 / A1 / A2** | praca normalna / awaria 72 h (15–17.01) / pięć przerw, łącznie 21 h |

**Konfiguracje pomocnicze** (nie są K1–K3, wolno ich używać wyłącznie jako materiału
porównawczego, z podaniem pełnej nazwy): *sama sieć*, *sama PV 124 kWp*,
*sama CHP 100 kW*, *CHP bez BESS*, *K4 — pełna praca wyspowa*, *wariant pośredni*.

---

## 1. Dane wejściowe obiektu

| Wielkość | Wartość | Źródło |
|---|---|---|
| Zużycie energii elektrycznej (2025) | **384,44 MWh/rok** | odpowiedź szpitala 21.09.2026 |
| Zużycie energii elektrycznej (2023 / 2024) | 373,24 / 275,68 MWh | tamże |
| Zużycie ciepła (2025) | **810,8 MWh/rok** (2 919 GJ) | tamże |
| Zużycie ciepła (2023 / 2024) | 783,6 / 766,7 MWh | tamże |
| Zużycie dobowe elektryczne | 1 053,3 kWh/d | profil własny |
| **Moc średnia** | **43,89 kW** | profil własny |
| **Moc szczytowa** | **61,42 kW** | profil własny — *wielkość wyznaczona, nie zmierzona* |
| Współczynnik obciążenia | 0,715 | profil własny |
| Obciążenie średnie w A1 | **46,79 kW** | profil własny |
| Zapotrzebowanie w A1 (72 h) | **3 369 kWh** | profil własny |
| Zapotrzebowanie w A2 (21 h) | **969 kWh** | profil własny |
| **Odbiory krytyczne (30% P_szcz, § 42)** | **18,40 kW** | przeliczenie |
| Moc cieplna średnia / szczytowa | 92,56 / 242,0 kW | profil własny |
| Baza cieplna letnia | ok. 33 kW | profil własny |
| Moc cieplna średnia w styczniu | ok. 168 kW | profil własny |
| Powierzchnia dachu | **2 384 m²** | odpowiedź szpitala |
| Powierzchnia użytkowa / kubatura | 7 495 m² / 29 840 m³ | tamże |
| Graniczna moc PV | **124 kWp** | przeliczenie, układ południowy |
| Zasób słoneczny (GHI) | 2,72 kWh/m²/d | NASA POWER |
| GHI styczeń / maj | 0,73 / 4,85 kWh/m²/d | tamże |
| Moc umowna | 422 kW | odpowiedź szpitala — *rozbieżność nierozstrzygnięta* |
| Taryfa | B22; 0,220 $/kWh zakup, 0,090 $/kWh sprzedaż | tamże / model |

### 1.1. Agregaty — stan istniejący

| Parametr | Grupel G0356BDGRAA5T4000S | ZPW 100 DTDEO |
|---|---|---|
| Moc pozorna STP / PRP | 356 / 323 kVA | 85 kVA |
| Moc czynna STP / PRP | 285 / **258 kW** | ≈ 68 kW |
| Zbiornik nominalny | 1 000 l | 120 l |
| Dopuszczalne napełnienie | **90%** (tabliczka) | 90% (przyjęte) |
| **Zbiornik użyteczny** | **900 l** | **108 l** |
| Obciążenie względne przy 46,79 kW | **18,1%** PRP | 69% |
| Nr seryjny / rok | 20024123 / 06.2023 | — |

---

## 2. Wariant A0 — praca normalna

| Architektura | NPC | LCOE | CAPEX | OZE | IRR | Zwrot | Czas pracy źródła |
|---|---|---|---|---|---|---|---|
| sama sieć *(odniesienie)* | 1,91 M$ | 0,220 | 0 $ | 0% | — | — | — |
| **sama PV 124 kWp** | 1,77 M$ | **0,188** | 121 869 $ | 8,67% | 16% | 6,0 lat | — |
| PV 124 + agregat | 1,80 M$ | 0,193 | 155 869 $ | 8,67% | 12% | 7,7 | agregat 0 h |
| PV 124 + BESS | 1,81 M$ | 0,200 | 146 638 $ | 8,50% | 12% | 7,4 | — |
| **K2** | **1,84 M$** | **0,205** | **180 638 $** | 8,50% | 9,5% | 9,1 | agregat **0 h** |
| **K1** | **1,93 M$** | **0,225** | **34 000 $** | 0% | — | — | agregat **0 h** |
| PV 124 + CHP *(bez BESS)* | 2,20 M$ | 0,270 | 571 869 $ | 8,66% | 0,01% | 25 | CHP 504 h |
| **K3** | **2,24 M$** | **0,285** | **596 638 $** | 8,50% | — | — | CHP **476 h** |
| sama CHP 100 kW | 2,31 M$ | 0,301 | 450 000 $ | 0% | — | — | CHP 1 976 h |

**Produkcja CHP w K3:** 24 937 kWh, zużycie gazu 8 363 m³.
**Produkcja PV (124 kWp):** ok. 114,7 MWh/rok (925 kWh/kWp).

> **Rozbieżność do wyjaśnienia.** 114,7 MWh / 1 195 MWh (suma obciążeń) = 9,6%,
> podczas gdy optymalizator podaje 8,50%. Różnica 1,1 pkt proc. odpowiada ok. 13 MWh
> i wymaga wyjaśnienia — `[DO UZUPEŁNIENIA: autokonsumpcja, eksport i straty z HOMER]`.

---

## 3. Wariant A1 — awaria 72-godzinna

| Architektura | NPC | LCOE | CAPEX | Czas pracy | Produkcja | Paliwo |
|---|---|---|---|---|---|---|
| sama sieć *(odniesienie)* | 1,30 M$ | 0,100 | 0 $ | — | — | brak pokrycia |
| sama PV 50 kWp | 1,31 M$ | 0,101 | 49 300 $ | — | — | — |
| **K1** | **1,35 M$** | **0,109** | 34 000 $ | **72,0 h** | 3 369 kWh | **1 013 l ON** |
| PV 50 + agregat | 1,36 M$ | 0,110 | 83 300 $ | 72,0 h | 3 147 kWh | 961 l ON |
| agregat + BESS | 1,41 M$ | 0,120 | 64 581 $ | 72,0 h | 3 315 kWh | 1 000 l ON |
| **K2** | **1,41 M$** | **0,120** | 113 300 $ | **72,0 h** | 3 093 kWh | **948 l ON** |
| sama CHP | 1,75 M$ | 0,188 | 450 000 $ | 72,0 h | 3 763 kWh | 1 263 m³ |
| PV 50 + CHP | 1,75 M$ | 0,189 | 499 300 $ | 72,0 h | 3 661 kWh | 1 239 m³ |
| CHP + BESS | 1,80 M$ | 0,199 | 480 698 $ | 72,0 h | 3 763 kWh | 1 263 m³ |
| **K3** | **1,80 M$** | **0,199** | **529 300 $** | **72,0 h** | 3 661 kWh | **1 239 m³** |

> **Uwaga.** W wariantach awaryjnych optymalizator dobrał **PV 50 kWp**, nie 124 kWp.
> Architektury K2 i K3 w A1/A2 nie są zatem tożsame z tymi z A0 — należy to zaznaczać
> przy każdym zestawieniu międzywariantowym. LCOE 0,100 dla samej sieci w A1
> wymaga sprawdzenia taryfy w modelu — `[DO UZUPEŁNIENIA: weryfikacja taryfy A1/A2]`.

### 3.1. Test przetrwania — wyczerpanie zapasu

| Układ | Zapotrzebowanie | Zbiornik | **Wyczerpanie** | Pokrycie 72 h |
|---|---|---|---|---|
| K1 *(model, 68 kW)* | 1 013 l | 900 l | **64,0 h** | nie — brak 113 l |
| K2 *(model, 68 kW)* | 948 l | 900 l | **68,4 h** | nie — brak 48 l |
| **Stan istniejący** — krzywa optymistyczna | — | 1 008 l | **76,5 h** | **tak — zapas 4,5 h** |
| **Stan istniejący** — krzywa średnia | — | 1 008 l | **65,6 h** | nie — brak 6,4 h |
| **Stan istniejący** — krzywa zachowawcza | — | 1 008 l | **57,8 h** | nie — brak 14,2 h |

### 3.2. Krzywe zużycia paliwa — F = a + b·P

| Krzywa | a [l/h] | b [l/kWh] | przy 46,79 kW | przy 18,40 kW | Status |
|---|---|---|---|---|---|
| wyznaczona z wyniku HOMER (68 kW) | 2,37 | 0,250 | 14,07 l/h | 6,97 l/h | z symulacji |
| Grupel — optymistyczna | 3,44 | 0,206 | 13,08 l/h | 7,23 l/h | **wartość przyjęta** `[ŹRÓDŁO]` |
| Grupel — średnia | 5,00 | 0,225 | 15,53 l/h | 9,14 l/h | **wartość przyjęta** `[ŹRÓDŁO]` |
| Grupel — zachowawcza | 6,45 | 0,246 | 17,96 l/h | 10,98 l/h | **wartość przyjęta** `[ŹRÓDŁO]` |

### 3.3. Autonomia Grupel przy zasilaniu całości (900 l)

| Krzywa | Czas pracy | Deficyt wobec 72 h |
|---|---|---|
| optymistyczna | 68,8 h | 3,2 h |
| średnia | 58,0 h | 14,0 h |
| zachowawcza | 50,1 h | 21,9 h |

### 3.4. Praca wyspowa na odbiorach krytycznych (18,40 kW)

| Krzywa | Czas pracy z 900 l | Pokrycie 72 h |
|---|---|---|
| HOMER (68 kW) | **129,1 h** | tak |
| optymistyczna | **124,5 h** | tak |
| średnia | **98,5 h** | tak |
| zachowawcza | **82,0 h** | tak |

**Obciążenie graniczne** (zużycie 12,50 l/h): HOMER 40,5 kW · optymistyczna 44,0 kW ·
średnia 33,3 kW · **zachowawcza 24,6 kW**. Warunek obowiązywania wniosku:
**P_kryt ≤ 24,6 kW**.

---

## 4. Wariant A2 — pięć przerw, łącznie 21 h

| Architektura | NPC | LCOE | CAPEX | Czas pracy | Produkcja | Paliwo |
|---|---|---|---|---|---|---|
| sama sieć *(odniesienie)* | 1,31 M$ | 0,100 | 0 $ | — | — | brak pokrycia |
| **K1** | **1,34 M$** | **0,106** | 34 000 $ | **21,0 h** | 969 kWh | **292 l ON** |
| PV 50 + agregat | 1,34 M$ | 0,107 | 83 300 $ | 21,0 h | 924 kWh | 282 l ON |
| agregat + BESS | 1,39 M$ | 0,117 | 64 581 $ | 21,0 h | 928 kWh | 283 l ON |
| **K2** | **1,40 M$** | **0,118** | 113 300 $ | **21,0 h** | 667 kWh | **221 l ON** |
| sama CHP | 1,74 M$ | 0,187 | 450 000 $ | 21,0 h | 1 068 kWh | 361 m³ |
| PV 50 + CHP | 1,75 M$ | 0,188 | 499 300 $ | 21,0 h | 1 057 kWh | 359 m³ |
| CHP + BESS | 1,80 M$ | 0,198 | 480 698 $ | 21,0 h | 1 060 kWh | 359 m³ |
| **K3** | **1,80 M$** | **0,199** | **529 300 $** | **21,0 h** | 1 052 kWh | **358 m³** |

**Efekt magazynu w A2:** produkcja agregatu 969 → 667 kWh (**−302 kWh**),
paliwo 292 → 221 l (**−24,3%**), obciążenie średnie agregatu 46,1 → 31,8 kW,
zużycie jednostkowe 0,301 → 0,331 l/kWh.

---

## 5. Emisje CO₂

Wskaźniki przyjęte: sieć **0,66 kg/kWh** `[ŹRÓDŁO]` · olej napędowy **2,68 kg/l**
`[ŹRÓDŁO]` · gaz ziemny **1,9 kg/m³** `[ŹRÓDŁO]` · wartość opałowa gazu
**9,97 kWh/m³** `[ŹRÓDŁO]`.

| Układ | Emisja własna | Emisja unikniona | Bilans roczny |
|---|---|---|---|
| K1 | 0 t | 0 t | 0,0 t |
| K2 | 0 t | 75,7 t | **−75,7 t** |
| K3 | 15,9 t | 92,2 t | **−76,3 t** |
| K4 *(pełna wyspa)* | ok. 283 t | ok. 254 t | **+29 t** |

Emisje na zdarzenie A1: K1 **2,71 t** · K2 **2,54 t** · K3 **2,35 t**.

---

## 6. Stosunki nakładów

```
K2 / K1 = 180 638 / 34 000 = 5,3×
K3 / K1 = 596 638 / 34 000 = 17,5×
ΔCAPEX (K3 − sama PV) = 596 638 − 121 869 = 474 769 $
ΔLCOE  (K3 − sama PV) = 0,285 − 0,188 = 0,097 $/kWh  (+51,6%)
```

---

## 7. Liczby WYCOFANE — nie wolno ich używać

| Wartość wycofana | Występowała jako | Wartość obowiązująca |
|---|---|---|
| 355 MWh | zużycie elektryczne | **384,44 MWh** |
| 700 MWh | zapotrzebowanie cieplne | **810,8 MWh** |
| 56,72 kW | moc szczytowa | **61,42 kW** |
| 40,53 kW | moc średnia | **43,89 kW** |
| 110 kWp | graniczna moc PV | **124 kWp** |
| 1 000 l | zbiornik użyteczny | **900 l** (1 000 l = nominał) |
| 17,0 kW | odbiory krytyczne | **18,40 kW** |
| 3 111 kWh | zapotrzebowanie w A1 | **3 369 kWh** |
| 944 l | paliwo K1 w A1 | **1 013 l** |
| § 30, § 41 | podstawa prawna agregatu | **§ 42** |
| 571 869 $ / 0,270 / 504 h / 1 263 m³ | K3 | **596 638 $ / 0,285 / 476 h / 1 239 m³** |
| 16,8× | stosunek K3/K1 | **17,5×** |
| 125 h, 753 h | czas pracy CHP w A0 | **476 h**, 1 976 h |
| 71 kW | moc cieplna CHP w K4 | **96,9 kW** |

---

## 8. Pozycje otwarte

| Znacznik | Czego dotyczy | Kto rozstrzyga |
|---|---|---|
| `[DO UZUPEŁNIENIA: autokonsumpcja PV]` | rozbieżność 8,50% / 9,6% | eksport z HOMER — **licencja wygasła** |
| `[DO UZUPEŁNIENIA: taryfa A1/A2]` | LCOE 0,100 dla samej sieci | jw. |
| `[DO UZUPEŁNIENIA: schemat rozdzielni]` | zakres odbiorów obu agregatów | szpital |
| `[DO UZUPEŁNIENIA: DTR Grupel]` | krzywa zużycia paliwa | producent / szpital |
| `[DO UZUPEŁNIENIA: odczyty 15-min]` | rzeczywista moc szczytowa | OSD |
| `[DO UZUPEŁNIENIA: taryfa ciepła]` | ocena K4 | szpital |
| `[DO UZUPEŁNIENIA: przyłącze gazowe]` | założenie o ciągłości dostawy gazu | szpital |
| `[DO UZUPEŁNIENIA: koszt automatyki odciążania]` | „dwa rzędy wielkości" | kosztorys |
| `[ŹRÓDŁO]` | wskaźniki emisji, krzywe a/b, SAIDI, 30–80%, 60–90 PLN/GJ, ceny komponentów, współczynnik 0,80 | literatura |

---

## Powiązane

[[04_Wyniki_V2_dane_rzeczywiste]] · [[07_Stan_istniejacy_test_przetrwania]] ·
[[05_Praca_wyspowa_odbiory_krytyczne]] · [[06_Konfiguracja_K4_praca_wyspowa]] ·
[[05_Agregat_GRUPEL_dane_z_tabliczki]] · [[02_Zasady_symulacji_HOMER]] ·
[[05_Zasady_zrodel_i_cytowan]]
