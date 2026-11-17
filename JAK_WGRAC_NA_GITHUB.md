# Jak wgrać zmiany na GitHub

Wszystko jest już przygotowane. Pliki, których **nie wolno publikować**, zostały
wpisane do `.gitignore` — GitHub Desktop sam ich nie pokaże i nie trzeba niczego
odznaczać.

---

## Trzy kroki

1. Otwórz **GitHub Desktop**. Powinien pokazać repozytorium
   *DyplomDesign-and-assessment-of-a-hospital-energy-system-* oraz listę zmienionych
   plików po lewej stronie (ok. 69 pozycji).

2. W polu **Summary** na dole po lewej wklej:

   ```
   Korekta recenzyjna: § 42, rozdzielenie stanu istniejącego od K1, przebudowa dokumentu
   ```

   W polu **Description** poniżej wklej:

   ```
   - § 42 Rozp. MZ w miejsce błędnych § 30 i § 41 (zweryfikowano w tekście aktu)
   - rozdzielenie stanu istniejącego (Grupel 258 kW + ZPW, 1008 l) od Konfiguracji K1 (model 68 kW)
   - uwzględnienie drugiego agregatu; test przetrwania 57,8-76,5 h (wynik nierozstrzygnięty)
   - korekta Konfiguracji K3: 596 638 USD / 0,285 / 476 h / 1239 m3 (wariant z magazynem)
   - tabela liczb wzorcowych jako dokument rozstrzygający
   - załączniki A-C: stan istniejący, praca wyspowa, Konfiguracja K4
   - naprawa dokumentu zbiorczego: A4, numeracja stron, tabele, duplikaty rozdziałów
   - terminologia: konfiguracje K1-K3, warianty stanu sieci A0-A2
   ```

3. Kliknij **Commit to main**, a następnie **Push origin** (przycisk u góry).

---

## Co zostało wykluczone i dlaczego

| Plik | Powód |
|---|---|
| `Odpowiedz_szpitala_2026-09-21.pdf` | podpis i imienne oznaczenie pracownika szpitala |
| `Tabliczka_znamionowa_agregat_GRUPEL.pdf` | numer seryjny urządzenia |
| `PRACA_CALOSC_do_sprawdzenia.docx` | wersja z błędami składu |
| `PRACA_CALOSC_v2_po_korekcie.docx` | j.w. |
| `PRACA_CALOSC_v3.docx` | j.w. |
| `PRACA_CALOSC_v4.docx` | duplikaty rozdziałów 6 i 9 |
| `Dyplom_zvit_ukrainska.docx` | nieaktualne dane Konfiguracji K3 |

Treść obu skanów jest przytoczona w plikach `.md`, więc dla promotora nic nie ginie:

- `02_Rozdzialy/04_Zalozenia_projektowe/04_Odpowiedz_szpitala_dane_rzeczywiste.md`
- `02_Rozdzialy/04_Zalozenia_projektowe/05_Agregat_GRUPEL_dane_z_tabliczki.md`

**Wersje obowiązujące w repozytorium:** `PRACA_CALOSC_v5.docx` (praca, 61 stron)
oraz `Dyplom_zvit_ukrainska_v2.docx` (streszczenie po ukraińsku, 14 stron).

---

## Dwie sprawy do sprawdzenia przy okazji

**Czy repozytorium jest prywatne?** Jeżeli publiczne — warto zmienić, ponieważ
system antyplagiatowy JSA przeszukuje źródła publiczne i może oznaczyć własny tekst
autora jako zapożyczenie. Ustawienie: *Settings → General → Danger Zone →
Change repository visibility*.

**Token dostępu.** Token wygenerowany 17.11.2026 nie jest już potrzebny — operacje
zapisu z tego środowiska są zablokowane po stronie platformy. Należy go usunąć:
*GitHub → Settings → Developer settings → Personal access tokens → Fine-grained →
Delete*.
