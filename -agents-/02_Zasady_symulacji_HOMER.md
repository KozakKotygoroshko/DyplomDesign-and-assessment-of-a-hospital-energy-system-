# Zasady prowadzenia symulacji w HOMER Pro — obowiązujące zawsze

> **Dokument nadrzędny.** Każda symulacja w HOMER Pro musi być zgodna z poniższymi
> zasadami. Przed uruchomieniem obliczeń należy zweryfikować kompletność modelu
> według listy kontrolnej z sekcji 4.

---

## 1. Zasada podstawowa — jeden przebieg zawiera wszystkie konfiguracje

HOMER Pro **nie liczy jednej konfiguracji na raz**. W jednym przebiegu optymalizator
przebiera **wszystkie kombinacje** komponentów obecnych w modelu i zwraca tabelę,
w której **każdy wiersz stanowi odrębną konfigurację**.

### Odwzorowanie scenariuszy pracy na wiersze tabeli wyników

| Wiersz w tabeli wyników | Scenariusz pracy |
|---|---|
| sama sieć | **punkt odniesienia** (nie jest scenariuszem) |
| sieć + agregat | **Scenariusz 1 — Baza** |
| sieć + agregat + PV + BESS | **Scenariusz 2 — Hybryda** |
| sieć + PV + BESS + CHP | **Scenariusz 3 — Zaawansowana mikrosieć** |
| pozostałe kombinacje | materiał uzupełniający |

**Wniosek praktyczny:** liczba przebiegów odpowiada liczbie **wariantów awarii**,
nie liczbie scenariuszy.

```
3 warianty awarii (A0, A1, A2) = 3 przebiegi
Każdy przebieg zawiera wszystkie trzy scenariusze w tabeli wyników
```

---

## 2. Komponenty obowiązkowe w KAŻDYM modelu

Model musi zawierać **komplet** poniższych komponentów, niezależnie od tego, który
scenariusz jest przedmiotem zainteresowania. Pominięcie któregokolwiek powoduje, że
odpowiadające mu wiersze w tabeli wyników **nie zostaną wygenerowane**.

| Komponent | Rola | Uwaga |
|---|---|---|
| **Sieć elektroenergetyczna** | obecna we wszystkich scenariuszach | taryfa 0,220 / 0,090 $/kWh |
| **Agregat prądotwórczy (Diesel)** | warunek Scenariuszy 1 i 2 | `Autosize Genset` |
| **Instalacja PV** | Scenariusze 2 i 3 | ograniczenie górne z analizy dachu |
| **Magazyn BESS** | Scenariusze 2 i 3 | SoC min. 40% |
| **Przekształtnik** | wymagany przy PV i BESS | dobór automatyczny |
| **Kogeneracja CHP** | Scenariusz 3 | jednostka **gazowa** z katalogu |
| **Kocioł szczytowy** | wymagany przy szynie cieplnej | gaz ziemny |

> **Błąd popełniony 19.09.2026:** w modelu finalnym pominięto agregat prądotwórczy.
> W konsekwencji Scenariusze 1 i 2 nie zostały obliczone, a porównanie sprowadzało się
> do zestawienia z układem pozbawionym jakiegokolwiek źródła rezerwowego — wariantem
> nieistniejącym w praktyce i niedopuszczalnym prawnie (§ 30 Rozp. MZ).

---

## 3. Warianty awarii — trzy przebiegi

| Wariant | Plik szeregu czasowego | Dopuszczalny niedobór mocy |
|---|---|---|
| **A0** — praca normalna | brak | 0% |
| **A1** — black-sky 72 h | `Awaria_blacksky_72h_styczen.csv` | **10%** |
| **A2** — seria przerw | `Awaria_seria_krotkich_przerw.csv` | **10%** |

**Konwencja szeregu czasowego:** wartość **1 = sieć dostępna**, **0 = awaria**.
Konwencja odwrotna do intuicyjnej.

**Podniesienie dopuszczalnego niedoboru do 10%** w wariantach awaryjnych jest konieczne —
przy wartości zerowej optymalizator odrzuca wszystkie konfiguracje jako niedopuszczalne
i nie zwraca żadnych wyników, uniemożliwiając pomiar skali niedoboru.

---

## 4. Lista kontrolna przed uruchomieniem obliczeń

Przed kliknięciem `Calculate` należy sprawdzić **panel schematu po lewej stronie**
i potwierdzić obecność wszystkich komponentów.

- [ ] Lokalizacja ustawiona na współrzędne obiektu rzeczywistego
- [ ] Profil elektryczny zaimportowany — **zweryfikować** zgodność metryk (kWh/d, szczyt, LF)
- [ ] Profil cieplny zaimportowany (jeśli analizowany jest Scenariusz 3)
- [ ] Rok modelowania: **2007** (1 stycznia = poniedziałek, zgodnie z profilem)
- [ ] Sieć obecna, taryfy ustawione
- [ ] **Agregat prądotwórczy obecny** ← najczęstszy błąd
- [ ] PV obecna, przestrzeń poszukiwań ograniczona powierzchnią dachu
- [ ] BESS obecny, SoC min. 40%
- [ ] CHP gazowy obecny (nie Diesel — jednostka wysokoprężna nie zostanie wybrana)
- [ ] Kocioł obecny
- [ ] Zasoby pobrane: GHI oraz temperatura
- [ ] Wariant awarii wczytany (A1/A2) lub usunięty (A0)
- [ ] Dopuszczalny niedobór mocy: 0% dla A0, 10% dla A1 i A2

---

## 5. Po zakończeniu obliczeń

| Czynność | Uzasadnienie |
|---|---|
| Zapisać plik `.homer` | Otwiera się bez aktywnej licencji |
| Wygenerować raport `Create Proposal` → DOCX | Zawiera wykresy; pozostaje dostępny po wygaśnięciu licencji |
| Odczytać kolumnę **Unmet Electric Load** | Wielkość mierzona w teście przetrwania |
| Odczytać **godziny pracy** źródeł sterowalnych | Weryfikacja poprawności modelu awarii |
| Sprawdzić komunikat `search space may be insufficient` | Oznacza osiągnięcie granicy zbioru — nie jest błędem, gdy ograniczeniem jest powierzchnia dachu |

---

## 6. Weryfikacja poprawności modelu awarii

Model jest poprawny, jeżeli **czas pracy źródła sterowalnego odpowiada czasowi trwania
awarii**:

| Wariant | Oczekiwany czas pracy | Potwierdzenie (19.09.2026) |
|---|---|---|
| A1 — 72 h | 72,0 h | ✅ 72,0 h, produkcja 3 111 kWh |
| A2 — 21 h | 21,0 h | ✅ 21,0 h, produkcja 895 kWh |

Dodatkowo: produkcja energii przez źródło sterowalne powinna odpowiadać obliczonemu
analitycznie zapotrzebowaniu obiektu w okresie awarii. Rozbieżność wskazuje na błąd
w profilu lub w szeregu czasowym awarii.

---

## 7. Dobór jednostki kogeneracyjnej — ograniczenie katalogu

Katalog HOMER Pro zawiera jednostki gazowe o mocy **minimum 100 kW** (2G Aura 404).
Dla obiektów o mocy średniej poniżej 50 kW jednostka taka jest przewymiarowana,
co skutkuje znikomym czasem pracy (125 h/rok dla Pyrzyc) i brakiem uzasadnienia
ekonomicznego.

**Postępowanie:** dla obiektów mniejszych należy pozyskać dane jednostki 30–40 kW
bezpośrednio od producenta i wprowadzić je jako komponent własny.

Jednostki wysokoprężne (`Autosize Genset` na oleju napędowym) **nigdy nie zostają
wybrane przez optymalizator jako źródło kogeneracyjne** — koszt paliwa przewyższa
cenę zakupu energii z sieci połączoną z produkcją ciepła w kotle gazowym.
