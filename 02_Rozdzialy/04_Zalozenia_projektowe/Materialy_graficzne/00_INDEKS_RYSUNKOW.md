# Indeks rysunków

Rejestr materiału graficznego pracy. **Każdy nowy rysunek należy tu wpisać** —
plik stanowi kanał wymiany informacji pomiędzy czatem graficznym a czatem redakcyjnym.

Konwencja nazw: `R<rozdział>_<numer>_<nazwa>.svg`

---

## Rozdział 4 — Założenia projektowe

| Plik | Podrozdział | Treść | Dane źródłowe | Status |
|---|---|---|---|---|
| `R4_1_Zuzycie_energii_2023_2025.svg` | 4.2.2 | Zużycie energii elektrycznej i ciepła, lata 2023–2025 | odpowiedź szpitala 21.09.2026 | ✅ wstawiony |
| `R4_2_Profil_dobowy_elektryczny.svg` | 4.2.4 | Profil dobowy własny vs syntetyczny HOMER | profil własny + HOMER Pro | ✅ wstawiony |
| `R4_3_Profil_cieplny_miesieczny.svg` | 4.2.3 | Sezonowość ciepła, baza letnia 33 kW | profil własny (stopniodni) | ✅ wstawiony |
| `R4_4_Dysproporcja_mocy.svg` | 4.3 | Moc agregatu wobec zapotrzebowania | tabliczka znamionowa Grupel | ✅ wstawiony |
| `R4_5_Uklady_rozmieszczenia_PV.svg` | 4.4.2 | Układ południowy vs wschód–zachód, GCR | przeliczenie własne | ✅ wstawiony |

### Brakujące

| Proponowany plik | Podrozdział | Treść | Przeszkoda |
|---|---|---|---|
| `R4_6_Zasob_sloneczny.svg` | 4.4.4 | Miesięczny rozkład napromieniowania (GHI) | **brak danych miesięcznych** — znane wyłącznie wartości dla stycznia (0,73), maja (4,85) i średnia roczna (2,72 kWh/m²/d). Tabelę należy odczytać z HOMER Pro: `Resources → Solar Resource` |

---

## Rozdział 7 — Analiza wyników

Lokalizacja plików: `03_Symulacje_Homer/B_Symulacje_finalne/Grafika/`

| Plik | Podrozdział | Treść | Dane źródłowe | Status |
|---|---|---|---|---|
| `R7_1_CAPEX_konfiguracji.svg` | do przypisania | CAPEX K1/K2/K3 i odniesienia (A0); K3/K1 = 16,8×, K2/K1 = 5,3× | wyniki V2, tab. A0 | ✅ gotowy (zastępuje F1) |
| `R7_2_LCOE_warianty_awarii.svg` | do przypisania | LCOE czterech architektur w wariantach A0, A1, A2 | wyniki V2, tab. A0–A2 | ✅ gotowy (zastępuje F2) |
| `R7_3_Zbiornik_paliwa_900l.svg` | do przypisania | Czas pracy agregatu w funkcji zapasu paliwa; próg 900 l, deficyt K1 113 l | wyniki V2 (A1) + tabliczka Grupel | ✅ gotowy (zastępuje F3) |
| `R7_4_Czas_pracy_zrodel_A0.svg` | do przypisania | Roczny czas pracy źródeł sterowalnych w A0: agregat 0 h, CHP 504 / 1 976 h | wyniki V2, tab. A0 | ✅ gotowy (zastępuje F4) |
| `R7_5_Zuzycie_paliwa_awarie.svg` | do przypisania | Zużycie paliwa w A1 i A2; przekroczenie 900 l w K1 i K2; −24,3% (BESS) w A2 | wyniki V2, tab. A1–A2 | ✅ gotowy (zastępuje F5) |
| `R7_6_Wyczerpanie_zbiornika_A1.svg` | do przypisania | **Rysunek kluczowy.** Paliwo w zbiorniku w funkcji czasu awarii A1; wyczerpanie K1 w 64,0 h, K2 w 68,4 h | wyniki V2 (A1) + tabliczka Grupel | ✅ gotowy |
| `R7_7_Analiza_wrazliwosci_paliwa.svg` | do przypisania | Autonomia przy 900 l dla krzywych 13,1 / 15,5 / 18,0 l/h oraz wyniku HOMER 14,07 l/h | `05_Agregat_GRUPEL_dane_z_tabliczki.md`, sekcje 3–4 | ✅ gotowy |

> **Uwaga do R7_6.** Przebieg wykreślono liniowo przy średnim zużyciu godzinowym z symulacji
> (K1: 1 013 l / 72 h = 14,07 l/h; K2: 948 l / 72 h = 13,17 l/h). Momenty wyczerpania
> (64,0 h i 68,4 h) są z tego wyznaczenia ścisłe; kształt krzywej K2 w rzeczywistości jest
> nieliniowy (praca PV w ciągu dnia). Szereg godzinowy wymaga eksportu z HOMER Pro.

> **Uwaga.** Pliki `F1`–`F5` (PNG) w tym samym folderze pochodzą z serii poprzedniej
> (355 MWh, zbiornik 1 000 l) i są **nieaktualne** — zastąpione przez `R7_1`–`R7_5`.
> Nie należy ich wstawiać do pracy.

### Brakujące

| Proponowany plik | Treść | Przeszkoda |
|---|---|---|
| `R7_8_SoC_BESS_A1.svg` | Stan naładowania magazynu w czasie awarii 72 h | brak szeregu godzinowego — eksport z HOMER Pro (`Time Series`) |
| `R7_9_Praca_zrodel_A1.svg` | Godzinowy rozdział produkcji źródeł w czasie awarii 72 h | jw. |

### Konwencja kolorów rozdziału 7

K1 `#8a6d1f` · K2 `#2c5f8d` · K3 `#4a7a4a` · odniesienie (sama sieć) `#a8a8a8` ·
deficyt / próg zbiornika `#b5452f` (kolor zarezerwowany wyłącznie dla deficytu).

---

## Zasady

- Format **SVG**, pisany ręcznie (nie matplotlib — środowisko bywa niedostępne)
- Styl i paleta: zob. `-agents-/03_Prompt_czat_graficzny.md`
- Język podpisów: **polski**, separator dziesiętny — przecinek
- Każdy rysunek przed wpisaniem do indeksu należy obejrzeć w podglądzie
  i sprawdzić, czy podpisy nie nachodzą na elementy wykresu

---

## Powiązane

**Zasady pracy:** [[03_Prompt_czat_graficzny]]

**Dane do wykresów:**

- [[04_Wyniki_V2_dane_rzeczywiste]] — wyniki symulacji
- [[05_Agregat_GRUPEL_dane_z_tabliczki]] — analiza wrażliwości zużycia paliwa
- [[04_Odpowiedz_szpitala_dane_rzeczywiste]] — zużycie energii w latach 2023–2025

**Rysunki wstawiono do:** [[04_Zalozenia_projektowe_TEKST]]

**Nawigacja:** [[00_STAN_PRAC]]
