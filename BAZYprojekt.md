

<!-- <style>
 p,li {
    font-size: 12pt;
  }
</style>  -->

<!-- <style>
 pre {
    font-size: 8pt;
  }
</style>  -->


---


**Temat:** (System do zarządzania rezerwacjami miejsc w hotelu)

**Autorzy:** (Mikołaj Rozwadowski, Kacper Gola)

--- 

# 1.  Zakres i krótki opis systemu

(np. Cel projektu, słowny opis realizowanego systemu systemu)

Celem projektu jest stworzenie bazy danych dla systemu hotelowego służącego do zarządzania rezerwacją miejsc noclegowych. System ma umożliwiać przechowywanie informacji o pokojach oraz rezerwacjach, z uwzględnieniem liczby osób przypisanych do danego pobytu.


# 2.	Wymagania i funkcje systemu

(np. lista wymagań, np. historyjki użytkownika, np. przypadki użycia itp.)

## Wymagania systemu

- System powinien umożliwiać przechowywanie informacji o pokojach hotelowych, takich jak numer pokoju, typ pokoju oraz maksymalna liczba osób.
- System powinien umożliwiać tworzenie nowych rezerwacji dla wybranego pokoju.
- System powinien umożliwiać określenie daty rozpoczęcia i zakończenia pobytu.
- System powinien umożliwiać zapisanie liczby osób przypisanych do rezerwacji.
- System powinien sprawdzać, czy liczba osób nie przekracza maksymalnej pojemności pokoju.
- System powinien umożliwiać sprawdzanie dostępności konkretnego pokoju w wybranym terminie.
- System powinien umożliwiać sprawdzenie, które pokoje są wolne w podanym zakresie dat.
- System powinien uniemożliwiać dodanie dwóch rezerwacji tego samego pokoju w tym samym czasie.
- System powinien umożliwiać anulowanie rezerwacji.
- System powinien umożliwiać przeglądanie wszystkich rezerwacji.
- System powinien umożliwiać wyszukiwanie rezerwacji według numeru pokoju lub zakresu dat.

## Funkcje systemu

Do głównych funkcji systemu będzie należało:

- dodawanie danych pokojów,
- przeglądanie listy pokojów,
- tworzenie rezerwacji według typu pokoju,
- określanie liczby pokoi oraz liczby osób,
- określanie terminu pobytu,
- sprawdzanie dostępności typu pokoju,
- sprawdzanie liczby dostępnych pokoi danego typu w wybranych datach,
- wyświetlanie listy wszystkich rezerwacji,
- wyszukiwanie rezerwacji według typu pokoju lub dat,
- anulowanie rezerwacji,
- wyświetlanie listy zajętych pokoi w danym terminie.


## Przykładowe przypadki użycia

### Przypadek użycia 1 – dodanie rezerwacji
Użytkownik wybiera pokój, podaje liczbę osób oraz daty pobytu. System sprawdza, czy pokój jest dostępny i czy liczba osób mieści się w jego pojemności. Jeśli warunki są spełnione, zapisuje rezerwację.

### Przypadek użycia 2 – sprawdzenie dostępności konkretnego pokoju
Użytkownik podaje numer pokoju oraz zakres dat, a system sprawdza, czy pokój jest wolny w tym terminie.

### Przypadek użycia 3 – sprawdzenie wolnych pokojów
Użytkownik podaje datę przyjazdu i wyjazdu, a system wyświetla listę wszystkich pokojów, które nie są zarezerwowane w podanym okresie.

### Przypadek użycia 4 – anulowanie rezerwacji
Użytkownik wybiera istniejącą rezerwację i zmienia jej status na anulowaną, dzięki czemu pokój staje się dostępny dla kolejnych rezerwacji.

### Przypadek użycia 5 – wyszukiwanie rezerwacji
Użytkownik wyszukuje rezerwacje według numeru pokoju lub zakresu dat.


# 3.	Projekt bazy danych

## Schemat bazy danych

(diagram (rysunek) przedstawiający schemat bazy danych) 



## Opis poszczególnych tabel

(Dla każdej tabeli opis w formie tabelki)


Nazwa tabeli: (nazwa tabeli)
- Opis: (opis tabeli, komentarz)

### RoomTypes
| Nazwa atrybutu | Typ            | Opis/Uwagi |
|----------------|----------------|------------|
| RoomTypeID     | int (PK)       | Unikalny identyfikator typu pokoju |
| Name           | varchar(50)    | Nazwa typu pokoju (Single, Double, Suite, Twin, Triple) |
| MaxGuests      | int            | Maksymalna liczba gości |
| PricePerNight  | decimal(10,2)  | Cena za jedną noc |

### HotelRooms
| Nazwa atrybutu | Typ         | Opis/Uwagi |
|----------------|-------------|------------|
| RoomID         | int (PK)    | Unikalny identyfikator pokoju |
| RoomNumber     | int         | Numer pokoju (unikalny) |
| RoomTypeID     | int (FK)    | Odwołanie do tabeli RoomTypes |
| Floor          | int         | Piętro, na którym znajduje się pokój |
| IsSmoking      | bit         | Czy pokój jest dla palących (1 = tak, 0 = nie) |

### Guests
| Nazwa atrybutu | Typ            | Opis/Uwagi |
|----------------|----------------|------------|
| GuestID        | int (PK)       | Unikalny identyfikator gościa |
| FirstName      | varchar(50)    | Imię |
| LastName       | varchar(50)    | Nazwisko |
| Phone          | varchar(20)    | Numer telefonu (opcjonalny) |
| Email          | varchar(100)   | Adres e-mail (unikalny, opcjonalny) |

### BookingStatus
| Nazwa atrybutu | Typ         | Opis/Uwagi |
|----------------|-------------|------------|
| StatusID       | int (PK)    | Unikalny identyfikator statusu |
| Name           | varchar(20) | Nazwa statusu (Active, Cancelled, Completed) |

### Bookings
| Nazwa atrybutu | Typ         | Opis/Uwagi |
|----------------|-------------|------------|
| BookingID      | int (PK)    | Unikalny identyfikator rezerwacji |
| GuestID        | int (FK)    | Odwołanie do tabeli Guests |
| DateFrom       | date        | Data rozpoczęcia pobytu |
| DateTo         | date        | Data zakończenia pobytu |
| StatusID       | int (FK)    | Odwołanie do tabeli BookingStatus |

### BookingRooms
| Nazwa atrybutu | Typ         | Opis/Uwagi |
|----------------|-------------|------------|
| BookingRoomID  | int (PK)    | Unikalny identyfikator przypisania pokoju |
| BookingID      | int (FK)    | Odwołanie do tabeli Bookings |
| RoomID         | int (FK)    | Odwołanie do tabeli HotelRooms |
| GuestsCount    | int         | Liczba gości w danym pokoju |

### Transactions
| Nazwa atrybutu | Typ            | Opis/Uwagi |
|----------------|----------------|------------|
| TransactionID  | int (PK)       | Unikalny identyfikator transakcji |
| BookingID      | int (FK)       | Odwołanie do tabeli Bookings |
| Amount         | decimal(10,2)  | Kwota płatności |
| PaymentDate    | datetime       | Data dokonania płatności |
| Method         | varchar(50)    | Metoda płatności (karta, gotówka) |


# 4.	Implementacja

## Kod poleceń DDL

(dla każdej tabeli należy wkleić kod DDL polecenia tworzącego tabelę)

```sql
create table tab1 (
   a int,
   b varchar(10)
)
```

## Widoki

(dla każdego widoku należy wkleić kod polecenia definiującego widok wraz z komentarzem)


## Procedury/funkcje

(dla każdej procedury/funkcji należy wkleić kod polecenia definiującego procedurę wraz z komentarzem)

## Triggery

(dla każdego triggera należy wkleić kod polecenia definiującego trigger wraz z komentarzem)




