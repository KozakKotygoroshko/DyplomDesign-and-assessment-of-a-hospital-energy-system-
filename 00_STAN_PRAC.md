# Stan prac — przegląd dla promotora

**Temat:** Projekt i ocena architektury systemu energetycznego szpitala z kogeneracją,
OZE oraz magazynami energii w kontekście bezpieczeństwa energetycznego

**Autor:** Hlieb Snitko · ZUT w Szczecinie, WKŚiR, Odnawialne Źródła Energii
**Aktualizacja:** 13 października 2026

---

## 1. Postęp w skrócie

| Rozdział | Stan | Uwagi |
|---|---|---|
| 1. Wstęp | ✅ **gotowy** | — |
| 2. Cel i zakres pracy | ✅ **gotowy** | — |
| 3. Przegląd literatury (3.1–3.5) | ✅ **gotowy** | 5 podrozdziałów |
| 4. Założenia projektowe | 🔄 **dane zebrane, redakcja przed nami** | obiekt wybrany i potwierdzony |
| 5. Projekt wariantów zasilania | 🔄 **modele zbudowane, opis przed nami** | 3 konfiguracje × 3 warianty awarii |
| 6. Analiza wyników | 🔄 **obliczenia wykonane, redakcja przed nami** | seria V2 na danych rzeczywistych |
| 7. Wnioski | ⏳ **wniosek zasadniczy ustalony** | wymaga redakcji |
| 8. Bibliografia | ⏳ | zbierana na bieżąco |

**Postęp merytoryczny: ok. 70%. Postęp redakcyjny: ok. 40%.**
Część obliczeniowa jest zamknięta — pozostaje przełożenie wyników na tekst.

---

## 2. Obiekt referencyjny — wybrany i potwierdzony

**Szpital Powiatowy w Pyrzycach**, plac Wolności 2, 74-200 Pyrzyce.
Współrzędne 53°08'49,93"N / 14°53'44,66"E.

Dane pozyskano **w trybie dostępu do informacji publicznej** — szpital odpowiedział
pismem z 21 września 2026 (Dział Gospodarczo-Techniczny). Uzupełniająco wykonano
dokumentację fotograficzną tabliczki znamionowej agregatu.

| Parametr | Wartość | Źródło |
|---|---|---|
| Zużycie energii elektrycznej (2025) | **384,44 MWh** | odpowiedź szpitala |
| Zużycie ciepła (2025) | **2 919 GJ = 810,8 MWh** | odpowiedź szpitala |
| **Źródło ciepła** | **sieć geotermalna** | odpowiedź szpitala |
| Powierzchnia dachu | **2 384 m²** | odpowiedź szpitala |
| Powierzchnia użytkowa / kubatura | 7 495 m² / 29 840 m³ | odpowiedź szpitala |
| Taryfa | B22 | odpowiedź szpitala |
| Agregat podstawowy | **Grupel G0356BDGRAA5T4000S**, 258 kW PRP | tabliczka znamionowa |
| **Pojemność zbiornika** | **1 000 l, napełnienie maks. 90% → 900 l użytecznych** | tabliczka znamionowa |
| Agregat pomocniczy | ZPW 100 DTDEO, 85 kVA, zbiornik 120 l | odpowiedź szpitala |

Praca opiera się zatem **wyłącznie na danych pierwotnych** — nie na wskaźnikach
literaturowych ani wartościach typowych.

---

## 3. Co zostało wykonane

### 3.1. Profile obciążenia (8760 h)

Opracowano godzinowe profile elektryczny i cieplny, kalibrowane na rocznych sumach
rzeczywistych. Profil elektryczny: moc średnia 43,89 kW, szczytowa 61,42 kW,
współczynnik obciążenia 0,715.

Wykazano, że profil syntetyczny generowany przez HOMER Pro **zawyża moc szczytową
3,2-krotnie** dla obiektu tej klasy — uzasadnia to opracowanie profilu własnego.

### 3.2. Modelowanie zdarzeń awaryjnych

Zbudowano szeregi czasowe dwóch typów awarii:

- **A1 — black-sky:** pojedyncza awaria 72 h, 15–17 stycznia (przypadek najbardziej
  niekorzystny: minimum zasobu słonecznego, maksimum zapotrzebowania cieplnego)
- **A2 — seria przerw krótkotrwałych:** 5 zdarzeń, łącznie 21 h, wg statystyki
  SAIDI/SAIFI polskich sieci dystrybucyjnych

### 3.3. Symulacje HOMER Pro

Wykonano **dwie serie obliczeniowe**:

| Seria | Dane | Status |
|---|---|---|
| **A — testowa** | modelowa, 1 GWh/rok | ✅ zamknięta; wnioski metodyczne |
| **B — właściwa (V2)** | rzeczywiste, 384,44 MWh/rok | ✅ zamknięta 21.09.2026 |

Każda seria obejmuje trzy przebiegi (po jednym na wariant awarii), z których każdy
zwraca wszystkie trzy konfiguracje jako wiersze tabeli optymalizacyjnej.

### 3.4. Analiza przestrzenna dachu

Powierzchnię zweryfikowano na państwowej ortofotomapie (Geoportal) oraz potwierdzono
odpowiedzią szpitala. Dach płaski, bez lądowiska. Graniczna moc PV: **ok. 124 kWp**.

---

## 4. Wyniki — stan na dziś

### 4.1. Zestawienie konfiguracji (wariant A1 — awaria 72 h)

| Konfiguracja | CAPEX | Pokrycie awarii | Paliwo | Ograniczenie |
|---|---|---|---|---|
| **K1** — sieć + agregat | 34 000 $ | 100% technicznie | **1 013 l ON** | zbiornik 900 l → **deficyt 113 l**, wyczerpanie w 64,0 h |
| **K2** — + PV + BESS | 180 638 $ | 100% technicznie | **948 l ON** | zbiornik 900 l → **deficyt 48 l**, wyczerpanie w 68,4 h |
| **K3** — + BESS + CHP gazowy | 596 638 $ | 100% | 1 239 m³ gazu | **brak ograniczenia** |

### 4.2. Wniosek zasadniczy

> Z trzech badanych konfiguracji **wyłącznie mikrosieć z kogeneracją gazową pokrywa
> zdarzenie 72-godzinne w pełnym zakresie**. Obie konfiguracje oparte na agregacie
> wysokoprężnym ograniczone są pojemnością użyteczną zbiornika (900 l) i wyczerpują
> zapas paliwa w 64.–68. godzinie awarii.

Wniosek potwierdzono **analizą wrażliwości** obejmującą trzy warianty charakterystyki
zużycia paliwa (13,1 / 15,5 / 18,0 l/h). W żadnym z nich zbiornik nie pokrywa 72 h —
wynik jest zatem odporny na niepewność danych wejściowych.

### 4.3. Wyniki uzupełniające

- **Agregat prądotwórczy nie pracuje ani godziny w roku bezawaryjnym.** Stanowi wyłącznie
  obciążenie kapitałowe — potwierdzenie ilościowe tezy z podrozdziału 3.2.
- **Instalacja PV ograniczona jest powierzchnią dachu, nie ekonomią.** Optymalizator
  osiąga górną granicę zbioru poszukiwań przy każdym jej podniesieniu (110 → 124 → 150 kWp).
  LCOE 0,188 $/kWh, okres zwrotu 6,0 lat, IRR 16%.
- **Magazyn bateryjny nie jest źródłem autonomii, lecz elementem ograniczającym pracę
  agregatu** — redukcja zużycia paliwa o 24,3% w wariancie serii przerw krótkotrwałych.
- **Obiekt zasilany jest ciepłem geotermalnym**, co zmienia ocenę środowiskową
  kogeneracji: CHP nie zastępuje kotła kopalnego, lecz konkuruje ze źródłem odnawialnym.

---

## 5. Co pozostało

### 5.1. Prace redakcyjne — zasadnicza część pozostałego nakładu

| Zadanie | Szacowany nakład |
|---|---|
| Redakcja rozdziału 4 (założenia projektowe) | materiał zebrany w całości |
| Redakcja rozdziału 5 (opis wariantów) | modele gotowe |
| Redakcja rozdziału 6 (analiza wyników) | obliczenia zamknięte |
| Rozdział 7 (wnioski) | wniosek zasadniczy ustalony |
| Bibliografia i aneks | zbierane na bieżąco |

### 5.2. Dane do uzupełnienia

| Pozycja | Wpływ na wynik | Status |
|---|---|---|
| Charakterystyka zużycia paliwa agregatu (DTR Grupel) | zawęża przedział 50–69 h do wartości jednej | pismo wysłane |
| Zakres odbiorów każdego z dwóch agregatów | umożliwia analizę pracy na odbiorach krytycznych | pismo wysłane |
| Obecność zasilaczy UPS | odbiory klasy 0,5 s wg PN-HD 60364-7-710 | pismo wysłane |
| Zasilanie rezerwowe ciepłowni geotermalnej | rozstrzyga o wartości odzysku ciepła w awarii | do ustalenia |
| Profil godzinowy z licznika (OSD) | zastąpienie profilu syntetycznego pomiarem | do ustalenia |

> **Uwaga.** Żadna z powyższych pozycji nie blokuje redakcji pracy. Ich uzupełnienie
> podnosi precyzję, nie zmienia natomiast wniosku zasadniczego.

---

## 6. Pytania do rozstrzygnięcia przez promotora

**6.1. Sposób sformułowania wniosku.** Analiza wykazała, że obiekt rzeczywisty,
formalnie spełniający wymóg § 42 Rozporządzenia Ministra Zdrowia, nie jest zdolny
do przetrwania zdarzenia 72-godzinnego. Czy wniosek ten przedstawić jako główny
rezultat pracy, czy w formie łagodniejszej — jako ograniczenie wykazane w analizie?

**6.2. Informowanie obiektu.** Szpital udostępnił dane dobrowolnie i w trybie pilnym.
Czy wynik analizy powinien zostać im przekazany?

**6.3. Rozszerzenie o pracę wyspową na odbiorach krytycznych.** Ograniczenie zasilania
do odbiorów grup 1 i 2 (18,4 kW zamiast 46,8 kW) wydłuża autonomię ok. dwukrotnie
i może wyprowadzić Konfigurację K1 poza próg 72 h. Czy włączyć to jako odrębny
podrozdział testu przetrwania?

**6.4. Dobór urządzeń — rozdział proponowany.** Symulacja w HOMER Pro operuje
komponentami generycznymi (`Generic flat plate PV`, `Generic converter`) i wyznacza
wyłącznie moce, nie zaś konkretne urządzenia. Słowo „Projekt" w temacie pracy sugeruje
konieczność przełożenia wyznaczonych mocy na dobór sprzętu wraz z obliczeniami
sprawdzającymi.

Proponuje się wprowadzenie odrębnego rozdziału 6 — *Dobór urządzeń i obliczenia
elektryczne* — obejmującego:

| Zakres | Zawartość |
|---|---|
| Moduł fotowoltaiczny | dobór konkretnego modelu, parametry elektryczne i temperaturowe |
| Falownik | dobór mocy, współczynnik DC/AC, konfiguracja wejść MPPT |
| Obliczenia łańcuchów | sprawdzenie Uoc przy −20 °C i Umpp przy +70 °C |
| Przewody | przekroje DC i AC, obciążalność, spadek napięcia |
| Zabezpieczenia | nadprądowe, ograniczniki przepięć, ochrona przeciwporażeniowa |
| Konstrukcja wsporcza | system balastowy, rozstaw rzędów, obciążenie dachu |
| Schemat jednokreskowy | układ połączeń źródeł i rozdziału odbiorów |

**Pytanie:** czy rozdział w takim zakresie jest oczekiwany, czy wystarczy dobór
komponentów z kartami charakterystyki, bez obliczeń sprawdzających? Zakres pełny
istotnie zwiększa objętość pracy.

---

## 7. Struktura repozytorium

```
00_Szkielet_Pracy.md            — spis treści z oznaczeniem stanu
00_Temat_i_metodyka.md          — zasady projektowe, metodyka testu przetrwania
00_STAN_PRAC.md                 — niniejszy dokument
01_Baza_Wiedzy/                 — wymogi edytorskie, instrukcja HOMER, źródła
02_Rozdzialy/
   01_Wstep/                    ✅
   02_Cel_i_zakres_pracy/       ✅
   03_Przeglad_literatury/      ✅ 3.1–3.5
   04_Zalozenia_projektowe/     🔄 dane obiektu, odpowiedź szpitala, tabliczka agregatu
03_Symulacje_Homer/
   A_Symulacje_testowe/         ✅ seria weryfikacyjna
   B_Symulacje_finalne/         ✅ seria właściwa V2 — modele, profile, wyniki, grafika
   Awarie_szeregi_czasowe/      ✅ szeregi A1 i A2
04_Korespondencja/              — pisma do szpitala
```

**Dokumenty najistotniejsze dla oceny postępu:**

1. [[04_Odpowiedz_szpitala_dane_rzeczywiste]] — dane pierwotne obiektu
2. [[05_Agregat_GRUPEL_dane_z_tabliczki]] — ustalenie rozstrzygające (zbiornik 900 l)
3. [[04_Wyniki_V2_dane_rzeczywiste]] — wyniki symulacji na danych rzeczywistych

---

## 8. Mapa dokumentów

### Dane pierwotne (źródła)

- [[04_Odpowiedz_szpitala_dane_rzeczywiste]] — odpowiedź szpitala z 21.09.2026
- [[05_Agregat_GRUPEL_dane_z_tabliczki]] — tabliczka znamionowa agregatu
- [[01_Rzeczywiste_dane_zuzycia_energii]] — dokumentacja przetargowa
- [[02_Charakterystyka_obiektu_Pyrzyce]] — karta obiektu
- [[03_Kwerenda_ogolnopolska_obiekty]] — kwerenda poprzedzająca wybór obiektu
- [[00_Kandydaci_obiekt_referencyjny]] — obiekty rozważane

### Obliczenia

- [[00_PRZEWODNIK_po_folderze]] — przewodnik po seriach symulacyjnych
- [[02_Zasady_symulacji_HOMER]] — zasady obowiązujące przy każdej symulacji
- [[04_Wyniki_V2_dane_rzeczywiste]] — **seria właściwa V2**
- [[01_Wyniki_symulacji_finalnych]] — seria poprzednia (dane szacowane)
- [[00_SYMULACJE_TESTOWE_raport_zbiorczy]] — seria weryfikacyjna
- [[03_Raport_wg_konfiguracji]] — raport wg konfiguracji K1/K2/K3

### Tekst pracy

- [[00_Szkielet_Pracy]] — spis treści ze stanem rozdziałów
- [[00_Temat_i_metodyka]] — temat i zasady projektowe
- [[01_Wstep]] · [[02_Cel_i_zakres_pracy]]
- [[3_1_Szpital_infrastruktura_krytyczna]] · [[3_2_Agregaty_Diesel]] · [[3_3_Instalacje_PV]] · [[3_4_Magazyny_BESS]] · [[3_5_Kogeneracja_CHP]]
- [[04_Zalozenia_projektowe_TEKST]] — rozdział 4

### Materiał graficzny i korespondencja

- [[00_INDEKS_RYSUNKOW]] — rejestr rysunków
- [[03_Prompt_czat_graficzny]] — zasady pracy czatu graficznego
- [[Pismo_2_DTR_agregatu]] — pismo uzupełniające do szpitala

---

> **Uwaga redakcyjna.** Struktura folderów w `02_Rozdzialy/` odpowiada numeracji
> sprzed wprowadzenia proponowanego rozdziału *Dobór urządzeń i obliczenia elektryczne*
> (punkt 6.4 powyżej). Jeżeli promotor rozdział zatwierdzi, foldery od 06 wzwyż
> wymagają przenumerowania.
