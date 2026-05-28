

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

- System powinien umożliwiać przechowywanie informacji o pokojach hotelowych, takichjak numer pokoju, typ pokoju oraz maksymalna liczba osób.
- System powinien umożliwiać tworzenie nowych rezerwacji dla wybranego typu pokoju.
- System powinien umożliwiać określenie daty rozpoczęcia i zakończenia pobytu.
- System powinien umożliwiać zapisanie liczby osób przypisanych do rezerwacji.
- System powinien sprawdzać, czy liczba osób nie przekracza maksymalnej pojemności pokoju.
- System powinien umożliwiać sprawdzanie dostępności wybranego typu pokoju w wybranym terminie.
- System powinien umożliwiać sprawdzenie liczby dostępnych pokoi danego typu w
- podanym zakresie dat.
- System powinien uniemożliwiać przekroczenie liczby dostępnych pokoi danego typu w tym samym czasie.
- System powinien umożliwiać anulowanie rezerwacji.
- System powinien umożliwiać przeglądanie wszystkich rezerwacji.
- System powinien umożliwiać wyszukiwanie rezerwacji według typu pokoju lub zakresu dat.
- System powinien umożliwiać obsługę różnych statusów rezerwacji.
- System powinien umożliwiać zmianę statusu rezerwacji.
- System powinien umożliwiać zmianę statusu rezerwacji, np. na planowaną, rozpoczętą, zakończoną lub anulowaną.

## Funkcje systemu

Do głównych funkcji systemu będzie należało:

- Dodawanie danych pokojów,
- Przeglądanie listy pokojów,
- Tworzenie rezerwacji według typu pokoju,
- Określanie liczby pokoi oraz liczby osób,
- Określanie terminu pobytu,
- Sprawdzanie dostępności typu pokoju,
- Sprawdzanie liczby dostępnych pokoi danego typu w wybranych datach,
- Sprawdzanie konkretnych wolnych pokoi w danym terminie,
- Przypisywanie konkretnych pokoi do pozycji rezerwacji,
- Wyświetlanie listy wszystkich rezerwacji,
- Wyszukiwanie rezerwacji według typu pokoju lub dat,
- Anulowanie rezerwacji poprzez zmianę statusu,
- Wyświetlanie listy przypisanych pokoi do rezerwacji,
- Obsługa płatności za rezerwacje.


## Przykładowe przypadki użycia

### Przypadek użycia 1 – dodanie rezerwacji
Użytkownik wybiera typ pokoju, podaje liczbę pokoi, liczbę osób oraz daty pobytu. System sprawdza dostępność wybranego typu pokoju oraz czy liczba osób nie przekracza maksymalnej pojemności. Jeśli warunki są spełnione, system zapisuje rezerwację.

### Przypadek użycia 2 – sprawdzenie dostępności typu pokoju
Użytkownik wybiera typ pokoju oraz zakres dat, a system sprawdza liczbę dostępnych pokoi tego typu.

### Przypadek użycia 3 – sprawdzenie dostępnych pokoi
Użytkownik podaje datę przyjazdu i wyjazdu, a system wyświetla konkretne wolne pokoje w danym terminie.

### Przypadek użycia 4 – anulowanie rezerwacji
Użytkownik wybiera pozycję rezerwacji i przypisuje do niej konkretny pokój hotelowy.

### Przypadek użycia 5 – wyszukiwanie rezerwacji
Użytkownik wybiera istniejącą rezerwację i zmienia jej status na anulowaną. Anulowana rezerwacja nie jest uwzględniana przy sprawdzaniu dostępności.

### Przypadek użycia 6 – wyszukiwanie rezerwacji 
Użytkownik wyszukuje rezerwacje według typu pokoju, zakresu dat lub statusu.


# 3.	Projekt bazy danych

## Schemat bazy danych

(diagram (rysunek) przedstawiający schemat bazy danych) 

<img width="1205" height="728" alt="image" src="https://github.com/user-attachments/assets/b3a6412d-2550-452c-bcac-94364a882dff" />


## Opis poszczególnych tabel

(Dla każdej tabeli opis w formie tabelki)


Nazwa tabeli: (nazwa tabeli)
- Opis: (opis tabeli, komentarz)

### RoomTypes
Opis: Tabela przechowuje typy pokoi dostępnych w hotelu.
| Nazwa atrybutu | Typ           | Opis/Uwagi                                                                           |
| -------------- | ------------- | ------------------------------------------------------------------------------------ |
| RoomTypeID     | int (PK)      | Unikalny identyfikator typu pokoju                                                   |
| Name           | varchar(50)   | Nazwa typu pokoju                                                                    |
| MaxGuests      | int           | Maksymalna liczba gości                                                              |
| PricePerNight  | decimal(10,2) | Cena za jedną noc                                                                    |

Cena rezerwacji zależy od typu pokoju, liczby pokoi oraz liczby dni pobytu.

### HotelRooms
Opis: Tabela przechowuje informacje o konkretnych pokojach hotelowych.
| Nazwa atrybutu | Typ      | Opis/Uwagi                                     |
| -------------- | -------- | ---------------------------------------------- |
| RoomID         | int (PK) | Unikalny identyfikator pokoju                  |
| RoomNumber     | int      | Numer pokoju (unikalny)                        |
| RoomTypeID     | int (FK) | Odwołanie do tabeli RoomTypes                  |
| Floor          | int      | Piętro, na którym znajduje się pokój           |

### Guests
Opis: Tabela przechowuje dane gości hotelowych dokonujących rezerwacji.
| Nazwa atrybutu | Typ          | Opis/Uwagi                          |
| -------------- | ------------ | ----------------------------------- |
| GuestID        | int (PK)     | Unikalny identyfikator gościa       |
| FirstName      | varchar(50)  | Imię                                |
| LastName       | varchar(50)  | Nazwisko                            |
| Phone          | varchar(20)  | Numer telefonu (opcjonalny)         |
| Email          | varchar(100) | Adres e-mail (unikalny, opcjonalny) |

### BookingStatus
Opis: Tabela przechowuje możliwe statusy rezerwacji.
| Nazwa atrybutu | Typ         | Opis/Uwagi                                             |
| -------------- | ----------- | ------------------------------------------------------ |
| StatusID       | int (PK)    | Unikalny identyfikator statusu                         |
| Name           | varchar(20) | Nazwa statusu rezerwacji                               |

### Bookings
Opis: Tabela przechowuje informacje o rezerwacjach dokonywanych przez gości.

| Nazwa atrybutu | Typ      | Opis/Uwagi                                    |
| -------------- | -------- | --------------------------------------------- |
| BookingID      | int (PK) | Unikalny identyfikator rezerwacji             |
| GuestID        | int (FK) | Odwołanie do tabeli Guests                    |
| DateFrom       | date     | Data rozpoczęcia pobytu                       |
| DateTo         | date     | Data zakończenia pobytu                       |
| StatusID       | int (FK) | Odwołanie do tabeli BookingStatus             |
| BookingDate    | datetime | Data utworzenia rezerwacji                    |

### BookingRooms
Opis: Tabela przechowuje informacje o typach pokoi przypisanych do rezerwacji, ich liczbie oraz cenie.

| Nazwa atrybutu | Typ           | Opis/Uwagi                                    |
| -------------- | ------------- | --------------------------------------------- |
| BookingRoomID  | int (PK)      | Unikalny identyfikator pozycji rezerwacji     |
| BookingID      | int (FK)      | Odwołanie do tabeli Bookings                  |
| RoomTypeID     | int (FK)      | Odwołanie do tabeli RoomTypes                 |
| RoomsCount     | int           | Liczba zarezerwowanych pokoi danego typu      |
| GuestsCount    | int           | Liczba gości przypisana do danego typu pokoju |
| Price          | decimal(10,2) | Cena za daną pozycję rezerwacji               |

### Transactions
Opis: Tabela przechowuje informacje o płatnościach za rezerwacje.
| Nazwa atrybutu | Typ           | Opis/Uwagi                            |
| -------------- | ------------- | ------------------------------------- |
| TransactionID  | int (PK)      | Unikalny identyfikator transakcji     |
| BookingID      | int (FK)      | Odwołanie do tabeli Bookings          |
| Amount         | decimal(10,2) | Kwota płatności                       |
| PaymentDate    | datetime      | Data dokonania płatności              |
| Method         | varchar(50)   | Metoda płatności (np. karta, gotówka) |

### AssignedRooms
Opis: Tabela przechowuje przypisanie konkretnych pokoi hotelowych do pozycji rezerwacji.

| Nazwa atrybutu | Typ      | Opis/Uwagi                                |
| -------------- | -------- | ----------------------------------------- |
| AssignedRoomID | int (PK) | Unikalny identyfikator przypisania pokoju |
| BookingRoomID  | int (FK) | Odwołanie do tabeli BookingRooms          |
| RoomID         | int (FK) | Odwołanie do tabeli HotelRooms            |

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




