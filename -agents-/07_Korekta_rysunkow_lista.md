# Korekta rysunków — lista wartości do zmiany

> Zadanie dla czatu graficznego. Wynika z recenzji drugiej (pkt 4 i N4).
> Wartości obowiązujące: [[06_Tabela_liczb_wzorcowych]].
> **Nie zmieniać niczego poza wymienionymi liczbami i podpisami.**

---

## 1. R7_1_CAPEX_konfiguracji.svg

| Element | Jest | **Ma być** |
|---|---|---|
| CAPEX K3 | 571 869 $ | **596 638 $** |
| Krotność K3/K1 | 16,8× | **17,5×** |
| Opis K3 | PV + CHP | **PV + BESS + CHP** |

## 2. R7_2_LCOE_warianty_awarii.svg

| Element | Jest | **Ma być** |
|---|---|---|
| LCOE K3 w A0 | 0,270 | **0,285** |
| LCOE K3 w A1 | 0,188 lub 0,189 | **0,199** |
| LCOE K3 w A2 | 0,187 lub 0,188 | **0,199** |

**Dodać adnotację na rysunku:** *„W wariantach A1 i A2 optymalizator dobrał PV 50 kWp
zamiast 124 kWp — wartości nie są porównywalne międzywariantowo."*

## 3. R7_3_Analiza_wrazliwosci_paliwa.svg

| Element | Jest | **Ma być** |
|---|---|---|
| Krzywa średnia — czas | 57,9 h | **58,0 h** |
| Krzywa średnia — deficyt | −14,1 h | **−14,0 h** |
| Podpis | „trzech wariantów krzywej zużycia" | **„trzech krzywych zużycia paliwa"** |
| Liczba słupków | 4 | **3** (usunąć słupek HOMER albo zmienić podpis na „czterech krzywych") |

## 4. R7_4_Czas_pracy_zrodel_A0.svg

| Element | Jest | **Ma być** |
|---|---|---|
| Czas pracy CHP (K3) | 504 h | **476 h** |
| Udział czasu roku | 5,8% | **5,4%** |
| Produkcja CHP | 26 343 kWh | **24 937 kWh** |
| Opis K3 | PV + CHP | **PV + BESS + CHP** |

Wartość **1 976 h** (sama CHP, bez PV i BESS) pozostaje bez zmian — zmienić jednak
podpis słupka na *„sama CHP 100 kW"*, nie *„K3 bez PV"*.

## 5. R7_5_Zuzycie_paliwa_awarie.svg

| Element | Jest | **Ma być** |
|---|---|---|
| Gaz K3 w A1 | 1 263 m³ | **1 239 m³** |
| Gaz K3 w A2 | 361 m³ | **358 m³** |

Wartości dla K1 (1 013 / 292 l) i K2 (948 / 221 l) pozostają bez zmian.

## 6. R7_6_Wyczerpanie_zbiornika_A1.svg

Rysunek **pozostaje poprawny** co do przebiegu (64,0 h i 68,4 h), wymaga natomiast
zmiany opisu — wartości te dotyczą **konfiguracji modelowych**, nie stanu istniejącego.

**Dodać do podpisu:** *„Przebieg dla konfiguracji modelowych (agregat 68 kW).
Ocenę stanu faktycznie istniejącego przedstawiono w podrozdziale 7.2.6."*

## 7. R4_5_Uklady_rozmieszczenia_PV.svg

| Element | Jest | **Ma być** |
|---|---|---|
| Układ południowy — moc | ok. 100–120 kWp | **123 kWp** |
| Układ południowy — GCR | 0,25–0,30 | **0,28** |
| Układ E–W — moc | ok. 240–280 kWp | **286 kWp** |
| Układ E–W — GCR | 0,60–0,70 | **0,65** |

**Dodać:** liczbę modułów (273 / 634) oraz wzór `P = A · GCR / 4,34`.

---

## 8. Rysunek nowy — do rozważenia

`R7_8_Stan_istniejacy_sekwencja.svg` — przebieg zapasu paliwa dla **stanu
istniejącego** w dwóch fazach (Grupel 900 l → ZPW 108 l), trzy krzywe zużycia.

| Krzywa | Faza I | Faza II | Razem |
|---|---|---|---|
| optymistyczna | 68,8 h | 7,7 h | **76,5 h** |
| średnia | 58,0 h | 7,7 h | **65,6 h** |
| zachowawcza | 50,1 h | 7,7 h | **57,8 h** |

Linia progu 72 h. Kolory: faza I `#8a6d1f`, faza II `#2c5f8d`, próg `#b5452f`.
Rysunek ten ilustruje **ustalenie zasadnicze pracy** i jest ważniejszy od pozostałych.

---

## Po wykonaniu

Wpisać zmiany do `00_INDEKS_RYSUNKOW.md` oraz usunąć stamtąd adnotacje
o nieaktualnych wartościach K3.
