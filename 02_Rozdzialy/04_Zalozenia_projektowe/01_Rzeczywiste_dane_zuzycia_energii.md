# Rzeczywiste dane o zużyciu energii — kwerenda dokumentacji przetargowej

Dokumentacja postępowań o udzielenie zamówienia publicznego na dostawę energii elektrycznej
stanowi **najwiarygodniejsze publicznie dostępne źródło** danych o rzeczywistym zużyciu energii
przez obiekty szpitalne. Zamawiający zobowiązany jest podać w niej planowany wolumen zakupu
z rozbiciem na punkty poboru i strefy czasowe.

---

## 1. Znalezione dane — Szpital Powiatowy w Pyrzycach

**Postępowanie:** „Zakup energii elektrycznej", nr ref. 2/2021
**Data:** 30.03.2021
**Źródło:** odpowiedzi na pytania wykonawców, pytanie nr 21

| Parametr | Wartość |
|---|---|
| Wolumen całkowity | **1 420 MWh** |
| Okres umowy | **4 lata** (od 01.05.2021) |
| **Zużycie roczne** | **355 MWh** |
| Grupa taryfowa | **B** (średnie napięcie) |
| Umowy | rozdzielone (sprzedaż + dystrybucja) |
| Status prosumenta / wytwórcy OZE | **brak** |
| Okres rozliczeniowy | miesięczny |

### Dane organizacyjne obiektu

| Oddział | Liczba łóżek |
|---|---|
| Chorób wewnętrznych | 60 (w tym 4 INK) |
| Chirurgii urazowo-ortopedycznej | 30 |
| Chirurgii ogólnej | 25 |
| Położnictwa i ginekologii | 20 |
| Neonatologiczny | 10 |
| Anestezjologii i intensywnej terapii | 5 |
| **Razem** | **150** |

Ponadto: blok operacyjny, izba przyjęć, Zakład Opiekuńczo-Leczniczy, 13 poradni
specjalistycznych, pracownie: tomografii komputerowej, RTG, USG, endoskopowa, fizjoterapii.

---

## 2. Wniosek — korekta założeń projektowych

### 2.1. Rozbieżność względem przyjętego modelu

| Wielkość | Model przyjęty w symulacjach testowych | Dane rzeczywiste (Pyrzyce) | Stosunek |
|---|---|---|---|
| Zużycie roczne | 1 000 MWh | **355 MWh** | **2,8 : 1** |
| Moc średnia | 114,2 kW | **40,5 kW** | 2,8 : 1 |
| Wskaźnik jednostkowy | 6 667 kWh/łóżko/rok | **2 367 kWh/łóżko/rok** | 2,8 : 1 |

**Model wykorzystany w symulacjach testowych zawyża zużycie blisko trzykrotnie.**

### 2.2. Interpretacja rozbieżności

Wskaźniki literaturowe dla obiektów szpitalnych, mieszczące się zazwyczaj w przedziale
15 000–30 000 kWh/łóżko/rok, dotyczą **szpitali wielospecjalistycznych i klinicznych**
o rozbudowanej infrastrukturze diagnostycznej (rezonans magnetyczny, angiografia,
akceleratory liniowe) oraz pełnej klimatyzacji.

Polski szpital powiatowy o profilu podstawowym charakteryzuje się natomiast:

- ograniczonym parkiem aparatury obrazowej (RTG, USG, tomograf komputerowy),
- brakiem klimatyzacji w większości pomieszczeń poza blokiem operacyjnym,
- wentylacją mechaniczną ograniczoną do stref czystych,
- ogrzewaniem i przygotowaniem c.w.u. realizowanym poza szyną elektryczną
  (kotłownia gazowa lub sieć ciepłownicza).

Ostatni czynnik ma znaczenie zasadnicze: energia cieplna nie obciąża bilansu elektrycznego,
co odróżnia obiekty polskie od modeli anglosaskich, w których powszechne jest ogrzewanie
elektryczne lub pompy ciepła.

### 2.3. Konsekwencje dla dalszych prac

| Zagadnienie | Skutek korekty |
|---|---|
| Profile obciążenia | Wymagają przeskalowania z 1 000 MWh na wartość rzeczywistą obiektu |
| Moc szczytowa | Spadek ze 159,8 kW do ok. 57 kW (przy zachowaniu LF = 0,715) |
| Dobór PV | Instalacja 250 kWp znacząco **przewymiarowana** — produkcja 232 MWh wobec zużycia 355 MWh oznaczałaby autokonsumpcję poniżej 100% |
| Dobór CHP | Jednostka 100 kW **przewymiarowana** — właściwy zakres 30–50 kW mocy elektrycznej |
| Dobór BESS | Pojemność 200 kWh zapewni ok. 3 h autonomii zamiast 1 h |
| Wnioski metodyczne | **Pozostają w mocy** — dotyczą relacji między konfiguracjami, nie wartości bezwzględnych |

> **Uwaga:** wnioski metodyczne sformułowane w raporcie z symulacji testowych zachowują
> ważność. Dotyczą one bowiem zależności jakościowych — nieadekwatności kryterium NPC,
> konieczności ograniczenia przestrzennego PV, przewagi kogeneracji gazowej nad agregatem —
> które nie zależą od bezwzględnej skali obiektu.

---

## 3. Metodyka pozyskiwania danych — wskazówki

Dokumentacja przetargowa okazała się skuteczniejszym źródłem niż strony informacyjne
placówek. Rekomendowana ścieżka poszukiwań:

| Krok | Źródło | Poszukiwana informacja |
|---|---|---|
| 1 | BIP szpitala → zakładka „Przetargi" / „Zamówienia publiczne" | Postępowania na zakup energii elektrycznej |
| 2 | **Odpowiedzi na pytania wykonawców** | Wolumen w MWh, grupa taryfowa, moc umowna |
| 3 | Załączniki do SWZ (zwykle „Szczegółowy opis przedmiotu zamówienia") | Rozbicie na punkty poboru i strefy czasowe |
| 4 | Platforma e-Zamówienia / Baza Konkurencyjności | Postępowania archiwalne |
| 5 | Postępowania na dostawę **gazu** lub **ciepła** | Zapotrzebowanie cieplne obiektu |

Szczególnie wartościowe są odpowiedzi na pytania wykonawców — zawierają one dane
uszczegóławiające, których brak w samym ogłoszeniu.

### Dane do dalszego pozyskania

- [ ] Zapotrzebowanie na **ciepło** (przetarg na dostawę gazu lub ciepła sieciowego)
- [ ] **Moc umowna** i grupa taryfowa (załącznik do SWZ)
- [ ] Rozbicie na **strefy czasowe** (szczyt / pozaszczyt) — umożliwia weryfikację kształtu profilu
- [ ] Powierzchnia użytkowa i kubatura obiektu (audyt energetyczny, dokumentacja termomodernizacji)
- [ ] Parametry istniejącego agregatu prądotwórczego (moc, pojemność zbiornika)

---

## 4. Status

Dane dla Szpitala Powiatowego w Pyrzycach potwierdzone i udokumentowane.
Kwerendę dla pozostałych obiektów kandydujących należy przeprowadzić analogicznie
przed ostatecznym wyborem obiektu referencyjnego.

**Źródło:** Szpital Powiatowy w Pyrzycach, „Dotyczy postępowania: Zakup energii elektrycznej",
30.03.2021, odpowiedź na pytanie nr 21 — http://szpital.pyrzyce.net.pl/?p=8988
