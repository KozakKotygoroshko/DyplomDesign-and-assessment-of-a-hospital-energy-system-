# Agregat prądotwórczy GRUPEL — dane z tabliczki znamionowej

**Źródło:** fotografia tabliczki znamionowej wykonana w obiekcie, 6 października 2026.
**Status:** dane pierwotne, odczyt bezpośredni z urządzenia.
**Dokumentacja:** `Tabliczka_znamionowa_agregat_GRUPEL.pdf` (w tym samym folderze)

> **Uwaga.** Dokument stanowi **odrębne źródło** wobec odpowiedzi szpitala
> z 21.09.2026 ([[04_Odpowiedz_szpitala_dane_rzeczywiste]]). Szpital podał oznaczenie
> „GO 356 BDLS, 326 kVA, zbiornik 1 000 l"; tabliczka precyzuje model, rozróżnia moc
> STP od PRP oraz zawiera **ograniczenie napełnienia zbiornika do 90%**, nieujęte
> w odpowiedzi. W razie rozbieżności rozstrzyga tabliczka.

| Pozycja | Odpowiedź szpitala | **Tabliczka znamionowa** |
|---|---|---|
| Model | GO 356 BDLS | **Grupel G0356BDGRAA5T4000S** |
| Moc pozorna | 326 kVA | **356 kVA (STP) / 323 kVA (PRP)** |
| Moc czynna | nie podano | **285 kW (STP) / 258 kW (PRP)** |
| Zbiornik | 1 000 l | 1 000 l, **napełnienie maks. 90% → 900 l** |

---

## 1. Dane odczytane

| Pozycja | Wartość |
|---|---|
| Producent | **Grupel S.A.**, Parque Industrial de Soza, Vagos, Portugalia |
| Model | **G0356BDGRAA5T4000S** |
| Numer seryjny | 20024123 |
| Data produkcji | **06/2023** |
| **Pojemność zbiornika** | **1 000 l** |
| **Dopuszczalny stopień napełnienia** | **90%** (oznaczenie ostrzegawcze „CAUTION FUEL CAPACITY 90%") |
| Moc pozorna STP / PRP | 356 / **323 kVA** |
| Moc czynna STP / PRP | 285 / **258 kW** |
| Prąd znamionowy | 514 A |
| Napięcie | 400/230 V, 3 fazy |
| Częstotliwość | 50 Hz |
| Współczynnik mocy | 0,8 |
| Masa | 2 674 kg |
| Wymiary | 3 320 × 1 400 × 1 850 mm |

**Oznaczenia dodatkowe:** praca wyłącznie w strefie wentylowanej (ostrzeżenie CO),
zakaz tankowania podczas pracy, zakaz podnoszenia z paliwem w zbiorniku.

---

## 2. Ustalenia zmieniające wynik analizy

### 2.1. Pojemność użyteczna zbiornika wynosi 900 l, nie 1 000 l

Tabliczka zawiera oznaczenie ostrzegawcze ograniczające napełnienie zbiornika do **90%
pojemności nominalnej**. Jest to zabezpieczenie przed rozszerzalnością cieplną paliwa
oraz przelaniem przy pracy urządzenia.

```
Pojemność nominalna:        1 000 l
Dopuszczalne napełnienie:      90%
POJEMNOŚĆ UŻYTECZNA:          900 l
```

Wszystkie wcześniejsze obliczenia autonomii przyjmowały 1 000 l. **Wartość należy
skorygować do 900 l.** Korekta pogarsza bilans o 100 l, tj. o 10%.

### 2.2. Moc znamionowa potwierdzona

Przyjęte wcześniej oszacowanie 261 kW (z przeliczenia 326 kVA × cos φ 0,8) okazało się
niemal dokładne. Wartość właściwa dla pracy awaryjnej to **PRP 258 kW** — moc ciągła
przy obciążeniu zmiennym, odpowiadająca charakterowi pracy podczas awarii sieci.

Obciążenie szpitala w czasie awarii (46,79 kW średnio) stanowi:

| Odniesienie | Obciążenie względne |
|---|---|
| wobec PRP (258 kW) | **18,1%** |
| wobec STP (285 kW) | 16,4% |

Reżim ten leży poniżej zakresu zalecanego przez producentów silników wysokoprężnych
(zwykle 30–80% mocy znamionowej). Praca długotrwała przy obciążeniu poniżej 30% prowadzi
do zjawiska *wet stacking* — niecałkowitego spalania, zaolejenia układu wydechowego
i obniżenia sprawności.

---

## 3. Analiza wrażliwości — autonomia przy zbiorniku 900 l

Tabliczka znamionowa nie zawiera charakterystyki zużycia paliwa. Przyjęto zatem trzy
warianty krzywej, obejmujące rozrzut spotykany dla jednostek tej klasy mocy. Krzywa
modelowana liniowo: **F = a·P_zn + b·P_wyj** [l/h].

Obciążenie przyjęte: **46,79 kW** (średnie w okresie awarii 72 h).

| Wariant krzywej | Zużycie [l/h] | Czas pracy z 900 l | Deficyt wobec 72 h | Brakuje paliwa |
|---|---|---|---|---|
| Optymistyczny *(silnik o niskim zużyciu jałowym)* | 13,1 | **68,8 h** | 3,2 h | 42 l |
| Średni | 15,5 | **57,9 h** | 14,1 h | 219 l |
| Zachowawczy *(krzywa domyślna HOMER)* | 18,0 | **50,1 h** | 21,9 h | 393 l |

### Wniosek z analizy wrażliwości

**W żadnym z trzech wariantów zbiornik nie pokrywa awarii 72-godzinnej.** Nawet przy
założeniu najkorzystniejszym autonomia kończy się na 68,8 h, tj. ponad trzy godziny
przed końcem zdarzenia.

Wniosek jest zatem **odporny na niepewność danych** — nie zależy od tego, który z wariantów
krzywej odpowiada rzeczywistości. Jest to argument mocniejszy niż oparty na pojedynczym
oszacowaniu punktowym, ponieważ nie wymaga obrony konkretnej wartości zużycia.

---

## 4. Weryfikacja wynikiem symulacji HOMER

Optymalizator HOMER, dobierając agregat o mocy **68 kW** (dopasowanej do obiektu),
wyznaczył zapotrzebowanie na paliwo w wariancie A1 na poziomie **1 013 l**, co odpowiada
średniemu zużyciu 14,07 l/h.

| Wielkość | Wartość |
|---|---|
| Zapotrzebowanie (agregat 68 kW, HOMER) | 1 013 l |
| Pojemność użyteczna zbiornika | 900 l |
| **Deficyt** | **113 l** |
| Czas pracy możliwy do uzyskania | **64,0 h** |
| Brakujący czas | **8,0 h** |

Zgodność wyniku HOMER (14,07 l/h) z wariantem optymistyczno-średnim analizy wrażliwości
potwierdza poprawność przyjętego zakresu. Jednostka faktycznie zainstalowana, czterokrotnie
przewymiarowana, zużywa paliwa więcej — deficyt jest zatem **większy niż 113 l**.

---

## 5. Konsekwencja dla pracy dyplomowej

Ustalenie to stanowi **empiryczne potwierdzenie tezy pracy** na danych pierwotnych,
odczytanych z urządzenia:

> Szpital Powiatowy w Pyrzycach, wyposażony w agregat prądotwórczy zgodny z wymogiem
> § 42 Rozporządzenia Ministra Zdrowia, **nie jest zdolny do przetrwania zdarzenia
> typu black-sky o czasie trwania 72 godzin** bez uzupełnienia paliwa w trakcie awarii.
> Ograniczeniem nie są parametry elektryczne układu, lecz pojemność użyteczna zbiornika
> wynosząca 900 litrów.

Uzupełnienie paliwa wymaga dostawy transportem drogowym — tj. zasobu, którego dostępność
podczas zdarzenia typu black-sky jest wątpliwa. Co więcej, tankowanie podczas pracy agregatu jest
zabronione oznaczeniem na tabliczce, co oznacza konieczność **przerwania zasilania**
na czas uzupełnienia.

---

## 6. Pozycje wciąż nieustalone

| Zadanie | Wpływ |
|---|---|
| Charakterystyka zużycia paliwa (DTR Grupel) | Zawęża przedział 50–69 h do wartości jednej |
| Zakres odbiorów zasilanych z agregatu | Umożliwia analizę pracy na odbiorach krytycznych (18,4 kW) |
| Obecność i parametry zasilaczy UPS | Odbiory klasy 0,5 s wg PN-HD 60364-7-710 |
| Umowa na awaryjne dostawy paliwa | Czy obiekt ma zapewnioną dostawę w czasie zdarzenia |

> **Uwaga.** Model `G0356BDGRAA5T4000S` jest jednostką katalogową producenta Grupel.
> Kartę katalogową można pozyskać bezpośrednio od producenta
> (formularz: grupel.eu — „Request a technical datasheet"), podając numer seryjny 20024123.

---

## Powiązane

**Dokument nadrzędny:** [[04_Odpowiedz_szpitala_dane_rzeczywiste]] — odpowiedź szpitala;
niniejszy dokument koryguje podaną tam pojemność zbiornika.

**Ustalenie wpływa na:**

- [[04_Wyniki_V2_dane_rzeczywiste]] — Konfiguracje K1 i K2 przestają pokrywać awarię 72 h
- [[04_Zalozenia_projektowe_TEKST]] — podrozdziały 4.1.2 i 4.3
- [[03_Raport_wg_konfiguracji]] — **wymaga aktualizacji** (zawiera wartość 1 000 l)

**Podstawa teoretyczna:** [[3_2_Agregaty_Diesel]] — *wet stacking*, zależność
od łańcucha dostaw paliwa

**Korespondencja:** [[Pismo_2_DTR_agregatu]] — wystąpienie o charakterystykę zużycia paliwa
