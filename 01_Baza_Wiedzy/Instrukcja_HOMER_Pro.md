# Instrukcja obsługi HOMER Pro — budowa modelu mikrosieci szpitalnej

Dokument roboczy. Opisuje kolejne kroki konfiguracji modelu w HOMER Pro x64 3.18.4
(Evaluation Edition) na przykładzie obiektu referencyjnego w Pyrzycach.

> **Uwaga o wersji:** wersja Evaluation posiada ograniczenia (m.in. brak możliwości
> zapisu plików i eksportu części wyników). Do finalnych symulacji wymagana jest
> licencja pełna lub akademicka.

---

## 1. Konfiguracja projektu (zakładka DESIGN → Home)

Po uruchomieniu programu otwiera się widok **DESIGN** z panelem `REQUIRED CHANGES`,
który wskazuje brakujące elementy modelu:

- `Add a load` — brak zdefiniowanego odbioru
- `Add a power source` — brak źródła zasilania
- `Add a renewable energy source` — brak źródła odnawialnego

### 1.1. Dane identyfikacyjne

| Pole | Wartość przyjęta |
|---|---|
| Name | `Test_Mikrosiec_Szpital_Scenariusz_2` |
| Author | Hlieb Snitko |
| Description | (opcjonalnie — opis wariantu) |

### 1.2. Lokalizacja

W polu wyszukiwania pod mapą wpisano nazwę miejscowości i **zatwierdzono klawiszem
Enter** (przycisk `Location Search` bywa zawodny — mapa potrafi przeskoczyć na
przypadkowe współrzędne).

Wynik: `plac Wolności 2, 74-200 Pyrzyce, Poland (53°8.8'N, 14°53.5'E)`

Strefa czasowa ustawia się automatycznie: `(UTC+01:00) Sarajevo, Skopje, Warsaw`.

> Współrzędne są kluczowe — na ich podstawie HOMER pobiera dane o nasłonecznieniu
> (NASA POWER) oraz temperaturze otoczenia dla modułów PV.

### 1.3. Parametry ekonomiczne (dolna część ekranu)

| Parametr | Domyślnie | Uwaga dla pracy |
|---|---|---|
| Discount rate (%) | 8,00 | do korekty wg stopy dyskontowej dla PL |
| Inflation rate (%) | 2,00 | do korekty wg celu inflacyjnego NBP |
| Annual capacity shortage (%) | 0,00 | **0% — wymóg dla obiektu infrastruktury krytycznej** |
| Project lifetime (years) | 25,00 | zgodne z żywotnością modułów PV |

Zerowa dopuszczalna niedostatecznosć mocy (`capacity shortage = 0%`) jest założeniem
wynikającym wprost z charakteru obiektu i powinna zostać uzasadniona w pracy.

---

## 2. Definicja obciążenia elektrycznego (LOAD → Electric #1)

Po kliknięciu `Electric #1` otwiera się `ELECTRIC LOAD SETUP` z trzema wariantami
wprowadzenia danych:

| Metoda | Zastosowanie |
|---|---|
| **Create a synthetic load from a profile** | Profil syntetyczny z biblioteki (Residential, Commercial, Industrial, Community, Blank) |
| **Access the Open EI Database** | Baza profili USA — dopasowanie po klasyfikacji klimatycznej Köppena-Geigera |
| **Import a load from a time series file** | **Import własnego pliku CSV (8760 h) — metoda docelowa dla pracy** |

### 2.1. Skalowanie profilu

Niezależnie od wybranego profilu bazowego, jego wielkość ustawia się polem
`Scaled Annual Average (kWh/day)` w dolnej części ekranu.

Dla założonego zużycia **1 GWh/rok**:

```
1 000 000 kWh / 365 dni = 2 740 kWh/dobę
```

**Sposób wprowadzenia wartości (istotne):** wpisanie liczby i naciśnięcie `Tab`
lub `Enter` **nie aktualizuje** tabeli metryk. Konieczne jest kliknięcie w dowolne
inne miejsce okna, aby wartość została zatwierdzona.

### 2.2. Wynik skalowania profilu przemysłowego

| Metric | Baseline | Scaled |
|---|---|---|
| Average (kWh/day) | 11,26 | 2 740 |
| Average (kW) | 0,47 | 114,17 |
| Peak (kW) | 2,09 | 508,72 |
| Load factor | 0,22 | 0,22 |

### 2.3. Wniosek metodyczny — dlaczego profil syntetyczny nie wystarczy

Uzyskany **współczynnik obciążenia (load factor) = 0,22** jest charakterystyczny dla
budynków mieszkalnych i **nie odpowiada rzeczywistości obiektu szpitalnego**, dla
którego wartość ta mieści się w przedziale **0,6–0,7** (praca ciągła 24/7, wypłaszczony
profil dobowy).

Konsekwencją zawyżonego rozrzutu jest nierealistycznie wysoka moc szczytowa
(508,72 kW przy średniej 114,17 kW), co prowadziłoby do przewymiarowania agregatu,
magazynu BESS oraz przekształtników.

**Wniosek:** dla pracy dyplomowej konieczne jest przygotowanie własnego profilu
godzinowego (8760 wartości) i zaimportowanie go przez `Import a load from a time
series file`. Profil taki musi odwzorowywać:

- wypłaszczony przebieg dobowy z płytką doliną nocną,
- podwyższone obciążenie w godzinach pracy bloku operacyjnego i diagnostyki,
- sezonową zmienność wynikającą z chłodzenia (lato) i wentylacji (zima).

---

## 3. Dodawanie komponentów (zakładka COMPONENTS)

*(sekcja w trakcie uzupełniania)*

---

## Napotkane problemy techniczne i obejścia

| Problem | Obejście |
|---|---|
| Przycisk `Location Search` przenosi mapę na błędne współrzędne | Wpisać nazwę w polu i zatwierdzić klawiszem `Enter` |
| Pole `Scaled Annual Average` nie aktualizuje metryk po `Tab`/`Enter` | Kliknąć w inne miejsce okna, aby zatwierdzić wartość |
| Okno nie reaguje na przycisk maksymalizacji | Dwukrotne kliknięcie w pasek tytułu |
