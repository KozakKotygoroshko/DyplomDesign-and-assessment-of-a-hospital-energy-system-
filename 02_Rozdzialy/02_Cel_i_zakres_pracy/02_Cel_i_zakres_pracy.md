# 2. Cel pracy i zakres pracy

## 2.1. Cel pracy

Głównym celem niniejszej pracy jest przeprowadzenie techniczno-ekonomicznej,
odpornościowej oraz środowiskowej oceny architektur zasilania referencyjnego obiektu
szpitalnego o zabudowie jednobryłowej, obejmujących instalację fotowoltaiczną (PV),
bateryjny magazyn energii (BESS) oraz układ kogeneracyjny (CHP).

Za cel nadrzędny przyjęto **rozstrzygnięcie, czy kryterium kosztowe oraz wymóg
bezpieczeństwa energetycznego dają się dla takiego obiektu pogodzić**, a jeżeli nie —
wskazanie, na czym polega konflikt między nimi oraz jakie rozwiązania ograniczają jego
skutki. Bezpieczeństwo energetyczne rozumiane jest przy tym jako **zdolność obiektu
do utrzymania zasilania odbiorów krytycznych przez czas trwania zdarzenia awaryjnego
z zasobów zgromadzonych na terenie obiektu** — nie zaś wyłącznie jako zgodność
z wymogiem normatywnym dotyczącym mocy źródła rezerwowego.

Weryfikacji poddano dwie tezy:

**Teza pierwsza.** Spełnienie wymogu § 42 Rozporządzenia Ministra Zdrowia, określającego
moc źródła rezerwowego na poziomie co najmniej 30% mocy szczytowej, **nie przesądza
o zdolności obiektu do przetrwania długotrwałej awarii sieci**, ponieważ przepis
odnosi się do mocy źródła, pomijając zapas paliwa.

**Teza druga.** Rozbudowa układu o instalację fotowoltaiczną i magazyn bateryjny,
uzasadniona kryterium ekonomicznym i środowiskowym, **nie zwiększa w istotnym stopniu
odporności obiektu na długotrwałe zdarzenie zimowe** — tj. przypadające w okresie
minimum zasobu słonecznego.

Odrębnym celem o charakterze metodycznym jest **ocena przydatności profili
syntetycznych** generowanych przez narzędzia optymalizacyjne do modelowania obiektów
szpitalnych o wysokim współczynniku obciążenia.

## 2.2. Zakres pracy

Zakres pracy obejmuje kolejne etapy inżynierskiego procesu projektowego, w ramach
którego zrealizowano następujące zadania:

1. Dokonano **identyfikacji referencyjnego obiektu szpitalnego** oraz pozyskano jego
   dane energetyczne ze źródeł pierwotnych — dokumentacji przetargowej, odpowiedzi
   udzielonej w trybie dostępu do informacji publicznej oraz dokumentacji własnej
   wykonanej w obiekcie.
2. Przeprowadzono **przegląd literatury przedmiotu oraz wymagań prawno-normatywnych**
   dotyczących zasilania obiektów ochrony zdrowia, ze szczególnym uwzględnieniem
   podziału odbiorów według dopuszczalnego czasu przerwy w zasilaniu.
3. Opracowano **godzinowe profile zapotrzebowania** na energię elektryczną i cieplną
   (8 760 wartości), kalibrowane na rocznych sumach rzeczywistych, oraz poddano je
   weryfikacji względem profilu syntetycznego narzędzia symulacyjnego.
4. Wyznaczono **graniczną moc instalacji fotowoltaicznej** na podstawie analizy
   przestrzennej powierzchni dachowej, z rozpatrzeniem dwóch układów rozmieszczenia
   modułów różniących się współczynnikiem pokrycia.
5. Zdefiniowano **trzy konfiguracje systemu zasilania** — K1 (sieć z agregatem
   prądotwórczym), K2 (sieć, agregat, PV i BESS) oraz K3 (sieć, PV, BESS i CHP
   ze wsparciem cieplnym) — oraz **trzy warianty stanu sieci nadrzędnej**: A0 (praca
   normalna), A1 (awaria 72-godzinna typu *black-sky*) oraz A2 (seria pięciu przerw
   krótkotrwałych).
6. Przeprowadzono **symulacje w środowisku HOMER Pro**, obejmujące roczne bilanse
   energetyczne oraz optymalizację doboru mocy komponentów dla każdego z wariantów
   stanu sieci.
7. Wykonano **test przetrwania** — ocenę czasu autonomii obiektu wyznaczonego
   z pojemności użytecznej zbiornika paliwa oraz charakterystyki zużycia źródła
   sterowalnego, przeprowadzoną zarówno dla konfiguracji modelowych, jak i dla
   **stanu faktycznie istniejącego** w obiekcie.
8. Przeprowadzono **analizę wrażliwości** wyniku testu przetrwania względem
   charakterystyki zużycia paliwa, nieudostępnionej przez obiekt.
9. Wykonano **wielokryterialną ocenę** wyników, uwzględniającą nakłady inwestycyjne
   (CAPEX), uśredniony koszt energii (LCOE), koszt bieżący netto (NPC), emisję CO₂
   oraz czas autonomii.
10. Sformułowano **wnioski końcowe**, obejmujące ocenę obu tez oraz wskazanie
    rozwiązań uszeregowanych według relacji efektu do nakładu.

### Poza zakresem pracy

Poza zakresem pracy pozostawiono:

- analizę stanów przejściowych oraz jakości energii elektrycznej,
- dobór aparatury łączeniowej oraz projekt rozdzielnic,
- szczegółowy projekt instalacji elektrycznej wraz z obliczeniami zwarciowymi,
- ocenę stanu technicznego urządzeń zainstalowanych w obiekcie;
- dobór aparatury rozdzielczej dla układu odciążania odbiorów nieistotnych.

Zagadnienia te mogą stanowić przedmiot odrębnych opracowań.

> **Uwaga redakcyjna.** W pracy wprowadzono konsekwentne rozróżnienie pojęć:
> **konfiguracja** (K1, K2, K3) oznacza architekturę systemu zasilania, natomiast
> **wariant stanu sieci** (A0, A1, A2) — stan sieci nadrzędnej przyjęty w symulacji.
> Pojęcie „scenariusz" nie jest stosowane.
