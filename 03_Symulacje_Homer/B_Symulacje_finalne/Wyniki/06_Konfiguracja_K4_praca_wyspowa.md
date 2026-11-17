# Konfiguracja K4 — pełna praca wyspowa

**Data:** 13 listopada 2026
**Charakter:** **oszacowanie analityczne**, nie wynik optymalizacji
**Powód:** licencja HOMER Pro wygasła — obliczenie wykonano metodą bilansu rocznego

---

## 1. Przesłanka

Konfiguracje K1–K3 zakładają obecność sieci elektroenergetycznej jako źródła
podstawowego, a źródła własne pełnią funkcję rezerwy uruchamianej na czas awarii.
Przy takim założeniu jednostka kogeneracyjna pracuje krótko (476 h rocznie
w Konfiguracji K3), ponieważ optymalizator uruchamia ją wyłącznie wtedy, gdy jest
to tańsze od zakupu energii z sieci.

Nasuwa się pytanie o układ odmienny: **kogeneracja jako źródło podstawowe**,
pokrywające zapotrzebowanie obiektu w sposób ciągły. W takim układzie jednostka
zastępuje nie tylko zakup energii elektrycznej, lecz również **zakup ciepła
z sieci geotermalnej** — a zatem obie pozycje kosztowe obiektu jednocześnie.

Okoliczność ta zmienia podstawę oceny ekonomicznej i wymaga odrębnego rozpatrzenia.

---

## 2. Założenia obliczeniowe

| Wielkość | Wartość | Źródło |
|---|---|---|
| Zapotrzebowanie elektryczne | 384,44 MWh/rok | dane szpitala |
| Zapotrzebowanie cieplne | 810,8 MWh/rok | dane szpitala |
| Jednostka CHP | 2G Aura 404, 100 kW | katalog HOMER |
| Krzywa zużycia paliwa | 5,20 + 0,236·P [m³/h] | karta jednostki |
| Minimalne obciążenie robocze | 50% (50 kW) | producent |
| Współczynnik odzysku ciepła | 57,2% | karta jednostki |
| Wartość opałowa gazu | 9,97 kWh/m³ | wartość normowa |
| Cena gazu | 0,65 $/m³ | model HOMER |
| Cena energii z sieci | 0,220 $/kWh | taryfa B22 |

---

## 3. Bilans roczny

### 3.1. Energia elektryczna

Jednostka pracuje przy obciążeniu minimalnym 50 kW, co odpowiada zapotrzebowaniu
średniemu obiektu (43,89 kW) powiększonemu o margines.

```
Czas pracy:        384 440 / 50 = 7 689 h/rok  (88% czasu roku)
Zużycie gazu:      (5,20 + 0,236 · 50) · 7 689 = 130 710 m³/rok
Koszt gazu:        130 710 · 0,65 = 84 961 $/rok
```

Dla porównania, zakup tej samej ilości energii z sieci kosztuje **84 577 $/rok**.
Różnica wynosi 384 $, tj. **0,5%** — koszty są praktycznie równe.

### 3.2. Ciepło

```
Energia paliwa:    130 710 · 9,97 = 1 303 178 kWh
Ciepło odzyskane:  1 303 178 · 0,572 = 745 418 kWh = 745,4 MWh
Pokrycie:          745,4 / 810,8 = 92%
Niedobór:          65,4 MWh -> kocioł szczytowy (7 715 m³ gazu, 5 015 $/rok)
```

**Jednostka pokrywa 92% zapotrzebowania na ciepło jako produkt uboczny wytwarzania
energii elektrycznej.** Pozostałe 8% wymaga kotła szczytowego.

---

## 4. Porównanie kosztów bieżących

Koszt ciepła sieciowego nie jest znany — szpital nie podał taryfy. Przyjęto
przedział typowy dla polskich sieci geotermalnych (60–90 PLN/GJ, kurs 4 PLN/$).

| Cena ciepła | Koszt obecny (prąd + ciepło) | Koszt w układzie K4 | **Oszczędność** |
|---|---|---|---|
| 60 PLN/GJ | 128 362 $/rok | 89 976 $/rok | **38 386 $/rok** |
| **75 PLN/GJ** | **139 308 $/rok** | **89 976 $/rok** | **49 332 $/rok** |
| 90 PLN/GJ | 150 254 $/rok | 89 976 $/rok | **60 278 $/rok** |

### Okres zwrotu

Przy nakładzie obejmującym jednostkę CHP (450 000 $), kocioł szczytowy (20 000 $)
oraz układ rozdzielczo-synchronizacyjny (ok. 50 000 $), tj. **520 000 $**:

```
Okres zwrotu przy 75 PLN/GJ:  520 000 / 49 332 = 10,5 lat
```

---

## 5. Ustalenie zasadnicze — i jego ograniczenie

### 5.1. Co zmienia Konfiguracja K4

W Konfiguracjach K1–K3 kogeneracja konkuruje wyłącznie z ceną energii elektrycznej
i przegrywa. **W układzie pracy ciągłej zastępuje natomiast obie pozycje kosztowe
obiektu** — zakup energii oraz zakup ciepła — przy koszcie paliwa równym samemu
tylko dotychczasowemu rachunkowi za prąd.

Jest to wynik **odmienny od uzyskanego w symulacjach**, a jego przyczyną nie jest
błąd obliczeń, lecz odmienne założenie o roli jednostki w systemie.

### 5.2. Dlaczego nie czyni to Konfiguracji K4 rozwiązaniem zalecanym

**Niezawodność.** Rezygnacja z zasilania sieciowego oznacza uzależnienie obiektu
infrastruktury krytycznej od **jednego silnika spalinowego**. Dostępność sieci
dystrybucyjnej w Polsce odpowiada wskaźnikowi SAIDI rzędu 200 minut rocznie;
dostępność pojedynczego agregatu kogeneracyjnego, z uwzględnieniem przeglądów
i awarii, jest istotnie niższa. Praca wyspowa bez redundancji stanowi zatem
**pogorszenie bezpieczeństwa zasilania**, nie jego poprawę.

Zapewnienie redundancji wymaga drugiej jednostki (układ N+1), co podnosi nakład
do ok. 970 000 $ i wydłuża okres zwrotu do **blisko 20 lat**. Wartość ta mieści się
wprawdzie w przyjętym okresie eksploatacji analizy (25 lat), lecz dla obiektu
publicznego finansowanego ze środków powiatu stanowi horyzont trudny
do zaakceptowania.

**Zależność od jednego nośnika.** Układ opiera całość zaopatrzenia — prąd i ciepło —
na dostawie gazu ziemnego. Przerwa w dostawie gazu pozbawia obiekt obu mediów
jednocześnie, podczas gdy układ obecny ma dwa niezależne źródła.

### 5.3. Konfiguracja pośrednia

Rozwiązaniem sensowniejszym od pełnej pracy wyspowej jest układ, w którym
**kogeneracja stanowi źródło podstawowe, a sieć pozostaje rezerwą**:

| Cecha | Pełna wyspa | Konfiguracja pośrednia |
|---|---|---|
| Źródło podstawowe | CHP | CHP |
| Sieć | odłączona | **zachowana jako rezerwa** |
| Redundancja | wymaga drugiej jednostki | zapewnia ją sieć |
| Nakład | ok. 970 000 $ (N+1) | ok. 520 000 $ |
| Okres zwrotu | ok. 20 lat | **ok. 10,5 lat** |
| Ryzyko przerwy w dostawie gazu | utrata obu mediów | przejście na sieć |

Wariant ten zachowuje korzyść ekonomiczną pełnej wyspy, nie przejmując jej
zasadniczej wady.

---

## 6. Ograniczenia obliczenia

| Pozycja | Charakter | Wpływ |
|---|---|---|
| **Cena ciepła sieciowego** | **nieznana** — przyjęto przedział | **rozstrzygająca dla okresu zwrotu** |
| **Bilans emisji CO₂** | **oszacowany poniżej** | zob. sekcja C6.2 |
| Cena gazu 0,65 $/m³ | z modelu HOMER | wymaga potwierdzenia taryfą |
| Brak optymalizacji | bilans roczny, nie symulacja godzinowa | rzeczywisty czas pracy może odbiegać |
| Pominięto zmienność sezonową ciepła | latem nadwyżka ciepła bez odbioru | **zawyża pokrycie cieplne** |
| Koszty obsługi i przeglądów CHP | pominięte | zaniża koszt bieżący |

> **Zastrzeżenie najważniejsze.** Obliczenie zakłada, że całość ciepła odzyskanego
> znajduje odbiór. Jednostka pracująca przy 50 kW mocy elektrycznej wytwarza
> **96,9 kW ciepła** (745 418 kWh / 7 689 h), podczas gdy letnie zapotrzebowanie obiektu
> wynosi ok. 33 kW. Nadwyżka rzędu 64 kW musiałaby zostać odprowadzona przez
> ok. 2 200 godzin sezonu letniego, co odpowiada ok. 140 MWh ciepła niewykorzystanego.
>
> Po uwzględnieniu tej straty pokrycie zapotrzebowania cieplnego spada z 92%
> do ok. **75%**, a roczna oszczędność — z 49 332 $ do ok. **40 000 $**, co wydłuża
> okres zwrotu z 10,5 do **ok. 13 lat**. **Rzetelne rozstrzygnięcie wymaga symulacji
> godzinowej** — a zatem działającej licencji HOMER Pro.

### 6.1. Weryfikacja założenia o czasie pracy

Przyjęty czas pracy 7 689 h/rok (88% czasu) wynika z podzielenia zapotrzebowania
rocznego przez minimalne obciążenie robocze jednostki. Założenie to jest wewnętrznie
niespójne z ideą pełnej pracy wyspowej: układ pozbawiony zasilania sieciowego musi
dysponować źródłem przez **8 760 godzin**, nie 7 689.

Praca ciągła przy 50 kW daje natomiast:

| Wielkość | Wartość | Zapotrzebowanie | Nadwyżka |
|---|---|---|---|
| Energia elektryczna | 438 000 kWh | 384 440 kWh | **+14%** |
| Ciepło | 849 267 kWh | 810 800 kWh | +5% |
| Zużycie gazu | 148 920 m³ | — | — |
| Koszt gazu | **96 798 $/rok** | — | — |

Nadwyżka energii elektrycznej wymagałaby odbioru (sprzedaż do sieci — niemożliwa
w układzie wyspowym) albo pracy jednostki poniżej minimum roboczego, co producent
wyklucza. **Układ wymaga zatem jednostki o mocy elektrycznej ok. 45 kWe, nie 100 kW** —
niedostępnej w katalogu HOMER Pro.

Ustalenie to wzmacnia wniosek z sekcji C5.2: pełna praca wyspowa na jednostce
katalogowej 100 kW jest rozwiązaniem niedopasowanym do skali obiektu.

---

## 7. Wniosek do pracy

Konfigurację K4 należy ująć w pracy jako **wariant rozpatrzony i omówiony**,
nie zaś jako rozwiązanie zalecane. Jej znaczenie polega na wykazaniu, że:

1. ocena kogeneracji **zależy od przyjętej roli jednostki w systemie** — jako
   rezerwy jest nieopłacalna, jako źródła podstawowego może być opłacalna;
2. wniosek ten nie unieważnia wyników symulacji, lecz wskazuje granicę
   ich stosowalności: optymalizator rozstrzygał zadanie postawione jako
   *sieć plus rezerwa*, nie jako *dobór źródła podstawowego*;
3. rozstrzygnięcie wymaga danych, których obiekt nie udostępnił — przede
   wszystkim **taryfy za ciepło sieciowe**;
4. korzyść ekonomiczna układu **nie przekłada się na korzyść środowiskową**:
   bilans emisji pozostaje zbliżony do stanu obecnego (sekcja C6.2), mimo zastąpienia
   odnawialnego ciepła geotermalnego spalaniem gazu ziemnego. Konfiguracja K4 ma zatem
   uzasadnienie wyłącznie kosztowe i odpornościowe.

Ujęcie takie jest uczciwsze od pominięcia wariantu i mocniejsze od przedstawienia
go jako rekomendacji opartej na oszacowaniu.
