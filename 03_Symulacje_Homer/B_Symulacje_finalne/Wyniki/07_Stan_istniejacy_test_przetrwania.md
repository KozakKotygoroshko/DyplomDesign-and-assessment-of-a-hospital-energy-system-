# Stan istniejący obiektu — test przetrwania

Załącznik przedstawia ocenę zdolności obiektu do przetrwania zdarzenia
72-godzinnego na parametrach **jednostek faktycznie zainstalowanych**, w odróżnieniu
od konfiguracji modelowych omówionych w rozdziale 7.

---

## 1. Rozróżnienie pojęciowe — obowiązujące w całej pracy

Ocena odporności obiektu wymaga odróżnienia dwóch wielkości: pojemności zbiornika
jednostki **faktycznie zainstalowanej** oraz zużycia paliwa jednostki **dobranej
przez optymalizator**. Zestawienie ich ze sobą prowadziłoby do wyniku
nieprzypisanego do żadnego rzeczywistego układu.

| Pojęcie | Agregat | Zbiornik użyteczny | CAPEX | Rola w pracy |
|---|---|---|---|---|
| **Stan istniejący** | Grupel G0356, **258 kW** PRP + ZPW 100 DTDEO, 68 kW | **900 + 108 = 1 008 l** | 0 $ (istnieje) | **punkt odniesienia testu przetrwania** |
| **Konfiguracja K1** | `Autosize Genset`, **68 kW** (dobór HOMER) | — (model nie ogranicza paliwa) | 34 000 $ | **punkt odniesienia analizy ekonomicznej** |

> **Zasada.** Wnioski dotyczące **czasu autonomii** odnoszą się do stanu istniejącego.
> Wnioski dotyczące **kosztu** odnoszą się do Konfiguracji K1, porównywalnej z K2 i K3
> pod względem metodyki doboru. Nie wolno zestawiać zbiornika stanu istniejącego
> ze zużyciem paliwa Konfiguracji K1.

---

## 2. Zasoby stanu istniejącego

| Agregat | Moc czynna | Zbiornik nominalny | Napełnienie | **Użyteczne** |
|---|---|---|---|---|
| Grupel G0356BDGRAA5T4000S | 258 kW (PRP) | 1 000 l | 90% | **900 l** |
| ZPW 100 DTDEO | ≈ 68 kW | 120 l | 90%¹ | **108 l** |
| **Razem** | — | 1 120 l | — | **1 008 l** |

¹ Ograniczenie 90% odczytano z tabliczki jednostki Grupel. Dla jednostki ZPW tabliczki
nie udokumentowano — przyjęto ten sam współczynnik jako wartość typową. Przy założeniu
pełnej pojemności 120 l wynik końcowy zmienia się o 0,9 h.

---

## 3. Przebieg zdarzenia 72-godzinnego

Przyjęto pracę sekwencyjną: jednostka Grupel pracuje do wyczerpania własnego zbiornika,
po czym następuje przełączenie odbiorów na jednostkę ZPW.

Obciążenie: **46,79 kW** (średnie w wariancie A1, zasilanie całości obiektu).

### 3.1. Jednostka ZPW w drugiej fazie

Przy obciążeniu 46,79 kW jednostka 68 kW pracuje na poziomie **69% mocy znamionowej** —
w zakresie zalecanym, w odróżnieniu od jednostki Grupel (18,1%).

```
F = 2,37 + 0,25 · 46,79 = 14,07 l/h
t = 108 / 14,07 = 7,7 h
```

### 3.2. Wynik łączny

| Krzywa zużycia Grupel | Zużycie [l/h] | Faza I (Grupel) | Faza II (ZPW) | **Razem** | Pokrycie 72 h |
|---|---|---|---|---|---|
| **Optymistyczna** | 13,08 | 68,8 h | 7,7 h | **76,5 h** | **TAK — zapas 4,5 h** |
| **Średnia** | 15,53 | 58,0 h | 7,7 h | **65,6 h** | **nie — brak 6,4 h** |
| **Zachowawcza** | 17,96 | 50,1 h | 7,7 h | **57,8 h** | **nie — brak 14,2 h** |

---

## 4. Wniosek — sformułowanie warunkowe

Uwzględnienie drugiej jednostki prądotwórczej **zmienia charakter wyniku**. Poprzednie
sformułowanie — „w żadnym z wariantów zdarzenie nie zostaje pokryte" — przestaje
obowiązywać.

> **Zdolność obiektu do przetrwania zdarzenia 72-godzinnego pozostaje
> nierozstrzygnięta.** Przy najkorzystniejszej z rozpatrywanych krzywych zużycia paliwa
> zapas obu jednostek wystarcza na 76,5 h, przy pozostałych dwóch — na 65,6 oraz 57,8 h.
> Rozstrzygnięcie zależy od charakterystyki zużycia paliwa agregatu Grupel, której
> obiekt nie udostępnił.

### 4.1. Warunki, od których zależy wynik pozytywny

Pokrycie zdarzenia w wariancie optymistycznym jest możliwe **wyłącznie przy łącznym
spełnieniu** poniższych warunków:

| Warunek | Status |
|---|---|
| Oba zbiorniki napełnione w chwili wystąpienia zdarzenia | nieudokumentowany |
| Możliwość przełączenia odbiorów z jednostki Grupel na ZPW | **wymaga schematu rozdzielni** |
| Zakres odbiorów obu jednostek obejmuje te same obwody | **wymaga schematu rozdzielni** |
| Rzeczywiste zużycie paliwa odpowiada krzywej optymistycznej | **wymaga DTR producenta** |
| Przełączenie następuje bez istotnej przerwy w zasilaniu | nieudokumentowane |

Niespełnienie któregokolwiek z nich prowadzi do wyniku negatywnego. **Żaden z warunków
nie został potwierdzony dokumentacją.**

### 4.2. Co pozostaje ustalone niezależnie od powyższego

Następujące wnioski zachowują ważność w każdym z wariantów:

1. **Pojedyncza jednostka Grupel nie pokrywa zdarzenia w żadnym wariancie**
   (50,1–68,8 h wobec wymaganych 72 h). Pokrycie wymaga sekwencyjnego użycia
   obu agregatów, co nie jest rozwiązaniem projektowym, lecz wymuszonym.
2. **Margines jest w każdym przypadku znikomy** — od −14,2 do +4,5 h przy zdarzeniu
   trwającym 72 h, tj. od −20% do +6%.
3. **Jednostka Grupel pracuje przy obciążeniu 18,1% mocy znamionowej**, poza zakresem
   zalecanym, co podwyższa jednostkowe zużycie paliwa. Jednostka ZPW, czterokrotnie
   mniejsza, pracuje w tych samych warunkach z sprawnością wyższą.
4. **Uzupełnienie paliwa w trakcie zdarzenia wymaga przerwania zasilania** — tabliczka
   znamionowa zawiera zakaz tankowania podczas pracy.
5. **Ograniczenie zasilania do odbiorów krytycznych usuwa problem w całości**
   (82–129 h, zob. 05_Praca_wyspowa_odbiory_krytyczne) — i pozostaje rozwiązaniem
   o najkorzystniejszej relacji efektu do nakładu.

---

## 5. Konsekwencje dla tekstu pracy

| Miejsce | Dotychczas | Wymagana korekta |
|---|---|---|
| 7.2.2 | „K1 — wyczerpanie w 64,0 h" | rozdzielić: stan istniejący 57,8–76,5 h; K1 jako wynik modelowy |
| 7.2.5 | „W żadnym z wariantów zdarzenie nie zostaje pokryte" | sformułować warunkowo, uwzględnić drugą jednostkę |
| 7.5.1 | „Pokrycie A1 z zapasu — nie" | „nierozstrzygnięte — zależne od krzywej zużycia" |
| 8.1 | „nie jest zdolny do przetrwania" | „zdolność nierozstrzygnięta; pokrycie wymaga sekwencyjnego użycia obu agregatów" |
| Zał. A | „K1 — stan istniejący, 0 $" | zastąpić tabelą z sekcji 1 niniejszego dokumentu |

---

## 6. Ocena wpływu na tezę pracy

Zebrane dane nie pozwalają na sformułowanie kategoryczne. Sformułowanie
nieznajdujące pokrycia w danych:

> *Szpital nie jest zdolny do przetrwania zdarzenia 72-godzinnego.*

Sformułowanie znajdujące pokrycie w danych:

> *Zdolność szpitala do przetrwania zdarzenia 72-godzinnego pozostaje
> nierozstrzygnięta i zależy od wielkości nieudokumentowanych przez obiekt —
> charakterystyki zużycia paliwa oraz możliwości przełączenia odbiorów między
> agregatami. Przy obciążeniu pełnym margines mieści się w przedziale od −20%
> do +6% czasu trwania zdarzenia. Ograniczenie zasilania do odbiorów krytycznych
> usuwa niepewność, zapewniając pokrycie we wszystkich rozpatrywanych wariantach.*

Sformułowanie drugie wskazuje zarówno brakujące dane, jak i rozwiązanie
niezależne od tego braku.
