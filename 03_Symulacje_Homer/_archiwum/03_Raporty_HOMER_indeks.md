# Raporty HOMER Pro — indeks

Pełne raporty wygenerowane przez HOMER Pro (`Simulation Results → Create Proposal`),
zawierające komplet wykresów, map cieplnych oraz tabel miesięcznych.

> Pliki `.docx` nie wyświetlają się bezpośrednio w Obsidianie — należy je otworzyć
> w programie Word. Kluczowe wykresy wyodrębniono do folderu `Grafika/` i osadzono
> w notatkach analitycznych.

## Raport 1 — Scenariusz 3 (praca normalna, bez awarii)

**Plik:** `Raport_HOMER_Scenariusz_3_Mikrosiec_PV_BESS_CHP.docx` (13 stron)

Konfiguracja: Sieć + PV 250 kW + przekształtnik 150 kW + kocioł gazowy
NPC 4,35 mln $ · LCOE 0,1958 $/kWh · udział OZE 7,5%

| Sekcja | Zawartość |
|---|---|
| Project Summary | Architektura systemu, podstawowe wskaźniki |
| Consumption Summary | Bilans zużycia elektrycznego i cieplnego |
| Engineering Details | Mapy cieplne produkcji PV, tabele miesięczne sieci, parametry przekształtnika i kotła |
| Cashflow Section | Przepływy pieniężne w cyklu 25 lat |

Wybrane wykresy: `Grafika/Scen3_*.png`

### Podsumowanie zużycia
![[Grafika/Scen3_05_Podsumowanie_zuzycia.png]]

### Instalacja PV — mapa cieplna produkcji godzinowej
![[Grafika/Scen3_06_Engineering_PV.png]]

### Bilans wymiany z siecią
![[Grafika/Scen3_07_Engineering_Siec.png]]

---

## Raport 2 — Test autonomii (awaria black-sky 72 h)

**Plik:** `Raport_HOMER_Test_autonomii_blacksky_72h.docx` (14 stron)

Konfiguracja: Sieć + PV 150 kW + BESS 200 kWh + przekształtnik 90 kW + kocioł
NPC 3,20 mln $ · LCOE 0,1092 $/kWh · **energia niedostarczona 7 966 kWh**

Analiza wyników: [[02_Test_autonomii_black_sky]]

Wybrane wykresy: `Grafika/Autonomia_*.png`

---

## Powiązane notatki

- [[00_Opis_profili_obciazenia]] — dokumentacja profili wejściowych
- [[01_Wyniki_symulacji_testowych]] — porównanie trzech scenariuszy (praca normalna)
- [[02_Test_autonomii_black_sky]] — test przetrwania
- [[Instrukcja_HOMER_Pro]] — instrukcja obsługi programu (folder `01_Baza_Wiedzy`)
