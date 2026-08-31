# Szpital Powiatowy w Pyrzycach — karta obiektu

Zestawienie danych zgromadzonych na potrzeby oceny przydatności obiektu jako
referencyjnego dla pracy dyplomowej.

**Adres:** ul. Jana Pawła II 2, 74-200 Pyrzyce
**Odległość od Szczecina:** ok. 45 km
**Organ założycielski:** Powiat Pyrzycki

---

## 1. Dane energetyczne (potwierdzone)

| Parametr | Wartość | Źródło |
|---|---|---|
| **Roczne zużycie energii elektrycznej** | **355 MWh** | Dokumentacja przetargowa 2021 |
| Wolumen kontraktowy | 1 420 MWh / 4 lata | jw. |
| **Grupa taryfowa** | **B (średnie napięcie)** | jw. |
| Struktura umów | rozdzielone: sprzedaż + dystrybucja | jw. |
| Układ pomiarowy | dostosowany do zasady TPA | jw. |
| Okres rozliczeniowy | miesięczny | jw. |
| Status prosumenta / wytwórcy OZE | **brak** | jw. |

### Wielkości wyprowadzone

| Wielkość | Wartość | Sposób wyznaczenia |
|---|---|---|
| Moc średnia | 40,5 kW | 355 000 kWh ÷ 8760 h |
| Moc szczytowa (szacunek) | ok. 57 kW | przy LF = 0,71 |
| Zużycie dobowe | 972 kWh/d | 355 000 ÷ 365 |
| Wskaźnik jednostkowy | 2 367 kWh/łóżko/rok | przy 150 łóżkach |

> **Znaczenie grupy taryfowej B:** przyłącze średniego napięcia oznacza obecność
> własnej stacji transformatorowej. Jest to okoliczność **korzystna** dla projektu
> mikrosieci — istnieje fizyczna możliwość przyłączenia źródeł wytwórczych po stronie
> SN oraz realizacji podziału na sekcje zasilania.

---

## 2. Profil medyczny — stan aktualny

Struktura organizacyjna uległa **redukcji** względem danych archiwalnych, co tłumaczy
stosunkowo niskie zużycie energii.

| Komórka | Stan wg danych archiwalnych | **Stan aktualny** |
|---|---|---|
| Oddział Chorób Wewnętrznych | 60 łóżek (4 INK) | **czynny** |
| Oddział Chirurgii Ogólnej | 25 łóżek | **czynny** |
| Oddział Chirurgii Urazowo-Ortopedycznej | 30 łóżek | **czynny** |
| Oddział Anestezjologii i Intensywnej Terapii | 5 łóżek | **czynny** |
| Blok Operacyjny | tak | **czynny** |
| Izba Przyjęć | tak | **czynna** |
| Zakład Opiekuńczo-Leczniczy | — | **czynny** |
| Oddział Położnictwa i Ginekologii | 20 łóżek | **zlikwidowany** (pozostała poradnia) |
| Oddział Neonatologiczny | 10 łóżeczek | **zlikwidowany** |

**Szacunkowa liczba łóżek stanu aktualnego: ok. 120** (oddziały czynne) plus ZOL.

### Odbiory krytyczne występujące w obiekcie

| Odbiór | Klasa przerwy | Grupa wg IEC 60364-7-710 |
|---|---|---|
| Blok operacyjny — oświetlenie pola i aparatura | **0,5 s** | **Grupa 2** |
| Oddział Anestezjologii i Intensywnej Terapii (5 łóżek) | **0,5 s** | **Grupa 2** |
| Tomograf komputerowy | 15 s | Grupa 1 |
| Pracownia RTG, USG, endoskopowa | 15 s | Grupa 1 |
| Oświetlenie ewakuacyjne, gazy medyczne | 15 s | — |
| Lądowisko dla śmigłowców — oświetlenie nawigacyjne | **0,5 s** | — |

Obecność bloku operacyjnego oraz OAiIT przesądza o kwalifikacji obiektu do
**grupy 2** według normy IEC 60364-7-710, z wynikającym stąd wymogiem sieci
izolowanej IT oraz zasilania klasy 0,5 s.

---

## 3. Charakterystyka budynku

| Cecha | Informacja | Status |
|---|---|---|
| **Termomodernizacja** | **przeprowadzona ze środków UE** | **potwierdzona** |
| Zakres modernizacji | ocieplenie, dostosowanie do wymogów technicznych | potwierdzony |
| Deklarowany efekt | obniżenie kosztów stałych jednostki | potwierdzony |
| **Lądowisko dla śmigłowców** | **obiekt dysponuje** | **potwierdzone** |
| Umiejscowienie lądowiska | **do ustalenia** (dach czy poziom terenu) | **wymaga weryfikacji** |
| Powierzchnia użytkowa | brak danych | do pozyskania |
| Liczba kondygnacji | brak danych | do pozyskania |
| Rodzaj przekrycia dachu | brak danych | do pozyskania |

### 3.1. Znaczenie faktu przeprowadzenia termomodernizacji

Realizacja termomodernizacji ze środków unijnych oznacza, że dla obiektu **sporządzono
audyt energetyczny** — dokument obligatoryjny w procedurze aplikacyjnej. Audyt taki
zawiera komplet danych niezbędnych dla pracy:

- powierzchnię użytkową i ogrzewaną,
- kubaturę budynku,
- **zapotrzebowanie na ciepło** (c.o. i c.w.u.) przed i po modernizacji,
- charakterystykę źródła ciepła (kotłownia własna lub sieć ciepłownicza),
- współczynniki przenikania ciepła przegród,
- powierzchnię dachu.

**Ścieżka pozyskania:** wniosek do Starostwa Powiatowego w Pyrzycach lub dyrekcji
szpitala o udostępnienie audytu energetycznego — jako dokumentu wytworzonego ze
środków publicznych podlega on udostępnieniu w trybie dostępu do informacji publicznej.

### 3.2. Lądowisko dla śmigłowców — czynnik krytyczny dla analizy PV

Obecność lądowiska wymaga bezwzględnego ustalenia jego lokalizacji.

| Wariant | Skutek dla instalacji PV |
|---|---|
| Lądowisko **na poziomie terenu** | Brak wpływu na powierzchnię dachu |
| Lądowisko **na dachu** | Wyłączenie znacznej części powierzchni; dodatkowo strefy podejścia i przeszkód lotniczych ograniczają zabudowę dachu w promieniu określonym przepisami lotniczymi |

Weryfikacja możliwa na zdjęciu satelitarnym — lądowisko dachowe jest rozpoznawalne
po charakterystycznym oznakowaniu (litera H w okręgu).

---

## 4. Ocena przydatności obiektu

### Argumenty za

**Dostępność danych rzeczywistych.** Zużycie energii elektrycznej potwierdzone
dokumentem przetargowym — nie jest to szacunek literaturowy.

**Pełny profil odbiorów krytycznych.** Blok operacyjny i OAiIT kwalifikują obiekt do
grupy 2 wg IEC 60364-7-710, co czyni analizę bezpieczeństwa energetycznego zasadną
merytorycznie, a nie wyłącznie formalną.

**Przyłącze średniego napięcia.** Grupa taryfowa B oznacza własną stację
transformatorową i realną możliwość przyłączenia źródeł wytwórczych.

**Istniejący audyt energetyczny.** Termomodernizacja ze środków UE gwarantuje
istnienie dokumentacji z danymi cieplnymi i budowlanymi.

**Brak instalacji OZE.** Status „brak wytwórcy / prosumenta" oznacza, że projekt
dotyczy stanu wyjściowego, bez konieczności uwzględniania istniejących instalacji.

**Skala odpowiednia dla pracy inżynierskiej.** Moc szczytowa rzędu 57 kW pozwala na
dobór komponentów o mocach dostępnych w katalogach — instalacja PV 60–100 kWp,
kogeneracja 30–50 kW, magazyn 100–200 kWh.

### Argumenty przeciw i ryzyka

**Zużycie niższe od pierwotnie zakładanego.** 355 MWh wobec przyjętego 1 GWh —
wymaga przeskalowania wszystkich profili i ponownego doboru komponentów.

**Lądowisko o nieustalonej lokalizacji.** W przypadku umiejscowienia na dachu
możliwości instalacji PV ulegają istotnemu ograniczeniu.

**Dane z roku 2021.** Wymagają aktualizacji — po likwidacji dwóch oddziałów zużycie
mogło ulec dalszemu obniżeniu.

**Bryła budynku niezweryfikowana.** Warunek monobloku pozostaje niepotwierdzony.

---

## 5. Zadania weryfikacyjne

| Zadanie | Źródło | Priorytet |
|---|---|---|
| Ustalenie lokalizacji lądowiska | Zdjęcie satelitarne / Geoportal | **krytyczny** |
| Potwierdzenie zwartości bryły (monoblok) | Zdjęcie satelitarne | **krytyczny** |
| Pomiar powierzchni dachu | Geoportal — narzędzie pomiaru | **krytyczny** |
| Pozyskanie audytu energetycznego | Wniosek o informację publiczną | wysoki |
| Aktualizacja danych o zużyciu (2024–2026) | Nowsze postępowania przetargowe | wysoki |
| Zapotrzebowanie na ciepło i źródło ciepła | Audyt / przetarg na gaz lub ciepło | wysoki |
| Parametry istniejącego agregatu | Dokumentacja techniczna obiektu | średni |

---

## 6. Wniosek wstępny

Obiekt spełnia kryteria merytoryczne pracy: posiada odbiory grupy 2, przyłącze SN,
udokumentowane zużycie energii oraz istniejącą dokumentację energetyczną.
Rekomenduje się **utrzymanie obiektu jako głównego kandydata**, pod warunkiem
pozytywnej weryfikacji geometrii bryły i dachu na materiałach kartograficznych.

**Źródła:**
- Szpital Powiatowy w Pyrzycach, „Dotyczy postępowania: Zakup energii elektrycznej", 30.03.2021 — http://szpital.pyrzyce.net.pl/?p=8988
- Szpital Powiatowy w Pyrzycach, „Szpital o nas" — http://szpital.pyrzyce.net.pl/?page_id=1912
