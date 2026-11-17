# Plan dalszych prac

**Aktualizacja:** 13 listopada 2026
**Założenie:** wobec braku odpowiedzi promotora przyjęto rozstrzygnięcia własne,
opisane w punkcie 1. Każde z nich jest odwracalne — dotyczą zakresu, nie treści.

---

## 1. Rozstrzygnięcia przyjęte samodzielnie

| Kwestia | Decyzja | Uzasadnienie |
|---|---|---|
| Zakres rozdziału *Dobór urządzeń* | **pełny** — z obliczeniami sprawdzającymi | Słowo „Projekt" w temacie. Nadmiar nie zaszkodzi, brak — może |
| Sformułowanie wniosku | **rzeczowe, bez wyostrzania** | „Analiza wykazała ograniczenie autonomii" — broni się niezależnie od stanowiska promotora |
| Informowanie szpitala | **poza zakresem pracy** | Decyzja promotora lub uczelni; nie blokuje redakcji |
| Praca wyspowa na odbiorach krytycznych | **włączyć** | Nakład niewielki, wzmocnienie istotne |

---

## 2. Co pozostało — podział według trudności

### 2.1. Łatwe — materiał gotowy, pozostaje redakcja

| Zadanie | Stan materiału |
|---|---|
| **Rozdział 5** — opis wariantów zasilania | modele zbudowane, parametry opisane |
| **Rozdział 7** — analiza wyników | obliczenia zamknięte, tabele gotowe |
| **Rozdział 8** — wnioski | wniosek zasadniczy sformułowany |
| Przeliczenie wykresów F1–F5 na serię V2 | dane w `04_Wyniki_V2_dane_rzeczywiste` |
| Aneks — karty komponentów | karty do zebrania, układ znany |

To **największa objętościowo** część pozostałej pracy, a zarazem najmniej ryzykowna.
Nie wymaga ani oprogramowania, ani danych zewnętrznych.

### 2.2. Średnie — wymaga nowego nakładu, lecz bez zależności zewnętrznych

| Zadanie | Charakter |
|---|---|
| **Rozdział 6** — dobór urządzeń i obliczenia elektryczne | nowy materiał, wymaga oprogramowania |
| Analiza pracy wyspowej (18,4 kW) | obliczenie analityczne, ewentualnie przebieg HOMER |
| **Bibliografia** | 5 pozycji książkowych, 10 artykułów, w tym 5 obcojęzycznych |

### 2.3. Trudne — zależne od stron trzecich

| Zadanie | Status | **Czy blokuje?** |
|---|---|---|
| Krzywa zużycia paliwa agregatu | pismo bez odpowiedzi | **Nie** — zastąpiona analizą wrażliwości |
| Profil godzinowy z licznika OSD | niewystąpiono | **Nie** — profil własny uzasadniony w 4.2.4 |
| Dane CHP 30–40 kW od producenta | niepozyskane | **Nie** — ograniczenie katalogu opisane jako wynik |
| Zasilanie rezerwowe ciepłowni | niewystąpiono | **Nie** — przyjęto założenie zachowawcze |
| Schemat rozdzielni obiektu | pismo bez odpowiedzi | **Nie** — przyjęto zasilanie całości obiektu |

> **Ustalenie zasadnicze.** Żadna pozycja z grupy 2.3 nie blokuje ukończenia pracy.
> Każda z nich została zastąpiona rozwiązaniem metodycznym — analizą wrażliwości,
> założeniem zachowawczym albo opisem ograniczenia jako wyniku. Praca może zostać
> ukończona wyłącznie na materiale już posiadanym.

---

## 3. Rozdział 6 — dobór urządzeń

### 3.1. Co jest potrzebne

| Element | Narzędzie | Obligatoryjność |
|---|---|---|
| Rozmieszczenie modułów na dachu | oprogramowanie PV lub CAD | rysunek wymagany |
| Porównanie uzysku: układ S vs E–W | PVGIS lub PV\*SOL / PVsyst | wymagane — rozstrzyga o mocy |
| Dobór modułu i falownika | karty katalogowe | wymagane |
| Obliczenia łańcuchów | **obliczenie własne** | wymagane — ręcznie, nie z programu |
| Przekroje przewodów, spadki napięć | **obliczenie własne** | wymagane |
| Zabezpieczenia, SPD | normy + karty | wymagane |
| Schemat jednokreskowy | CAD / narzędzie rysunkowe | wymagane |

> **Uwaga.** Obliczenia łańcuchów i przewodów muszą zostać **przedstawione w pracy
> jako obliczenia**, nie jako wydruk z programu. Oprogramowanie służy do rozmieszczenia
> modułów i wyznaczenia uzysku — reszta to rachunek, który podlega ocenie.

### 3.2. Oprogramowanie — warianty

| Narzędzie | Koszt | Co daje | Ocena |
|---|---|---|---|
| **PVGIS** | bezpłatne, przeglądarka | uzysk dla dowolnej orientacji i pochylenia, dane europejskie | **punkt wyjścia** — wystarcza do porównania S vs E–W |
| **PV\*SOL premium** | wersja próbna 30 dni | rozmieszczenie 3D, zacienienie, wizualizacja, raport | **zalecane** — standard w Polsce, raport nadaje się do aneksu |
| **PVsyst** | wersja próbna 30 dni | analiza szczegółowa, uznawana w środowisku naukowym | alternatywa, trudniejszy próg wejścia |
| **Sunny Design** (SMA) | bezpłatne | dobór falownika i łańcuchów | przydatne do weryfikacji obliczeń własnych |
| Konfigurator producenta falownika | bezpłatne | sprawdzenie zgodności łańcuchów | weryfikacja |

**Postępowanie zalecane:**

1. **PVGIS** — porównać uzysk roczny układu południowego (25°) i wschód–zachód (12°)
   dla współrzędnych obiektu. Wynik rozstrzyga, który układ przyjąć.
2. **PV\*SOL w wersji próbnej** — wykonać rozmieszczenie na rzeczywistym obrysie dachu,
   uzyskać liczbę modułów i raport do aneksu. Trzydzieści dni wystarcza z zapasem.
3. **Obliczenia łańcuchów wykonać samodzielnie**, wynik porównać z konfiguratorem
   producenta falownika — zgodność potwierdza poprawność rachunku.

> Wersję próbną uruchomić **dopiero wtedy**, gdy dach jest obmierzony, a moduł i falownik
> wybrane. Inaczej część z trzydziestu dni zostanie zużyta na przygotowania.

---

## 4. Kolejność prac

### Etap I — redakcja na materiale gotowym

Równolegle, bez zależności zewnętrznych:

1. Rozdział 5 — opis trzech konfiguracji i modelowania awarii
2. Rozdział 7 — analiza wyników serii V2
3. Rozdział 8 — wnioski
4. *(czat graficzny)* przeliczenie wykresów F1–F5 na serię V2

Po tym etapie praca jest **kompletna merytorycznie** w zakresie pierwotnym.

### Etap II — rozdział 6

1. PVGIS — rozstrzygnięcie układu rozmieszczenia
2. Wybór modułu i falownika z kart katalogowych
3. PV\*SOL — rozmieszczenie i raport
4. Obliczenia własne: łańcuchy, przewody, zabezpieczenia
5. Schemat jednokreskowy

### Etap III — uzupełnienia

1. Analiza pracy wyspowej na odbiorach krytycznych (18,4 kW)
2. Bibliografia
3. Aneks — karty komponentów, profile, szeregi awarii
4. Skład całości wg wymogów edytorskich WKŚiR

---

## 5. Ryzyka

| Ryzyko | Skutek | Przeciwdziałanie |
|---|---|---|
| **Wygaśnięcie licencji HOMER Pro** | brak możliwości dodatkowych przebiegów | Sprawdzić **niezwłocznie**. Pliki `.homer` otwierają się bez licencji; analizę wyspową da się wykonać analitycznie |
| Nieotrzymanie odpowiedzi promotora | niepewność co do zakresu rozdziału 6 | Przyjęto zakres pełny — nadmiar nie szkodzi |
| Krzywa próbna PV\*SOL wykorzystana przedwcześnie | utrata narzędzia | Uruchomić dopiero po przygotowaniu danych |
| Przenumerowanie rozdziałów | rozjazd folderów ze spisem treści | Foldery `06`–`09` przenumerować po zatwierdzeniu rozdziału 6 |

---

## 6. Pozycje nieblokujące — do odnotowania w pracy

Zamiast oczekiwać na dane, które mogą nie nadejść, każde ograniczenie opisano
jako **wynik metodyczny**:

| Brak danych | Sposób ujęcia w pracy |
|---|---|
| Krzywa zużycia paliwa | analiza wrażliwości — wynik niezmienny w przedziale 13,1–18,0 l/h |
| Profil godzinowy | uzasadnienie profilu własnego i wykazanie wady profilu syntetycznego |
| CHP poniżej 100 kW | ograniczenie katalogu HOMER opisane jako ustalenie |
| Zasilanie ciepłowni | założenie zachowawcze, wzmacniające rolę odzysku ciepła |

Podejście to jest **mocniejsze niż oczekiwanie**: ograniczenie opisane i obsłużone
stanowi wynik pracy, ograniczenie przemilczane — jej słabość.

---

## Powiązane

[[00_STAN_PRAC]] · [[00_Szkielet_Pracy]] · [[04_Wyniki_V2_dane_rzeczywiste]] ·
[[05_Agregat_GRUPEL_dane_z_tabliczki]] · [[03_Prompt_czat_graficzny]]
