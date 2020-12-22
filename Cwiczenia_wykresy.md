## Ćwiczenia na wykresach

_**Opis pracy nad wykresami w Jupyterze**_

1. Zaczynam od zaimportowania bibliotek
```
import matplotlib.pyplot as plt
from collections import Counter
import pandas as pd 
import numpy as np
```
Teraz przywołuję plik z danymi i je wyświetlam w całości
(wymyślone dane jakiejś firmy, które wpisałem do pliku Excel i zapisałem z rozszerzeniem .csv)
```
dane=pd.read_csv(r'C:\Users\Dell\Desktop\wyniki.csv')
print(dane)
```

Lp.| rok  |  zysk | strata
--|------|-------|-------
0 | 2000 | 634883|   5445
1 | 2001 | 924897| 887258
2 | 2002 |  82799|   9054
3 | 2003 | 765272|    983
4 | 2004 |  89235|  76367
5 | 2005 |  56143|    775
6 | 2006 |  93427|  75454
7 | 2007 | 642554|    776
8 | 2008 | 923476|  98343
9 | 2009 | 490342|  54455
10| 2010 |  34348|   7767
11| 2011 | 561498|   8858
12| 2012 |3434889|   6225
13| 2013 |7776670| 232525
14| 2014 | 342008|  98998
15| 2015 |  71400|  44422
16| 2016 |  73465|  87658
17| 2017 | 653878|   7634
18| 2018 | 198922|  76682
19| 2019 | 676722|  88686
20| 2020 |8023762|  92642

dla wygody pokazuję teraz tylko pierwsze pięć rzędów korzystając z funkcji _head_
```
dane.head()
```
Lp.| rok  |  zysk | strata
--|------|-------|-------
0 | 2000 | 634883|   5445
1 | 2001 | 924897| 887258
2 | 2002 |  82799|   9054
3 | 2003 | 765272|    983
4 | 2004 |  89235|  76367

2. Następnie tworzę ciąg zmiennych z poszczególnych kolumn tabeli
```
rok=dane.rok
zysk=dane.zysk
strata=dane.strata
```
Teraz zamiana danych o latach z liczb na tekst (żeby ich użyć jako etykiet na wykresie)
```
rok=rok.to_list()
```
3. Tworzę teraz własną funkcję do rysowania wykresu liniowego
```
def wykres_liniowy():
    plt.plot(rok, zysk, color='blue', marker='x', linestyle='solid')
    
    #tytuły obu osi
    plt.xlabel('lata')
    plt.ylabel('zysk')
    
    #typ skali osi pionowej
    plt.yscale('linear')
    
    #obrócenie etykiet osi x o 90 stopni
    plt.xticks(rotation=90)
    
    #wywołanie wyświetlenia wykresu
    plt.show()
```
Teraz wywołuję funkcję _wykres_liniowy_
```
wykres_liniowy()
```
4. Kolejny krok to próba wykonania obliczeń na kolumnach (policzenie zysku netto)
```
zysk_netto = zysk - strata
```
Tworzę funkcję rysującą wykres złożony - z kilkoma seriami danych
```
def wykres_zlozony():

    plt.plot(rok, zysk,     'g-',  label='zysk')            # zielona linia ciągła
    plt.plot(rok, strata, 'r-.', label='strata')            # czerwona przerywana linia
    plt.plot(rok, zysk_netto,  'b:',  label='zysk netto')   # niebieska kropkowana linia


    plt.legend(loc=9)   # położenie legendy na środku wykresu
    plt.xlabel("rok")
    plt.xticks(rotation=90)
    plt.show()
 ```
 I już mogę wywołać funkcję rysującą wykres:
 ```
 wykres_zlozony()
 ```
 5. Kolejny etap to wykres kolumnowy, 
 ale dla jego czytelności skupię się na danych z ostatnich pięciu lat,
 co będzie zawarte dzięki wyeksportowaniu nowej listy:
 ```
ostatnie_lata=rok[-5:]      # [-5:] oznacza pięć ostatnich elementów z listy
print(ostatnie_lata)
```
>['2016', '2017', '2018', '2019', '2020']

Stworzenie funkcji tworzenia wykresu kolumnowego z etykietami:
```
def wykres_kolumnowy():
    # ponieważ kolumny/słupki mają domyślną szerokość 0.8, dodając 0.5 do ich współrzędnych 
    # wtedy każdy słupek będzie bardziej pośrodku etykiety
    xs = [i + 0.5 for i, _ in enumerate(rok)]

    # rysowanie słupków o współrzędnych [xs], i wysokości [zysk_netto]
    plt.bar(xs, zysk_netto)
    plt.ylabel("zysk netto")

    # ustawienie położenia etykiet poszczególnych słupków
    plt.xticks([i + 0.5 for i, _ in enumerate(rok)], rok)
    plt.xticks(rotation=90)
    #wyświetlenie wykresu
    plt.show()
```
![wykres kolumnowy](C:\Users\Dell\Desktop\Markdown\wykres_kolumnowy.png)
