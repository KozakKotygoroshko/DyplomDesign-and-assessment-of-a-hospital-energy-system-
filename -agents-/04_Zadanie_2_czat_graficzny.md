# Zadanie drugie — czat graficzny

> Treść do wklejenia w czacie graficznym po wykonaniu zadania pierwszego.

---

## 0. NAJPIERW — korekta danych K3

W pliku wyników znajdował się **błąd przypisania**, obecnie poprawiony.
Jako Konfigurację K3 podano wiersz **bez magazynu bateryjnego**, podczas gdy
zgodnie z definicją K3 = **sieć + PV + BESS + CHP + kocioł**.

Rysunki `R7_1`, `R7_2`, `R7_4` i `R7_5` zawierają wartości nieaktualne.
Poniżej wartości obowiązujące:

| Wielkość | Było (błędnie) | **Jest (poprawnie)** |
|---|---|---|
| CAPEX K3 (A0) | 571 869 $ | **596 638 $** |
| NPC K3 (A0) | 2,20 M$ | **2,24 M$** |
| LCOE K3 (A0) | 0,270 | **0,285** |
| Czas pracy CHP (A0) | 504 h | **476 h** |
| Produkcja CHP (A0) | 26 343 kWh | **24 937 kWh** |
| Paliwo K3 (A1) | 1 263 m³ | **1 239 m³** |
| NPC / LCOE K3 (A1) | 1,75 M$ / 0,188 | **1,80 M$ / 0,199** |
| CAPEX K3 (A1, A2) | 450 000 $ | **529 300 $** |
| Paliwo K3 (A2) | 361 m³ | **358 m³** |
| NPC / LCOE K3 (A2) | 1,74 M$ / 0,187 | **1,80 M$ / 0,199** |
| Stosunek CAPEX K3/K1 | 16,8× | **17,5×** |

Wartość **1 976 h** (CHP bez PV i bez magazynu) pozostaje prawidłowa jako wiersz
porównawczy — nie jest natomiast Konfiguracją K3 i tak należy ją opisać.

Źródło zaktualizowane: `04_Wyniki_V2_dane_rzeczywiste.md`, sekcje 2–5.
**Popraw te cztery rysunki przed przystąpieniem do zadań poniżej.**

---

Робота з першого завдання прийнята — сім рисунків R7_1…R7_7 готові,
індекс заповнений правильно, обмеження позначені чесно. Далі три речі.

## 1. Приписати рисунки до підрозділів

В індексі у графі «Podrozdział» для всіх R7_x стоїть «do przypisania».
Простав номери за структурою зі `00_Szkielet_Pracy.md` (розділ 7):

| Рисунок | Підрозділ |
|---|---|
| R7_1 CAPEX | 7.3 Analiza ekonomiczna |
| R7_2 LCOE | 7.3 Analiza ekonomiczna |
| R7_3 Zbiornik 900 l | 7.2.5 Ograniczenia autonomii |
| R7_4 Czas pracy A0 | 7.1.1 Pokrycie zapotrzebowania |
| R7_5 Zużycie paliwa | 7.2.2 / 7.2.3 Wyniki A1 i A2 |
| R7_6 Wyczerpanie zbiornika | **7.2.2 — rysunek centralny rozdziału** |
| R7_7 Analiza wrażliwości | 7.2.5 Ograniczenia autonomii |

## 2. Прибрати застарілі PNG

Файли `F1`–`F5` у `B_Symulacje_finalne/Grafika/` — серія на даних 355 MWh
і баку 1000 л. Вони **нікуди не підуть**, але лежать поруч із новими
і їх легко сплутати.

Перенеси їх у підпапку `_nieaktualne/` у тій самій теці
(видаляти не треба — хай лишаються як історія).

## 3. Новий рисунок до розділу 5

Потрібна **схема трьох конфігурацій** — блокова, по три панелі в ряд
або одна під одною. Для кожної конфігурації показати склад:

| | Блоки |
|---|---|
| **K1** | Sieć → Szpital · Agregat 68 kW (rezerwa) |
| **K2** | Sieć → Szpital · Agregat 68 kW · PV 124 kWp · BESS 100 kWh · Przekształtnik |
| **K3** | Sieć → Szpital · PV 124 kWp · CHP 100 kW (prąd + ciepło) · Kocioł szczytowy |

Під кожною конфігурацією — рядок із CAPEX (34 000 / 180 638 / 571 869 $)
та підписом, чи покриває 72-годинну аварію з наявного запасу
(K1 — ні, K2 — ні, K3 — так).

Назва файлу: `R5_1_Schemat_trzech_konfiguracji.svg`,
тека: `02_Rozdzialy/05_Projekt_wariantow_zasilania/Materialy_graficzne/`
(створи теку, якщо її немає).

Кольори конфігурацій — ті самі, що ти вже закріпив у розділі 7:
K1 `#8a6d1f`, K2 `#2c5f8d`, K3 `#4a7a4a`.

---

## Заблоковане — поки не бери

| Рисунок | Чому |
|---|---|
| `R4_6_Zasob_sloneczny` | потрібна таблиця місячних GHI з HOMER |
| `R7_8_SoC_BESS_A1` | потрібен погодинний ряд із HOMER |
| `R7_9_Praca_zrodel_A1` | те саме |

Ліцензія HOMER Pro, найімовірніше, вже недійсна. Якщо так — ці три рисунки
до роботи не ввійдуть, і це нормально: у тексті буде зазначено, що
відповідні ряди не експортовано.

**Нічого з цього не вигадуй.** Краще відсутній рисунок, ніж правдоподібний.
