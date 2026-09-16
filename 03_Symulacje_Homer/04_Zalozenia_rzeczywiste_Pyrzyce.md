# Założenia projektowe dla obiektu rzeczywistego — Szpital Powiatowy w Pyrzycach

Przeskalowanie modelu z wartości modelowych na dane rzeczywiste, pozyskane
z dokumentacji przetargowej oraz z pomiarów kartograficznych.

---

## 1. Dane wejściowe — status potwierdzenia

| Wielkość | Wartość | Źródło | Status |
|---|---|---|---|
| Zużycie energii elektrycznej | **355 MWh/rok** | Dokumentacja przetargowa 2021 | ✅ potwierdzone |
| Grupa taryfowa | **B** (średnie napięcie) | jw. | ✅ potwierdzone |
| **Powierzchnia zabudowy** | **2 110,43 m²** | Geoportal — pomiar własny | ✅ potwierdzone |
| Wymiary bryły głównej | **72,39 × 25,33 m** | jw. | ✅ potwierdzone |
| **Współrzędne** | **53°08'49,93"N, 14°53'44,66"E** | jw. | ✅ potwierdzone |
| Rzędne terenu | 36,0–37,8 m n.p.m. | jw. | ✅ potwierdzone |
| Rodzaj przekrycia | **stropodach płaski** | Ortofotomapa | ✅ potwierdzone |
| Lądowisko na dachu | **brak** | Ortofotomapa | ✅ potwierdzone |
| Zapotrzebowanie na ciepło | 700 MWh/rok | **oszacowanie** | ⬜ wniosek złożony |
| Parametry agregatu | — | — | ⬜ wniosek złożony |

> **Współrzędne 53,1472°N / 14,8957°E** należy wprowadzić do HOMER Pro zamiast
> lokalizacji „Szczecin" — dane NASA POWER zostaną pobrane dla właściwego punktu.

---

## 2. Profil obciążenia elektrycznego

Plik: `Profil_elektryczny_PYRZYCE_355MWh.csv`

| Parametr | Wartość |
|---|---|
| Energia roczna | **355,0 MWh** |
| Moc średnia | **40,53 kW** |
| **Moc szczytowa** | **56,72 kW** |
| Moc minimalna | 25,35 kW |
| Współczynnik obciążenia | 0,715 |
| Zużycie dobowe | 972,6 kWh/d |

### Odbiory krytyczne

Zgodnie z § 30 Rozporządzenia MZ agregat musi pokryć **minimum 30% mocy szczytowej**:

**0,30 × 56,72 kW = 17,0 kW**

W czasie 72-godzinnej awarii odpowiada to zapotrzebowaniu **1 225 kWh**.

---

## 3. Profil obciążenia cieplnego (oszacowanie)

Plik: `Profil_cieplny_PYRZYCE_700MWh.csv`

**Podstawa oszacowania:** powierzchnia zabudowy 2 110 m², przyjęte 2–3 kondygnacje
użytkowe → powierzchnia ogrzewana ok. 5 000 m². Po przeprowadzonej termomodernizacji
przyjęto wskaźnik 90 kWh/m²/rok dla c.o., co daje 450 MWh; wraz z c.w.u.
i procesami technologicznymi — **700 MWh/rok**.

| Parametr | Wartość |
|---|---|
| Energia roczna | 700,0 MWh |
| Moc średnia | 79,91 kW |
| Moc szczytowa | 208,92 kW |
| **Letnia baza cieplna (VI–VIII)** | **28,8 kW** |

> Wartość do zweryfikowania po otrzymaniu audytu energetycznego.
> Letnia baza cieplna 28,8 kW stanowi podstawę doboru mocy cieplnej jednostki CHP.

---

## 4. Potencjał instalacji fotowoltaicznej

| Etap | Wartość | Założenie |
|---|---|---|
| Powierzchnia dachu (brutto) | 2 110 m² | pomiar Geoportal |
| Odliczenie infrastruktury technicznej | −45% | **gęsto zabudowana purkrywa** — liczne wyrzutnie wentylacyjne widoczne na ortofotomapie |
| Powierzchnia użyteczna | ok. 1 160 m² | — |
| Współczynnik pokrycia (GCR) | 0,40 | odstępy międzyrzędowe dla dachu płaskiego |
| Powierzchnia modułów | ok. 465 m² | — |
| **Moc szacunkowa** | **100–110 kWp** | do potwierdzenia w PV\*SOL |

### Bilans roczny przy 105 kWp

```
105 kWp × 930 kWh/kWp = 97,6 MWh/rok
97,6 MWh ÷ 355 MWh = 27,5% zapotrzebowania
```

Przy mocy średniej obiektu 40,5 kW i mocy szczytowej instalacji ok. 85 kW
(105 kWp × 0,8) wystąpią okresowe nadwyżki w godzinach południowych sezonu letniego.
Autokonsumpcja pozostanie jednak wysoka — szacunkowo 85–92%.

---

## 5. Czas autonomii — przeliczenie dla skali rzeczywistej

Warunki: awaria 72 h, 15–17 stycznia. Obciążenie średnie **43,2 kW**, szczytowe 55,1 kW.
Energia do dostarczenia: **3 111 kWh** (wobec 8 762 kWh w modelu testowym).

### 5.1. Agregat prądotwórczy

Przyjęte zużycie jednostkowe 0,28 l/kWh.

| Zbiornik | Pełne obciążenie | Tylko odbiory krytyczne |
|---|---|---|
| 500 l | 41,3 h | 105,0 h |
| **1 000 l** | **82,7 h** ✅ | **209,9 h** |
| 1 500 l | 124,0 h | 314,9 h |
| 2 000 l | 165,3 h | 419,8 h |

**Wniosek zmieniony względem modelu testowego:** przy rzeczywistej skali obiektu
zbiornik o pojemności **1 000 litrów wystarcza na pokrycie pełnej awarii 72-godzinnej**
przy pełnym obciążeniu. W modelu testowym (obciążenie 121,7 kW) wymagane było
2 430 litrów. Różnica wynika wyłącznie ze skali obiektu.

### 5.2. Magazyn bateryjny (SoC 100% → 40%)

| Pojemność | Pełne obciążenie | Tylko odbiory krytyczne |
|---|---|---|
| 100 kWh | 1,39 h | 3,53 h |
| 200 kWh | 2,78 h | 7,05 h |
| **300 kWh** | **4,17 h** | **10,58 h** |
| 600 kWh | 8,33 h | 21,16 h |

**Wniosek:** magazyn 100 kWh spełnia z zapasem wymóg **60 minut podtrzymania**
dla odbiorów klasy 0,5 s (3,53 h w trybie krytycznym wobec wymaganej 1 h).
Pojemność 300 kWh zapewnia ponad 10 godzin pracy odbiorów krytycznych — wartość
istotna dla scenariusza opóźnionego uruchomienia źródła sterowalnego.

### 5.3. Jednostka kogeneracyjna

| Moc elektryczna | Pokrycie obciążenia średniego | Pokrycie odbiorów krytycznych |
|---|---|---|
| 30 kW | 69% | **100%** |
| **40 kW** | **93%** | **100%** |
| 50 kW | **100%** | **100%** |

**Dobór rekomendowany: 40–50 kW mocy elektrycznej.** Jednostka 50 kW pokrywa
całość obciążenia elektrycznego obiektu w warunkach awarii. Weryfikacji wymaga
zgodność mocy cieplnej z letnią bazą 28,8 kW — przy typowym stosunku mocy
cieplnej do elektrycznej 1,4:1 jednostka 30 kW daje ok. 42 kW ciepła,
co przewyższa bazę letnią i wymusi pracę na obniżonej mocy w sezonie letnim.

---

## 6. Porównanie skali — model testowy a obiekt rzeczywisty

| Wielkość | Model testowy | **Pyrzyce (rzeczywiste)** | Stosunek |
|---|---|---|---|
| Zużycie elektryczne | 1 000 MWh | **355 MWh** | 2,8 : 1 |
| Moc szczytowa | 159,8 kW | **56,7 kW** | 2,8 : 1 |
| Odbiory krytyczne | 47,9 kW | **17,0 kW** | 2,8 : 1 |
| Energia w 72 h awarii | 8 762 kWh | **3 111 kWh** | 2,8 : 1 |
| Moc PV | 250 kWp | **100–110 kWp** | 2,3 : 1 |
| Moc CHP | 100 kW | **40–50 kW** | 2,2 : 1 |
| Zbiornik dla 72 h | 2 430 l | **970 l** | 2,5 : 1 |

### Wnioski jakościowe — niezmienione

Wszystkie wnioski metodyczne sformułowane na podstawie symulacji testowych
zachowują ważność, ponieważ dotyczą relacji między konfiguracjami, nie zaś
wartości bezwzględnych:

- kryterium najniższego NPC prowadzi do wyboru układu bez źródła rezerwowego,
- magazyn bateryjny pełni funkcję pomostową, nie zaś źródła autonomii długoterminowej,
- kogeneracja gazowa zapewnia niezależność od transportu drogowego paliwa,
- sezonowość zasobu słonecznego wyklucza autonomię opartą na PV w okresie zimowym.

### Wniosek ilościowy — zmieniony

**Przy rzeczywistej skali obiektu osiągnięcie autonomii 72-godzinnej jest
znacznie łatwiejsze niż wynikało z modelu testowego.** Zbiornik 1 000 l zamiast
2 430 l, magazyn 100 kWh spełniający wymóg klasy 0,5 s z ponadtrzykrotnym zapasem,
jednostka CHP 50 kW pokrywająca pełne obciążenie — wszystkie te wartości mieszczą
się w zakresie rozwiązań standardowych, dostępnych katalogowo.

---

## 7. Parametry do wprowadzenia w HOMER Pro

| Pozycja | Wartość |
|---|---|
| Lokalizacja | 53,1472°N / 14,8957°E |
| Profil elektryczny | `Profil_elektryczny_PYRZYCE_355MWh.csv` |
| Profil cieplny | `Profil_cieplny_PYRZYCE_700MWh.csv` (tymczasowy) |
| PV — przestrzeń poszukiwań | {0; 50; 75; 100; 110} kWp |
| BESS — przestrzeń poszukiwań | {0; 1; 2; 3; 6} × 100 kWh |
| CHP — moc | 30 / 40 / 50 kW (gaz ziemny) |
| Agregat — moc | 20 kW (≈ 30% P.szczytowej, wariant minimalny) lub 60 kW (pełne pokrycie) |
| Przekształtnik | dobierany automatycznie |
| Awarie | pliki A1 i A2 bez zmian |

---

## 8. Pozostałe do potwierdzenia

| Dana | Wpływ na wynik | Źródło |
|---|---|---|
| Zapotrzebowanie na ciepło | Dobór mocy cieplnej CHP i kotła | Audyt energetyczny |
| Źródło ciepła (kotłownia / sieć) | Struktura kosztów w Scenariuszu 3 | Audyt / przetarg na gaz |
| **Pojemność zbiornika paliwa** | **Bezpośrednio wyznacza czas autonomii K1** | Dokumentacja techniczna |
| Moc agregatu | Weryfikacja zgodności z § 30 | jw. |
| Moc umowna | Analiza opłat za moc, *peak shaving* | Faktura / przetarg |
| Aktualne zużycie (2024–2026) | Weryfikacja wartości 355 MWh po likwidacji oddziałów | Nowszy przetarg |

Wniosek o udostępnienie informacji publicznej złożony 8 września 2026
(Szpital Powiatowy w Pyrzycach oraz Starostwo Powiatowe w Pyrzycach).
Termin ustawowy odpowiedzi: **22 września 2026**.
