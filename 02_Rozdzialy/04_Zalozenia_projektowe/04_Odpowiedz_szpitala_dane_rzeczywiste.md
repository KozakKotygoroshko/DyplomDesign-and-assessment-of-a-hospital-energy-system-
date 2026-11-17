# Odpowiedź Szpitala Powiatowego w Pyrzycach — dane rzeczywiste obiektu

**Nadawca:** Szpital Powiatowy w Pyrzycach, Dział Gospodarczo-Techniczny
**Podpis:** inż. Marek J., Kierownik Działu Gospodarczo-Technicznego
**Data:** 21 września 2026
**Skan:** `Odpowiedz_szpitala_2026-09-21.pdf`
**Tryb:** odpowiedź na wniosek o udostępnienie informacji publicznej

> Dokument stanowi **pierwotne źródło danych** dla całej części projektowej pracy.
> Zastępuje wszystkie wcześniejsze oszacowania. W razie rozbieżności rozstrzyga ten dokument.

---

## 1. Dane przekazane przez obiekt

### 1.1. Geometria budynku

| Wielkość | Wartość |
|---|---|
| Powierzchnia dachu | **2 384 m²** |
| Powierzchnia użytkowa | 7 495 m² |
| Kubatura | 29 840 m³ |

### 1.2. Agregaty prądotwórcze — stan istniejący

| Agregat | Moc pozorna | Moc czynna (cos φ 0,8) | Zbiornik paliwa |
|---|---|---|---|
| **ZPW 100 DTDEO** | 85 kVA | ≈ 68 kW | **120 l** |
| **GO 356 BDLS** | 326 kVA | ≈ 261 kW | **1 000 l** |

### 1.3. Zaopatrzenie w ciepło

**Źródło: geotermia** (miejska sieć ciepłownicza zasilana ze źródła geotermalnego).

| Rok | Zużycie ciepła [GJ] | Przeliczenie [MWh] |
|---|---|---|
| 2023 | 2 821 | 783,6 |
| 2024 | 2 760 | 766,7 |
| **2025** | **2 919** | **810,8** |
| Średnia | 2 833 | **787,0** |

### 1.4. Energia elektryczna

| Pozycja | Wartość |
|---|---|
| Taryfa | **B22** |
| Moc umowna | 422 (jednostka podana jako MWh — patrz uwaga 3.3) |
| 2023 | 373,24 MWh |
| 2024 | 275,68 MWh |
| **2025** | **384,44 MWh** |
| Średnia trzyletnia | **344,45 MWh** |

### 1.5. Stan dokumentacji

Termoizolacja budynku wykonana w **2005 r.** Dokumentacja zachowana szczątkowo,
**audyt energetyczny nie istnieje** — obiekt jest obecnie w trakcie jego wykonywania.

---

## 2. Weryfikacja wcześniejszych założeń

| Wielkość | Założenie przyjęte | Dane rzeczywiste | Ocena |
|---|---|---|---|
| Zużycie elektryczne | 355 MWh/rok | 344,45 (śr.) / **384,44** (2025) | ✅ zgodne, błąd 3% |
| Powierzchnia dachu | 2 110 m² (pomiar Geoportal) | **2 384 m²** | ✅ pomiar zaniżony o 11,5% |
| Zapotrzebowanie cieplne | 700 MWh/rok (oszacowanie) | **787 MWh** (śr.) | ⚠️ zaniżone o 12% |
| Źródło ciepła | kocioł gazowy (założenie) | **geotermia** | ❌ **założenie błędne** |
| Zbiornik paliwa | 1 000 l (wartość typowa) | **1 000 l** | ✅ potwierdzone |
| Moc agregatu | 63 kW (dobór optymalizatora) | **261 kW** (istniejący) | ❌ **przewymiarowany 4,6×** |

---

## 3. Konsekwencje dla modelu — trzy ustalenia zasadnicze

### 3.1. Istniejący agregat nie pokrywa awarii 72-godzinnej

Agregat GO 356 BDLS o mocy czynnej 261 kW pracuje przy obciążeniu szpitala
(ok. 43 kW) na poziomie **16,5% mocy znamionowej**. Reżim ten leży znacznie poniżej
zakresu sprawności optymalnej, wskutek czego jednostkowe zużycie paliwa rośnie.

| Wielkość | Wartość |
|---|---|
| Obciążenie względne | 16,5% mocy znamionowej |
| Szacowane zużycie godzinowe | **15–16 l/h** |
| Zapas 1 000 l wystarcza na | **ok. 64,5 h** |
| Wymagane pokrycie | 72 h |
| **Niedobór** | **ok. 7,5 h — deficyt 116 l** |

Agregat mniejszy (ZPW 100 DTDEO, zbiornik 120 l) zapewnia autonomię rzędu **11 godzin**.

> **Wniosek:** obiekt w stanie istniejącym **nie jest zdolny przetrwać zdarzenia
> typu black-sky o czasie trwania 72 godzin** bez uzupełnienia paliwa w trakcie
> awarii. Teza pracy zyskuje potwierdzenie na danych rzeczywistych, nie zaś
> na wartościach przyjętych typowo.

Ustalenie to wzmacnia wynik symulacji: model optymalizacyjny dobrał agregat 63 kW
zużywający 944 l, podczas gdy jednostka faktycznie zainstalowana zużywa o ok. 18%
więcej paliwa wskutek pracy niskoobciążeniowej.

### 3.2. Źródło ciepła stanowi geotermia — rewizja Konfiguracji K3

Założenie o kotle gazowym jest **nieaktualne**. Obiekt zasilany jest ciepłem
z sieci geotermalnej, co zmienia ocenę kogeneracji w dwojaki sposób:

**Przeciw kogeneracji:** ciepło pozyskiwane jest już ze źródła odnawialnego,
o niskim koszcie zmiennym. Kogeneracja gazowa nie zastępuje zatem kotła
kopalnego, lecz konkuruje ze źródłem geotermalnym — argument środowiskowy
na rzecz CHP zostaje w znacznej części unieważniony.

**Za kogeneracją:** sieć geotermalna wymaga zasilania elektrycznego pomp
obiegowych oraz pomp głębinowych. Podczas awarii systemowej dostawa ciepła
może zatem ustać niezależnie od stanu instalacji wewnętrznej szpitala.
Wymaga to weryfikacji u operatora sieci — Geotermia Pyrzyce Sp. z o.o.

> **Zadanie:** ustalić, czy ciepłownia geotermalna dysponuje własnym zasilaniem
> rezerwowym. Odpowiedź rozstrzyga o tym, czy szpital traci ciepło podczas
> zdarzenia black-sky, a zatem czy odzysk ciepła z CHP ma wartość podczas tego zdarzenia.

### 3.3. Moc umowna — rozbieżność jednostkowa wymagająca wyjaśnienia

W dokumencie podano „Moc umowna – 422 MWh". Moc umowna w taryfie B22 wyrażana jest
w kW; wartość 422 odczytywać należy zatem jako **422 kW**.

Przy rocznym zużyciu 384,44 MWh odpowiada to współczynnikowi wykorzystania mocy
umownej na poziomie **10,4%**, co jest wartością nietypowo niską. Możliwe przyczyny:

1. moc umowna ustalona historycznie z dużym zapasem (przypadek częsty w obiektach
   publicznych — opłata przesyłowa stała jest wówczas zawyżona),
2. występowanie krótkotrwałych szczytów mocy (tomografia, sterylizatornia,
   pompy ciepła węzła geotermalnego) nieujętych w profilu godzinowym,
3. błąd redakcyjny w odpowiedzi.

Profil zbudowany dla symulacji przyjmuje moc szczytową 56,72 kW przy współczynniku
obciążenia 0,715. Rozbieżność wobec mocy umownej nie wpływa na bilans energii ani
na wynik testu przetrwania, natomiast **uniemożliwia analizę opłat przesyłowych**
do czasu wyjaśnienia.

> **Zadanie:** wystąpić o profil godzinowy lub odczyty 15-minutowe z licznika
> za rok 2025 oraz o fakturę wskazującą rzeczywistą moc szczytową.

---

## 4. Aktualizacja parametrów wejściowych

| Parametr | Wartość przyjęta do dalszych obliczeń | Podstawa |
|---|---|---|
| Zużycie elektryczne | **384,44 MWh/rok** (rok 2025) | odpowiedź szpitala |
| Zapotrzebowanie cieplne | **810,8 MWh/rok** (2 919 GJ, rok 2025) | odpowiedź szpitala |
| Powierzchnia dachu | **2 384 m²** | odpowiedź szpitala |
| Graniczna moc PV | **ok. 124 kWp** (po korekcie powierzchni) | przeliczenie |
| Zbiornik paliwa | **1 000 l** | odpowiedź szpitala |
| Moc agregatu istniejącego | **261 kW** (326 kVA) | odpowiedź szpitala |
| Źródło ciepła | **sieć geotermalna** | odpowiedź szpitala |

Przyjęcie roku 2025 jako reprezentatywnego uzasadnione jest tym, że rok 2024
(275,68 MWh) odbiega od pozostałych o ok. 27%, co wskazuje na okoliczność
jednorazową (przerwa w funkcjonowaniu oddziału, remont) wymagającą wyjaśnienia.

---

## 5. Zadania wynikające z odpowiedzi

| Zadanie | Adresat | Priorytet |
|---|---|---|
| Zasilanie rezerwowe ciepłowni geotermalnej | Geotermia Pyrzyce Sp. z o.o. | **wysoki** — rozstrzyga o K3 |
| Profil godzinowy / odczyty 15-min za 2025 | szpital / OSD Enea Operator | **wysoki** |
| Wyjaśnienie mocy umownej 422 kW | szpital | średni |
| Przyczyna spadku zużycia w 2024 | szpital | średni |
| Audyt energetyczny po zakończeniu | szpital | niski — poza harmonogramem pracy |
| Powtórzenie symulacji na 384,44 MWh i PV 124 kWp | — | **wysoki** |

---

## Powiązane

**Dokument uzupełniający:** [[05_Agregat_GRUPEL_dane_z_tabliczki]] — tabliczka znamionowa
agregatu; koryguje pojemność zbiornika z 1 000 na **900 l użytecznych**.

**Wykorzystanie danych:**

- [[04_Zalozenia_projektowe_TEKST]] — rozdział 4 pracy
- [[04_Wyniki_V2_dane_rzeczywiste]] — symulacje przeliczone na te dane
- [[02_Charakterystyka_obiektu_Pyrzyce]] — karta obiektu

**Korespondencja:** [[Pismo_2_DTR_agregatu]]

**Zastępuje:** [[01_Rzeczywiste_dane_zuzycia_energii]] (dane z dokumentacji przetargowej)
