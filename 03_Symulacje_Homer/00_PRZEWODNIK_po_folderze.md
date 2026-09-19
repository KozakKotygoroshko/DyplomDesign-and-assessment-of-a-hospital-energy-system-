# Symulacje HOMER Pro — przewodnik po folderze

Folder zawiera **dwie niezależne serie symulacyjne**. Różnią się skalą obiektu
i pochodzeniem danych wejściowych. Wyniki jednej serii **nie są porównywalne**
z wynikami drugiej.

---

## 📂 A_Symulacje_testowe — seria weryfikacyjna

**Dane:** modelowe, oparte na wskaźnikach literaturowych
**Skala:** 1 000 MWh/rok elektrycznej, 1 800 MWh/rok cieplnej
**Lokalizacja:** Szczecin (punkt ogólny)
**Cel:** sprawdzenie poprawności metodyki, rozpoznanie narzędzia, identyfikacja pułapek modelowych
**Status:** ✅ **zakończona**

| Podfolder | Zawartość |
|---|---|
| `Modele/` | 5 plików `.homer` — trzy scenariusze + warianty z CHP gazowym |
| `Profile/` | Profile obciążenia 8760 h (elektryczny 1 GWh, cieplny 1,8 GWh) |
| `Wyniki/` | Raport zbiorczy `.md` + `RAPORT_KONCOWY_Symulacje_testowe.docx` (17 stron) + raporty natywne HOMER |
| `Grafika/` | 21 wykresów: 6 własnych porównawczych (W1–W6) + 15 wyodrębnionych z raportów HOMER |

**Do czego służy:** materiał wysłany promotorowi. Zawiera wnioski metodyczne,
które zachowują ważność niezależnie od skali obiektu.

---

## 📂 B_Symulacje_finalne — seria właściwa

**Dane:** rzeczywiste — Szpital Powiatowy w Pyrzycach
**Skala:** 355 MWh/rok elektrycznej (potwierdzone), 700 MWh/rok cieplnej (oszacowanie)
**Lokalizacja:** 53°08'49,93"N / 14°53'44,66"E (współrzędne rzeczywiste)
**Cel:** wyniki końcowe pracy dyplomowej
**Status:** 🔄 **profile gotowe, symulacje przed nami**

| Podfolder | Zawartość |
|---|---|
| `04_Zalozenia_rzeczywiste_Pyrzyce.md` | Komplet założeń, przeliczenia autonomii, parametry do HOMER |
| `Profile/` | Profile przeskalowane na dane rzeczywiste |
| `Modele/` | *(puste — do uzupełnienia)* |
| `Wyniki/` | *(puste — do uzupełnienia)* |
| `Grafika/` | *(puste — do uzupełnienia)* |

---

## 📂 Awarie_szeregi_czasowe — wspólne dla obu serii

Szeregi czasowe zdarzeń awaryjnych (8760 wartości, konwencja: **1 = sieć dostępna, 0 = awaria**).

| Plik | Wariant | Opis |
|---|---|---|
| `Awaria_blacksky_72h_styczen.csv` | **A1** | Pojedyncza awaria 72 h, 15–17 stycznia |
| `Awaria_seria_krotkich_przerw.csv` | **A2** | 5 przerw, łącznie 21 h (SAIDI 1260 min, SAIFI 5/rok) |

Pliki niezależne od skali obiektu — używane w obu seriach bez modyfikacji.

---

## 📂 _archiwum

Wcześniejsze, rozproszone wersje notatek oraz nieaktualne wersje raportów.
Zachowane wyłącznie na wypadek potrzeby odtworzenia historii prac.

---

## Kluczowe różnice między seriami

| Wielkość | A — testowa | B — finalna | Stosunek |
|---|---|---|---|
| Zużycie elektryczne | 1 000 MWh | **355 MWh** | 2,8 : 1 |
| Moc szczytowa | 159,8 kW | **56,7 kW** | 2,8 : 1 |
| Odbiory krytyczne (30%) | 47,9 kW | **17,0 kW** | 2,8 : 1 |
| Energia w 72 h awarii | 8 762 kWh | **3 111 kWh** | 2,8 : 1 |
| Moc PV | 250 kWp | **100–110 kWp** | 2,3 : 1 |
| Moc CHP | 100 kW | **40–50 kW** | 2,2 : 1 |
| Zbiornik paliwa dla 72 h | 2 430 l | **970 l** | 2,5 : 1 |

### Co pozostaje wspólne

Wnioski **jakościowe** obu serii są zbieżne, ponieważ dotyczą relacji między
konfiguracjami, nie zaś wartości bezwzględnych:

- kryterium najniższego NPC prowadzi do wyboru układu pozbawionego źródła rezerwowego,
- magazyn bateryjny pełni funkcję pomostową dla klasy 0,5 s, nie zaś źródła autonomii,
- kogeneracja gazowa zapewnia niezależność od transportu drogowego paliwa,
- sezonowość zasobu słonecznego wyklucza autonomię opartą na PV zimą.

### Co się zmienia

Wnioski **ilościowe** — przy rzeczywistej skali obiektu autonomia 72-godzinna
jest osiągalna przy użyciu komponentów standardowych, katalogowych.

---

## Stan licencji HOMER Pro

Licencja Evaluation przedłużona o **7 dni** — ważna do ok. **26 września 2026**.

> **Zalecenie:** po wykonaniu symulacji serii B natychmiast wygenerować raporty
> w formacie DOCX (`Simulation Results → Create Proposal`) oraz zachować pliki
> `.homer`. Raporty pozostaną dostępne niezależnie od statusu licencji.

---

## Powiązane materiały poza tym folderem

- `01_Baza_Wiedzy/Instrukcja_HOMER_Pro.md` — instrukcja obsługi programu krok po kroku
- `02_Rozdzialy/04_Zalozenia_projektowe/` — karta obiektu, dane rzeczywiste, kwerenda
- `00_Temat_i_metodyka.md` — zasady projektowe i metodyka testu przetrwania
