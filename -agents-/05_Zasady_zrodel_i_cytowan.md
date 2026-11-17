# Zasady dotyczące źródeł i cytowań — obowiązujące bezwzględnie

> **Dokument nadrzędny.** Dotyczy każdego fragmentu pracy zawierającego odwołanie
> do aktu prawnego, normy, publikacji naukowej, karty katalogowej lub danych obiektu.
> Obowiązuje wszystkie czaty pracujące nad tym projektem.

---

## 1. Zakaz zasadniczy

**Nie wolno podawać numeru aktu prawnego, normy, artykułu, paragrafu, publikacji,
autora ani roku wydania, którego nie potwierdzono w źródle.**

Zakaz obejmuje również formy pozornie bezpieczne:

- „typowa norma dla tego zagadnienia to PN-EN…" — jeżeli nie sprawdzono, że istnieje
- „zgodnie z § 12 rozporządzenia…" — jeżeli numeru paragrafu nie odczytano z tekstu aktu
- „Kowalski (2021) wykazał, że…" — jeżeli publikacji nie odnaleziono
- uzupełnianie niepełnego cytowania o brakujący rok, numer tomu lub stron

**Uzasadnienie.** Odwołanie do nieistniejącego aktu lub publikacji jest w pracy
dyplomowej błędem dyskwalifikującym. Recenzent sprawdza wybrane pozycje
bibliografii; pozycja nieistniejąca podważa wiarygodność całości, łącznie
z wynikami obliczeń, które są poprawne.

---

## 2. Postępowanie w razie braku pewności

| Sytuacja | Postępowanie |
|---|---|
| Treść znana, numer aktu niepewny | opisać treść wymogu, numer oznaczyć `[DO UZUPEŁNIENIA]` |
| Teza znana z literatury, źródło niepamiętane | sformułować bez przypisu, oznaczyć `[ŹRÓDŁO?]` |
| Dane techniczne komponentu niepotwierdzone | podać jako oszacowanie z wyraźnym zastrzeżeniem |
| Wartość normowa (gęstość, wskaźnik emisji) | wskazać, że wartość przyjęto, nie zaś zacytowano |

Oznaczenie `[DO UZUPEŁNIENIA]` jest rozwiązaniem **właściwym**, nie zaś
tymczasowym brakiem. Lepszy jawny znacznik niż prawdopodobnie wyglądający wymysł.

---

## 3. Źródła potwierdzone w tej pracy

Poniższe odwołania zweryfikowano i wolno ich używać bez dodatkowego sprawdzania.

### 3.1. Akty prawne i normy

| Źródło | Zakres wykorzystania |
|---|---|
| Rozporządzenie Ministra Zdrowia w sprawie szczegółowych wymagań, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą — **§ 42** | moc źródła rezerwowego: min. 30% mocy szczytowej |
| tamże — **§ 42** | zasilacze UPS dla odbiorów wymagających przerwy ≤ 0,5 s |
| **PN-HD 60364-7-710** | podział odbiorów na grupy 0/1/2, klasy przerw 0,5 s i 15 s |
| Ustawa z dnia 6 września 2001 r. o dostępie do informacji publicznej | tryb pozyskania danych obiektu, termin 14 dni |

> Pełnych numerów dziennika ustaw oraz dat nowelizacji **nie zweryfikowano** —
> przed złożeniem pracy należy je odczytać z ISAP i uzupełnić.

### 3.2. Dane pierwotne obiektu

| Źródło | Co potwierdza |
|---|---|
| Odpowiedź Szpitala Powiatowego w Pyrzycach, 21.09.2026 | zużycie energii 2023–2025, ciepło, geometria, agregaty, geotermia |
| Tabliczka znamionowa Grupel G0356BDGRAA5T4000S, nr 20024123 | moc STP/PRP, zbiornik 1 000 l, napełnienie maks. 90% |
| NASA POWER | GHI 2,72 kWh/m²/d dla współrzędnych obiektu |
| Geoportal | pomiar powierzchni dachu |
| Dokumentacja przetargowa | zużycie energii elektrycznej |

### 3.3. Dane z modelu HOMER Pro

Parametry komponentów generycznych (PV 800 $/kW, BESS 30 000 $/szt., kocioł η 85%,
2G Aura 404) pochodzą z katalogu programu. **Są to dane katalogowe narzędzia,
nie zaś oferty rynkowe** — tak należy je opisywać.

---

## 4. Wartości przyjęte, nie zacytowane

Poniższe wielkości zastosowano w obliczeniach jako przyjęte. Przy każdym użyciu
należy to zaznaczyć.

| Wielkość | Przyjęta wartość | Status |
|---|---|---|
| Wskaźnik emisyjności miksu PL | 0,66 kg CO₂/kWh | wartość przyjęta — wymaga źródła |
| Emisyjność oleju napędowego | 2,68 kg CO₂/l | wartość normowa — wymaga źródła |
| Emisyjność gazu ziemnego | 1,9 kg CO₂/m³ | wartość normowa — wymaga źródła |
| Wartość opałowa gazu | 9,97 kWh/m³ | wartość normowa — wymaga źródła |
| Cena ciepła sieciowego | 60–90 PLN/GJ | **oszacowanie** — szpital nie podał taryfy |
| Krzywe zużycia paliwa agregatu | 3 warianty | **oszacowanie** — brak DTR |
| Współczynnik wykorzystania dachu | 0,80 | założenie projektowe |
| Uzysk jednostkowy PV | 925 kWh/kWp | z symulacji HOMER |
| Kurs PLN/USD | 4,0 | założenie upraszczające |

---

## 5. Wymogi bibliografii WKŚiR

| Pozycja | Wymóg |
|---|---|
| Pozycje książkowe | **maks. 5** |
| Artykuły naukowe | **min. 10** |
| w tym obcojęzyczne | **min. 5** |
| System | autorsko-rocznikowy |

**Postępowanie przy kompletowaniu bibliografii:**

1. Każdą pozycję odnaleźć w bazie (Scopus, Web of Science, Google Scholar,
   repozytorium wydawcy) i odczytać dane bibliograficzne **ze strony publikacji**.
2. Zapisać DOI — jego obecność potwierdza istnienie pozycji.
3. Pozycji bez DOI lub bez możliwości odnalezienia **nie umieszczać**.
4. Nie tworzyć pozycji na podstawie samej pamięci o temacie.

---

## 6. Kontrola przed złożeniem pracy

- [ ] Każdy paragraf i numer normy odczytany z tekstu aktu, nie z pamięci
- [ ] Pełne numery dzienników ustaw uzupełnione z ISAP
- [ ] Każda pozycja bibliografii posiada DOI lub odnośnik do wydawcy
- [ ] Brak znaczników `[DO UZUPEŁNIENIA]` i `[ŹRÓDŁO?]` w tekście finalnym
- [ ] Wartości z sekcji 4 opisane jako przyjęte, nie jako zacytowane
- [ ] Odwołania do rysunków i tabel zgodne z ich numeracją i treścią

---

## Powiązane

[[02_Zasady_symulacji_HOMER]] · [[00_STAN_PRAC]] · [[00_PLAN_DALSZYCH_PRAC]] ·
[[04_Odpowiedz_szpitala_dane_rzeczywiste]] · [[05_Agregat_GRUPEL_dane_z_tabliczki]]
