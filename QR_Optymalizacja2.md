*** QR - Optymalizacja II -  Zapis binarny*** 

**Założenia:**

Kodujemy poszczególne pola z protokołu wyborczego z 2011r. 
- 1 pole to kod terytorialny
- 2 pole to numer obowdu
- 3 pole to okręg wyborczy
- 4 pole to pole 1 z protokołu
- 5 pole to pole 1a z protokołu
- 6 pole to pole 2 z protokołu
- itd, 
- Po polu 9 są listy komitetów wyborczych 
- Całkowita liczba głosów na listę 
- A następnie 40 kandydatów w liscie a dokładniej wyników liczbowych dla nich

Zważywszy na fakt przyjęcia dla przykładu aż 20 Komitetów Wyborczych w kazdym okręgu wyborczym - użyto następującego przykładowego zakodowania:
19X listę PIS i 1x Listę PO - z Protokołu wyborczego OKW 625  W Warszawie. 

**Algorytm zapisu danych w QR:**  
Generalnie nie różni się  działania od zapisu HEX.  Przyjmijmy ze mamy tablicę [0 1 2 3 4 5 6 7 8 9 a b c d e f]

Bierzemy tablicę tab, dowolnej długości (generyczną), n elementową.  Wydzielamy i usuwamy  z niej znaki specjalne (separatory, przecinki,$, % itd). 

Na początek, bierzemy  INT w zakresie 0 do długość tablicy, losujemy  rodzaj ,,ziarna'' od którego potem wszystko będziemy kodować/dekodować. Przyjmijmy że wylosowanym intem jest m (indeks w tablicy). Int ten nigdy się nie zmienia w danym kodowaniu (czy też odkodowywaniu).  Kopiujęmy wartość z m powiedzmy do c. A  wszystko co zakoduje (to co chcemy wrzucić do QRa) wpisujęmy do listy o nazwie LIST
Od razu żeby nie zapomnieć do listy LIST dodaję pierwszy element z tablicy czyli tab[m] i zwiększam c o jeden oczywiście jest to nadal indeks w tablicy więc inkrementować to trzeba tak żeby nie przekroczyć wielkości tablicy. Zresztą c inkrementuje się przy dodaniu czegokolwiek do naszej listy LIST.

Nasze c jest bieżącym indeksem od którego będziemy zaczynać kodowanie kolejnego znaku...
Także jak pierwszym co chcemy zakodować będzie 0, to to będzie to tab[c] gdzie c = m + 1.
Na pojedynczym znaku maksymalnie możemy zakodować wartość n - 1.
Jeśli wartość do zakodowania jest większa od n no to kodowane jest na większej ilości znaków ;) i to jest robione tak jak kodowanie w HEX tyle że z tym przesunięciem, każdy znak jest brany z pozycji c + 1.

 **Przykłady :** 
 
 1. test-qr1441575865178.png

 1VX+:PY:K:WE$:T:IIR:R*:F:V4:SE:C:Y:L*:Y:VD:53:5L:G:9:R:R:.:H:I:A:S:-:K:K:X:C:M:0:%:+:.:0:1:3:5:8:9:W:R:U:O:P:D:G:H:X:X:C:B:M:-:1 :1G:A:5:9:9:%:S:R:U:I:$:F:F:J:K:C:-:B:M:%:-:.: :1:4:5:7:9:E:T:Y:O:A:S:J:J:K:Z:C:$:.+:.A:U:1:5:5:B:I:9:E:R:V:P:P:D:F:K:$:Z:C:B:$:%:+:.:0:1:3:5:8:Q:W:T:U:I:D:D:F:H:K:V:%M:%U:E:.:1:1:Z:R:5:8:9:L:Y:Y:O:P:F:V:H:K:Z:V:B:M:%:-:.: :1:4:6:7:Q:E:R:O:O:P:S:F:L:BC:BE:8:%:.:.:H:9:1:4:5:G:W:W:T:Y:P:L:S:F:H:L:Z:C:B:$:%:+:.:0:2:3:6:8:9:T:T:Y:I:P:G:ZK:Z8:4:B:%:%:S:5:.:0:1:A:7:7:Q:W:Y:G:I:P:S:G:H:K:Z:V:B:M:%:-:/: :2:4:5:Q:Q:W:R:Y:A:HF:H4:0:Z:B:B:I:1:%:-:.:U:3:3:6:7:W:A:R:Y:I:A:S:F:H:L:Z:C:B:$:*:+:/:0:1:6:6:7:9:W:U:SP:S0:-:H:Z:Z:R:.:B:$:%:E: : :2:3:7:U:9:W:R:U:I:P:S:G:H:K:Z:V:N:M:*:-:.:2:2:3:5:7:E:IY:I-:$:S:H:H:9:%:Z:V:B:8:+:+:/: :3:E:5:7:9:E:R:Y:I:A:S:F:H:L:X:C:N:$:%:/:/: :1:3:8:RW:R$:V:I:S:S:5:B:H:L:Z:4:M:M:*:+: :8:1:3:5:8:9:W:R:U:I:P:S:G:J:K:X:V:B:*:*:+:.: :4:97:9V:L:R:I:I:1:Z:S:G:H:0:C:C:N:M:+:4:.: :1:4:5:7:9:E:R:Y:I:A:D:F:J:L:Z:N:N:M:%:+:0:53:5L:G:9:R:R:.:H:I:A:S:-:K:K:X:C:M:0:%:+:.:0:1:3:5:8:9:W:R:U:O:P:D:G:H:X:X:C:B:M:-:1 :1G:A:5:9:9:%:S:R:U:I:$:F:F:J:K:C:-:B:M:%:-:.: :1:4:5:7:9:E:T:Y:O:A:S:J:J:K:Z:C:$:.+:.A:U:1:5:5:B:I:9:E:R:V:P:P:D:F:K:$:Z:C:B:$:%:+:.:0:1:3:5:8:Q:W:T:U:I:D:D:F:H:K:V:%M:%U:E:.:1:1:Z:R:5:8:9:L:Y:Y:O:P:F:V:H:K:Z:V:B:M:%:-:.: :1:4:6:7:Q:E:R:O:O:P:S:F:L:BC:BE:8:%:.:.:H:9:1:4:5:G:W:W:T:Y:P:L:S:F:H:L:Z:C:B:$:%:+:.:0:2:3:6:8:9:T:T:Y:I:P:G:ZK:Z8:4:B:%:%:S:5:.:0:1:A:7:7:Q:W:Y:G:I:P:S:G:H:K:Z:V:B:M:%:-:/: :2:4:5:Q:Q:W:R:Y:A:HF:H4:0:Z:B:B:I:1:%:-:.:U:3:3:6:7:W:A:R:Y:I:A:S:F:H:L:Z:C:B:$:*:+:/:0:1:6:6:7:9:W:U:SP:S0:-:H:Z:Z:R:.:B:$:%:E: : :2:3:7:U:9:W:R:U:I:P:S:G:H:K:Z:V:N:M:*:-:.:2:2:3:5:7:E:BC:ZO:P1:6:K:9:Z:M:/:M:3:+:.:6:3:7:9:4:6:8:T:E:A:A:P:A:5:L:K:Z:V:V:N:+:*: :/:1:W:6:Q


 2. test-test-qr1441575902832.png
79-*3:KF:M:PA0:D:HHS:S2:C:-E:ZA:+:F:$2:F:-X:RW:R$:V:I:S:S:5:B:H:L:Z:4:M:M:*:+: :8:1:3:5:8:9:W:R:U:I:P:S:G:J:K:X:V:B:*:*:+:.: :4:97:9V:L:R:I:I:1:Z:S:G:H:0:C:C:N:M:+:4:.: :1:4:5:7:9:E:R:Y:I:A:D:F:J:L:Z:N:N:M:%:+:0:53:5L:G:9:R:R:.:H:I:A:S:-:K:K:X:C:M:0:%:+:.:0:1:3:5:8:9:W:R:U:O:P:D:G:H:X:X:C:B:M:-:1 :1G:A:5:9:9:%:S:R:U:I:$:F:F:J:K:C:-:B:M:%:-:.: :1:4:5:7:9:E:T:Y:O:A:S:J:J:K:Z:C:$:.+:.A:U:1:5:5:B:I:9:E:R:V:P:P:D:F:K:$:Z:C:B:$:%:+:.:0:1:3:5:8:Q:W:T:U:I:D:D:F:H:K:V:%M:%U:E:.:1:1:Z:R:5:8:9:L:Y:Y:O:P:F:V:H:K:Z:V:B:M:%:-:.: :1:4:6:7:Q:E:R:O:O:P:S:F:L:BC:BE:8:%:.:.:H:9:1:4:5:G:W:W:T:Y:P:L:S:F:H:L:Z:C:B:$:%:+:.:0:2:3:6:8:9:T:T:Y:I:P:G:ZK:Z8:4:B:%:%:S:5:.:0:1:A:7:7:Q:W:Y:G:I:P:S:G:H:K:Z:V:B:M:%:-:/: :2:4:5:Q:Q:W:R:Y:A:HF:H4:0:Z:B:B:I:1:%:-:.:U:3:3:6:7:W:A:R:Y:I:A:S:F:H:L:Z:C:B:$:*:+:/:0:1:6:6:7:9:W:U:SP:S0:-:H:Z:Z:R:.:B:$:%:E: : :2:3:7:U:9:W:R:U:I:P:S:G:H:K:Z:V:N:M:*:-:.:2:2:3:5:7:E:IY:I-:$:S:H:H:9:%:Z:V:B:8:+:+:/: :3:E:5:7:9:E:R:Y:I:A:S:F:H:L:X:C:N:$:%:/:/: :1:3:8:RW:R$:V:I:S:S:5:B:H:L:Z:4:M:M:*:+: :8:1:3:5:8:9:W:R:U:I:P:S:G:J:K:X:V:B:*:*:+:.: :4:97:9V:L:R:I:I:1:Z:S:G:H:0:C:C:N:M:+:4:.: :1:4:5:7:9:E:R:Y:I:A:D:F:J:L:Z:N:N:M:%:+:0:53:5L:G:9:R:R:.:H:I:A:S:-:K:K:X:C:M:0:%:+:.:0:1:3:5:8:9:W:R:U:O:P:D:G:H:X:X:C:B:M:-:1 :1G:A:5:9:9:%:S:R:U:I:$:F:F:J:K:C:-:B:M:%:-:.: :1:4:5:7:9:E:T:Y:O:A:S:J:J:K:Z:C:$:.+:.A:U:1:5:5:B:I:9:E:R:V:P:P:D:F:K:$:Z:C:B:$:%:+:.:0:1:3:5:8:Q:W:T:U:I:D:D:F:H:K:V:%M:%U:E:.:1:1:Z:R:5:8:9:L:Y:Y:O:P:F:V:H:K:Z:V:B:M:%:-:.: :1:4:6:7:Q:E:R:O:O:P:S:F:L:BC:BE:8:%:.:.:H:9:1:4:5:G:W:W:T:Y:P:L:S:F:H:L:Z:C:B:$:%:+:.:0:2:3:6:8:9:T:T:Y:I:P:G:ZK:Z8:4:B:%:%:S:5:.:0:1:A:7:7:Q:W:Y:G:I:P:S:G:H:K:Z:V:B:M:%:-:/: :2:4:5:Q:Q:W:R:Y:A:.+:%J:K9:T:M:I:%: :6: :W:3:5:T:W:Y:I:E:T:U:D:A:L:L:K:L:R:$:M:%:-:-:/:3:2:7:6:9:P:T:O


 3.  test-qr1441575932271.png


TU31Q:NX:/:JK7:Z:VVL:L9:*:3P:$K:2:X: 9:X:3%:AO:A :+:G:L:L:E:-:V:M:$:W:/:/:1:2:6:Y:8:Q:E:Y:U:O:A:F:G:J:L:C:B:N:%:+:-:1:1:2:4:6:W:UT:U+:M:A:G:G:8:$:L:C:V:7:*:*:.:/:2:W:4:6:8:W:E:T:U:P:A:D:G:K:Z:X:B:M:$:.:.:/:0:2:7:EQ:EM:C:U:A:A:4:V:G:K:L:3:N:N:%:*:/:7:0:2:4:7:8:Q:E:Y:U:O:A:F:H:J:Z:C:V:%:%:*:-:/:3:86:8C:K:E:U:U:0:L:A:F:G: :X:X:B:N:*:3:-:/:0:3:4:6:8:W:E:T:U:P:S:D:H:K:L:B:B:N:$:*: :42:4K:F:8:E:E:-:G:U:P:A:+:J:J:Z:X:N: :$:*:-: :0:2:4:7:8:Q:E:Y:I:O:S:F:G:Z:Z:X:V:N:+:0/:0F:P:4:8:8:$:A:E:Y:U:M:D:D:H:J:X:+:V:N:$:+:-:/:0:3:4:6:8:W:R:T:I:P:A:H:H:J:L:X:M:-*:-P:Y:0:4:4:V:U:8:W:E:C:O:O:S:D:J:M:L:X:V:M:$:*:-: :0:2:4:7:9:Q:R:Y:U:S:S:D:G:J:C:$N:$Y:W:-:0:0:L:E:4:7:8:K:T:T:I:O:D:C:G:J:L:C:V:N:$:+:-:/:0:3:5:6:9:W:E:I:I:O:A:D:K:VX:VW:7:$:-:-:G:8:0:3:4:F:Q:Q:R:T:O:K:A:D:G:K:L:X:V:M:$:*:-: :1:2:5:7:8:R:R:T:U:O:F:LJ:L7:3:V:$:$:A:4:-: :0:P:6:6:9:Q:T:F:U:O:A:F:G:J:L:C:V:N:$:+:.:/:1:3:4:9:9:Q:E:T:P:GD:G3: :L:V:V:U:0:$:+:-:Y:2:2:5:6:Q:P:E:T:U:P:A:D:G:K:L:X:V:M:%:*:.: :0:5:5:6:8:Q:Y:AO:A :+:G:L:L:E:-:V:M:$:W:/:/:1:2:6:Y:8:Q:E:Y:U:O:A:F:G:J:L:C:B:N:%:+:-:1:1:2:4:6:W:UT:U+:M:A:G:G:8:$:L:C:V:7:*:*:.:/:2:W:4:6:8:W:E:T:U:P:A:D:G:K:Z:X:B:M:$:.:.:/:0:2:7:EQ:EM:C:U:A:A:4:V:G:K:L:3:N:N:%:*:/:7:0:2:4:7:8:Q:E:Y:U:O:A:F:H:J:Z:C:V:%:%:*:-:/:3:86:8C:K:E:U:U:0:L:A:F:G: :X:X:B:N:*:3:-:/:0:3:4:6:8:W:E:T:U:P:S:D:H:K:L:B:B:N:$:*: :42:4K:F:8:E:E:-:G:U:P:A:+:J:J:Z:X:N: :$:*:-: :0:2:4:7:8:Q:E:Y:I:O:S:F:G:Z:Z:X:V:N:+:0/:0F:P:4:8:8:$:A:E:Y:U:M:D:D:H:J:X:+:V:N:$:+:-:/:0:3:4:6:8:W:R:T:I:P:A:H:H:J:L:X:M:-*:-P:Y:0:4:4:V:U:8:W:E:C:O:O:S:D:J:M:L:X:V:M:$:*:-: :0:2:4:7:9:Q:R:Y:U:S:S:D:G:J:C:$N:$Y:W:-:0:0:L:E:4:7:8:K:T:T:I:O:D:C:G:J:L:C:V:N:$:+:-:/:0:3:5:6:9:W:E:I:I:O:A:D:K:42:0B:NU:S:/:G:0:6:R:6:O:Q:E:S:O:D:G:P:S:F:Z:K:M:M:N:M:A: :/:0:3:3:5:Q:9:T:R:U:J:S:H

Gdzie: 

WE$ to wartość pola z pola numer 1 protokołu czyli 2048 w przykładzie 1

Odpowiednio w przykładzie numer 2: PA0 też oznacza wartość pola numer 1 z tego samego protokołu i też jest to 2048 ;)


Z trzecim przykładem tak samo... JK7 oznacza 2048





