# Kwerenda ogólnopolska — poszukiwanie obiektu z pełną dokumentacją energetyczną

Rozszerzenie poszukiwań poza województwo zachodniopomorskie, w celu znalezienia obiektu,
dla którego dostępny jest **komplet danych** niezbędnych do symulacji: zużycie energii
elektrycznej, zapotrzebowanie na ciepło oraz charakterystyka budynku.

---

## 1. Wnioski metodyczne z kwerendy

Pojedyncze źródło zawierające komplet danych **praktycznie nie występuje**. Konieczne jest
zestawienie informacji z trzech niezależnych rodzajów dokumentów:

| Dokument | Zawiera | Gdzie szukać |
|---|---|---|
| **Dokumentacja przetargowa — energia elektryczna** | zużycie [MWh/rok], moc umowna, grupa taryfowa, liczba PPE | BIP szpitala → Przetargi; szczególnie **odpowiedzi na pytania wykonawców** |
| **Audyt energetyczny** | powierzchnia, kubatura, zapotrzebowanie na ciepło [GJ/rok], wskaźniki EP/EK, przegrody | Strona szpitala (często publikowany jako załącznik do przetargu), BIP organu założycielskiego |
| **Studium wykonalności / wniosek o dofinansowanie** | bilans energetyczny, koncepcja PV/CHP, powierzchnia dachu | Baza Konkurencyjności, mapadotacji.gov.pl |

### Weryfikacja skuteczności metody

Metodę potwierdzono empirycznie:

- **Dokumentacja przetargowa** — dla Szpitala Powiatowego w Pyrzycach uzyskano
  potwierdzone zużycie **355 MWh/rok** oraz grupę taryfową B.
- **Audyt energetyczny** — dla Pawilonu C Szpitala w Tarnobrzegu odnaleziono pełny audyt
  publikowany na stronie placówki, zawierający kubaturę (2 583 m³), powierzchnię netto
  (492,14 m²), powierzchnię zabudowy (310,40 m²), zapotrzebowanie na c.o. i c.w.u. [GJ/rok]
  oraz udział OZE (54,79%). Obiekt zbyt mały dla celów pracy, lecz **struktura dokumentu
  potwierdza kompletność danych** możliwych do pozyskania tą drogą.

---

## 2. Kierunek najbardziej obiecujący — obiekty po modernizacji energetycznej

Szpitale, które zrealizowały projekty poprawy efektywności energetycznej ze środków
publicznych, **muszą** posiadać komplet dokumentacji: audyt energetyczny, studium
wykonalności oraz dokumentację powykonawczą. Dokumenty te podlegają udostępnieniu.

### Zidentyfikowane obiekty referencyjne

| Obiekt | Zakres projektu | Wartość dla pracy |
|---|---|---|
| **Szpital Specjalistyczny nr 2 w Bytomiu** | 2 instalacje PV po **49,6 kWp** na 3 dachach + **magazyn energii** + pompa ciepła z buforem c.w.u. | Konfiguracja niemal identyczna z badaną (PV + BESS); dostępna dokumentacja projektowa |
| **Szpital Specjalistyczny im. Świętej Rodziny w Warszawie** | Układ **kogeneracji** + energia słoneczna i geotermalna | Jedyny zidentyfikowany obiekt z wdrożonym CHP — materiał porównawczy dla Scenariusza 3 |
| Szpital Reumatologiczny w Ustroniu | Audyt kotłowni z rekomendacją kogeneracji i/lub PV | Przykład analizy wariantowej źródeł |
| Miejski Szpital Zespolony w Częstochowie | Audyt energetyczny budynków | Dane o zapotrzebowaniu na ciepło wentylacyjne |

> **Uwaga:** obiekty te posiadają **już wykonane** instalacje OZE. Dla pracy oznacza to,
> że nie mogą pełnić roli obiektu projektowanego, lecz stanowią **materiał porównawczy** —
> możliwość zestawienia wyników symulacji z rzeczywistymi parametrami wdrożonych instalacji.

### Nowy program finansowania — źródło przyszłych danych

Fundusz Modernizacyjny uruchamia program priorytetowy „Poprawa efektywności energetycznej
budynków szpitalnych" na lata **2026–2030** (start planowany na II połowę 2026).
Obejmuje termomodernizację, OZE oraz **magazyny energii**.

Znaczenie dla pracy: program wygeneruje falę dokumentacji projektowej dla szpitali,
a sama tematyka pracy zyskuje bezpośrednie uzasadnienie praktyczne — możliwość powołania
się na aktualny instrument finansowania w rozdziale 1 lub 7.

---

## 3. Zestawienie kandydatów — stan danych

| Obiekt | Energia elektryczna | Ciepło | Budynek | Dach | Ocena |
|---|---|---|---|---|---|
| **Pyrzyce** — Szpital Powiatowy | ✅ **355 MWh/rok**, taryfa B | ⬜ audyt istnieje, do pozyskania | 🔶 termomodernizacja potwierdzona | ⬜ do weryfikacji | **Kandydat główny** |
| Goleniów — SCM | ⬜ | ⬜ | ⬜ | ⬜ | Do kwerendy |
| Nowogard — SPSR | ⬜ | ⬜ | ⬜ | ⬜ | Do kwerendy |
| Bytom — Szpital Spec. nr 2 | ⬜ | ⬜ | ✅ dokumentacja projektu UE | ✅ PV 2 × 49,6 kWp | Materiał porównawczy |
| Warszawa — Św. Rodziny | ⬜ | ⬜ | ✅ dokumentacja projektu UE | — | Materiał porównawczy (CHP) |

Legenda: ✅ potwierdzone · 🔶 częściowe · ⬜ brak danych

---

## 4. Rekomendacja

### 4.1. Obiekt projektowany

Utrzymanie **Szpitala Powiatowego w Pyrzycach** jako kandydata głównego. Uzasadnienie:

- jedyny obiekt z **potwierdzonym** zużyciem energii elektrycznej,
- przyłącze średniego napięcia (taryfa B) — możliwość przyłączenia źródeł wytwórczych,
- pełny profil odbiorów krytycznych (blok operacyjny, OAiIT — grupa 2 wg IEC 60364-7-710),
- brak istniejących instalacji OZE — projekt dotyczy stanu wyjściowego,
- istniejący audyt energetyczny (termomodernizacja ze środków UE),
- skala odpowiednia dla pracy inżynierskiej.

### 4.2. Obiekty porównawcze

Wykorzystanie dokumentacji szpitali w **Bytomiu** (PV + magazyn energii) oraz
**Warszawie** (kogeneracja) w rozdziale 6 — jako weryfikacja wyników symulacji
względem rozwiązań rzeczywiście wdrożonych. Wzmacnia to wiarygodność pracy: wyniki
modelowe zostają skonfrontowane z parametrami instalacji istniejących.

---

## 5. Plan działania

| Krok | Czynność | Wykonawca |
|---|---|---|
| 1 | Weryfikacja geometrii dachu i bryły na materiałach kartograficznych | Dyplomant → zrzuty ekranu |
| 2 | Ocena przydatności obiektu na podstawie zrzutów | Asystent |
| 3 | Kwerenda przetargowa dla obiektów alternatywnych (Goleniów, Nowogard) | Asystent |
| 4 | Wniosek o audyt energetyczny w trybie dostępu do informacji publicznej | Dyplomant |
| 5 | Analiza rozmieszczenia modułów PV | Dyplomant (PV\*SOL) |
| 6 | Przeskalowanie profili i ponowne symulacje | Asystent → Dyplomant |

---

## 6. Wzór wniosku o udostępnienie audytu energetycznego

```
Starostwo Powiatowe w Pyrzycach
[lub: Dyrekcja Szpitala Powiatowego w Pyrzycach]

WNIOSEK O UDOSTĘPNIENIE INFORMACJI PUBLICZNEJ

Na podstawie art. 2 ust. 1 ustawy z dnia 6 września 2001 r.
o dostępie do informacji publicznej (Dz.U. 2022 poz. 902 z późn. zm.)
wnoszę o udostępnienie:

1. Audytu energetycznego budynku Szpitala Powiatowego w Pyrzycach,
   sporządzonego na potrzeby projektu termomodernizacji
   współfinansowanego ze środków Unii Europejskiej.
2. Danych o rocznym zużyciu energii elektrycznej oraz ciepła
   za lata 2023–2025.
3. Informacji o mocy zainstalowanej i pojemności zbiornika paliwa
   agregatu prądotwórczego stanowiącego rezerwowe źródło zasilania.

Wnioskowane informacje wykorzystane zostaną wyłącznie w celach
naukowych, w ramach pracy dyplomowej inżynierskiej realizowanej
na Zachodniopomorskim Uniwersytecie Technologicznym w Szczecinie
pod kierunkiem [imię i nazwisko promotora].

Preferowana forma udostępnienia: elektroniczna, na adres [e-mail].

[imię i nazwisko, nr albumu, kierunek studiów]
```

Termin odpowiedzi: **14 dni** od złożenia wniosku (art. 13 ust. 1 ustawy).

---

**Źródła:**
- Szpital Powiatowy w Pyrzycach, dokumentacja przetargowa 2021 — http://szpital.pyrzyce.net.pl/?p=8988
- Audyt energetyczny Pawilonu C — https://szpitaltbg.pl/wp-content/uploads/2019/10/Pawilon-C-Audyt-energetyczny-LIPIEC.pdf
- Mapa Dotacji UE, projekt Szpitala Specjalistycznego nr 2 w Bytomiu — https://mapadotacji.gov.pl/projekty/1699066/
- Mapa Dotacji UE, projekt kogeneracji w Warszawie — https://mapadotacji.gov.pl/projekty/707652/
- Program priorytetowy Funduszu Modernizacyjnego — https://www.collect.pl/blog/2026/fundusz-modernizacyjny-wspiera-termomodernizacje-szpitali-nowy-program-priorytetowy-w-konsultacjach/
