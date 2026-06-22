# **Systemy operacyjne (SO)**







## Wprowadzenie do systemów operacyjnych.



##### System operacyjny

To oprogramowanie będące warstwą pośrednią pomiędzy użytkownikiem, a sprzętem. Nadzorujące wykorzystanie zasobów fizycznych i zapewniające środowisko niezbędne do uruchamiania i działania aplikacji oraz procesów i ich komunikacji z komponentami systemu w sposób wydajny i bezpieczny.



##### Budowa SO:

* jądro systemu
* system plików
* powłoka



##### System operacyjny zarządza:

* procesami
* pamięcią
* systemem plików
* operacjami wejścia/wyjścia
* zasobami systemowymi
* bezpieczeństwem
* siecią
* interfejsem użytkownika
* energią
* wirtualizacją











## Procesy.



###### Zadania systemu:

* tworzenie i planowanie procesów
* planowanie dostępu do CPU
* synchronizacja i komunikacja
* zarządzanie zasobami



##### 

##### Program a proces

Program jest statycznym zbiorem instrukcji zapisanych w pamięci trwałej, a proces to dynamiczna instancja tego programu w trakcie wykonywania.



###### **Proces zawiera:**

* kod programu
* aktualne wartości zmiennych
* stan rejestrów procesora
* licznik rozkazów
* informacje o przydzielonych zasobach



Oznacza to, że **jeden pogram może być wykonywany wielokrotnie** jako różne procesy, każdy w innym stanie.



###### Kontekst procesu

To kompletny zestaw informacji opisujący aktualny stan procesu. Obejmuje on m.in:

* zawartość liczników procesora
* licznik rozkazów
* wskaźnik stosu



###### Struktura pamięci procesu

Każdy proces posiada własną przestrzeń adresową, która jest logicznie podzielona na kilka segmentów:

* kod
* dane
* stos
* sterta



###### Izolacja procesów

Oznacza ona, że każdy proces działa w swojej własnej przestrzeni pamięci i nie ma bezpośredniego dostępu do danych innych procesów. Izolacja jest realizowana przez mechanizmy sprzętowe i programowe, takie jak wirtualna pamięć i ochrona przestrzeni adresowej. Korzyścią takiej izolacji jest bezpieczeństwo i stabilność.

###### 

###### Cykl życia procesów

System operacyjny monitoruje i zarządza przejściami między etapami życia procesów tak aby efektywnie współdzielić CPU.



**Stany procesu:**

* nowy
* gotowy
* wykonywany
* oczekujący
* zakończony



Przejścia pomiędzy stanami procesu są wynikiem, różnych działań mechanizmów systemowych jak: planowanie, przerywania, operacje I/0. Proces może zostać np. wywłaszczony i wrócić do kolejki gotowych lub przejść do stanu oczekiwania.



##### 

##### PCB- podstawowa struktura procesu

**Blok sterowania procesem (Process Control Block)** - specjalna struktura danych wykorzystywana przez SO do nadzorowania działań procesów. Każdy uruchomiony proces ma własny PCB, który jest tworzony i aktualizowany przez jądro systemu. Dzięki informacjom zapisanym w tej strukturze, możliwe jest sprawne zarządzanie wykonywaniem procesów oraz ich przełączaniem 



###### Elementy składowe:

* identyfikator procesu (PID)
* aktualny stan procesu
* licznik rozkazów
* zawartość rejestrów procesora
* informacje związane z pamięcią
* dane wykorzystywanie do przy planowaniu
* informacje statyczne
* dane dot. operacji I/O



###### Rola PCB:

* zarządzanie procesami
* Przełączanie kontekstu
* synchronizacja i komunikacja
* bezpieczeństwo i izolacja



###### Planowanie procesora

Procesor jest zasobem ograniczonym dlatego ważne jest, podejmowanie decyzji o tym, który proces będzie wykonywany w danym momencie. Jest to kluczowy problem dla wydajności systemu i komfortu użytkownika. Procesy są przechowywane w różnych kolejkach w zależności od swojego stanu. Kolejka gotowych zawiera procesy oczekujące na CPU, natomiast kolejki oczekujących zawierają procesy czekające na konkretne zdarzenia.



###### Wywłaszczanie

Umożliwia ono przerwanie procesu i przekazanie procesora innemu.



##### 

##### Wątki

Podstawowa jednostka wykonywania w ramach procesu. Jeden proces może zawierać wiele wątków, które współdzielą jego zasoby. Dzięki temu możliwe jest wykonywanie wielu zadań jednocześnie w obrębie jednej aplikacji.

Każdy wątek posiada własny kontekst wykonania, na który składa się:

* licznik rozkazów
* rejestry procesora
* stos, przechowujący dane lokalne i wywołania funkcji
* 

Jednocześnie wszystkie wątki w obrębie jedno procesu współdzielą:

* pamięć 
* kod programu
* otwarte pliki i zasoby systemowe



##### 

##### Systemy niewywłaszczające 

W systemach niewywłaszczających proces działa aż do zakończenia lub do przejścia w stan oczekiwania. Rozwiązanie to jest prostsze, ale może prowadzić do niskiej responsywności systemu.



##### 

##### Przełączanie kontekstu - mechanizm

Przełączanie kontekstu to operacja wykonywana przez SO, gdy CPU przestaje wykonywać jeden proces lub wątek i zaczyna wykonywać inny.



###### Jak wygląda przełączanie krok po kroku?

* przerwanie aktualnego procesu
* zapis kontekstu procesu A
* wybór nowe procesu
* odtworzenie kontekstu procesu B
* wznowienie wykonania procesu B

Przełączanie kontekstu nie wykonuje pracy użytkowej, tylko administracyjną, to tak zwany "narzut"



###### Skąd bierze się koszt?

* zapisywanie i odczytywanie rejestrów
* dostęp do pamięci
* zmiana przestrzeni adresowej
* przejście między trybem użytkownika, a jądra systemu.





##### Algorytmy planowania

Określają sposób wyboru procesu do wykonania. Wybór algorytmu ma bezpośredni wpływ na wydajność i zachowanie systemu.



###### Przykłady:

* FCFS
* SJF
* SRTF
* Round Robin













## Szeregowanie procesów.



##### Strategia FCFS(First Came First Served)

Strategia ta polega na przydzielaniu czasu w kolejności zgłaszania się procesów. Jest najprostszą implementacją bez wywłaszczania.



###### Zalety:

* sprawiedliwy, niski narzut systemowy
* nie ma groźby zagłodzenia procesów, proces zawsze dostanie się do CPU (po pewnym czasie)



###### Wady:

* długi/średni czas oczekiwania i duża wariancja czasu oczekiwania
* niewydajne wykorzystanie CPI
* jest krzywdzący dla krótkich procesów, które są wstrzymywane przez procesy długie
* kłopotliwy w systemach z podziałem czasu, w których ważne jest uzyskiwanie procesora w regularnych odstępach czasu



##### 

##### Strategia SJF(Shortest Job First)

Algorytm bierze pod uwagę długość najbliższej fazy procesora każdego procesu, lecz nie sprawdza całkowitej długości procesu lecz jedynie długość następnej fazy procesora. Gdy procesor jest dostępny to jest przydzielany procesowi o najkrótszej fazie procesora, a jeżeli są dwa procesy o takiej samej długości następnej fazy procesora to problem jest rozwiązywany metodą FCFS. 



###### Wnioski:

* SJF jest optymalny, daje minimalny czas oczekiwania dla danego zbioru procesów
* trudnością jest określenie długości następnego zamówienia na przydział procesora
* metodę można z powodzeniem stosować w planowaniu długoterminowym
* nie można wprost realizować planowania krótkoterminowego, gdyż nie ma sposobu na poznanie dokładnej długości następnej fazy procesora procesu



##### 

##### Strategia SRTF(Shortes Remaining Time First)

Odmiana algorytmu SJF z dodanym wywłaszczeniem

Planista musi być wywołany, poza momentem zakończenia każdego procesu jak zwykle, jedynie w chwili pojawienia się nowego procesu, wybierając ten z najkrótszym pozostałym przewidywanym czasem obliczeń



##### 

##### Strategia RR(Round Rubin)

Jest to wywłaszczeniowy algorytm FCFS zaprojektowany dla systemów z podziałem czasu. Przełączanie procesów następuje z czasem zwanym kwantem lub odcinkiem czasu, a każdemu procesowi przydziela się procesor na czas nie dłuższy niż kwant czasu. Jeżeli faza procesora procesu wykonywanego jest krótsza niż 1 kwant czasu, wówczas proces z własnej inicjatywy zwolni procesor. Procesy do wykonania są pobierane z kolejki procesów gotowych do wykonania metodą FCFS. 



###### Wady:

* długi/średni czas oczekiwania 
* wydajność metody w dużym stopniu zależy od rozmiaru kwanta czasu
* kwant czasu bardzo długi - metoda FCFS
* kwant czasu bardzo krótki - dzielenie procesora











## 

## Komunikacja i synchronizowanie procesów.



##### Proces i wątek

###### **Proces**

jest niezależną jednostką wykonania programu, posiadającą własną przestrzeń adresową, co zapewnia izolację od innych procesów, Dzięki temu błędy w jednym procesie nie wpływają na drugi.



###### **Wątki**

są lżejszymi jednostkami wykonania działającymi w obrębie jednego procesu. Współdzielą one pamięć, co znacząco przyśpiesza komunikację, ale jednocześnie zwiększa ryzyko wystąpienia problemów współbieżności. Z punktu widzenia programisty ocznacza to konieczność większej ostrożności przy operacjach na wspólnych danych.



Komunikacja i synchronizowanie procesów stanowią fundament działania współczesnych SO oraz aplikacji wielowątkowych. W środowisku, w którym wiele procesów i wątków działa jednocześnie, konieczne jest zapewnienie mechanizmów umożliwiających ich bezpieczną współpracę.

Brak odpowiedniej synchronizacji prowadzi do błędów logicznym, niespójności danych oraz zachowań trudnych do przewidzenia i debugowania. Dlatego SO oferują różne mechanizmy umożliwiające kontrolę dostępu do zasobów oraz komunikację między procesami



##### 

##### Współbieżność a równoległość

Współbieżność odnosi się do zdolności SO do obsługi wielu zadań w tym samym czasie logicznym poprzez przełączanie kontekstu. Równoległość natomiast oznacza rzeczywiste jednoczesne wykonywanie wielu zadań na różnych rdzeniach procesora.

##### 

##### 

##### Problem współdzielenia zasobów

Współdzielenie takich zasobów jak pamięć, pliki czy urządzenia I/O prowadzi do potencjalnych konfliktów. Jeśli dwa procesy jednocześnie modyfikują ten sam zasób, wynik operacji może być niepoprawny. 

Klasycznym przykładem jest inkrementacja zmiennej przez wiele wątków, gdzie brak synchronizacji prowadzi do utraty części operacji.



##### 

##### Komunikacja między procesami (IPC)

Mechanizmy IPC umożliwiają procesom wymianę danych oraz synchronizację działań. W zależności od potrzeb stosuje się różne rozwiązania, które różnią się wydajnością, poziomem abstrakcji oraz zastosowaniem.

Wybór odpowiedniego mechanizmu IPC zależy od charakteru aplikacji oraz wymagań dot. wydajności oraz bezpieczeństwa.



##### 

##### Potoki (pipes)

Są one jednym z najprostszych mechanizmów komunikacji między procesami. Umożliwiają przesyłanie danych w sposób strumieniowy, zazwyczaj między procesem rodzicem a potomkiem.

Potok można sobie wyobrazić jako jednokierunkowy tunel w pamięci RAM, zarządzany przez jądro SO. Dane są do niego wpisane z jednego końca i doczytywane z drugiego zgodnie z zasadą FIFO (First-In, First-Out).



###### Rodzaje potoków:

* nienazwane - istnieją i żyją w pamięci tak długo jak procesy, które je stworzyły
* nazwane - są widoczne w systemie plików jako specjalne pliki. Pozwalają na komunikację pomiędzy niespokrewnionymi procesami



###### Wady i ograniczenia:

* jednokierunkowość (simplex)
* brak struktury danych
* ograniczony rozmiar bufora



##### 

##### Kolejki komunikatów

Pozwalają one na przesyłanie uporządkowanych wiadomości między procesami. Każdy komunikat ma określony typ oraz priorytet.



###### Zalety:

* asynchroniczność 
* odklejanie
* brak konieczności pokrewieństwa
* trwałość



##### 

##### Pamięć współdzielona

Jest to najszybszy mechanizm IPC, ponieważ eliminuje konieczność kopiowania danych między procesami. Procesy uzyskują dostęp do tego samego obszaru pamięci.

W tym rozwiązaniu nie istnieje możliwość kopiowania, ale jest ono niemal tak szybkie jak dostęp do pamięci lokalnej wewnątrz jednego procesu. 

* brak wbudowanej kontroli
* konieczność zewnętrznej synchronizacji



##### 

##### Gniazda (sockets)

Gniazda umożliwiają komunikacje zarówno lokalną jak i sieciową. Są podstawą działania aplikacji klient-serwer i systemów rozproszonych.



###### Kluczowe komponenty adresu gniazda:

* adres IP
* numer portu
* protokół



###### Rodzaje gniazd:

* strumieniowe
* datagramowe
* lokalne



##### 

##### Sygnały

Jest to programowe przerwanie, które wymusza na procesie nagłą zmianę toku wykonania. Może je wysyłać jądro systemu, użytkownik lub inny proces.



###### Obsługa sygnałów

Proces po otrzymaniu sygnału może zareagować zgodnie z zaprogramowaną logiką:

* Maska sygnałów: proces może tymczasowo zablokować określone sygnały, aby nie przerwały one krytycznych obliczeń.
* Funkcja obsługi (Handler): specjalna funkcja, do której system skacze w momencie nadejścia sygnału. Po jej zakończeniu program wraca do miejsca, w którym został przerwany.

Jest to ważne, ponieważ pozwala to na bezpieczne wyłączenie aplikacji.



##### 

##### Wyścig (Race Condition)

Sytuacja, w której wynik końcowy zależy od tego, który proces był szybszy (kolejność wykonania).



##### 

##### Semafory

Semafor s to chroniona zmienna całkowita, do której dostęp mają wyłącznie dwie atomowe operacje systemowe: P (wait), V (signal).



###### Implementacja wewnątrz jądra:

* Semafor nie jest zwykłym licznikiem, posiada powiązaną kolejkę procesów zablokowanych.
* Gdy proces wykonuje P(S) o S<=0, jądro zmienia stan procesu na WAITING, zawiesza jego wykonanie i umieszcza w kolejce.
* Operacja V(S) nie tylko zwiększa licznik, ale sprawdza kolejkę: jeśli nie jest pusta, jeden z procesó jest przenoszony do stanu READY.



**Atomowość:** system gwarantuje, że operacje na semaforze nie zostaną przerwane przez planistę.



##### 

##### Muteksy

Są uproszczoną formą semofora o stanie binarnym, zaprojektowana specjalnie do ochrony sekcji krytycznych. Muteks pamięta, który wątek go zablokował. Tylko ten sam wątek może go odblokować. Zapobiega to błędom logicznym, gdzie jeden proces zwalnia blokadę należącego do innego.

Optymalizacja wydajności (Futex - Fast Userspace Mutex):

* unikanie kosztownego przełączania trybu jądra
* jeśli nie ma rywalizacji o zasób to operacja lock odbywa się całkowicie w przestrzeni użytkownika
* przejście do jądra następuje tylko wtedy, gdy wymagane jest uśpienie wątku z powodu zajętego zasobu



###### Muteksy rekurencyjne:

Pozwalają temu samemu wątkowi na wielokrotne zablokowanie tego samego muteksu bez wywołania zakleszczenia.



##### 

##### Zakleszczenia (Deadlock)

Jest to stan, w którym każdy proces z pewnego zbioru oczekuje na zwolnienie zasobu, które może zostać wywołane jedynie przez inny proces z tego samego zbioru.

Wynik: procesy trwają w nieskończonym oczekiwaniu.

Aby doszło do zakleszczenia muszą wystąpić jednocześnie te cztery czynniki (Warunki Coffmana):

1. Wzajemne wykluczenie.
2. Przetrzymanie i oczekiwanie.
3. Brak wywłaszczania.
4. Czekanie cykliczne.



###### Strategia radzenia sobie z zakleszczaniem:

* zapobieganie - projektowanie systemu tak, aby wyeliminować jeden z warunków
* unikanie - dynamiczne sprawdzanie bezpieczeństwa
* wykrywanie i naprawa
* Metoda Strusia - ignorowanie problemu















## Pamięć pomocnicza i systemy plików.

Pamięć pomocnicza stanowi trwały magazyn danych, który rozszerza ograniczona pojemność RAM-u.

###### Zalety:

* nielotna
* pojemna
* ekonomiczna









## 

## Zarządzanie pamięcią operacyjną i współdzielenie pamięci.

**RAM (Random-Access Memory)** - pamięć operacyjna, Pełni ona funkcje przestrzeni roboczej dla aktualnie wykonywanych programów oraz danych. Jest znacznie szybsza od pamięci masowej, co umożliwia efektywne przetwarzanie informacji.

Każdy proces otrzymuje własną przestrzeń adresową, co zapobiega przypadkowemu lub celowemu naruszeniu danych innych procesów.

Efektywne zarządzanie pamięcią bezpośrednio wpływa na wydajność systemu, czas reakcji oraz stabilność działania aplikacji.



###### Cele zarządzania pamięcią:

* maksymalizację wykorzystania dostępnej pamięci fizycznej
* minimalizację fragmentacji
* zapewnienie bezpieczeństwa i izolacji procesów
* umożliwienie współdzielenia pamięci
* zapewnienie abstrakcji pamięci wirtualnej



##### Organizacja pamięci

Pamięć dzieli się na:

* **pamięć fizyczną** (RAM)
* **pamięć logiczną** (widoczną dla procesu)
* **pamięć pomocniczą** (dysk)



##### Adresowanie pamięci

Polega ono na przypisywaniu unikalnych adresów do komórek pamięci.



###### Rozróżniamy:

* **adresy fizyczne** - rzeczywiste położenie danych w RAM
* **adresy logiczne** - generowane przez program



Mechanizm translacji adresów pozwala na mapowanie adresów logicznych na fizyczne, co umożliwia izolację procesów i implementację pamięci wirtualnej.



##### Fragmentacja pamięci

To zjawisko powstawania nieużytecznych obszarów pamięci: 

* fragmentacja zewnętrzna
* fragmentacja wewnętrzna



Obniża ona efektywność wykorzystania pamięci i wymaga stosowania mechanizmów jej redukcji



##### Przydział pamięci

Proces przypisywania fragmentów pamięci procesom. Może być realizowany przez:

* przydział statyczny
* przydział dynamiczny
* 

SO musi równoważyć szybkość przydziału z efektywnością wykorzystania pamięci.



###### Strategie przydziału:

* First Fit
* Best Fit
* Worst Fit



Współdzielenie pamięci pozwala wielu procesom korzystać z tym samych danych.

Jest stosowane w celu:

* oszczędności pamięci
* szybkiej komunikacji między procesami
* współpracy aplikacji



Mechanizmy współdzielenia wymagają synchronizacji, aby zapobiec konfliktom.

Do najważniejszych mechanizmów należą:

* pamięć współdzielona
* mapowanie plików do pamięci
* segmentacja współdzielona

Zapewniają one szybki dostęp do danych bez konieczności kopiowania.



Współdzielenie pamięci wymaga kontroli dostępu. Stosuje się przy tym:

* semafory
* muteksy
* monitory

Zapobiegają one problemom takim jak warunki wyścigu.



##### Stronicowanie (pagin)

Technika podziału pamięci na jednostki o stałym rozmiarze - strony.

Procesy są dzielone na strony, a pamięć fiz. na ramki. Strony mogą być umieszczanie w dowolnych ramkach, co eliminuje fragmentację zewnętrzną.

Tablice stron przechowują mapowanie między stronami logicznymi, a ramkami fizycznymi.



###### Każdy wpis zawiera:

* numer ramki
* bity kontroli dostępu
* informacje o obecności strony w pamięci



Tablica stron jest kluczowym elementem translacji adresów.



###### Translacja adresów polega na przekształcaniu adresu log. w fiz. Obejmuje:

* podział adresu na numer strony i offset
* wyszukiwanie tablicy stron
* dodanie offsetu do adresu ramki

Proces ten jest realizowany sprzętowo przez NMU.



###### TLB

Szybka pamięć podręczna przechowująca najczęściej używane wpisy tablicy stron.

Pozwala znacząco przyśpieszyć translacje adresów redukując liczbę odwołań do pamięci głównej.



##### Stronicowanie

###### Zalety:

* eliminuje fragmentacje zewn. i upraszcza zarządzanie pamięcią
* umożliwia implementację pamięci wirtualnej oraz efektywne współdzielenie danych między procesami

###### Wady:

* fragmentacja zewnętrzna 
* narzut związany z tablicami stron
* złożoność sprzętowa
* w dużych systemach tablice mogą zajmować znaczną ilość pamięci



###### Stronicowanie na żądanie.

Polega ono na ładowaniu stron do pamięci tylko wtedy, gdy są potrzebne.

Zmniejsza to zużycie pamięci i przyśpiesza uruchamianie programów.



##### Błędy strony (page fault)

Występuje wtedy, gdy proces odwołuje się do strony nieobecnej w pamięci.

SO musi wtedy:

* załadować stronę z dysku
* zaktualizować tablicę stron
* wznowić proces



###### Algorytmu zastępowania stron:

* FIFU
* LRU
* OPT

Ich celem jest wybór strony do usunięcia z pamięci.



###### Pamięć wirtualna

Umożliwia ona wykonywanie programów większych niż dostępna pamięć fiz..

Tworzy iluzję dużej, ciągłej przestrzeni adresowej, niezależnej od rzeczywistej pamięci RAM..



###### Thrashing

Występuje, gdy system spędza więcej czasu na wymienia stron niż na wykonywaniu procesów.

Prowadzi to do drastycznego spadku wydajności.



##### Lokalność odniesień

###### Programy wykazują lokalność:

* czasową
* przestrzenną

Mechanizmy pamięci wykorzystują tę właściwość do optymalizacji.



###### Segmentacja

Dzieli pamięć na logiczne segmenty (np. kod lub dane). Ułatwia to organizację programu, ale może prowadzić do fragmentacji zewnętrznej.



##### Segmentacja vs stronicowanie

###### Segmentacja: 

* logiczny podział
* większa elastyczność, ale większa również fragmentacja

###### Stronicowanie:

* stałe rozmiary bloków
* brak fragmentacji zew.



##### Bezpieczeństwo pamięci

###### SO zapewnia:

* izolację procesów
* kontrolę dostępu
* ochronę przed błędami



Mechanizmy te są kluczowe dla stabilności systemu



###### Współczesne systemu stosują

* pamięć NUMA
* huge pages
* zaawansowane algorytmy zarządzania



Pozwalają one zwiększyć wydajność w systemach wielordzeniowych.











## Zarządzanie systemem wejścia/wyjścia.



##### Wprowadzenie do systemów I/O

System I/O jest kluczowym elem. sprzętu operacyjnego, odpowiedzialnym za komunikację między jednostką centralną a otoczeniem sprzętowym. Jego głównym zadaniem jest zarządzanie ogromną różnorodnością urządzeń zew., które różnią się prędkością, formatem danych i sposobem obsługi.



###### Cele podsystemu I/O

* abstrakcja sprzętu poprzez ujednolicony interfejs dla programisty
* efektywne zarządzanie współbieżnym dostępem zasobów
* minimalizacja wpływu wolnych urządzeń zew. na wydajność procesora



###### Złożoność zarządzania

Zarządzanie I/O musi uwzględniać specyfikę urządzeń od bardzo wolnych po ekstremalnie szybkie, co wymaga stosowania zaawansowanych mechanizmów buforowania i harmonogramowania



##### 

##### Warstwowa architektura I/O

Nowoczesne SO stosują podejście warstwowe w obsłudze I/O, co pozwala na separację logiki od fiz. implementacji urządzenia.



|**WARSTWA**|**OPIS FUNKCJI**|
|-|-|
|Oprogramowanie użytkownika|Wywołanie biblioteczne (np. printf, scanf) generujące żądania I/O.|
|Niezależne oprogramowanie jądra|Zarządzanie nazwami urządzeń, buforowanie, raportowanie błędów i ochrona dostępu.|
|Sterowniki urządzeń|Kod specyficzny dla danego typu sprzętu, odpowiedzialny za wysyłanie poleceń do kontrolera. |
|Procedury obsługi przerwań|Reagowanie na sygnały fiz. wysłane przez sprzęt po zakończeniu operacji.|



##### 

##### Sposoby komunikacji: Polling



###### Programowanie I/O Polling

Polling nazywany również metodą odpytywania jest najprostszą formą komunikacji między procesorem a urządzenia zew.. Procesor w pętli sprawdza bit gotowości w rejestrze stanu urządzenia, czekając na zakończenie operacji



###### Charakterystyka:

Metoda ta wiąże się ze zjawiskiem aktywnego oczekiwania. Procesor nie może wykonywać innych zadań, dopóki urządzenie nie potwierdzi zakończenia pracy, co prowadzi do ogromnej straty cyki zegarowych.



###### Zastosowanie:

Uzasadnione jedyne w bardzo prostych systemach wbudowanych lub w przypadku urządzeń o czasie reakcji krótszym niż koszt przełączenie kontekstu.



##### 

##### Komunikacja sterowana przerwaniami

Mechanizm przerwaniowy pozwala procesorowi na zajęcie się innymi zadaniami podczas oczekiwania na dane ze sprzętu, co radykalnie zwiększa jego wydajność wielozadaniowości.



###### Przebieg procesu

* CPU inicjuje I/O i zapisuje proces do stanu oczekiwania
* urządzenie wykonuje pracę niezależnie
* po zakończeniu, kontroler urządzenia generuje sygnał na magistrali przerwań
* CPU wstrzymuje bieżący proces i wykonuje procedurę obsługi (ISR)



###### Wnioski wydajnościowe

Główną zaletą jest brak marnotrawstwa czasu CPU. Wadą jest narzut związany z przełączaniem kontekstu i obsługą samego przerwania, co przy bardzo częstych, małych transferach może obciążać system.



##### 

##### Direct Memory Access (DMA)



###### Bezpośredni dostęp do pamięci

DMA jest wyspecjalizowanym układem sprzętowym, który przejmuje od procesora zadanie kopiowania danych między urządzeniem a pamięcią RAM. Jest to kluczowe dla urządzeń generujących duże ilości danych w krótkim czasie



###### Mechanizm działania:



Procesor konfiguruje kontroler DMA, a następnie zwalnia magistralę. Kontroler samodzielnie przesyła dane. Po zakończeniu całego bloki transferu, DMA generuje jedno przerwanie dla procesora

###### Efekt: 

Procesor zostaje odciążony od prozaicznego zadania przenoszenia bajtów, co pozwala mu skupić się na obliczeniach. DMA jest standardem w kartach sieciowych, kontrolerach dysków i kartach graficznych.



##### 

##### Efektywność metod komunikacji



|**Metoda**|**Obciążenie procesora**|
|-|-|
|Polling|100%|
|Przerwania|35%|
|DMA|5%|



##### 

##### Urządzenia blokowe



###### Definicja i charakterystyka

Urządzenia blokowe to takie, które przechowują info. w blokach o stałym, określonym rozmiarze. Każdy blok posiada swój unikalny adres fiz. na nośniku.

* **adresowalność** - możliwość odczytu lub zapisu dowolnego bloku niezależnie od innych
* **dostęp** - wspierają swobodny dostęp
* **buforowanie** - SO niemal zawsze buforuje bloki w RAMie



###### Przykłady:

* dyski HDD
* dyski SSD
* pamięć flash
* napędy CD/DVD



##### 

##### Urządzenia znakowe

###### Definicja i charakterystyka

Urządzenia znakowe dostarczają strumień znaków bez zachowania jakiejkolwiek struktury blokowej. W ich przypadku pojęcie adresu bloku nie istnieje.

* **sekwencyjność** - dane są przetwarzane w kolejności ich pojawienia
* **brak adresowalności** - nie można przewinąć strumienia do konkretnego miejsca
* **interakcja** - często służą do komunikacji w czasie rzeczywistym
* 

###### Przykłady:

* klawiatury i myszy
* karty dźwiękowe
* porty szeregowe
* drukarki



##### 

##### Blokowe VS znakowe



|**Cecha**|**Urządzenia blokowe**|**Urządzenia znakowe**|
|-|-|-|
|Jednostka danych|Stały blok (np. 5KB)|Pojedynczy bajt|
|Model dostępu|Swobodny (Random Access)|Sekwencyjny (Stream)|
|Możliwość zaadresowania|Tak|Nie|
|Zastosowanie|Systemy plików, bazy danych|Terminal, sterowanie, wejście|



##### 

##### Zarządzanie: buforowanie i spooling



###### Buforowanie

Polega na kopiowaniu danych do obszaru pamięci pośredniej przed ich faktycznym użyciem. Pozwala to wyrównać różnice prędkości między producentem a konsumentem oraz dopasować rozmiary jednostek transferu.



###### Spooling

Technika polegająca na zapisywaniu żądań I/O w kolejce na dysku przed wysłaniem ich do urządzenia, które może obsługiwać tylko jedno żądanie (np. drukarka). Dzięki temu procesy użytkownika nie są blokowane przez wolny sprzęt.





















