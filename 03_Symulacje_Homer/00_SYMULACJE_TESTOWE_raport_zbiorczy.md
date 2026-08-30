# Symulacje testowe w HOMER Pro — raport zbiorczy

> ## ⚠ STATUS: SYMULACJE TESTOWE
>
> Niniejszy dokument przedstawia **wstępną, weryfikacyjną serię symulacji**.
> Obiekt referencyjny nie został jeszcze wybrany, a profile obciążenia mają charakter
> modelowy — opracowano je na podstawie wskaźników literaturowych, nie zaś pomiarów.
> Celem serii było sprawdzenie poprawności przyjętej metodyki, rozpoznanie możliwości
> narzędzia oraz identyfikacja pułapek modelowych **przed** przystąpieniem do obliczeń
> właściwych. Wartości liczbowe nie stanowią wyników końcowych pracy.

Środowisko: HOMER Pro x64 3.18.4 (Evaluation Edition)
Lokalizacja modelowa: Szczecin, 53°25,7'N / 14°33,2'E

---

## 1. Dane wejściowe

### 1.1. Zasoby środowiskowe (NASA POWER, średnie z lat 1983–2025)

| Wielkość | Wartość roczna | Minimum | Maksimum |
|---|---|---|---|
| Napromieniowanie GHI | 2,72 kWh/m²/d (≈ 993 kWh/m²/rok) | XII: 0,58 | V: 4,96 |
| Temperatura otoczenia | 8,32 °C | I: −1,68 °C | VII: 18,75 °C |

Stosunek napromieniowania maj/grudzień wynosi **8,6 : 1**.

### 1.2. Profile obciążenia

Opracowano dwa profile godzinowe (8760 wartości), wspólne dla wszystkich scenariuszy.

| Parametr | Profil elektryczny | Profil cieplny |
|---|---|---|
| Energia roczna | 1 000 MWh | 1 800 MWh |
| Moc średnia | 114,16 kW | 205,48 kW |
| Moc szczytowa | 159,76 kW | 537,22 kW |
| Moc minimalna | 71,41 kW | 13,43 kW |
| Współczynnik obciążenia | **0,715** | 0,382 |
| Miesiąc szczytowy | sierpień | styczeń |

**Struktura profilu cieplnego:** c.o. 63,9% (1 150 MWh, sterowane stopniodniami dla
temperatury bazowej 15 °C), c.w.u. 25,0% (450 MWh, całoroczne), sterylizacja i pralnia
11,1% (200 MWh, dni robocze 6:00–18:00).

**Letnia baza cieplna:** VI–VIII moc średnia 73–75 kW — wartość determinująca dobór
mocy cieplnej jednostki kogeneracyjnej.

### 1.3. Weryfikacja profilu elektrycznego

| Metryka | Profil syntetyczny HOMER | Profil własny | Wartość literaturowa dla szpitali |
|---|---|---|---|
| Moc szczytowa | 508,72 kW | **159,76 kW** | — |
| Współczynnik obciążenia | 0,22 | **0,715** | 0,6–0,7 |

Profil wbudowany zawyża moc szczytową **3,2-krotnie**, prowadząc do przewymiarowania
wszystkich komponentów. Zastosowanie profilu własnego jest zatem warunkiem koniecznym
wiarygodności wyników.

### 1.4. Parametry ekonomiczne i komponenty

| Parametr | Wartość |
|---|---|
| Stopa dyskontowa / inflacja | 8% / 2% |
| Okres analizy | 25 lat |
| Cena energii z sieci / odsprzedaży | 0,220 / 0,090 $/kWh |
| Cena gazu ziemnego | 0,65 $/m³ |
| Cena oleju napędowego | 1,55 $/L |

| Komponent | Model | CAPEX | Parametry |
|---|---|---|---|
| PV | Generic flat plate | 800 $/kW | derating 80%, 25 lat |
| BESS | Generic 100 kWh Li-Ion | 30 000 $/szt. | SoC min **40%**, η 90% |
| Przekształtnik | System Converter | 300 $/kW | η 95% |
| Agregat | Autosize Genset (Diesel) | 500 $/kW | min. obciążenie 25% |
| **CHP** | **2G Aura 404** | **450 000 $** | **100 kW, gaz ziemny, odzysk ciepła 57,2%, min. obciążenie 50%, 60 000 h** |
| Kocioł | Generic Boiler | — | η 85%, gaz ziemny |

**Ograniczenie przestrzenne:** moc PV ograniczono do zbioru {0; 100; 150; 200; 250} kW
zgodnie z szacowaną powierzchnią stropodachu 1 000–1 500 m².

---

## 2. Konfiguracje i warianty awarii

### Konfiguracje

| Oznaczenie | Architektura |
|---|---|
| **K1 — Baza** | Sieć + agregat prądotwórczy (Diesel) |
| **K2 — Hybryda** | Sieć + agregat + PV + BESS |
| **K3 — Mikrosieć** | Sieć + PV + BESS + **CHP gazowy** + kocioł szczytowy |

### Warianty awarii sieci

| Wariant | Charakterystyka | Plik |
|---|---|---|
| **A0** | Brak awarii — praca normalna | — |
| **A1 — Black-sky** | Pojedyncza awaria **72 h**, 15–17 stycznia | `Awaria_blacksky_72h_styczen.csv` |
| **A2 — Serie krótkie** | **5 przerw**, łącznie **21 h** (SAIDI 1260 min, SAIFI 5/rok) | `Awaria_seria_krotkich_przerw.csv` |

Wariant A2 odwzorowuje statystykę polskich sieci dystrybucyjnych: przerwy o czasie
trwania 2–7 h rozłożone w ciągu roku (styczeń, marzec, czerwiec, wrzesień, listopad).

> **Konwencja zapisu szeregu czasowego w HOMER:** wartość **1 = sieć dostępna**,
> **0 = awaria**. Konwencja odwrotna do intuicyjnej.

W wariantach A1 i A2 dopuszczalny niedobór mocy podniesiono z 0% na 10% — przy
wartości zerowej optymalizator odrzuca wszystkie konfiguracje jako niedopuszczalne,
uniemożliwiając pomiar skali niedoboru.

---

## 3. Wyniki — wariant A0 (praca normalna)

| Konfiguracja | NPC | LCOE [$/kWh] | CAPEX | Koszt operacyjny [$/rok] | Udział OZE | Zwrot |
|---|---|---|---|---|---|---|
| K1 — sama sieć (odniesienie) | 2,84 M$ | 0,220 | 0 $ | 220 000 | 0% | — |
| K1 — sieć + agregat 180 kW | 2,91 M$ | 0,225 | 90 000 $ | 218 374 | 0% | — |
| **K2 — PV 250 kW** | **2,54 M$** | **0,196** | 245 000 $ | 177 865 | 21,0% | **5,7 lat** |
| K2 — PV 250 + BESS 100 kWh | 2,58 M$ | 0,199 | 273 500 $ | 178 638 | 21,4% | 6,3 lat |

**Obserwacja K1:** agregat pracuje **0 godzin w roku**. Stanowi wyłącznie obciążenie
kapitałowe podnoszące NPC o 2,5%, bez udziału w produkcji energii — ilościowe
potwierdzenie tezy o pasywnym charakterze klasycznego zasilania rezerwowego.

**Obserwacja K2:** produkcja PV 232 811 kWh/rok (931 kWh/kWp — wartość typowa dla PL),
z czego do sieci oddano jedynie 5 400 kWh. **Autokonsumpcja 97,7%.**

### Wpływ ograniczenia przestrzennego

| Wariant | Moc PV | Wymagana powierzchnia | LCOE | Okres zwrotu |
|---|---|---|---|---|
| Bez ograniczeń | 1 043 kWp | 5 000–6 000 m² | 0,123 $/kWh | 8,5 lat |
| **Z ograniczeniem** | **250 kWp** | 1 000–1 500 m² | 0,196 $/kWh | **5,7 lat** |

Ograniczenie mocy PV pogarsza wskaźnik LCOE, lecz **skraca okres zwrotu** — cała
energia jest konsumowana lokalnie po pełnej stawce taryfowej, bez odsprzedaży nadwyżek.

---

## 4. Wyniki — konfiguracja K3 z CHP gazowym

Zastąpienie generycznego agregatu wysokoprężnego rzeczywistą jednostką kogeneracyjną
**2G Aura 404** zmieniło wynik optymalizacji w sposób zasadniczy.

| Wskaźnik | K3 z CHP **diesel** | K3 z CHP **gazowym** |
|---|---|---|
| Czy CHP wybrany przez optymalizator? | **NIE** (0 h pracy) | **TAK** |
| NPC | 4,35 M$ | **4,30 M$** |
| LCOE | 0,196 $/kWh | **0,192 $/kWh** |
| Godziny pracy CHP | 0 | **7 112 h/rok (81% roku)** |
| Produkcja CHP | 0 | **662 876 kWh/rok** |
| Zużycie gazu | — | 193 533 m³/rok |
| Okres zwrotu | — | 7,9 lat |

**Przyczyna:** jednostka `Autosize Genset` pracuje wyłącznie na oleju napędowym
(1,55 $/L). Koszt wytworzenia energii przewyższał wówczas cenę zakupu z sieci połączoną
z produkcją ciepła w kotle gazowym. Zasilanie gazem ziemnym (0,65 $/m³) odwraca tę relację.

### Struktura pokrycia zapotrzebowania elektrycznego (K3, wariant A0)

| Źródło | Energia [kWh/rok] | Udział |
|---|---|---|
| Kogeneracja Aura 404 | 662 876 | **64,6%** |
| Instalacja PV | 232 811 | 22,7% |
| Zakup z sieci | 129 927 | 12,7% |

Obiekt pokrywa **87,3% zapotrzebowania ze źródeł własnych**.

---

## 5. Wyniki — wariant A1 (black-sky 72 h, styczeń)

Pomiar zasadniczy: **energia niedostarczona** (*Unmet Electric Load*).

| Konfiguracja | Energia niedostarczona | Pokrycie deficytu | Paliwo |
|---|---|---|---|
| Sama sieć (bez rezerwy) | **8 762 kWh** | 0% | — |
| PV 150 kW + BESS 200 kWh | 7 966 kWh | **9,1%** | — |
| **PV 250 + CHP gazowy 100 kW** | **1 046 kWh** | **88,1%** | 193 584 m³ gazu |
| Agregat Diesel 180 kW | **0 kWh** | 100% | 2 425 L ON |

### 5.1. Dlaczego PV + BESS nie zapewniają autonomii zimą

**Ograniczenie zasobu:** w styczniu napromieniowanie wynosi 0,73 kWh/m²/d — 15% wartości
majowej. Produkcja PV występuje wyłącznie w godzinach 9:00–15:00.

**Ograniczenie pojemności:** magazyn 200 kWh przy minimalnym SoC 40% udostępnia 120 kWh
energii użytecznej. Przy obciążeniu styczniowym ~120 kW odpowiada to **około jednej
godzinie** pracy autonomicznej wobec wymaganych 72 godzin.

Wniosek: **BESS w rozpatrywanej skali nie stanowi źródła autonomii długoterminowej**,
lecz element pomostowy zapewniający ciągłość w klasie 0,5 s do czasu uruchomienia
źródła sterowalnego — zgodnie z rolą przypisaną w podrozdziale 3.4.

### 5.2. Przewaga kogeneracji gazowej nad agregatem wysokoprężnym

Oba źródła sterowalne zapewniają porównywalne pokrycie deficytu, różnią się jednak
zasadniczo pod względem **odporności logistycznej**:

| Kryterium | Agregat Diesel | CHP gazowy |
|---|---|---|
| Zapotrzebowanie na paliwo (72 h) | 2 425 L | 193 584 m³/rok (dostawa ciągła) |
| Sposób dostawy | transport drogowy | sieć gazowa |
| Podatność na *black-sky* | **wysoka** — przy typowej pojemności zbiornika 1 000–1 500 l konieczne uzupełnienie w trakcie zdarzenia | **niska** — sieć gazowa niezależna od transportu drogowego |
| Praca poza awarią | 0 h/rok | 7 112 h/rok (produkcja ciągła) |

Kogeneracja gazowa eliminuje zależność od łańcucha dostaw paliwa opisaną w podrozdziale 3.2,
jednocześnie uczestnicząc w bieżącej optymalizacji kosztów przez cały rok.

---

## 6. Wyniki — wariant A2 (seria 5 przerw krótkotrwałych, 21 h)

| Konfiguracja | Energia niedostarczona | Niedobór mocy | Redukcja względem wariantu bazowego |
|---|---|---|---|
| Sama sieć (bez rezerwy) | **2 520 kWh (0,252%)** | 2 772 kWh | — |
| **PV 250 + CHP gazowy 100 kW** | **279 kWh (0,028%)** | 628 kWh | **−88,9%** |

Konfiguracja z kogeneracją redukuje energię niedostarczoną **niemal dziewięciokrotnie**.
Pozostałe 279 kWh odpowiada przerwom występującym w godzinach, w których jednostka CHP
pracowała z mocą niższą od chwilowego zapotrzebowania.

---

## 7. Zestawienie zbiorcze

| | K1 Baza | K2 Hybryda | K3 Mikrosieć (CHP gaz) |
|---|---|---|---|
| **NPC (A0)** | 2,84 M$ | 2,54 M$ | 4,30 M$ ¹ |
| **LCOE (A0)** | 0,220 | 0,196 | 0,192 |
| **CAPEX** | 0–90 tys. $ | 245 tys. $ | 695 tys. $ |
| **Okres zwrotu** | — | 5,7 lat | 7,9 lat |
| **Udział źródeł własnych** | 0% | 21,0% | **87,3%** |
| **Energia niedostarczona (A1)** | 8 762 kWh | 7 966 kWh | **1 046 kWh** |
| **Energia niedostarczona (A2)** | 2 520 kWh | — | **279 kWh** |
| **Emisje CO₂** | — | 914,5 t/rok ² | — |
| **Odporność na black-sky** | zależna od zapasu paliwa | brak | **wysoka** |

¹ Wartości NPC dla K3 obejmują dodatkowo koszt paliwa gazowego na pokrycie zapotrzebowania
cieplnego (1 800 MWh/rok). Bezpośrednie porównanie z K1 i K2 wymaga wprowadzenia szyny
cieplnej również do tych konfiguracji.

² Wartość dla konfiguracji K2 w wariancie A0.

---

## 8. Ocena konfiguracji pod kątem bezpieczeństwa energetycznego

Odpowiedź na zasadnicze pytanie pracy: **która architektura najlepiej realizuje wymóg
ciągłości zasilania obiektu infrastruktury krytycznej.** Kryterium ekonomiczne pełni
tu rolę podrzędną wobec kryterium niezawodności.

### 8.1. Ocena porównawcza

| Kryterium | K1 Baza | K2 Hybryda | K3 Mikrosieć |
|---|---|---|---|
| Energia niedostarczona (A1, 72 h) | 0 kWh ¹ | 7 966 kWh | **1 046 kWh** |
| Energia niedostarczona (A2) | 0 kWh ¹ | — | **279 kWh** |
| Czas autonomii bez uzupełnienia paliwa | 30–45 h ² | ok. 1 h | **nieograniczony** ³ |
| Niezależność od transportu drogowego | **NIE** | tak | **TAK** |
| Pokrycie klasy 0,5 s | **NIE** | TAK | **TAK** |
| Udział źródeł własnych | 0% | 21,0% | **87,3%** |
| Praca poza awarią | 0 h/rok | — | **7 112 h/rok** |
| LCOE [$/kWh] | 0,220–0,225 | 0,196 | **0,192** |

¹ Wyłącznie w wariancie z agregatem. Bez agregatu: 8 762 kWh.
² Przy zbiorniku 1 000–1 500 l i zużyciu 33,7 l/h — **niewystarczające na 72 h**.
³ Pod warunkiem ciągłości dostaw gazu siecią dystrybucyjną.

### 8.2. Konfiguracja rekomendowana: K3 — mikrosieć z kogeneracją gazową

Cztery argumenty rozstrzygające:

**Redukcja energii niedostarczonej o 88%** względem układu bez rezerwy, przy zachowaniu
tej zdolności w **obu** badanych typach awarii — długotrwałej i serii przerw krótkich.

**Niezależność od transportu drogowego paliwa.** Cecha odróżniająca kogenerację gazową
od agregatu w sposób jakościowy: w scenariuszu *black-sky*, gdy infrastruktura
transportowa ulega dezorganizacji, agregat zachowuje zdolność wytwórczą wyłącznie do
wyczerpania zbiornika — oszacowanego na **30–45 h wobec wymaganych 72**.

**Praca ciągła przez 81% roku.** Jednostka CHP nie jest urządzeniem oczekującym
w spoczynku, lecz elementem czynnym o sprawności weryfikowanej w sposób ciągły.
Eliminuje to ryzyko niepowodzenia rozruchu w sytuacji awaryjnej — istotną przyczynę
zawodności klasycznych układów rezerwowych.

**Najniższy LCOE (0,192 $/kWh).** Zwiększenie bezpieczeństwa nie odbywa się kosztem
pogorszenia wskaźników ekonomicznych.

### 8.3. Konfiguracja docelowa — architektura hierarchiczna

Żadna z badanych konfiguracji **nie zapewnia pełnego pokrycia** we wszystkich
scenariuszach. K3 pozostawia 1 046 kWh energii niedostarczonej — wartość dla szpitala
niedopuszczalną. Jako rozwiązanie docelowe proponuje się układ czteropoziomowy:

| Poziom | Źródło | Funkcja | Czas reakcji |
|---|---|---|---|
| **I** | BESS | Odbiory klasy 0,5 s, tryb *grid-forming* | milisekundy |
| **II** | CHP gazowy | Podstawowe źródło autonomii, obciążenie bazowe | minuty |
| **III** | PV | Wsparcie sezonowe, redukcja poboru z sieci | — |
| **IV** | Agregat Diesel | **Rezerwa ostatniej instancji** — przy jednoczesnej awarii sieci gazowej | 15 s |

W układzie takim agregat zachowuje rolę rezerwy ostatniej instancji, uruchamianej
wyłącznie przy jednoczesnej niedostępności sieci elektroenergetycznej **i** gazowej.
Jego moc może zostać ograniczona do **ustawowego minimum 30%** mocy szczytowej,
ponieważ obciążenie bazowe przejmuje jednostka kogeneracyjna — co obniża nakłady
względem układu klasycznego, gdzie agregat wymiarowany jest na pełne obciążenie.

Weryfikacja ilościowa tej architektury stanowi przedmiot obliczeń właściwych.

---

## 9. Wnioski metodyczne

### 9.1. Kryterium najniższego NPC prowadzi do rozwiązania niedopuszczalnego

We wszystkich wariantach awaryjnych konfiguracją o najniższym koszcie bieżącym netto
pozostaje układ **pozbawiony źródła rezerwowego** — ten sam, który generuje kilka tysięcy
kilowatogodzin energii niedostarczonej. Optymalizator uznaje niedostarczenie energii do
szpitala za rozwiązanie tańsze niż zakup źródła rezerwowego.

Koszt zapewnienia pełnego pokrycia wynosi ok. **220 000 $ NPC** (wzrost LCOE o 16%).

**Konsekwencja dla pracy:** ocena wielokryterialna w rozdziale 6 musi traktować energię
niedostarczoną jako **ograniczenie twarde** (`Unmet Load = 0`), nie zaś jako składnik
funkcji celu.

### 9.2. Ograniczenie przestrzenne jest warunkiem wiarygodności

Bez ograniczenia mocy PV optymalizator wskazuje konfigurację wymagającą powierzchni
pięciokrotnie większej od dostępnej. Wprowadzenie zbioru dopuszczalnych mocy na podstawie
analizy CAD rozmieszczenia modułów jest niezbędne.

### 9.3. Dobór jednostki CHP determinuje sens Scenariusza 3

Generyczny agregat wysokoprężny nie jest dysponowany przez optymalizator w żadnym
wariancie. Zastosowanie rzeczywistej jednostki gazowej z katalogu producenta zmienia
wynik jakościowo — kogeneracja pracuje 81% roku i pokrywa 64,6% zapotrzebowania
elektrycznego.

### 9.4. Sezonowość zasobu słonecznego wyklucza autonomię opartą na PV

Stosunek GHI maj/grudzień 8,6:1 oznacza, że w warunkach polskich instalacja
fotowoltaiczna nie może stanowić podstawy zasilania awaryjnego w okresie zimowym.
Uzasadnia to obecność źródła sterowalnego w architekturze mikrosieci.

---

## 10. Zadania przed obliczeniami właściwymi

| Zadanie | Priorytet |
|---|---|
| Wybór rzeczywistego obiektu referencyjnego i pozyskanie danych pomiarowych | **wysoki** |
| Analiza CAD rozmieszczenia modułów PV → wyznaczenie granicznej mocy [kWp] | **wysoki** |
| Wprowadzenie szyny cieplnej do konfiguracji K1 i K2 (porównywalność bilansów) | **wysoki** |
| Przełączenie waluty modelu na PLN | średni |
| Powtórzenie testu A1 dla okresu letniego | średni |
| Zwiększenie przestrzeni poszukiwań BESS — wyznaczenie pojemności zapewniającej 60 min autonomii dla odbiorów klasy 0,5 s | średni |
| Ograniczenie testu autonomii do obciążeń krytycznych (30% mocy szczytowej) | średni |
| Pozyskanie licencji akademickiej HOMER Pro | **wysoki** ³ |

³ Licencja Evaluation Edition wygasa 5 września 2026.

---

## 11. Pliki modeli

| Plik | Zawartość |
|---|---|
| `Scenariusz_1_Baza_Siec_Diesel.homer` | K1, wariant A0 |
| `Scenariusz_2_Hybryda_Siec_Diesel_PV_BESS.homer` | K2, wariant A0 |
| `Scenariusz_3_Mikrosiec_PV_BESS_CHP.homer` | K3 z agregatem Diesel (wariant odrzucony) |
| `TEST_Scenariusz_3_CHP_gazowy_Aura404.homer` | K3 z CHP gazowym, warianty A0 i A1 |
| `TEST_Scen3_CHP_gazowy_serie_krotkich_przerw.homer` | K3 z CHP gazowym, wariant A2 |
| `Profil_obciazenia_elektrycznego_szpital_8760h.csv` | Profil elektryczny |
| `Profil_obciazenia_cieplnego_szpital_8760h.csv` | Profil cieplny |
| `Awaria_blacksky_72h_styczen.csv` | Szereg czasowy wariantu A1 |
| `Awaria_seria_krotkich_przerw.csv` | Szereg czasowy wariantu A2 |

Materiał ilustracyjny: folder `Grafika/`
Raporty pełne HOMER: `Raport_HOMER_*.docx`
Instrukcja obsługi programu: `01_Baza_Wiedzy/Instrukcja_HOMER_Pro.md`
