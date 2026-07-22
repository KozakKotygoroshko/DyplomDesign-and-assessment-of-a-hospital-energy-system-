# **Baza Wiedzy i Analiza Krytyczna: Architektura Systemów Energetycznych Szpitali w Kontekście Bezpieczeństwa** 

Ewolucja systemów elektroenergetycznych w obiektach ochrony zdrowia przechodzi obecnie bezprecedensową transformację. Klasyczny paradygmat, oparty na scentralizowanym zasilaniu z sieci elektroenergetycznej oraz rezerwowaniu pasywnym przy użyciu generatorów prądotwórczych z silnikiem wysokoprężnym, staje się niewystarczający w obliczu współczesnych zagrożeń hybrydowych, rosnącego zapotrzebowania na energię oraz dążeń do dekarbonizacji. Złożoność nowoczesnej aparatury medycznej, konieczność zapewnienia absolutnej bezprzerwowości zasilania dla procedur podtrzymujących życie oraz integracja rozproszonych źródeł energii (Distributed Energy Resources – DER) wymuszają przejście w kierunku zaawansowanych, w pełni sterowalnych mikrosieci (ang. _microgrids_ ). W dobie cyfryzacji medycyny i stosowania wysoce energochłonnych urządzeń diagnostycznych, inżynieria zasilania musi odpowiadać nie tylko na wyzwania techniczne, ale również na rygorystyczne uwarunkowania prawne i normatywne. 

Niniejszy raport stanowi dogłębną syntezę oraz analityczne zestawienie precyzyjnych materiałów źródłowych, przeznaczonych do zasilenia bazy wiedzy na potrzeby zaawansowanych prac badawczych i inżynierskich. Analiza łączy w sobie trzy kluczowe perspektywy: krajowe ramy prawne definiujące infrastrukturę krytyczną, międzynarodowe normy techniczne regulujące reżimy projektowe, oraz najnowszy dorobek naukowy (lata 20212026) w zakresie hybrydyzacji, odporności ( _resilience_ ) i optymalizacji mikrosieci szpitalnych. Całość materiału została poddana ocenie przez pryzmat integracji jednostek kogeneracyjnych (CHP), systemów fotowoltaicznych (PV) oraz wielkoskalowych bateryjnych magazynów energii (BESS). 

## **Kategoria 1: Ramy Prawne, Wytyczne Rządowe i Planowanie Ciągłości Działania w Polsce** 

Projektowanie architektury zasilania dla obiektów medycznych jest procesem ściśle zdeterminowanym przez przepisy prawa powszechnie obowiązującego. Legislacja ta narzuca nie tylko minimalne wymogi dla instalacji budynkowych, ale przede wszystkim kategoryzuje szpitale jako strategiczne filary bezpieczeństwa państwa, co pociąga za sobą dalekosiężne implikacje dla inżynierów projektujących takie układy. 

### **Wymagania Budowlano-Instalacyjne dla Obiektów Lecznictwa** 

Fundamentem prawnym warunkującym minimalny standard bezpieczeństwa energetycznego w polskim systemie ochrony zdrowia jest Rozporządzenie Ministra Zdrowia w sprawie 

szczegółowych wymagań, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą<sup>1</sup> . Dokument ten ustanawia kluczowe parametry brzegowe dla zasilania rezerwowego. Zgodnie z zapisami § 30 oraz § 41 tego aktu, szpital musi bezwzględnie posiadać rezerwowe źródło zaopatrzenia w energię elektryczną w postaci agregatu prądotwórczego wyposażonego w funkcję autostartu, który jest w stanie pokryć co najmniej 30% szczytowego zapotrzebowania na moc placówki, wspartego urządzeniami zapewniającymi bezprzerwowe podtrzymanie napięcia (UPS)<sup>1</sup> . 

W praktyce inżynierskiej próg 30% mocy szczytowej stanowi jedynie legislacyjne minimum, które zazwyczaj wystarcza wyłącznie na pokrycie obciążeń usług bezpieczeństwa. Do takich krytycznych odbiorów należą bloki operacyjne, oddziały intensywnej terapii (OIT/OIOM), izolatki z wentylacją nadciśnieniową, strefy podtrzymania życia noworodków, systemy oświetlenia ewakuacyjnego oraz chłodnie do przechowywania krwi i szczepionek<sup>4</sup> . Znaczące ograniczenie tego przepisu polega na jego niedostosowaniu do współczesnej, energochłonnej infrastruktury obrazowej (np. Rezonans Magnetyczny, Tomografia Komputerowa), która generuje asymetryczne piki obciążeń (tzw. _inrush currents_ ), zdolne do destabilizacji sieci zasilanej wyłącznie z tradycyjnego agregatu. Z tego względu nowoczesne projekty architektur energetycznych traktują to rozporządzenie jako punkt wyjścia, integrując mikrosieci zdolne do przejęcia znacznej większości lub wręcz całości obciążeń obiektu poprzez wyspową współpracę jednostek CHP i magazynów energii. Taka topologia nie tylko realizuje wymogi prawne, ale przekształca zasilanie z pasywnego centrum kosztowego w aktywny węzeł efektywności energetycznej. 

### **Infrastruktura Krytyczna państwa a Zarządzanie Kryzysowe** 

Szpitale pełnią fundamentalną rolę w systemie ratowniczym i bezpieczeństwie publicznym, co znajduje swoje odzwierciedlenie w Ustawie z dnia 26 kwietnia 2007 r. o zarządzaniu kryzysowym (tekst jednolity Dz.U. 2026 poz. 574)<sup>9</sup> . Ustawa ta definiuje w art. 3 infrastrukturę krytyczną (IK) jako systemy oraz wchodzące w ich skład powiązane ze sobą funkcjonalnie obiekty, urządzenia, instalacje i usługi, które są kluczowe dla bezpieczeństwa państwa i jego obywateli<sup>9</sup> . W katalogu tym wprost wyszczególniono systemy ochrony zdrowia, ratownicze oraz zaopatrzenia w energię<sup>16</sup> . 

Rozpoznanie infrastruktury szpitalnej jako elementu IK przenosi projektowanie systemów energetycznych z domeny wyłącznie elektrotechnicznej w sferę bezpieczeństwa narodowego. Wymusza to uwzględnienie w projektach tzw. map ryzyka i analiz zagrożeń, w tym zjawisk pogodowych, powodzi, katastrof budowlanych oraz ataków terrorystycznych i cybernetycznych<sup>10</sup> . Inżynier systemu musi zatem projektować mikrosieć w sposób umożliwiający jej separację (zarówno galwaniczną, jak i informatyczną) od zewnętrznych perturbacji, zapewniając zdolność do autonomicznej pracy w warunkach ekstremalnego izolowania, tzw. _islanding_ . 

### **Narodowy Program Ochrony Infrastruktury Krytycznej i Analizy BIA/BCP** 

Mechanizmy wykonawcze do wyżej wymienionej ustawy precyzują wytyczne Rządowego Centrum Bezpieczeństwa (RCB), zebrane w Narodowym Programie Ochrony Infrastruktury Krytycznej (NPOIK)<sup>18</sup> . Z technicznego punktu widzenia, kluczowym mechanizmem narzuconym przez RCB jest konieczność stworzenia i implementacji Planów Ciągłości Działania (Business Continuity Planning - BCP) opartych na pogłębionej Analizie Wpływu na Biznes (Business Impact Analysis - BIA)<sup>22</sup> . 

Z perspektywy projektowania zasilania gwarantowanego, analiza BIA stanowi absolutny fundament wymiarowania parametrów systemu. Wymusza ona na zarządcach obiektów wyznaczenie dla każdego procesu medycznego wskaźników krytycznych, takich jak RTO (Recovery Time Objective – docelowy, maksymalny czas przywrócenia zasilania) oraz MTPD (Maximum Tolerable Period of Disruption – maksymalny tolerowany okres przestoju)<sup>22</sup> . Wartości te bezpośrednio korelują ze standardami technicznymi: jeśli dla stołu operacyjnego analiza BIA wskaże RTO na poziomie 0 sekund (brak tolerancji na przerwę), wymusza to zastosowanie zasilaczy UPS w topologii VFI (Voltage and Frequency Independent) i lokalnych magazynów energii. Dokumenty strategiczne RCB podkreślają ponadto wagę redundancji krytycznych układów. Wytyczne zalecają powielanie systemów łączności, rozbudowę niezależnych przyłączy, a także dywersyfikację źródeł (np. połączenie fotowoltaiki, kogeneracji gazowej i agregatów Diesla), by zapobiec zjawisku pojedynczego punktu awarii (Single Point of Failure)<sup>22</sup> . 

Rozporządzenia i akty planistyczne stanowią zatem spójny ekosystem wymuszający na inżynierach odejście od prostych kalkulacji sumy mocy na rzecz wdrożenia zintegrowanych, dynamicznych i w pełni odpornych na zakłócenia systemów zarządzania energią. 

|**Lp.**|**Tytuł**<br>**Dokumentu /**<br>**Aktu**<br>**Prawnego**|**Sygnatura /**<br>**Numer**|**Typ**<br>**Dokumentu**|**Bezpośredni**<br>**Link do**<br>**Systemu /**<br>**Pliku (Polska)**|
|---|---|---|---|---|
|1.|Rozporządzeni<br>e Ministra<br>Zdrowia z dnia<br>26 marca 2019<br>r. w sprawie<br>szczegółowyc<br>h wymagań,<br>jakim powinny<br>odpowiadać<br>pomieszczenia|Dz.U. 2019 poz.<br>595 (t.j. Dz.U.<br>2022 poz. 402)|Akt prawny<br>(Ustawa/Rozpo<br>rządzenie)|ISAP Dz.U.<br>2019 poz. 595|



||i urządzenia<br>podmiotu<br>wykonującego<br>działalność<br>leczniczą||||
|---|---|---|---|---|
|2.|Ustawa z dnia<br>26 kwietnia<br>2007 r. o<br>zarządzaniu<br>kryzysowym<br>(Defnicja<br>Infrastruktury<br>Krytycznej i<br>plany<br>zarządzania)|Dz.U. 2007 nr<br>89 poz. 590 (t.j.<br>Dz.U. 2026<br>poz. 574)|Akt prawny<br>(Ustawa)|ISAP Dz.U.<br>2007 nr 89<br>poz. 590|
|3.|Narodowy<br>Program<br>Ochrony<br>Infrastruktury<br>Krytycznej<br>(NPOIK) -<br>Dokument<br>Główny|Uchwała Rady<br>Ministrów<br>(wytyczne<br>RCB)|Dokument<br>Rządowy /<br>Wytyczne<br>Strategiczne|RCB NPOIK<br>(PDF)|
|4.|Standardy<br>służące<br>zapewnieniu<br>sprawnego<br>funkcjonowani<br>a infrastruktury<br>krytycznej –<br>dobre praktyki<br>i<br>rekomendacje<br>(Załącznik nr 1)|Załącznik do<br>NPOIK (RCB)|Dokument<br>Rządowy /<br>Przewodnik<br>(BCP/BIA)|RCB Standardy<br>IK (PDF)|



## **Kategoria 2: Normatywne Aspekty Projektowania i Integracji (Normy Techniczne Polska/UE)** 

Implementacja wytycznych prawnych w realnym środowisku inżynieryjnym nie byłaby możliwa bez rygorystycznego aparatu normalizacyjnego. W architekturach, gdzie błąd obliczeniowy może bezpośrednio kosztować ludzkie życie, normy elektrotechniczne IEC (International Electrotechnical Commission) oraz ich lokalne adaptacje (PN-HD, EN) stanowią absolutne ramy dla projektowania instalacji, zapewnienia kompatybilności elektromagnetycznej, zabezpieczeń przeciwpożarowych oraz strategii automatyki przełączającej w stanach awaryjnych. **Zasilanie Obiektów Medycznych (IEC 60364-7-710) i Specyfika Sieci** 

### **IT** 

Centralną osią projektowania zasilania dla służby zdrowia jest międzynarodowa norma **IEC 60364-7-710** (zharmonizowana w Polsce jako PN-HD 60364-7-710), dotycząca wymagań specjalnych dla instalacji w pomieszczeniach medycznych<sup>26</sup> . Norma ta dokonuje kategoryzacji obszarów szpitalnych na podstawie ryzyka związanego z przerwą w dostawie prądu, dzieląc je na Grupę 0 (brak części aplikacyjnych, np. sale zabiegowe bez zaawansowanego sprzętu), Grupę 1 (procedury nie zagrażające życiu w przypadku zaniku) oraz Grupę 2 (np. bloki operacyjne, sale intensywnej terapii, oddziały kardiochirurgii), w których przerwa w zasilaniu może doprowadzić do utraty funkcji życiowych pacjenta<sup>29</sup> . Z medycznego punktu widzenia, obniżenie rezystancji skóry pacjenta podczas zabiegów chirurgicznych sprawia, że prądy upływowe rzędu zaledwie ułamków miliamperów mogą wywołać defibrylację serca. Z tego powodu dla Grupy 2 norma nakazuje stosowanie sieci izolowanej IT (tzw. medycznej sieci IT) wspomaganej stałym monitorowaniem stanu izolacji<sup>31</sup> . Porażenie w układzie IT przy pierwszym zwarciu doziemnym (tzw. ) nie wyzwala natychmiastowego wyłączenia aparatury _first fault_ ratującej życie, co ma krytyczne znaczenie dla powodzenia operacji i daje personelowi czas na bezpieczne dokończenie procedur. 

Wymiarowanie mikrosieci dla szpitali silnie opiera się również na wytycznych normatywnych definiujących klasy przerw zasilania (restytucji) w obwodach o krytycznym znaczeniu, co jest dogłębnie opisane w materiałach i poradnikach wiodących producentów układów zasilania, takich jak Eaton, Schneider Electric czy Bender<sup>28</sup> . Klasyfikacja przerw przedstawia się następująco: 



- **Klasa 0,5 s (Klasa 0.5):** Obwody bezprzerwowe. Restytucja energii musi nastąpić w czasie nie dłuższym niż pół sekundy. Dotyczy m.in. oświetlenia stołów operacyjnych oraz systemów podtrzymywania życia i aparatury do krążenia pozaustrojowego. Rolę źródła dla tej klasy muszą przejąć urządzenia UPS na bazie baterii lub szybko reagujące magazyny BESS typu _online_ . Przewodniki projektowe narzucają w tej klasie również wymóg zapewnienia podtrzymania przez absolutne minimum 60 minut w przypadku całkowitej awarii sieci zewnętrznej oraz jednoczesnego braku wsparcia z agregatów<sup>28</sup> . 



- **Klasa 15 s (Klasa 15):** Czas dopuszczalny na pełen rozruch i przejęcie obciążenia przez scentralizowany agregat prądotwórczy (generator Diesla). Obejmuje m.in. zasilanie systemów gazów medycznych, wentylację nadciśnieniową w strefach czystych, oświetlenie dróg ewakuacyjnych oraz windy ratownicze<sup>27</sup> . 

- **Klasa > 15 s:** Obwody i systemy ogólne, np. sterylizatornie ogólne, klimatyzacja stref pobytu dziennego czy urządzenia socjalne pacjentów, których wyłączenie nie ma katastrofalnego skutku. 

W systemach mikrosieciowych integracja układów CHP, paneli PV oraz baterii BESS powoduje głębokie zmiany w podejściu do tych restrykcyjnych klasyfikacji. Ponieważ uruchomienie masywnej turbiny gazowej (CHP) z reguły trwa kilkadziesiąt sekund do minut, mikrosieć wykorzystuje inwertery magazynów energii w trybie formowania sieci ( _Grid-Forming_ ) do utrzymywania ciągłości zasilania, bezproblemowo spełniając normę klasy 0.5s<sup>28</sup> . 

### **Systemy Zasilania Gwarantowanego (IEC 62040) i Magazyny BESS (IEC 62933)** 

Projektowanie komponentów aktywnych w mikrosieci wymaga wzięcia pod uwagę wieloczęściowych norm produktowych. Konwencjonalne układy UPS podlegają serii norm **IEC 62040** , definiującej zarówno ogólne rygory bezpieczeństwa pożarowego (Część 1), wymagania kompatybilności elektromagnetycznej (Część 2), jak i metodykę certyfikowania wydajności, efektywności oraz dynamiki przełączania zasilaczy (Część 3)<sup>35</sup> . 

Znacznie szerszym i bardziej współczesnym dokumentem jest powoli stabilizująca się norma **IEC 62933** , obejmująca wielkoskalowe zintegrowane systemy magazynowania energii elektrycznej (EES/BESS)<sup>40</sup> . Kluczową pozycją dla szpitali jest IEC 62933-5-2 (bezpieczeństwo systemów elektrochemicznych połączonych z siecią) regulująca aspekty powstrzymywania lawinowego wzrostu temperatury w ogniwach bateryjnych (tzw. _Thermal Runaway_ )<sup>38</sup> . Zważywszy, że współczesne układy litowo-jonowe cechują się ogromną gęstością magazynowania przy pewnej wrażliwości cieplnej, norma wymusza instalację zaawansowanych algorytmów zarządzania BMS (Battery Management System), odpowiednich stref izolacji przeciwpożarowej i ochrony przed wybuchem w przypadku zastosowania ich np. na dachach placówek medycznych. Nowy standard IEC 62933-4-3 z 2025 roku dodaje uwarunkowania środowiskowe i klimatyczne, istotne w planowaniu odporności w warunkach katastrof naturalnych<sup>40</sup> . 

### **Wymagania Ochronne dla Fotowoltaiki (PN-HD 60364-7-712)** 

Aby zasilić szpital w ujęciu holistycznym i zwiększyć jego samodzielność energetyczną, konieczna jest integracja OZE. Dla układów fotowoltaicznych ramy narzuca zaktualizowana norma **PN-HD 60364-7-712** dotycząca obwodów i zasilania z paneli PV<sup>44</sup> . Oprócz podstawowych metod wymiarowania przewodów w stronę prądu stałego (DC), norma nakłada restrykcyjne procedury w obszarze ochrony odgromowej oraz stosowania ograniczników przepięć (SPD). Co niezmiernie istotne, norma ta wymaga traktowania 

generatora fotowoltaicznego jako systemu stale znajdującego się pod napięciem w warunkach oświetlenia (nawet przy odciętym falowniku). Rodzi to poważne wyzwania w procedurach bezpieczeństwa straży pożarnej w obiektach wielkopowierzchniowych, wymuszając implementację lokalnych rozłączników ppoż. obniżających napięcie z poziomu stringów<sup>44</sup> . 

|**Lp.**|**Sygnatura**<br>**Normy**|**Angielski**<br>**Tytuł**<br>**(Oryginalny)**|**Krótki Opis w**<br>**Kontekście**<br>**Szpitalnym**|**Linki**<br>**(Metadane/Pr**<br>**zewodniki**<br>**Inżynierskie**<br>**producentów)**|
|---|---|---|---|---|
|1.|**IEC 60364-7-**<br>**710**<br>(PN-HD<br>60364-7-710)|_Low-voltage_<br>_electrical_<br>_installations -_<br>_Part 7-710:_<br>_Requirements_<br>_for special_<br>_installations or_<br>_locations -_<br>_Medical_<br>_locations_|Klasyfkacja<br>przerw (0,5 s;<br>15 s) oraz<br>defniowanie<br>izolowanych<br>obwodów<br>medycznych<br>(układy IT),<br>niezbędna w<br>podziale<br>zasilania<br>krytycznego i<br>priorytetyzacji<br>obciążeń<br>wyspowych.|Przewodnik<br>EATON:<br>Healthcare<br>Critical Power<br>Design (PDF)|
|2.|**IEC 62040-3**<br>(EN IEC<br>62040-3:2021)|_Uninterruptibl_<br>_e power_<br>_systems (UPS)_<br>_- Part 3:_<br>_Method of_<br>_specifying the_<br>_performance_<br>_and test_<br>_requirements_|Określanie<br>wydajności,<br>testów zjawisk<br>przejściowych i<br>dynamiki<br>transferu<br>zasilaczy<br>podtrzymujący<br>ch np.<br>diagnostykę i<br>OIOM.|Baza<br>standardów<br>BSI/CENELEC<br>(Podgląd<br>metadanych)|



|3.|**IEC 62933-5-2**<br>(oraz IEC<br>62933-4-3)|_Electrical_<br>_energy_<br>_storage (EES)_<br>_systems - Part_<br>_5-2: Safety_<br>_requirements_<br>_for grid-_<br>_integrated EES_<br>_systems -_<br>_Electrochemic_<br>_al-based_<br>_systems_|Normy dla<br>megawatowyc<br>h magazynów<br>BESS<br>integrowanych<br>z układem<br>kogeneracji.<br>Wymogi<br>bezpieczeństw<br>a bateryjnego i<br>ochrony przed<br>lawiną<br>termiczną.|Lista i<br>kategoryzacja<br>norm IEC<br>62933 EES (IEC<br>Webstore)|
|---|---|---|---|---|
|4.|**PN-HD**<br>**60364-7-712**|_Low-voltage_<br>_electrical_<br>_installations -_<br>_Part 7-712:_<br>_Solar_<br>_photovoltaic_<br>_(PV) power_<br>_supply_<br>_systems_|Zasady<br>ochrony<br>przeciwporaże<br>niowej,<br>odgromowej<br>oraz<br>projektowania<br>okablowania<br>dla<br>zintegrowanyc<br>h systemów PV<br>na budynkach<br>medycznych.|PKN (Katalog i<br>wykaz norm<br>wycofanych/ak<br>tywnych)|



## **Kategoria 3: Literatura Naukowa i Techniczna (Open Access 2021-2026)** 

Światowa literatura naukowa z ostatnich lat koncentruje się na odejściu od pasywnego systemu zasilania awaryjnego na rzecz inteligentnych, zoptymalizowanych ekonomicznie i proaktywnych energetycznie architektur w postaci mikrosieci wyspowych<sup>48</sup> . W świetle badawczym klasyczne systemy oparte o generator z silnikiem Diesla postrzegane są jako archaiczne. Chociaż charakteryzują się one dużą gęstością mocy, ich wysoka emisyjność, zależność od zawodnych logistycznie łańcuchów dostaw paliwa oraz nieadekwatna dynamika rozruchu skłania inżynierów do koncepcji ukierunkowanych na odporność krzyżową ( _crosssector resilience_ ) obejmującą hybrydowe zasilanie ze źródeł OZE, kogeneracji (CHP) z paliw 

##### niskoemisyjnych i wreszcie buforowych magazynów energii<sup>48</sup> . 

### **Hybrydyzacja, Resilience i Tryb Wyspowy** 

Koncept odporności – _Resilience_ – przewija się w niemal każdej nowszej publikacji, zastępując tradycyjne pojęcie niezawodności ( _Reliability_ ). Jak wykazują autorzy opracowań, niezawodność to zdolność dostarczania mocy w warunkach standardowych ujęta modelami 

prawdopodobieństwa awarii, podczas gdy odporność skupia się na przetrwaniu, działaniu w stanach skrajnego obciążenia i szybkiej restytucji po wystąpieniu zjawisk niszczycielskich uderzających we wszystko (tzw. zjawiska HILP – _High-Impact, Low-Probability_ )<sup>49</sup> . Przykładem takiej rewolucji jest łączenie systemów kogeneracyjnych z wielkoskalowymi magazynami energii. Tradycyjna jednostka CHP oparta np. na mikroturbinie gazowej napotyka na poważny problem wydajnościowy: aby uniknąć strat eksploatacyjnych, obniżenia żywotności, korozji oraz wysokiej emisyjności wynikającej z niepełnego spalania, silnik ten nie może pracować na niskich i często oscylujących mocach zrzutowych. Oznacza to, że zrzuty lub spadki obciążeń nocnych w szpitalach prowadziły w przeszłości do marnotrawstwa paliwa lub eksportu taniej energii do sieci zewnętrznej. Zastosowanie BESS rozwiązuje ten problem całkowicie: układ magazynujący stabilizuje krzywą poboru – turbina CHP wytwarza stałą, nominalną (wysokoefektywną) moc, podczas gdy BESS przyjmuje lub oddaje nagłe impulsy mocy ze strony sieci obiektowej<sup>53</sup> . 

Kolejnym kluczowym elementem nowożytnej infrastruktury jest nadrzędny system sterowania – EMS (Energy Management System). Zaawansowane algorytmy zarządzania bazujące np. na Inteligencji Maszynowej (ML), modelowaniu predykcyjnym czy algorytmach ewolucyjnych Roju Cząstek (Particle Swarm Optimization - PSO) przejmują sterowanie mikrosiecią<sup>56</sup> . 

Odpowiednie, stochastyczne algorytmy dbają by SoC (State of Charge – stopień naładowania) baterii gwarantował ciągłe pokrycie rezerwowego zapotrzebowania dyktowanego przez krzywą obciążeń szpitalnych, a zarazem dokonywał aktywnego ucinania szczytów z poboru zewnętrznego ( _Peak Shaving_ )<sup>59</sup> . To dzięki takim algorytmom inwestycja z pasywnego bezpiecznika medycznego staje się ekonomicznie samofinansującym się wehikułem, redukującym nakłady placówki na rachunki prądowe w taryfach zmiennych<sup>59</sup> . 

Co do zasady układ inwerterów podtrzymujących w mikrosieciach wyposażony jest w sterowanie hierarchiczne (na poziomie podstawowym, wtórnym i wyższym), które dba o automatyczną regulację dryftu napięcia i częstotliwości. Przy przejściu w tryb wyspowy inwertery BESS przejmują rolę "Grid-Forming" (tworzących sztuczną bezwładność sieciową i narzucających sinusową falę napięcia), dając reszcie systemu czas na uruchomienie i zsynchronizowanie agregatów zapasowych i obwodów priorytetowych<sup>34</sup> . 

|**Lp.**|**Autorzy (Rok)**|**Tytuł**|**Główny**|**Bezpośredni**|
|---|---|---|---|---|
|||**Artykułu /**|**Wniosek**|**Link do**|
|||**Czasopismo**|**Badawczy (1**|**Publikacji**|



||**Naukowe**|**zdanie)**|**(DOI / PDF**<br>**Open Access)**|
|---|---|---|---|
|1.<br>**Eyimaya, S.E.**<br>**et al. (2026)**|_Design of_<br>_Microgrid-_<br>_Based_<br>_Resilience_<br>_Solutions to_<br>_Improve Public_<br>_Health_<br>_Impacts of_<br>_Earthquake-_<br>_Induced_<br>_Power_<br>_Outages_<br>(MDPI<br>Sustainability)|Hybrydowe<br>mikrosieci<br>integrujące<br>słoneczną<br>produkcję PV,<br>bufory<br>bateryjne i<br>priorytetowe<br>odrzucanie<br>obciążeń,<br>podnoszą<br>wskaźnik<br>ciągłości<br>krytycznych<br>usług w<br>ekstremalnym<br>zaciemnieniu z<br>48% (tylko<br>diesel) do<br>niemal 87%,<br>obniżając<br>ryzyko<br>wyczerpania<br>zapasów<br>paliw.<sup>48</sup>|htps://<br>doi.org/<br>10.3390/<br>su18052552|
|2.<br>**Tenti, F. et al.**<br>**(2026)**|_Microgrid_<br>_Architecture_<br>_and Control:_<br>_Resilience_<br>_Evaluation_<br>_under Cyber-_<br>_Physical_<br>_Disturbances_<br>(MDPI|Implementacja<br>zdecentralizow<br>anego,<br>hierarchiczneg<br>o sterowania w<br>inwerterach<br>formujących<br>sieć (Grid-<br>Forming)<br>kompensuje|htps://<br>doi.org/<br>10.3390/<br>en19010148|



||Energies)|utratę<br>naturalnej<br>bezwładności<br>generatorów<br>synchroniczny<br>ch,<br>umożliwiając<br>łagodne i<br>bezpieczne<br>przejście<br>obiektu w tryb<br>pracy<br>wyspowej<br>(islanding).<sup>34</sup>||
|---|---|---|---|
|3.<br>**Santos, C. et**<br>**al. (2023)**|_Microgrids_<br>_with Batery_<br>_Energy_<br>_Storage_<br>_Systems_<br>_(BESS) paired_<br>_with_<br>_photovoltaic_<br>_systems (PV)_<br>_for reliable_<br>_auxiliary_<br>_power..._<br>(MDPI<br>Energies)|BESS<br>operujące w<br>roli nadrzędnej<br>("master") w<br>mikrosieci są w<br>stanie<br>precyzyjnie<br>zapewnić<br>rygorystyczne<br>podtrzymanie<br>obciążeń<br>pomocniczych<br>przez<br>minimum 12<br>godzin, co<br>minimalizuje<br>zapady<br>napięcia<br>niezgodne z<br>wymogami<br>zakładu<br>dystrybucji<br>zasilania.<sup>63</sup>|htps://<br>doi.org/<br>10.3390/<br>en16021012|
|4.<br>**Yilmaz, M. et**|_Optimal Sizing_|Algorytm Roju|htps://|



|**al. (2022)**|_of BESS and_<br>_PV in a Grid-_<br>_Connected_<br>_Microgrid via_<br>_Particle Swarm_<br>_Optimization..._<br>(MDPI Applied<br>Sciences)|Cząstek (PSO)<br>wykorzystany<br>do<br>równoległego<br>wymiarowania<br>baterii i paneli<br>solarnych<br>skutecznie<br>minimalizuje<br>kapitałowy<br>koszt systemu<br>i zapobiega<br>niefortunnemu<br>przewymiarow<br>aniu<br>pojemności<br>akumulatorów<br>dla obciążeń w<br>stanach<br>krytycznych.<sup>56</sup>|doi.org/<br>10.3390/<br>app12168247|
|---|---|---|---|
|5.<br>**Khan, A. et al.**<br>**(2025)**|_Economic_<br>_dispatch of_<br>_BESS in MG-_<br>_integrated_<br>_distribution_<br>_networks..._<br>(MDPI<br>Energies)|Model<br>ekonomiczneg<br>o<br>dysponowania<br>bateriami w<br>połączonych<br>mikrosieciach<br>udowadnia, że<br>operacyjne<br>wykorzystanie<br>BESS do<br>niwelowania<br>skoków<br>szczytowych<br>(_peak shaving_)<br>skutecznie<br>obniża<br>całkowity<br>koszt zakupu|htps://<br>doi.org/<br>10.3390/<br>en18236335|



|||energii i<br>opóźnia<br>degradację<br>żywotności<br>zestawów<br>ogniw.<sup>59</sup>||
|---|---|---|---|
|6.<br>**Smith, J. et al.**<br>**(2023)**|_Optimization_<br>_of Combined_<br>_Heat and_<br>_Power (CHP)_<br>_Dispatch with_<br>_BESS in_<br>_Microgrids_<br>(MDPI<br>Energies)|Aby uniknąć<br>poważnych<br>spadków<br>efektywności i<br>silnej<br>emisyjności<br>węglowej z<br>jednostek CHP<br>przy zrzucie<br>obciążeń<br>(praca <50%),<br>wymagana jest<br>wirtualna<br>kompensacja<br>magazynami<br>BESS, która<br>ładuje moduły<br>z nadmiarowej<br>generacji i<br>zapobiega<br>eksportowi<br>taniej energii.<sup>53</sup>|htps://<br>doi.org/<br>10.3390/<br>en16031274|
|7.<br>**Rahman, Z. et**<br>**al. (2024)**|_Enhancing_<br>_Grid-_<br>_Connected_<br>_Microgrid_<br>_Resilience_<br>_through_<br>_Advanced_<br>_Forecasting_<br>_and ML_|Integracja<br>technik<br>maszynowego<br>uczenia<br>predykcyjnego<br>(ML) do<br>zunifkowaneg<br>o systemu<br>prognozująceg<br>o produkcję|htps://<br>doi.org/<br>10.3390/<br>en16217300|





(MDPI OZE poprawiła Energies) przewidywalno ść dostaw prądu, skracając czas uśpienia krytycznych obciążeń wyspowych o ponad 25%.<sup>57</sup> 



## **Zaawansowana Synteza Projektowa – Wnioski Translacyjne** 

Powyższy obszerny zestaw materiałów dowodzi nierozerwalnego splotu pomiędzy wymaganiami prawa, norm i technologii operacyjnych. Przeprowadzenie analizy zintegrowanej skłania do wyciągnięcia wielopłaszczyznowych wniosków koncepcyjnych z drugiego i trzeciego rzędu (Second/Third-Order Insights), które bezpośrednio profilują kształt prawidłowo napisanej rozprawy i modelu inżynierskiego: 

### **Paradoks Minimum Ustawowego a Zdolności Kineto-Dynamicznych** 

Zdefiniowanie przez organy państwowe poziomu rezerwy na poziomie co najmniej 30% zapotrzebowania szczytowego agregatem autostartowym okazuje się dzisiaj zaledwie wektorem przetrwania obiektów starych technologicznie<sup>1</sup> . Jak wskazują normy instalacyjne (m.in. IEC 60364-7-710 dla pomieszczeń z Grupy 2), aparatury te mogą wymagać zasilania klasy 0.5 sekundy<sup>28</sup> . Typowy, masywny agregat z turbiną spalinową, z powodu swojej gigantycznej bezwładności rotacyjnej, nie jest w stanie uruchomić się i dostarczyć napięcia z wymaganą dla elektroniki dokładnością w czasie krótszym niż kilkanaście sekund. Stwarza to konieczność użycia pomostowego BESS. Inżynier w projektowanej mikrosieci nie tylko łata "dziurę 15-sekundową", ale dzięki pojemności BESS zdolnej do uwalniania zmagazynowanej energii przy skokowym obciążeniu (inrush), odciąża mechaniczne turbiny CHP i Diesla przed dławieniem. Pozwala to na bardziej racjonalne (współczynnikowo mniejsze i tańsze) przewymiarowanie (sizing) samego zespołu prądotwórczego<sup>28</sup> . 

### **Transpozycja Wskaźników BIA na Strukturę Kontrolną Mikrosieci** 

Istnieje uderzająca i systemowa asocjacja pomiędzy sferą zarządczą z NPOIK a fizyką sieciową. Analiza Wpływu na Biznes (BIA), powszechnie stosowana przez działy zarządzania kryzysowego w ramach Planów Ciągłości Działania (BCP), bezpośrednio wnika w ustrój algorytmów systemu zarządzania EMS. Architektura kontrolna w mikrosieci nie optymalizuje bowiem wyłącznie profilu kosztowego z rynków giełdowych; głównym więzłem jest to, że 

nadrzędne wartości z modelu BIA – czyli MTPD (maksymalne przestoje), RTO oraz mapy ryzyk powodziowych/terrorystycznych<sup>22</sup> – są programowane w oprogramowaniu SCADA jako twarde limity algorytmiczne. W rezultacie magazyny energii utrzymują tzw. nienaruszalny próg SoC (często nie poniżej np. 40-50%), który gwarantuje, że zapas prądu zapewni zasilanie najczulszym salom do czasu napraw awarii zewnętrznych z mapy uwarunkowań kryzysowych, pozostawiając resztę pojemności operacyjnej na dobowy arbitraż cen i Peak Shaving<sup>59</sup> . Zgromadzona, poszerzona baza wiedzy ukazuje bezdyskusyjnie, że innowacyjne układy wspierające szpitale nie stoją już w opozycji do twardych regulacji ustawowych oraz normalizacyjnych. Współczesny ekosystem prawny celowo pozostawia konstruktorom szeroką swobodę (normatywne minima), otwierając inżynieriom medycznym drogę do tworzenia układów wysoce sprężystych, wieloźródłowych i chronionych sztuczną inteligencją dyspozytorską, definiując bezpieczeństwo nowej dekady. 

#### **Джерела** 

1. § 30. - Szczegółowe wymagania, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu leczniczego dla osób pozbawionych... - Dz.U.2024.1441 t.j. - - - - - 

OpenLEX, htps://sip.lex.pl/akty <u>prawne/dzu dziennik ustaw/szczegolowe</u> - - - - - - - 

<u>wymagania jakim powinny odpowiadac pomieszczenia i 17898249/par 30</u> 

2. Nadzór podmiotów leczniczych - Powiatowa Stacja Sanitarno-Epidemiologiczna - - 

w Chrzanowie - Portal Gov.pl, htps://www.gov.pl/web/psse <u>chrzanow/nadzor</u> - 

<u>podmiotow leczniczych</u> 

3. Status prawny Szpitala - BIP Szpital Karowa - Szpital Kliniczny im ks. Anny - - 

Mazowieckiej, htps://bip.szpitalkarowa.pl/status <u>prawny szpitala</u> 

4. Rozporządzenie Ministra Zdrowia z dnia 26 marca 2019 r. w sprawie szczegółowych wymagań, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą (tekst jedn.: Dz.U. z 2022 r., poz. 402) - Serwis ZOZ, <u>htps://serwiszoz.pl/dzialalnosc-lecznicza/rozporzadzenie-ministra-zdrowia-zdnia-26-marca-2019-r.-w-sprawie-szczegolowych-wymagan-jakim-powinny-</u> - - - - - - - 

<u>odpowiadac pomieszczenia i urzadzenia podmiotu wykonujacego dzialalnosc lecznicza-tekst-jedn.-dz.u.-z-2022-r.-poz.-402-4581.html</u> 

5. Rozporządzenie Ministra Zdrowia z dnia 26 marca 2019 r. w sprawie szczegółowych wymagań, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą - ELI - European <u>htps://eli.gov.pl/eli/DU/2019/595/ogl</u> 

6. Legislation Identifier, 41. - Szczegółowe wymagania jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą. - Dz.U.2012.739 - LEX, - - - - - 

<u>htps://sip.lex.pl/akty prawne/dzu dziennik ustaw/szczegolowe wymagania</u> - - - - - - 

<u>jakim powinny odpowiadac pomieszczenia i 17894616/par 41</u> 

7. Szczegółowe wymagania, jakim powinny odpowiadać pomieszczenia i urządzenia podmiotu wykonującego działalność leczniczą. - Dz.U.2022.402 t.j. - 

- - - - ustawy, htps://sip.lex.pl/akty <u>prawne/dzu dziennik ustaw/szczegolowe</u> - - - - - - <u>wymagania jakim powinny odpowiadac pomieszczenia i 18834203</u> 

8. Wymagania sanitarno – higieniczne dla podmiotów wykonujących działalność - - - - 

leczniczą - Gov.pl, htps://www.gov.pl/atachment/302ac505 <u>0127 42f4 b754 b43fe806515c</u> 

9. Zarządzanie kryzysowe. - Dz.U.2026.574 t.j. - OpenLEX - ustawy, - - - - 

<u>htps://sip.lex.pl/akty prawne/dzu dziennik ustaw/zarzadzanie</u> - 

- 

- <u>kryzysowe 17348453</u> - 

- 10. Art. 5. - Ustawa o zarządzaniu kryzysowym - LexLege, htps://lexlege.pl/ustawa <u>o-zarzadzaniu-kryzysowym/art-5/</u> 

11. [Pojęcie zarządzania kryzysowego] - Art. 2. - Zarządzanie kryzysowe. - Dz.U.2026.574 t.j., - - - - 

<u>htps://sip.lex.pl/akty prawne/dzu dziennik ustaw/zarzadzanie</u> - - 

<u>kryzysowe 17348453/art 2</u> 

12. [Zadania Centrum] - Art. 11. - Zarządzanie kryzysowe. - Dz.U.2026.574 t.j. - - - - - 

ustawy, htps://sip.lex.pl/akty <u>prawne/dzu dziennik ustaw/zarzadzanie</u> - - 

<u>kryzysowe 17348453/art 11</u> 

13. [Definicje] - Art. 3. - Zarządzanie kryzysowe. - Dz.U.2026.574 t.j. - ustawy, htps://sip.lex.pl/akty-prawne/dzu-dziennik-ustaw/zarzadzanie- - 

<u>kryzysowe 17348453/art 3</u> 

14. Opublikowano tekst jednolity ustawy o zarządzaniu kryzysowym (dokument), - - - - 

<u>htps://samorzad.pap.pl/kategoria/prawo/opublikowano tekst jednolity ustawy o-zarzadzaniu-kryzysowym-dokument</u> - 

15. Art. 3. - Ustawa o zarządzaniu kryzysowym - LexLege, htps://lexlege.pl/ustawa <u>o-zarzadzaniu-kryzysowym/art-3/</u> 

16. Infrastruktura krytyczna – ochrona infrastruktury krytycznej - Energetyka.plus, - - - - 

<u>htps://www.energetyka.plus/infrastruktura krytyczna ochrona infrastruktury krytycznej/</u> 

17. Plany zarządzania kryzysowego w Polsce: kto je tworzy, co zawierają. Czym jest infrastruktura krytyczna? - Forsal, - - 

<u>htps://forsal.pl/kraj/bezpieczenstwo/artykuly/11215574,plany zarzadzania kryzysowego-w-polsce-kto-je-tworzy-co-zawieraja-czym-jest-infrastrukturakrytyczna.html</u> 

18. Narodowy Program Ochrony Infrastruktury Krytycznej - Rządowe Centrum - 

Bezpieczeństwa - Portal Gov.pl, htps://www.gov.pl/web/rcb/narodowy - - - 

<u>program ochrony infrastruktury krytycznej</u> 

19. Narodowy Program Ochrony Infrastruktury Krytycznej - Gov.pl, - - - - 

<u>htps://www.gov.pl/atachment/ee334990 ec9c 42ab ae12 477608d94eb1</u> 

20. ORGANY I PODMIOTY UCZESTNICZĄCE W OCHRONIE INFRASTRUKTURY KRYTYCZNEJ, ICH ROLA I ODPOWIEDZIALNOŚĆ, - 

<u>htps://archiwalna.wsge.edu.pl/wp content/uploads/Projekty/EFS/ORGANY_POD MIOTY_UCZESTNICZACE_OCHRONIE_INFRASTRUKTURY_KRYTYCZNEJ.pdf</u> 

21. Narodowy Program Ochrony Infrastruktury Krytycznej 2018 w kształtowaniu 

bezpieczeństwa Rzeczypospolitej Polskiej, - - - <u>htps://vistula.edu.pl/wp content/uploads/2022/02/103 brocki artykua.pdf</u> - 22. Jak wdrożyć KSC / NIS2– ciągłość działania - ODO 24, htps://odo24.pl/blog - - - - <u>post.jak wdrozyc nis2 ciaglosc dzialania</u> 

23. Analiza BIA i ciągłość działania w bankach spółdzielczych – praktyczne podejście Servus Comp - Premium Bank, - - - - - 

<u>htps://premiumbank.zadbajobezpieczenstwo.pl/analiza bia i ciaglosc dzialania w-bankach-spoldzielczych-praktyczne-podejscie-servus-comp/</u> 

24. Narodowy Program Ochrony Infrastruktury Krytycznej - Rządowe Centrum Bezpieczeństwa, <u>htps://archiwum.rcb.gov.pl/wp-content/uploads/Za%C5%82%C4%85cznik-nr-1-</u> - - - - 

<u>Standardy s%C5%82u%C5%BC%C4%85ce zapewnieniu sprawnego</u> - - - - - - - 

<u>funkcjonowania infrastruktury krytycznej %E2%80%93 dobre praktyki i rekomendacje.pdf</u> 

25. KOMPLEKSOWE PODEJŚCIE DO WYŁANIANIA I OCHRONY INFRASTRUKTURY KRYTYCZNEJ - Kwartalnik Policyjny, <u>htps://kwartalnik.csp.edu.pl/download/21/28036/Kompleksowepodejsciedowylan ianiaiochronyinfrastrukturykrytycznejWitoldSkomra.pdf</u> 

26. Komunikat on-line - Polski Komitet Normalizacyjny, - 

<u>htps://www.pkn.pl/komunikat online</u> 

27. Reference design guide: Critical power for healthcare | EATON, - 

<u>htps://www.eaton.com/content/dam/eaton/markets/buildings/reference</u> - - - - - - - - 

<u>design/eaton guide reference design healthcare critical power en us.pdf</u> 

28. Poradnik projektowy: Zasilanie krytyczne obiektów medycznych - Eaton, - 

<u>htps://www.eaton.com/content/dam/eaton/markets/buildings/pl/consulting</u> - - - - - - - 

<u>application guide /eaton guide reference design healthcare pl.pdf</u> 

29. Safety According To Iec 60364-7-710.2002-11 | PDF | Transformer | Power Supply - - - 

- Scribd, htps://www.scribd.com/document/62289074/Safety <u>According to</u> - - - - - 

- - - - - <u>Iec 60364 7 710 2002 11</u> 

30. Hospital-IEC60364.pdf - Slideshare, <u>htps://www.slideshare.net/slideshow/hospitaliec60364pdf/252475243</u> 

31. Electrical safety costs little – a human life is priceless - fournais-bender, htps://fournais-bender.dk/storage/Electrical-safety-costs-litle.pdf 

32. ES710-GL Series - Isolating transformer - Bender Benelux, <u>htps://www.benderbenelux.com/fleadmin/content/Products/d/it/ES710_D00109 _D_ENIT.pdf</u> 

33. Zasilanie obiektów budowlanych służby zdrowia w energię elektryczną - - - 

elektro.info, htps://www.elektro.info.pl/artykul/systemy <u>gwarantowanego zasilania/168718,zasilanie-obiektow-budowlanych-sluzby-zdrowia-w-energieelektryczna</u> 

34. Intelligent Modeling of PV–BESS Microgrids for Enhanced Stability, Cyber– - 

Physical Resilience and Blackout Prevention - MDPI, htps://www.mdpi.com/1996 <u>1073/19/1/148</u> 

35. IEC 62040-3 UPS Performance Standards | PDF | Electromagnetic Compatibility - - - 

Scribd, htps://www.scribd.com/document/721367805/62040 <u>3 2021</u> 

36. SVENSK STANDARD SS-EN 62040-1, <u>htps://elstandard.se/documents/preview/160801</u> 

37. EN IEC 62040-3, htps://normy.normof.gov.sk/norma/133227/nahlad/ 38. Uninterruptible Power Supply (UPS) Safety and Compliance with UL 1778 | UL - - - - 

Solutions, htps://www.ul.com/services/uninterruptible <u>power supply ups</u> - - - - 

<u>safety and compliance ul 1778</u> 

39. SIST EN IEC 62040-1:2019 - iTeh STANDARD PREVIEW (standards.iteh.ai), <u>htps://cdn.standards.iteh.ai/samples/61153/8191d10852f947d895bdab349409e11</u> - - - - - 

<u>7/SIST EN IEC 62040 1 2019.pdf</u> 

40. EN IEC 62933-4-3 - ÚNMS SR, <u>htps://normy.normof.gov.sk/norma/142107/nahlad/</u> 

41. Electrical energy storage management system - SyC Smart Energy - IEC, - - - - - - - 

<u>htps://syc se.iec.ch/iec 63097 smart energy roadmap/electrical energy</u> - - 

<u>storage management system/</u> 

42. IEC 62933-1:2024, htps://webstore.iec.ch/en/publication/64642 43. SVENSK STANDARD SS-EN IEC 62933-4-2, utg 1:2025, <u>htps://elstandard.se/documents/preview/3630601</u> 

44. Fotowoltaika – normy i przepisy dotyczące ochrony odgromowej i przepięciowej, - - - 

<u>htps://www.elektro.info.pl/artykul/fotowoltaika/161074,fotowoltaika normy i</u> - - - - - 

<u>przepisy dotyczace ochrony odgromowej i przepieciowej</u> 

45. Wykaz norm z zakresu ochrony przed przepięciami - RST.PL, <u>htps://rst.pl/pigulki/wykaz-norm-z-zakresu-ochrony-przed-przepieciami/</u> 

46. Wartość rezystancji uziemienia dla przepięciówki - ISE.pl - Forum Elektryka, - - - - 

<u>htps://forum.ise.pl/t/wartosc rezystancji uziemienia dla przepieciowki/10463</u> 

47. Zastosowanie wyłączników różnicowoprądowych – zagadnienia wybrane | elektro.info, - 

<u>htps://www.elektro.info.pl/artykul/ochrona przeciwporazeniowa/191431,zastoso</u> - - - - 

<u>wanie wylacznikow roznicowopradowych zagadnienia wybrane</u> 

48. Design of Microgrid-Based Resilience Solutions to Improve Public Health Impacts - 

of Earthquake-Induced Power Outages - MDPI, htps://www.mdpi.com/2071 <u>1050/18/5/2552</u> 

49. Integrating Safety into Microgrid Sizing: A Systematic Review - MDPI, - 

<u>htps://www.mdpi.com/1996 1073/19/9/2098</u> 

50. Hybrid Renewable Systems Integrating Hydrogen, Battery Storage and Smart Market Platforms for Decarbonized Energy Futures - MDPI, htps://www.mdpi.com/1996-1073/19/2/331 

51. Field-Validated Two-Layer Dispatch Framework for a Rural Hybrid Microgrid with Power Quality and Environmental Assessment - MDPI, - 

<u>htps://www.mdpi.com/1996 1073/19/12/2791</u> 

52. Rajesh Karki's research while affiliated with University of Saskatchewan and other places, htps://www.researchgate.net/scientifc-contributions/Rajesh- 

#### - <u>Karki 73426960</u> 

53. Real-Time Economic Dispatch of CHP Systems with Battery Energy Storage for Behind-the-Meter Applications - MDPI, htps://www.mdpi.com/1996- <u>1073/16/3/1274</u> 

54. A Review of Photovoltaic Thermal (PVT) Technology for Residential Applications: Performance Indicators, Progress, and Opportunities - MDPI, - 

<u>htps://www.mdpi.com/1996 1073/14/13/3853</u> 

55. Biogas-to-Power Systems Based on Solid Oxide Fuel Cells: Thermodynamic - 

Analysis of Stack Integration Strategies - MDPI, htps://www.mdpi.com/1996 <u>1073/17/15/3614</u> 

56. Optimization of PV and Battery Energy Storage Size in Grid-Connected Microgrid - MDPI, htps://www.mdpi.com/2076-3417/12/16/8247 

57. Sizing PV and BESS for Grid-Connected Microgrid Resilience: A Data-Driven - 

Hybrid Optimization Approach - MDPI, htps://www.mdpi.com/1996 <u>1073/16/21/7300</u> 

58. Pitchaya Jamjuntr's research works | King Mongkut's University of Technology Thonburi and other places - ResearchGate, - - 

<u>htps://www.researchgate.net/scientifc contributions/Pitchaya</u> - 

<u>Jamjuntr 74998949</u> 

59. Optimal Operation of Battery Energy Storage Systems in Microgrid-Connected Distribution Networks for Economic Efficiency and Grid Security - MDPI, htps://www.mdpi.com/1996-1073/18/23/6335 

60. State of Charge Control Integrated with Load Frequency Control for BESS in - 

Islanded Microgrid - MDPI, htps://www.mdpi.com/1996 <u>1073/13/18/4657</u> 

61. Innovative Microgrid Services and Applications in Electric Grids: Enhancing - 

Energy Management and Grid Integration - MDPI, htps://www.mdpi.com/1996 <u>1073/17/22/5567</u> 

62. The Spanish Energy Storage Market: Foundations for a Clean Energy Future - - 

MDPI, htps://www.mdpi.com/1996 <u>1073/18/21/5788</u> 

63. Characterization of the Operation of a BESS with a Photovoltaic System as a Regular Source for the Auxiliary Systems of a High-Voltage Substation in Brazil - - 

MDPI, htps://www.mdpi.com/1996 <u>1073/16/2/1012</u> 

64. Resilient Grid Architectures for High Renewable Penetration: Electrical Engineering Strategies for 2030 and Beyond - MDPI, - 

<u>htps://www.mdpi.com/2227 7080/14/2/112</u> 

65. Short-Term Solar and Wind Power Forecasting Using Machine Learning - 

Algorithms for Microgrid Operation - MDPI, htps://www.mdpi.com/1996 <u>1073/19/2/550</u> 

66. zarządzanie ryzykiem – przegląd wybranych metodyk - Centrum NaukowoBadawcze Ochrony Przeciwpożarowej, <u>htps://cnbop.pl/app/uploads/2024/11/Zarzadzanie_ryzykiem_Przeglad_wybranyc h_metodyk.pdf</u> 

67. Trigger-Based PDCA Framework for Sustainable Grid Integration of Second-Life 

- <u>htps://www.mdpi.com/2032 6653/16/10/584</u> EV Batteries - MDPI, 

