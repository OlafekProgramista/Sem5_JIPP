# Sem5_JIPP
Projekt zręcznościowej gry sprzętowej opartej na platformie Micro:bit, wyposażonej w system zapisywania wyników i globalny ranking.

```
@startuml
left to right direction

package "Warstwa Gry" {
  [Micro:bit - Gracz] as G1
}

package "Brama / Gateway" {
  [Micro:bit - Odbiornik] as Odbiornik
  [Arduino z Wi-Fi np. ESP32] as WiFi
}

package "Chmura / Backend" {
  database "Baza Danych (Firebase)" as DB
  [API serwera] as API
}

package "Prezentacja Wyników" {
  [Strona Web - Ranking] as WWW
  [Fizyczna Tablica - Arduino+LCD] as Fizyczny
}

G1 -.-> Odbiornik : Micro:bit Radio
Odbiornik --> WiFi : Kabel (UART)
WiFi -.-> API : Internet (HTTP POST)
API <--> DB
API -.-> WWW : Internet (HTTP GET)
API -.-> Fizyczny : Internet (HTTP GET)

@enduml
