# Temat pracy dyplomowej

**Projekt i ocena architektury systemu energetycznego szpitala z kogeneracją, OZE oraz magazynami energii w kontekście bezpieczeństwa energetycznego**

Autor: Borsurk (Hlieb Snitko)
Kierunek: Odnawialne Źródła Energii (OZE)
Wydział: Kształtowania Środowiska i Rolnictwa (WKŚiR), ZUT w Szczecinie

---

## Zasady projektowe (obowiązujące)

- Analizowany jest **jeden obiekt referencyjny** — szpital o zabudowie jednobryłowej (monoblok).
- Rozpatrywane są **trzy scenariusze** w środowisku HOMER Pro:
  1. **Scenariusz 1 (Baza):** Sieć elektroenergetyczna + agregat prądotwórczy (Diesel)
  2. **Scenariusz 2 (Hybryda):** Sieć + agregat + PV + BESS
  3. **Scenariusz 3 (Zaawansowana mikrosieć):** Sieć + PV + BESS + CHP (ze wsparciem cieplnym)
- Styl: chłodny język inżynierski i akademicki, strona bierna („zbadano", „przeanalizowano").
- Format roboczy: czysty Markdown (Obsidian); dokumenty finalne — DOCX wg wytycznych WKŚiR.

---

## Podział ról w części obliczeniowej

| Etap | Wykonawca |
|---|---|
| Profile obciążeń (CSV 8760 h), dobór komponentów, parametry wejściowe | Asystent |
| Modelowanie przestrzenne PV (CAD / PV*SOL) — układ modułów, GCR, zacienienie | Dyplomant |
| Implementacja modelu i symulacje w HOMER Pro | Dyplomant |
| Analiza wyników, tabele porównawcze, redakcja tekstu | Asystent |

---

## Rozszerzenia metodyczne

### 1. Test przetrwania (Resilience / Autonomy Test)

Poza standardową analizą ekonomiczną (LCOE, NPC) i emisyjną przeprowadzona zostanie
analiza autonomii obiektu: wyznaczenie maksymalnego czasu (godzin/dni) pracy szpitala
w pełnym trybie wyspowym, bez dostępu do sieci nadrzędnej, w warunkach długotrwałej
awarii systemowej (*black-sky hazard*). Test obejmuje scenariusze 2 i 3.

### 2. Modelowanie przestrzenne PV poza HOMER Pro

HOMER Pro nie zawiera środowiska CAD, w związku z czym rozmieszczenie modułów
fotowoltaicznych na stropodachu (analiza zacienienia, dobór odstępów międzyrzędowych,
wyznaczenie GCR) wykonane zostanie w osobnym oprogramowaniu (PV*SOL / AutoCAD)
na podstawie materiałów kartograficznych i zdjęć satelitarnych. Wynikiem tej analizy
jest maksymalna fizycznie możliwa moc zainstalowana instalacji [kWp], przyjmowana
następnie jako **twarde ograniczenie górne (upper bound)** dla optymalizatora HOMER Pro.

---

## Kryteria doboru obiektu referencyjnego

| Kryterium | Wymóg |
|---|---|
| Lokalizacja | Preferowane woj. zachodniopomorskie (Szczecin i okolice, Goleniów, Gryfino, Stargard); dopuszczalna inna lokalizacja w Polsce przy pełnym spełnieniu warunków architektonicznych |
| Architektura | Bezwzględnie monoblok — bryła zwarta, wielokondygnacyjna; wykluczony układ pawilonowy |
| Dach | Płaski stropodach, powierzchnia wolna pod instalację PV ok. 1000–1500 m² |
| Skala | Szpital powiatowy/miejski, ok. 60–150 łóżek |
| Energia | Roczne zużycie energii elektrycznej ok. 1 GWh (1000 MWh); ciągłe zapotrzebowanie na ciepło (c.w.u., sterylizacja, pralnia) |
