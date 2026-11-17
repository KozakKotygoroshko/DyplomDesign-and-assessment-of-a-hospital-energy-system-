# Praca wyspowa na odbiorach krytycznych — analiza uzupełniająca

**Data:** 13 listopada 2026
**Charakter:** obliczenie analityczne, bez udziału HOMER Pro
**Przedmiot:** czy ograniczenie zasilania do odbiorów krytycznych pozwala
Konfiguracji K1 pokryć zdarzenie 72-godzinne z zapasu zgromadzonego na obiekcie

---

## 1. Przesłanka

Analiza w 04_Wyniki_V2_dane_rzeczywiste wykazała, że Konfiguracje K1 oraz K2
wyczerpują zapas paliwa odpowiednio w 64,0 oraz 68,4 godzinie awarii 72-godzinnej.
Obliczenia te przeprowadzono przy założeniu zasilania **całości obiektu** —
podejściu zachowawczym, przyjętym wobec braku schematu rozdzielni.

Założenie to nie odpowiada jednak sposobowi, w jaki obiekty szpitalne pracują
w rzeczywistości. Norma PN-HD 60364-7-710 dzieli odbiory na grupy według
dopuszczalnego czasu przerwy, a § 42 Rozporządzenia Ministra Zdrowia określa moc
źródła rezerwowego na poziomie **30% mocy szczytowej** — nie zaś 100%. Zakłada się
zatem, że podczas awarii część odbiorów zostaje odłączona.

Niniejsza analiza bada, jak zmienia się bilans paliwowy po uwzględnieniu
tego ograniczenia.

---

## 2. Założenia

| Wielkość | Wartość | Podstawa |
|---|---|---|
| Pojemność użyteczna zbiornika | 900 l | 05_Agregat_GRUPEL_dane_z_tabliczki |
| Czas trwania zdarzenia | 72 h | wariant A1 |
| Obciążenie pełne (średnie w A1) | 46,79 kW | profil własny |
| **Obciążenie krytyczne** | **18,40 kW** | 30% mocy szczytowej (§ 42) |
| Redukcja obciążenia | 60,7% | przeliczenie |

Krzywą zużycia paliwa przyjęto w postaci liniowej **F = a + b·P** [l/h], gdzie
składnik stały `a` odwzorowuje zużycie jałowe silnika, a `b` — zużycie zależne
od mocy wyjściowej.

Dla agregatu dobranego przez optymalizator (68 kW) współczynniki wyznaczono
z wyniku symulacji: zużycie 1 013 l w ciągu 72 h przy obciążeniu 46,79 kW daje
średnio 14,07 l/h, co przy nachyleniu b = 0,25 l/kWh odpowiada a = 2,37 l/h.

Dla agregatu faktycznie zainstalowanego (Grupel, 258 kW) zastosowano trzy warianty
krzywej, przyjęte wcześniej w analizie wrażliwości.

---

## 3. Wyniki

### 3.1. Zapotrzebowanie na energię

| Tryb pracy | Energia w 72 h | Redukcja |
|---|---|---|
| Zasilanie całości obiektu | 3 369 kWh | — |
| **Zasilanie odbiorów krytycznych** | **1 325 kWh** | **60,7%** |

### 3.2. Autonomia

| Krzywa zużycia | Zużycie przy 18,4 kW | **Czas pracy z 900 l** | Paliwo na 72 h | Zapas |
|---|---|---|---|---|
| HOMER, agregat 68 kW | 6,97 l/h | **129,1 h** | 502 l | 398 l |
| Grupel — optymistyczna | 7,23 l/h | **124,5 h** | 521 l | 379 l |
| Grupel — średnia | 9,14 l/h | **98,5 h** | 658 l | 242 l |
| Grupel — zachowawcza | 10,98 l/h | **82,0 h** | 790 l | 110 l |

### Ustalenie zasadnicze

**We wszystkich rozpatrywanych wariantach krzywej zużycia ograniczenie zasilania
do odbiorów krytycznych pozwala pokryć zdarzenie 72-godzinne z zapasu
zgromadzonego na obiekcie.** Najmniej korzystny wariant daje 82,0 godziny,
tj. o 10 godzin więcej, niż wymaga zdarzenie.

Dla porównania, przy zasilaniu całości obiektu żaden z wariantów nie osiągał
72 godzin (przedział 50,1–68,8 h).

---

## 4. Obciążenie graniczne

Wielkością rozstrzygającą jest moc, powyżej której zapas 900 l przestaje
wystarczać na 72 godziny. Odpowiada jej zużycie 900 / 72 = **12,50 l/h**.

| Krzywa zużycia | Obciążenie graniczne | Udział mocy szczytowej |
|---|---|---|
| HOMER, agregat 68 kW | 40,5 kW | 66% |
| Grupel — optymistyczna | 44,0 kW | 72% |
| Grupel — średnia | 33,3 kW | 54% |
| **Grupel — zachowawcza** | **24,6 kW** | **40%** |

Odbiory krytyczne wg § 42 stanowią 18,4 kW, tj. **30% mocy szczytowej** — wartość
leżącą poniżej obciążenia granicznego w każdym z wariantów. Margines wynosi
od 6,2 kW (krzywa zachowawcza) do 25,6 kW (wariant optymistyczny).

> **Ograniczenie analizy.** Wielkość 18,4 kW stanowi **wymóg normatywny**, nie zaś
> zmierzone zapotrzebowanie odbiorów grup 1 i 2 w tym obiekcie. Rzeczywista moc
> odbiorów krytycznych może być wyższa. Przy wariancie zachowawczym krzywej
> przekroczenie 24,6 kW — tj. 40% mocy szczytowej — oznaczałoby niepokrycie
> zdarzenia. Ustalenie rzeczywistego zakresu odbiorów wymaga schematu rozdzielni,
> o który wystąpiono pismem z 21.09.2026.

---

## 5. Wniosek i jego znaczenie dla pracy

Analiza ujawnia **trzecią drogę**, nieuwzględnioną w pierwotnym zestawieniu
konfiguracji:

| Rozwiązanie | Pokrycie 72 h | Nakład inwestycyjny |
|---|---|---|
| Stan istniejący, zasilanie całości obiektu | **nierozstrzygnięte** (57,8–76,5 h) | 0 $ (istnieje) |
| K2 — rozbudowa o PV i magazyn | **nie** (68,4 h) | 180 638 $ |
| **K3 — mikrosieć z kogeneracją** | **tak** | 596 638 $ |
| **K1 + automatyka odciążania** | **tak** (82–129 h) | rząd kilku tysięcy $ |

Układ samoczynnego odciążania odbiorów nieistotnych — rozdzielnica z wydzieloną
sekcją odbiorów krytycznych oraz sterownik odłączający pozostałe przy przejściu
na zasilanie rezerwowe — stanowi rozwiązanie o koszcie niższym o **dwa rzędy
wielkości** od kogeneracji, zapewniając przy tym pokrycie tego samego zdarzenia.

Nie unieważnia to analizy Konfiguracji K3. Kogeneracja pozostaje jedynym
rozwiązaniem **niezależnym od zapasu paliwa na obiekcie**, a zatem jedynym
zapewniającym pracę przez czas nieograniczony oraz dostawę ciepła, która
— przy przyjętym założeniu o ustaniu zasilania ciepłowni geotermalnej —
podczas zdarzenia zimowego ma znaczenie samoistne.

Wniosek pracy przyjmuje zatem postać stopniowaną:

1. **Zdolność stanu istniejącego do przetrwania zdarzenia 72-godzinnego pozostaje
   nierozstrzygnięta** — wynik mieści się w przedziale 57,8–76,5 h zależnie
   od przyjętej krzywej zużycia paliwa;
2. **Rozwiązaniem o najkorzystniejszej relacji efektu do nakładu jest automatyka
   odciążania**, nie zaś rozbudowa źródeł;
3. **Rozwiązaniem zapewniającym autonomię nieograniczoną pozostaje kogeneracja**,
   właściwą jednak dla zdarzeń dłuższych niż rozpatrywane 72 godziny lub dla
   obiektów, w których utrata dostawy ciepła jest niedopuszczalna.
