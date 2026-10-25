# Sem5_JIPP
Projekt zręcznościowej gry sprzętowej opartej na platformie Micro:bit, wyposażonej w system zapisywania wyników i globalny ranking.


Architektura
```mermaid
graph LR
    subgraph Warstwa Gry
        G1[Micro:bit - Gracz]
    end

    subgraph Brama / Gateway
        Odbiornik[Micro:bit - Odbiornik]
        WiFi[Arduino z Wi-Fi np. ESP32]
    end

    subgraph Chmura / Backend
        API[API serwera]
        DB[(Baza Danych np. Firebase)]
    end

    subgraph Prezentacja Wyników
        Fizyczny[Fizyczna Tablica - Arduino+LCD]
        WWW[Strona Web - Ranking]
    end

    G1 -- "Micro:bit Radio" --> Odbiornik
    Odbiornik -- "Kabel (UART)" --> WiFi
    WiFi -- "Internet (HTTP POST)" --> API
    API <--> DB
    API -- "Internet (HTTP GET)" --> Fizyczny
    API -- "Internet (HTTP GET)" --> WWW
