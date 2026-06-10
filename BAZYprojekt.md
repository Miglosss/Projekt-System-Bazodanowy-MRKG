

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

Celem projektu jest stworzenie bazy danych dla systemu hotelowego służącego do zarządzania rezerwacjami miejsc noclegowych. System umożliwia zarządzanie pokojami hotelowymi, rezerwacjami, przypisywaniem konkretnych pokoi, obsługą statusów rezerwacji oraz rejestrowaniem płatności.


# 2.	Wymagania i funkcje systemu

(np. lista wymagań, np. historyjki użytkownika, np. przypadki użycia itp.)

## Wymagania systemu

- System powinien umożliwiać przechowywanie informacji o pokojach hotelowych, takich jak numer pokoju, typ pokoju oraz maksymalna liczba osób.
- System powinien umożliwiać tworzenie nowych rezerwacji dla wybranego typu pokoju.
- System powinien umożliwiać określenie daty rozpoczęcia i zakończenia pobytu.
- System powinien umożliwiać zapisanie liczby osób przypisanych do rezerwacji.
- System powinien sprawdzać, czy liczba osób nie przekracza maksymalnej pojemności pokoju.
- System powinien umożliwiać sprawdzenie liczby dostępnych pokoi danego typu w podanym zakresie dat.
- System powinien uniemożliwiać przekroczenie liczby dostępnych pokoi danego typu w tym samym czasie.
- System powinien umożliwiać przeglądanie wszystkich rezerwacji.
- System powinien umożliwiać wyszukiwanie rezerwacji według typu pokoju lub zakresu dat.
- System powinien umożliwiać obsługę różnych statusów rezerwacji.
- System powinien umożliwiać zmianę statusu rezerwacji, np. na Planowaną, Rozpoczętą, Zakończoną lub Anulowaną.
- System umożliwia dodawanie płatności do rezerwacji.
- System umożliwia sprawdzanie sumy wpłat dla rezerwacji.
- System automatycznie oblicza koszt rezerwacji.
- System sprawdza dostępność pokoi w wybranym terminie.
- System blokuje rezerwacje z niepoprawnymi datami.
- System blokuje przypisanie tego samego pokoju do dwóch aktywnych rezerwacji w tym samym terminie.
- System kontroluje, czy liczba gości nie przekracza maksymalnej pojemności pokoju.

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

### Przypadek użycia 4 – przypisanie pokoju
Użytkownik wybiera pozycję rezerwacji i przypisuje do niej konkretny pokój hotelowy. Dzięki temu system wie, w którym pokoju zostanie zakwaterowany gość.

### Przypadek użycia 5 – anulowanie rezerwacji
Użytkownik wybiera rezerwację i zmienia jej status na anulowaną. Rezerwacja pozostaje w bazie jako historia, ale nie jest brana pod uwagę przy sprawdzaniu dostępności.

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
| Nazwa atrybutu | Typ           | Opis/Uwagi                          |
| -------------- | ------------- | ----------------------------------- |
| RoomTypeID     | int (PK)      | Unikalny identyfikator typu pokoju  |
| Name           | varchar(50)   | Nazwa typu pokoju                   |
| MaxGuests      | int           | Maksymalna liczba gości             |
| PricePerNight  | decimal(10,2) | Cena za jedną noc                   |

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

Statusy rezerwacji pozwalają określić aktualny stan rezerwacji, np. planowana, rozpoczęta, zakończona lub anulowana. Dzięki temu system może poprawnie obsługiwać dostępność pokoi oraz historię rezerwacji.

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
Opis: Tabela przechowuje informacje o typach pokoi przypisanych do rezerwacji, ich liczbie oraz cenie. Przechowuje informację o tym, jaki typ pokoju został zarezerwowany oraz w jakiej liczbie.

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
Przechowuje ona dopiero konkretne pokoje przypisane do rezerwacji, np. pokój numer 103. Dzięki temu system działa podobnie do rzeczywistego hotelu, gdzie najpierw rezerwuje się typ pokoju, a konkretny numer pokoju można przypisać później.

| Nazwa atrybutu | Typ      | Opis/Uwagi                                |
| -------------- | -------- | ----------------------------------------- |
| AssignedRoomID | int (PK) | Unikalny identyfikator przypisania pokoju |
| BookingRoomID  | int (FK) | Odwołanie do tabeli BookingRooms          |
| RoomID         | int (FK) | Odwołanie do tabeli HotelRooms            |

# 4.	Implementacja

## Kod poleceń DDL

(dla każdej tabeli należy wkleić kod DDL polecenia tworzącego tabelę)

### RoomTypes
```sql
CREATE TABLE RoomTypes (
    RoomTypeID INT IDENTITY(1,1) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    MaxGuests INT NOT NULL,
    PricePerNight DECIMAL(10,2) NOT NULL
);
```

### HotelRooms
```sql
CREATE TABLE HotelRooms (
    RoomID INT IDENTITY(1,1) PRIMARY KEY,
    RoomNumber INT NOT NULL UNIQUE,
    RoomTypeID INT NOT NULL,
    Floor INT NOT NULL,
    CONSTRAINT FK_HotelRooms_RoomTypes
        FOREIGN KEY (RoomTypeID) REFERENCES RoomTypes(RoomTypeID)
);
```

### Guests
```sql
CREATE TABLE Guests (
    GuestID INT IDENTITY(1,1) PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Phone VARCHAR(20),
    Email VARCHAR(100) UNIQUE
);
```

### BookingStatus
```sql
CREATE TABLE BookingStatus (
    StatusID INT IDENTITY(1,1) PRIMARY KEY,
    Name VARCHAR(20) NOT NULL
);
```

### Bookings
```sql
CREATE TABLE Bookings (
    BookingID INT IDENTITY(1,1) PRIMARY KEY,
    GuestID INT NOT NULL,
    DateFrom DATE NOT NULL,
    DateTo DATE NOT NULL,
    StatusID INT NOT NULL,
    BookingDate DATETIME NOT NULL DEFAULT GETDATE(),
    CONSTRAINT FK_Bookings_Guests
        FOREIGN KEY (GuestID) REFERENCES Guests(GuestID),
    CONSTRAINT FK_Bookings_BookingStatus
        FOREIGN KEY (StatusID) REFERENCES BookingStatus(StatusID)
);
```

### BookingRooms
```sql
CREATE TABLE BookingRooms (
    BookingRoomID INT IDENTITY(1,1) PRIMARY KEY,
    BookingID INT NOT NULL,
    RoomTypeID INT NOT NULL,
    RoomsCount INT NOT NULL,
    GuestsCount INT NOT NULL,
    Price DECIMAL(10,2) NOT NULL,
    CONSTRAINT FK_BookingRooms_Bookings
        FOREIGN KEY (BookingID) REFERENCES Bookings(BookingID),
    CONSTRAINT FK_BookingRooms_RoomTypes
        FOREIGN KEY (RoomTypeID) REFERENCES RoomTypes(RoomTypeID)
);
```

### AssignedRooms
```sql
CREATE TABLE AssignedRooms (
    AssignedRoomID INT IDENTITY(1,1) PRIMARY KEY,
    BookingRoomID INT NOT NULL,
    RoomID INT NOT NULL,
    CONSTRAINT FK_AssignedRooms_BookingRooms
        FOREIGN KEY (BookingRoomID) REFERENCES BookingRooms(BookingRoomID),
    CONSTRAINT FK_AssignedRooms_HotelRooms
        FOREIGN KEY (RoomID) REFERENCES HotelRooms(RoomID)
);
```

### Transactions
```sql
CREATE TABLE Transactions (
    TransactionID INT IDENTITY(1,1) PRIMARY KEY,
    BookingID INT NOT NULL,
    Amount DECIMAL(10,2) NOT NULL,
    PaymentDate DATETIME NOT NULL,
    Method VARCHAR(50) NOT NULL,
    CONSTRAINT FK_Transactions_Bookings
        FOREIGN KEY (BookingID) REFERENCES Bookings(BookingID)
);
```

## Widoki

(dla każdego widoku należy wkleić kod polecenia definiującego widok wraz z komentarzem)

### View_BookingDetails

Widok prezentuje szczegółowe informacje dotyczące rezerwacji oraz powiązanych z nimi pokoi. Ułatwia analizę danych rezerwacyjnych bez konieczności wykonywania wielu połączeń między tabelami.

```sql
CREATE VIEW View_BookingDetails AS
SELECT 
    b.BookingID,
    g.FirstName,
    g.LastName,
    rt.Name AS RoomType,
    br.RoomsCount,
    br.GuestsCount,
    br.Price,
    b.DateFrom,
    b.DateTo,
    bs.Name AS Status
FROM BookingRooms br
JOIN Bookings b ON br.BookingID = b.BookingID
JOIN Guests g ON b.GuestID = g.GuestID
JOIN RoomTypes rt ON br.RoomTypeID = rt.RoomTypeID
JOIN BookingStatus bs ON b.StatusID = bs.StatusID;
GO
```
Uruchomienie
```
SELECT * FROM View_BookingDetails;
```

### View_RoomTypeAvailabilitySummary

Widok przedstawia informacje o dostępnych typach pokoi w hotelu. Pozwala szybko sprawdzić liczbę pokoi danego typu, ich pojemność oraz ceny.

```sql
CREATE VIEW View_RoomTypeAvailabilitySummary AS
SELECT
    rt.RoomTypeID,
    rt.Name AS RoomType,
    rt.MaxGuests,
    rt.PricePerNight,
    COUNT(hr.RoomID) AS TotalRooms
FROM RoomTypes rt
LEFT JOIN HotelRooms hr ON rt.RoomTypeID = hr.RoomTypeID
GROUP BY rt.RoomTypeID, rt.Name, rt.MaxGuests, rt.PricePerNight;
GO
```
Uruchomienie
```
SELECT * FROM View_RoomTypeAvailabilitySummary;
```

### View_AssignedRoomsDetails

Widok pokazuje konkretne pokoje przypisane do poszczególnych rezerwacji. Może być wykorzystywany przez recepcję podczas meldowania gości oraz zarządzania zajętością pokoi.

```sql
CREATE VIEW View_AssignedRoomsDetails AS
SELECT 
    ar.AssignedRoomID,
    b.BookingID,
    br.BookingRoomID,
    hr.RoomNumber,
    rt.Name AS RoomType,
    g.FirstName,
    g.LastName,
    b.DateFrom,
    b.DateTo,
    bs.Name AS Status
FROM AssignedRooms ar 
JOIN BookingRooms br ON ar.BookingRoomID = br.BookingRoomID
JOIN Bookings b ON br.BookingID = b.BookingID
JOIN Guests g ON b.GuestID = g.GuestID
JOIN HotelRooms hr ON ar.RoomID = hr.RoomID
JOIN RoomTypes rt ON hr.RoomTypeID = rt.RoomTypeID
JOIN BookingStatus bs ON b.StatusID = bs.StatusID;
GO
```
Uruchomienie
```
SELECT * FROM View_AssignedRoomsDetails;
```

### View_PaymentSummary

Widok przedstawia informacje dotyczące rozliczeń rezerwacji. Pozwala sprawdzić wartość rezerwacji, dokonane wpłaty oraz pozostałą kwotę do zapłaty.

```sql
CREATE VIEW View_PaymentSummary AS
SELECT 
    b.BookingID,
    g.FirstName,
    g.LastName,
    SUM(br.Price) AS BookingValue,
    ISNULL(SUM(t.Amount), 0) AS PaidAmount,
    SUM(br.Price) - ISNULL(SUM(t.Amount), 0) AS AmountLeft
FROM Bookings b
JOIN Guests g ON b.GuestID = g.GuestID
JOIN BookingRooms br ON b.BookingID = br.BookingID
LEFT JOIN Transactions t ON b.BookingID = t.BookingID
GROUP BY b.BookingID, g.FirstName, g.LastName;
GO
```
Uruchomienie
```
SELECT * FROM View_PaymentSummary;
```

## Procedury

(dla każdej procedury/funkcji należy wkleić kod polecenia definiującego procedurę wraz z komentarzem)



### AddBooking

Procedura służy do tworzenia nowych rezerwacji w systemie. Sprawdza dostępność pokoi oraz weryfikuje poprawność liczby gości przed zapisaniem danych.

```sql
CREATE PROCEDURE AddBooking
    @GuestID INT,
    @RoomTypeID INT,
    @RoomsCount INT,
    @GuestsCount INT,
    @DateFrom DATE,
    @DateTo DATE
AS
BEGIN
    DECLARE @MaxGuests INT;
    DECLARE @PricePerNight DECIMAL(10,2);
    DECLARE @AvailableRooms INT;
    DECLARE @BookingID INT;

    SELECT 
        @MaxGuests = MaxGuests,
        @PricePerNight = PricePerNight
    FROM RoomTypes
    WHERE RoomTypeID = @RoomTypeID;

    SELECT @AvailableRooms = COUNT(*)
    FROM HotelRooms
    WHERE RoomTypeID = @RoomTypeID;

    SELECT @AvailableRooms = @AvailableRooms - ISNULL(SUM(br.RoomsCount), 0)
    FROM BookingRooms br
    JOIN Bookings b ON br.BookingID = b.BookingID
    WHERE br.RoomTypeID = @RoomTypeID
      AND b.DateFrom < @DateTo
      AND b.DateTo > @DateFrom
      AND b.StatusID <> 4;

    IF @GuestsCount > (@MaxGuests * @RoomsCount)
    BEGIN
        RAISERROR('Liczba gości przekracza maksymalną pojemność.', 16, 1);
        RETURN;
    END;

    IF @RoomsCount > @AvailableRooms
    BEGIN
        RAISERROR('Brak wystarczającej liczby wolnych pokoi.', 16, 1);
        RETURN;
    END;

    INSERT INTO Bookings (GuestID, DateFrom, DateTo, StatusID, BookingDate)
    VALUES (@GuestID, @DateFrom, @DateTo, 1, GETDATE());

    SET @BookingID = SCOPE_IDENTITY();

    INSERT INTO BookingRooms (BookingID, RoomTypeID, RoomsCount, GuestsCount, Price)
    VALUES (
        @BookingID,
        @RoomTypeID,
        @RoomsCount,
        @GuestsCount,
        @PricePerNight * @RoomsCount * DATEDIFF(DAY, @DateFrom, @DateTo)
    );
END;
GO
```
Uruchomienie
```
EXEC AddBooking 1, 2, 1, 2, '2026-06-10', '2026-06-13';
```

System zakłada, że status „Anulowana” posiada identyfikator StatusID = 4, dlatego takie rezerwacje nie są uwzględniane podczas obliczania dostępności.


### CheckFreeRooms

Procedura umożliwia sprawdzenie dostępnych pokoi w określonym terminie. Uwzględnia istniejące rezerwacje oraz pomija rezerwacje anulowane.

```sql
CREATE PROCEDURE CheckFreeRooms
    @DateFrom DATE,
    @DateTo DATE,
    @RoomTypeID INT = NULL
AS
BEGIN
    SELECT 
        hr.RoomID,
        hr.RoomNumber,
        rt.Name AS RoomType,
        hr.Floor
    FROM HotelRooms hr
    JOIN RoomTypes rt ON hr.RoomTypeID = rt.RoomTypeID
    WHERE (@RoomTypeID IS NULL OR hr.RoomTypeID = @RoomTypeID)
      AND hr.RoomID NOT IN (
          SELECT ar.RoomID
          FROM AssignedRooms ar
          JOIN BookingRooms br ON ar.BookingRoomID = br.BookingRoomID
          JOIN Bookings b ON br.BookingID = b.BookingID
          WHERE b.DateFrom < @DateTo
            AND b.DateTo > @DateFrom
            AND b.StatusID <> 4
      );
END;
GO
```
Uruchomienie
```
EXEC CheckFreeRooms '2026-06-10', '2026-06-13', 2;
```

### AssignRoom

Procedura przypisuje konkretny pokój hotelowy do wcześniej utworzonej rezerwacji. Pozwala przejść od rezerwacji typu pokoju do przypisania fizycznego numeru pokoju. Sama procedura wykonuje prostą operację dodania danych, natomiast poprawność przypisania kontroluje trigger, który blokuje przypisanie zajętego pokoju w tym samym terminie.

```sql
CREATE PROCEDURE AssignRoom
    @BookingRoomID INT,
    @RoomID INT
AS
BEGIN
    INSERT INTO AssignedRooms (BookingRoomID, RoomID)
    VALUES (@BookingRoomID, @RoomID);
END;
GO
```
Uruchomienie
```
EXEC AssignRoom 1, 3;
```

### ChangeBookingStatus

Procedura umożliwia zmianę statusu istniejącej rezerwacji. Dzięki niej można oznaczać rezerwacje jako aktywne, zakończone lub anulowane.

```sql
CREATE PROCEDURE ChangeBookingStatus
    @BookingID INT,
    @StatusID INT
AS
BEGIN
    UPDATE Bookings
    SET StatusID = @StatusID
    WHERE BookingID = @BookingID;
END;
GO
```
Uruchomienie
```
EXEC ChangeBookingStatus 1, 2;
```

Rezerwacje oznaczone jako anulowane nie są uwzględniane przy sprawdzaniu dostępności pokoi, jednak pozostają zapisane w systemie jako dane historyczne.


### AddPayment

Procedura dodaje informacje o płatności do konkretnej rezerwacji. Automatycznie zapisuje kwotę, metodę płatności oraz datę wykonania transakcji.

```sql
CREATE PROCEDURE AddPayment
    @BookingID INT,
    @Amount DECIMAL(10,2),
    @Method VARCHAR(50)
AS
BEGIN
    INSERT INTO Transactions (BookingID, Amount, PaymentDate, Method)
    VALUES (@BookingID, @Amount, GETDATE(), @Method);
END;
GO
```
Uruchomienie
```
EXEC AddPayment 1, 500.00, 'Karta';
```

## Funkcje

### GetTotalRoomsByType

Funkcja zwraca całkowitą liczbę pokoi wybranego typu. Może być wykorzystywana podczas analizowania struktury hotelu lub raportowania.

```sql
CREATE FUNCTION GetTotalRoomsByType
(
    @RoomTypeID INT
)
RETURNS INT
AS
BEGIN
    DECLARE @Count INT;

    SELECT @Count = COUNT(*)
    FROM HotelRooms
    WHERE RoomTypeID = @RoomTypeID;

    RETURN @Count;
END;
GO
```
Uruchomienie
```
SELECT dbo.GetTotalRoomsByType(2);
```

### GetAvailableRoomsByType

Funkcja oblicza liczbę dostępnych pokoi określonego typu w wybranym terminie. Ułatwia szybkie sprawdzanie dostępności podczas procesu rezerwacji.

```sql
CREATE FUNCTION GetAvailableRoomsByType
(
    @RoomTypeID INT,
    @DateFrom DATE,
    @DateTo DATE
)
RETURNS INT
AS
BEGIN
    DECLARE @TotalRooms INT;
    DECLARE @ReservedRooms INT;

    SELECT @TotalRooms = COUNT(*)
    FROM HotelRooms
    WHERE RoomTypeID = @RoomTypeID;

    SELECT @ReservedRooms = ISNULL(SUM(br.RoomsCount), 0)
    FROM BookingRooms br
    JOIN Bookings b ON br.BookingID = b.BookingID
    WHERE br.RoomTypeID = @RoomTypeID
      AND b.DateFrom < @DateTo
      AND b.DateTo > @DateFrom
      AND b.StatusID <> 4;

    RETURN @TotalRooms - @ReservedRooms;
END;
GO
```
Uruchomienie
```
SELECT dbo.GetAvailableRoomsByType(2, '2026-07-01', '2026-07-05');
```

### CalculateBookingPrice

Funkcja automatycznie wylicza koszt rezerwacji na podstawie liczby pokoi, liczby nocy oraz ceny pokoju. Pozwala uniknąć ręcznego obliczania kosztów.

```sql
CREATE FUNCTION CalculateBookingPrice
(
    @RoomTypeID INT,
    @RoomsCount INT,
    @DateFrom DATE,
    @DateTo DATE
)
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @PricePerNight DECIMAL(10,2);

    SELECT @PricePerNight = PricePerNight
    FROM RoomTypes
    WHERE RoomTypeID = @RoomTypeID;

    RETURN @PricePerNight * @RoomsCount * DATEDIFF(DAY, @DateFrom, @DateTo);
END;
GO
```
Uruchomienie
```
SELECT dbo.CalculateBookingPrice(2, 1, '2026-06-10', '2026-06-13');
```

### GetPaidAmountForBooking

Funkcja zwraca sumę wszystkich wpłat wykonanych dla wybranej rezerwacji. Może być wykorzystywana podczas kontroli rozliczeń z gośćmi.


```sql
CREATE FUNCTION GetPaidAmountForBooking
(
    @BookingID INT
)
RETURNS DECIMAL(10,2)
AS
BEGIN
    DECLARE @PaidAmount DECIMAL(10,2);

    SELECT @PaidAmount = ISNULL(SUM(Amount), 0)
    FROM Transactions
    WHERE BookingID = @BookingID;

    RETURN @PaidAmount;
END;
GO
```
Uruchomienie
```
SELECT dbo.GetPaidAmountForBooking(1);
```

## Triggery

(dla każdego triggera należy wkleić kod polecenia definiującego trigger wraz z komentarzem)

### trg_CheckBookingDates
 
Trigger kontroluje poprawność dat rezerwacji podczas dodawania lub edycji danych. Blokuje rezerwacje z błędnymi terminami, datami z przeszłości oraz zbyt odległymi terminami.

```sql
CREATE TRIGGER trg_CheckBookingDates
ON Bookings
AFTER INSERT, UPDATE
AS
BEGIN
    IF EXISTS (
        SELECT 1
        FROM inserted
        WHERE DateFrom < CAST(GETDATE() AS DATE)
           OR DateTo <= DateFrom
           OR DateFrom > DATEADD(YEAR, 2, CAST(GETDATE() AS DATE))
           OR DateTo > DATEADD(YEAR, 2, CAST(GETDATE() AS DATE))
    )
    BEGIN
        RAISERROR('Nie można utworzyć rezerwacji z błędnymi datami.', 16, 1);
        ROLLBACK TRANSACTION;
    END;
END;
GO
```

### trg_PreventAssignedRoomConflict
 
Trigger zabezpiecza system przed przypisaniem tego samego pokoju do kilku aktywnych rezerwacji jednocześnie. Dzięki temu zapobiega występowaniu overbookingu pokoi.

```sql
CREATE TRIGGER trg_PreventAssignedRoomConflict
ON AssignedRooms
AFTER INSERT
AS
BEGIN
    IF EXISTS (
        SELECT 1
        FROM inserted i
        JOIN BookingRooms br1 ON i.BookingRoomID = br1.BookingRoomID
        JOIN Bookings b1 ON br1.BookingID = b1.BookingID
        JOIN AssignedRooms ar2 ON i.RoomID = ar2.RoomID
        JOIN BookingRooms br2 ON ar2.BookingRoomID = br2.BookingRoomID
        JOIN Bookings b2 ON br2.BookingID = b2.BookingID
        WHERE i.AssignedRoomID <> ar2.AssignedRoomID
          AND b1.DateFrom < b2.DateTo
          AND b1.DateTo > b2.DateFrom
          AND b1.StatusID <> 4
          AND b2.StatusID <> 4
    )
    BEGIN
        RAISERROR('Ten pokój jest już przypisany w wybranym terminie.', 16, 1);
        ROLLBACK TRANSACTION;
    END;
END;
GO
```

### trg_CheckGuestsLimit

Trigger kontroluje, czy liczba gości nie przekracza maksymalnej pojemności zarezerwowanych pokoi. Zapewnia spójność danych oraz poprawność rezerwacji.

```sql
CREATE TRIGGER trg_CheckGuestsLimit
ON BookingRooms
AFTER INSERT, UPDATE
AS
BEGIN
    IF EXISTS (
        SELECT 1
        FROM inserted i
        JOIN RoomTypes rt ON i.RoomTypeID = rt.RoomTypeID
        WHERE i.GuestsCount > (rt.MaxGuests * i.RoomsCount)
    )
    BEGIN
        RAISERROR('Liczba gości przekracza maksymalną pojemność pokoi.', 16, 1);
        ROLLBACK TRANSACTION;
    END;
END;
GO
```


