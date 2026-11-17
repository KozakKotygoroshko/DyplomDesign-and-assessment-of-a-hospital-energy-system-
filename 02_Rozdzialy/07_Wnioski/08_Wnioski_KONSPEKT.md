# 8. Wnioski

> **Rozdział w opracowaniu.** Poniżej konspekt wyprowadzony z rozdziału 7
> po korekcie recenzyjnej.

## 8.1. Ocena tezy pierwszej

**Teza:** spełnienie wymogu § 42 nie przesądza o zdolności obiektu do przetrwania
długotrwałej awarii sieci.

**Teza potwierdzona.** Agregat zainstalowany w obiekcie przewyższa wymóg normatywny
(18,4 kW) czternastokrotnie, dysponując mocą 258 kW. Mimo to zapas paliwa zgromadzony
na obiekcie daje autonomię od 57,8 do 76,5 h przy zasilaniu całości obiektu —
wobec 72 h trwania zdarzenia. Przepis odnosi się do mocy źródła i nie zawiera
wymogu dotyczącego zapasu paliwa, który okazuje się wielkością rozstrzygającą.

**Zdolność obiektu do przetrwania pozostaje nierozstrzygnięta** i zależy
od charakterystyki zużycia paliwa oraz od możliwości sekwencyjnego użycia obu
agregatów — wielkości nieudokumentowanych przez obiekt.

## 8.2. Ocena tezy drugiej

**Teza:** rozbudowa o PV i magazyn nie zwiększa istotnie odporności na zdarzenie
długotrwałe.

**Teza potwierdzona.** Konfiguracja K2 przesuwa moment wyczerpania zapasu o 4,4 h
(64,0 → 68,4 h w ujęciu modelowym), zużywając o 65 l paliwa mniej. Wkład instalacji
fotowoltaicznej w bilans zdarzenia styczniowego wynosi 276 kWh z wymaganych 3 369 kWh,
tj. 8,2%, co wynika z napromieniowania na poziomie 15% wartości majowej.

## 8.3. Wniosek stopniowany

Analiza nie prowadzi do wskazania jednej konfiguracji, lecz do trzech poziomów
rozwiązań o rosnącym nakładzie i rosnącym zakresie ochrony (podrozdział 7.5.2):
automatyka odciążania, instalacja fotowoltaiczna, kogeneracja gazowa.

## 8.4. Architektura hierarchiczna

Żadne z analizowanych źródeł nie zastępuje pozostałych; odporność wynika z ich
współdziałania w odmiennych skalach czasowych zdarzenia (podrozdział 7.5.3).

## 8.5. Wnioski metodyczne

1. Profil syntetyczny narzędzia optymalizacyjnego zawyża moc szczytową
   **analizowanego obiektu** 3,2-krotnie. Wniosku nie rozciąga się na inne obiekty —
   porównaniu poddano dwa profile, z których żaden nie jest pomiarem.
2. Kryterium najniższego kosztu bieżącego netto prowadzi do wyboru konfiguracji
   pozbawionej źródła rezerwowego. Energia niedostarczona musi być traktowana
   jako ograniczenie twarde, nie jako składnik kosztu.
3. Ocena układu kogeneracyjnego zależy od przypisanej mu roli: jako rezerwa jest
   nieopłacalna, jako źródło podstawowe może być opłacalna (załącznik C).

## 8.6. Kierunki dalszych prac

Weryfikacja rzeczywistego zakresu odbiorów krytycznych; pozyskanie charakterystyki
zużycia paliwa agregatu; symulacja godzinowa Konfiguracji K4 (załącznik C);
przeliczenie modelu z zakupem ciepła sieciowego w miejsce kotła gazowego;
rozpatrzenie jednostki kogeneracyjnej o mocy 20–50 kWe.
