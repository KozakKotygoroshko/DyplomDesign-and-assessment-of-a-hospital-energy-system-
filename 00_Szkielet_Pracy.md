# Spis treści (szkielet pracy)

**Temat:** Projekt i ocena architektury systemu energetycznego szpitala z kogeneracją,
OZE oraz magazynami energii w kontekście bezpieczeństwa energetycznego

---

## 1. Wstęp

*Status: ✅ napisany*

## 2. Cel pracy i zakres pracy

*Status: ✅ napisany*

## 3. Przegląd literatury i wymagań prawno-normatywnych

*Status: ✅ napisany (3.1–3.5)*

- **3.1.** Szpital jako infrastruktura krytyczna i wymogi zasilania rezerwowego
  (Rozp. MZ § 42 — agregat 30% mocy szczytowej i UPS; IEC 60364-7-710 —
  grupy 0/1/2, klasy przerw 0,5 s i 15 s)
- **3.2.** Agregaty prądotwórcze (Diesel) w zasilaniu awaryjnym — *wet stacking*,
  zależność od łańcucha dostaw paliwa, *black-sky hazards*
- **3.3.** Instalacje fotowoltaiczne (PV) w obiektach użyteczności publicznej —
  ograniczenia dachu płaskiego, GCR, autokonsumpcja
- **3.4.** Bateryjne magazyny energii (BESS) i strategie zarządzania energią —
  klasa 0,5 s, *peak shaving*, strategie CC i LF
- **3.5.** Układy kogeneracyjne (CHP) w mikrosieciach szpitalnych — sprawność
  skojarzona 80–85%, całoroczna baza cieplna, źródło *dispatchable*

## 4. Założenia projektowe

*Status: 🔄 dane zebrane w całości — redakcja przed nami.
Obiekt: **Szpital Powiatowy w Pyrzycach**, dane pierwotne pozyskane
w trybie dostępu do informacji publicznej (21.09.2026) oraz z tabliczki
znamionowej agregatu (06.10.2026).*

- **4.1.** Analiza lokalizacji i profil medyczny wybranego obiektu (szpital jednobryłowy)
  - 4.1.1. Kryteria doboru obiektu referencyjnego
  - 4.1.2. Charakterystyka obiektu — dane organizacyjne i energetyczne
  - 4.1.3. Pozyskanie danych rzeczywistych z dokumentacji przetargowej
- **4.2.** Profil zapotrzebowania na energię elektryczną i cieplną
  - 4.2.1. Metodyka opracowania profilu godzinowego (8760 h)
  - 4.2.2. Profil elektryczny — współczynnik obciążenia, sezonowość
  - 4.2.3. Profil cieplny — c.o., c.w.u., sterylizacja i pralnia; letnia baza cieplna
  - 4.2.4. Weryfikacja względem profilu syntetycznego
- **4.3.** Identyfikacja obciążeń krytycznych (klasy przerw 0,5 s i 15 s)
- **4.4.** Analiza przestrzenna dachu i wyznaczenie granicznej mocy PV *(CAD / PV\*SOL)*

## 5. Projekt wariantów zasilania szpitala (scenariusze)

*Status: 🔄 modele zbudowane i obliczone (seria V2, 21.09.2026) — opis przed nami*

- **5.1.** Dobór komponentów i narzędzie symulacyjne (HOMER Pro)
- **5.2.** **Scenariusz 1 (Baza):** Sieć elektroenergetyczna + agregat prądotwórczy
- **5.3.** **Scenariusz 2 (Hybryda):** Sieć + agregat + PV + magazyn energii (BESS)
- **5.4.** **Scenariusz 3 (Zaawansowana mikrosieć):** Sieć + PV + BESS + kogeneracja
  gazowa (CHP) ze wsparciem cieplnym
- **5.5.** Modelowanie zdarzeń awaryjnych
  - 5.5.1. **Wariant A1 — awaria długotrwała (*black-sky*):** pojedyncze zdarzenie
    72 h w okresie zimowym (przypadek najbardziej niekorzystny)
  - 5.5.2. **Wariant A2 — seria przerw krótkotrwałych:** 5 przerw wg statystyki
    SAIDI/SAIFI polskich sieci dystrybucyjnych
  - 5.5.3. Implementacja szeregów czasowych w module Grid Reliability

## 6. Dobór urządzeń i obliczenia elektryczne

*Status: ⏳ **rozdział proponowany — do uzgodnienia z promotorem**.
Symulacja w HOMER Pro operuje komponentami generycznymi (`Generic flat plate PV`,
`Generic converter`) i wyznacza moce, nie zaś konkretne urządzenia. Słowo „Projekt"
w temacie pracy uzasadnia przełożenie wyznaczonych mocy na dobór sprzętu
wraz z obliczeniami sprawdzającymi.*

- **6.1.** Dobór modułu fotowoltaicznego
  - 6.1.1. Kryteria doboru i zestawienie modułów rozważanych
  - 6.1.2. Parametry przyjętego modułu (Pmpp, Uoc, Umpp, Isc, współczynnik temperaturowy)
  - 6.1.3. Liczba modułów i rzeczywista moc instalacji wobec granicy 124 kWp
- **6.2.** Dobór falownika
  - 6.2.1. Dobór mocy i współczynnik DC/AC
  - 6.2.2. Liczba i konfiguracja wejść MPPT
- **6.3.** Obliczenia łańcuchów (stringów)
  - 6.3.1. Sprawdzenie napięcia jałowego przy temperaturze minimalnej (−20 °C)
  - 6.3.2. Sprawdzenie napięcia MPP przy temperaturze maksymalnej (+70 °C)
  - 6.3.3. Sprawdzenie prądu wejściowego
- **6.4.** Dobór przewodów
  - 6.4.1. Strona DC — przekrój, obciążalność prądowa, spadek napięcia
  - 6.4.2. Strona AC — przyłączenie do rozdzielnicy obiektu
- **6.5.** Zabezpieczenia i ochrona przepięciowa
  - 6.5.1. Zabezpieczenia nadprądowe DC i AC
  - 6.5.2. Ograniczniki przepięć (SPD typ 1+2), połączenia wyrównawcze
  - 6.5.3. Ochrona przeciwporażeniowa
- **6.6.** Konstrukcja wsporcza na dachu płaskim
  - 6.6.1. System balastowy — obciążenie dachu, obliczenia wiatrowe
  - 6.6.2. Rozstaw rzędów i współczynnik pokrycia (GCR)
- **6.7.** Dobór pozostałych komponentów
  - 6.7.1. Magazyn energii (BESS) i przekształtnik dwukierunkowy
  - 6.7.2. Jednostka kogeneracyjna
  - 6.7.3. Agregat prądotwórczy — stan istniejący (Grupel G0356, 258 kW PRP)
- **6.8.** Schemat jednokreskowy układu

## 7. Analiza wyników symulacji

*Status: 🔄 obliczenia zamknięte — redakcja przed nami.
Wynik zasadniczy: wyłącznie Konfiguracja K3 (CHP gazowy) pokrywa awarię 72 h;
K1 i K2 ograniczone pojemnością użyteczną zbiornika 900 l.*

- **7.1.** Analiza techniczna — bilanse energetyczne i wskaźniki niezawodności
  - 7.1.1. Pokrycie zapotrzebowania i udział źródeł własnych
  - 7.1.2. Energia niedostarczona (EENS) i niedobór mocy
- **7.2.** **Test przetrwania (Resilience Test) — czas autonomii obiektu**
  - 7.2.1. Metodyka wyznaczania czasu autonomii
  - 7.2.2. Wyniki dla wariantu A1 (awaria 72 h)
  - 7.2.3. Wyniki dla wariantu A2 (serie przerw)
  - 7.2.4. Tryb awaryjny z odrzuceniem obciążeń nieistotnych
  - 7.2.5. Ograniczenia autonomii: zapas paliwa, pojemność magazynu, ciągłość dostaw gazu
- **7.3.** Analiza ekonomiczna (CAPEX, OPEX, LCOE, NPC)
- **7.4.** Analiza ekologiczna (redukcja emisji CO₂)
- **7.5.** Porównanie wielokryterialne i ocena wariantów
  - 7.5.1. Kryteria oceny i ich wagi
  - 7.5.2. Konfiguracja rekomendowana pod kątem bezpieczeństwa energetycznego
  - 7.5.3. Propozycja architektury hierarchicznej (BESS → CHP → PV → agregat)

## 8. Wnioski

*Status: ⏳ wniosek zasadniczy ustalony, redakcja przed nami*

## 9. Bibliografia

*Wymogi WKŚiR: maks. 5 pozycji książkowych, min. 10 artykułów naukowych,
w tym min. 5 obcojęzycznych. System autorsko-rocznikowy (APA/Harvard).*

---

## Aneks

**Karty charakterystyki zastosowanych komponentów:**

- Agregat prądotwórczy (Diesel)
- Moduł fotowoltaiczny
- Falownik / przekształtnik systemowy
- Moduł bateryjnego magazynu energii (BESS)
- **Jednostka kogeneracyjna gazowa (CHP)**
- Kocioł szczytowy

**Materiały uzupełniające:**

- Profile obciążenia elektrycznego i cieplnego (8760 h)
- Szeregi czasowe zdarzeń awaryjnych (warianty A1 i A2)
- Raporty z symulacji HOMER Pro
- Dokumentacja fotograficzna i kartograficzna obiektu

---

## Uwagi do struktury

**Rozszerzenie względem wersji pierwotnej.** Wprowadzono podrozdział 5.5 (modelowanie
awarii) oraz 6.2 (test przetrwania) jako odrębne jednostki redakcyjne. Wynika to
z przyjętej metodyki: analiza czasu autonomii stanowi niezależne kryterium oceny,
nierozstrzygalne na gruncie analizy ekonomicznej.

**Uzasadnienie.** Symulacje testowe wykazały, że kryterium najniższego NPC prowadzi
do wyboru konfiguracji pozbawionej źródła rezerwowego — optymalizator uznaje
niedostarczenie energii do szpitala za rozwiązanie tańsze niż zakup agregatu.
Ocena wielokryterialna musi zatem traktować energię niedostarczoną jako ograniczenie
twarde, co uzasadnia wyodrębnienie testu przetrwania w osobnym podrozdziale.

**Test obejmuje wszystkie trzy scenariusze** — Scenariusz 1 pełni funkcję wariantu
odniesienia, bez którego wyniki wariantów hybrydowych pozbawione są punktu
porównawczego.
