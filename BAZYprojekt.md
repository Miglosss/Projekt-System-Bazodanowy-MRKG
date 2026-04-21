

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

np. lista wymagań, np. historyjki użytkownika, np. przypadki użycia itp.)

(System powinien umożliwiać przechowywanie informacji o pokojach hotelowych, takich jak numer pokoju, typ pokoju oraz maksymalna liczba osób.

System powinien umożliwiać tworzenie nowych rezerwacji dla wybranego pokoju.

System powinien umożliwiać określenie daty rozpoczęcia i zakończenia pobytu.

System powinien umożliwiać zapisanie liczby osób przypisanych do rezerwacji.

System powinien sprawdzać, czy liczba osób nie przekracza maksymalnej pojemności pokoju.

System powinien umożliwiać sprawdzanie dostępności konkretnego pokoju w wybranym terminie.

System powinien umożliwiać sprawdzenie, które pokoje są wolne w podanym zakresie dat.

System powinien uniemożliwiać dodanie dwóch rezerwacji tego samego pokoju w tym samym czasie.

System powinien umożliwiać anulowanie rezerwacji.

System powinien umożliwiać przeglądanie wszystkich rezerwacji.

System powinien umożliwiać wyszukiwanie rezerwacji według numeru pokoju lub zakresu dat.

System powinien zapewniać spójność danych oraz poprawne powiązania między tabelami.

System powinien umożliwiać dalszą rozbudowę systemu w przyszłości.

# 3.	Projekt bazy danych

## Schemat bazy danych

(diagram (rysunek) przedstawiający schemat bazy danych) 

## Opis poszczególnych tabel

(Dla każdej tabeli opis w formie tabelki)


Nazwa tabeli: (nazwa tabeli)
- Opis: (opis tabeli, komentarz)

| Nazwa atrybutu | Typ  | Opis/Uwagi |
|----------------|------|------------|
| Atrybut 1 …    |      |            |
| Atrybut 2 …    |      |            |


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




