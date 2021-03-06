# Distributed monitor for study project - algorytm Suzuki-Kasami
Rozproszony monitor

Właściwa biblioteka znajduje się w pliku sk.py

## Requirements
- Python 3
- ZeroMQ library (pip install zmq)


### Examples/Przykłady

#### Program producent.py
Program generuje liczby i dokłada je do współdzielonej listy. Po wygenerowaniu 20 liczb kończy swoje działanie.

Parametry:
1. Służy do oznaczenia, który węzeł jako pierwszy będzie miał token. 1 oznacza token.
2. Adres i port bieżącego węzła.
3. i następne to adresy innych węzłów

#### Program konsument.py
Program pobiera ze wspóldzielonej listy liczby i wyświetla je. Po 5 nieudanych próbach (lista jest pusta) pobrania liczby kończy swoje działanie.

Parametry:
1. Adres i port bieżącego węzła
2. i następne to adresy innych węzłów

#### Konfiguracja systemu producent-konsument dla 2 producentów i 2 konsumentów
Każdy z węzłów nasłuchuje na swoim porcie i adresie 127.0.0.1

- python3 producent.py 1 127.0.0.1:2222 127.0.0.1:3333 127.0.0.1:4444 127.0.0.1:5555
- python3 producent.py 0 127.0.0.1:3333 127.0.0.1:2222 127.0.0.1:4444 127.0.0.1:5555
- python3 konsument.py 127.0.0.1:4444 127.0.0.1:5555 127.0.0.1:2222 127.0.0.1:3333
- python3 konsument.py 127.0.0.1:5555 127.0.0.1:4444 127.0.0.1:2222 127.0.0.1:3333

##### Uruchomienie
Każdy z węzłów czeka na uruchomienie wszystkich innych. Jako ostatni uruchomiony musi być węzeł, który pierwszy będzie miał token.
