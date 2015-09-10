*** QR - Optymalizacja III -  Zapis binarny*** 

**Założenia:**
- Po przeanalizowaniu próbkowo i wybiórczo zbioru 100 protokołów wyborczych z terenu RP liczba kandydatów którzy nie otrzymali zadnych głósów  w OKW  wynosi od  ok 60 - 69 %. Mozna więc przyjąć i uśredniając ten wynik, iż statystycznie  liczba ta oscyluje w granicach  65 %  
- 20 Komitetów wyborczych zgłaszajcych listy kandydatów w każdym okręgu (w 2011 r. było 11)  
- 40 kandydatów na jednej liscie (Warszawa: 20 mandatów x 2 kandydatów na 1 miejsce z każdej listy - w 2011 było maksymalnie 292 kandydatów w okręgu 16 mandatowym, 261 kandydatów statystycznie)
- 65 % kandydatów z 261 = 90 Kandydatów do zakodowania w QR
- Do obliczeń przyjęto dane z OKW 502 Warszawa Wawer. Liczba głosów i kandydatów w OKW rozkłada się następująco: 

261 - Kandydatów

183 - Nie otrzymało zadnych głosów 

78  - Otrzymało jakiekolwiek głosy

w tym 

2 - z glosami przekazanymi w 3 znakach

7 - z glosami przekazanymi w 2 znakach

69  - z glosami przekazanymi w 1 znaku


Sumaryczny narzut na przekazanie ilości głosów dla konkretnej OKW  = 2x3 + 7x2 + 69x1 = 89  
Przyjęto uśredniony sumaryczny narzut dla wszytkich OKW = 100

 **Algorytm zapisu danych w QR:**  
Krok 1 
 - Kandydatów oznaczamy strukturą :
  id, ilość otrzymanych głosów ;

gdzie: 
id = NrKomitetu_PozycjaKandydata

Np: 0923,4;  - oznacza  komitet wyborczy nr 9 oraz 23-ciego kandydata w tymże komitecie, 4 otrzymane głosy 

Np: 1104,345; - Komitet 11, Kadydat nr 4 na liscie, 345 głosów 
 
Krok 2

Sortujemy wszystkich kandydatów po wartośći otrzymanych głosów 

Krok 3

Kasujemy wszystkich kandydatów z wartośćią zerową  i zapisujemy tylko w QR tych, którzy otrzymali jakiekolwiek głosy.  Przykładowo dla OKW  z W-Wa nr 779 liczba kandydatów =  68 z 261, OKW 501 = 95/261 ,OKW 582 =76/261

Krok 4. 
W backend po otrzymaniu danych z OKW za pomocą QR odtwarzarzane są dane kandydatów  a następnie uzupełniane domyslnie wartosciami zerowymi dla wszyskich innych kandydatów nie przekazanych w samym QR. 

 **Wyliczenia QR  dla Obszaru PL :**  

Nagłówek:
TERYT – 6 znaków + 1 rozdzielający
Nr obwodu – 4 znaki + 1 rozdzielający

Rozliczenie kart:
1. Uprawnieni do głosowania - 4 znaków +1 rozdzielający
2. Otrzymane karty do głosowania - 4 znaków +1 rozdzielający
3. Niewykorzystane karty - 4 znaków +1 rozdzielający
4. Wydano kart do głosowania - 4 znaków +1 rozdzielający
5. Głosujący przez pełnomocnika - 4 znaków +1 rozdzielający
6. Głosujący na podstawie zaświadczenia - 4 znaków +1 rozdzielający

Rozliczenie głosowania korespondencyjnego:
7. Wydano pakietów - 3 znaków +1 rozdzielający
8. Otrzymano koperty zwrotne - 3 znaków +1 rozdzielający
8a. Brak oświadczenia - 3 znaków +1 rozdzielający
8b. Brak podpisu na oświadczeniu - 3 znaków +1 rozdzielający
8c. Brak koperty na kartę do głosowania - 3 znaków +1 rozdzielający
8d. Niezaklejona koperta na kartę do głosowania - 3 znaków +1 rozdzielający
8e. Koperty na kartę do głosowania wrzucone do urny - 3 znaków +1 rozdzielający

Ustalenia wyników
9. Karty wyjęte z urny - 4 znaków +1 rozdzielający
9a. liczba kart z kopert na kartę do głosowania - 4 znaków +1 rozdzielający
10. Karty nieważne - 4 znaków +1 rozdzielający
11. Karty ważne - 4 znaków +1 rozdzielający
12. Głosy nieważne - 4 znaków +1 rozdzielający
13. Głosy ważne - 4 znaków +1 rozdzielający


Kandydaci 
14. 90 kandydatów x 4 znaki (id) + 1 znak (rozdzielający) + 1 znak (konczący) + 100  (przyjęty szacunkowy narzut całosciowy ilości głosów w OKW) 

Uwagi i adnotacje - 
Rezygnujemy z przekazania tych danych


Podpisy członłów komisji - 
Rezygnujemy z przekazania tych danych

**Łącznie cały string dla PL równa się: 640 znaków**

**Aproksymacja**
- Zważywaszy na fakt, iż do wyliczeń użyto przykladowych danych z 2011 roku - przyjęto  następujący liniowy wspólczynnik bezpieczęstwa x 3 w stosunku do ilośći komitetów wyborczych i x 5 w stosunku do sumarycznego narzutu potrzebnych znaków do przekazania ilośći głosów. Przy czym należy zaznaczyć, że są to ze względów bezpieczęstwa mocno zawyżone dane.

**Wyliczenia:**

 3 x 90 kandydatow x 6 znaków  + 500 (sumaryczny narzut) = 2120 znaków. 
 
 **Kompresja:**
Aby obniżyc liczbę znaków do przekazania w QR - można zastosować kompresje danych np ZIP, RAR, która obniży te liczbę o ok 30 % tj - do liczby ok 850 znaków. 
 
Liczbę tę można spokojnie przekazać w  Jednym QR kodzie. Zważywszy jednak na złe warunki oswietleniowe i problemy z odczytem QR z szyby w nocy a także ich wydrukowaniem zastosować można mechanizm multiplikowania danych. 
 
  **Multiplikowanie danych :**
Idea multiplikowania danych opiera się na klasycznym przekazaniu nadmiaru danych w wiekszej ilosci kodów QR - pomimo, iż dane mogły by być przekazywane w jednym kodzie.  I tak przy pomocy mechanizmu sekretu można by ilość 850 bądz wiecej znaków porozdzielać na 3 QR w taki sposób ze zeskanowanie dowolnych 2 z 3 QR ( bez koniecznosci sekwencyjnego skanowania w kolejnosci ) przekazywało by 100 % danych. Takie rozwiązanie ma nięwątpliwą zalete, gdyż nie wymusza skanowania w kolejnosci kodów  QR a ponad to umozliwia szybszy i sprawniejszy odczyt QR uwarunkowany mozliwosciami technicznymi urządzen skanujących (Smartfony)  i złymi warunkami oswietleniowymi.  


**Pomysly :**
W celu zapewnienia spójnosci i autentyfikacji przekazywanych danych  - moznaby przekazywać link do JSON z danej OKW w samym QR kodzie. Link ten w celu bezpieczęstwa byłby zaszyfrowany bądz przekazywany dynamicznie w taki sposób aby nie moznabyło odgadnąc strukrury serwerów a takze katalogów przechowujących JSON`y przez nieautoryzowane osoby. Po odczytaniu linka system sprawdzałby i porównywał dane pomiedzy samym QR a oficialnym JSON z PKW  z danej komisji. Jesli dane te sie zgadzałyby sie - oznaczałoby to ze przekazane dane są oryginalne i autentyczne. W przypadku rozbierznosci ( np zmiana protokołu w OKW ) - w sposób łatwy moznaby wyłapywać takie anomalie i weryfikować problemy w OKW.  Co wiecej po prowadzeniu metod licencjonowania i/albo stępli czasowych można zastosować automatyzacje uaktualnień wyników wyborów.  


