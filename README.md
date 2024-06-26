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

<style>
		.page-break-before {
            page-break-before: always;
        }

        .page-break-after {
            page-break-after: always;
        }
</style>

**Temat:**
System bazy danych krwiodawstwa

**Autorzy:**

Filip Przepiórka
Wiktor Piotrowski

---

# 1. Zakres i opis systemu

Projekt ma na celu stworzenie systemu krwiodawstwa. W projektowanej bazie danych będą rejestrowane wszelkie informacje wymagane do poprawnego funkcjonowania systemu krwiodawstwa. Wszystkie rekordy będą odpowiednio zapisywane w utworzonych tabelach pod unikalnymi wierszami. Dodatkowo w systemie są zaimplementowane funkcje, widoki oraz procedury, mające na celu ułatwienie czynności związanych z obsługą systemu oraz prowadzeniem analizy danych.

Dawca, który chce oddać krew, musi najpierw przejść badanie krwi, aby sprawdzić, czy jest zdrowy i może oddać krew. Wyniki badania są rejestrowane w tabeli blood_test. Jeżeli wynik testu jest "Pozytywny", dawca jest uznawany za zdrowego i może oddać krew. Jeśli wynik jest "Negatywny", dawca nie może oddać krwi i konieczne jest wygenerowanie raportu medycznego, który zostanie zapisany w tabeli report.

Krew oddana przez dawcę jest rejestrowana jako transakcja w tabeli blood_transaction, gdzie zapisywane są informacje o dawcy, pacjencie do którego trafia krew, banku krwi, który przeprowadza cały proces, dacie transakcji oraz ilości oddanej krwi. Każda transakcja jest przechowywana z unikalnym identyfikatorem, aby zapewnić śledzenie i integralność danych.

Pacjent, który potrzebuje krwi, ma przypisaną odpowiednią grupę krwi, zapisaną w tabeli patient. Grupy krwi są zdefiniowane w tabeli blood_type, co pozwala na łatwe dopasowanie dawcy do pacjenta.

System zarządza również danymi pracowników, którzy pracują w bankach krwi. Informacje o pracownikach są przechowywane w tabeli employee, która jest połączona z tabelą blood_bank, gdzie przechowywane są dane o poszczególnych bankach krwi.

# 2. Wymagania i funkcje systemu

System musi umożliwiać rejestrację nowych dawców oraz pacjentów, zapisując ich podstawowe dane osobowe oraz informacje o grupie krwi.
System musi rejestrować wyniki badań krwi dla dawców i umożliwiać ich przeglądanie oraz aktualizowanie.
System musi automatycznie generować raporty medyczne dla dawców, którzy mają negatywne wyniki badań krwi.
System uniemożliwia choremu dawcy oddawać krew. Jeżeli jest to choroba przewlekła, dawca może ponowić test po jej wyleczeniu.
System musi umożliwiać dawcom umawianie się na wizyty i zarządzanie harmonogramem wizyt.
System musi przechowywać informacje o pracownikach banków krwi, w tym ich dane osobowe i przypisanie do konkretnego banku krwi.
System musi przechowywać informacje o bankach krwi, w tym ich nazwy, adresy i dane kontaktowe.
System musi umożliwiać dopasowanie krwi dawcy do pacjenta na podstawie grupy krwi.
System musi zapewniać integralność danych poprzez mechanizmy takie jak transakcje i klucze obce.
System musi umożliwiać przeglądanie historii transakcji krwi dla poszczególnych dawców i pacjentów.
System musi umożliwiać pracownikom przeglądanie harmonogramu wizyt dawców.
System musi umożliwiać generowanie statystyk dotyczących ilości oddanej krwi, liczby dawców i pacjentów oraz innych istotnych danych.
System powinien zawierać odpowiednie funkcje, procedury i widoki umożliwiające intergalność i przejrzystość danych.
Jako dawca, chcę wiedzieć jaki typ krwii wyjdzie mi w badaniu.
Jako dawca, chcę wiedzieć na co jestem chory.
Jako pacjent, chcę mieć możliwość dowiedzieć od kogo dostałem krew.
Jako pracownik, chcę mieć możliwość uzyskania raportu z transakcji krwii.

# 3. Diagramy przypadków użycia

**1. Rejestracja dawcy**

![image](https://github.com/fprzepio/Blood-Bank-Database/assets/132128402/b8d0edf1-488b-4a2d-9a7e-c61821d3c994)

Diagram przedstawia proces rejestracji dawcy krwi, w którym dawca i pracownik mają określone role. Dawca wprowadza swoje dane, które są następnie przetwarzane i potwierdzane przez pracownika, w tym przeprowadzenie badań krwi. Diagram pokazuje, jak poszczególne przypadki użycia są ze sobą powiązane i jakie kroki muszą być podjęte, aby dawca mógł zostać zarejestrowany i oddać krew.

**2. Oddanie krwi**

![obraz_2024-06-26_202712248](https://github.com/fprzepio/Blood-Bank-Database/assets/132128402/523190a2-fa77-4b6a-861a-1109c34f9b76)

Diagram przedstawia proces przeprowadzania badania krwi, w którym dawca i pracownik mają określone role. Dawca stawia się na badanie, oddaje próbkę krwi, która jest następnie badana w laboratorium. Pracownik przeprowadza badania w celu identyfikacji grupy krwi oraz ewentualnych chorób. Wyniki badań są następnie umieszczane w systemie.

**3. Zestawienie pacjenta z dawcom**

![obraz_2024-06-26_203959308](https://github.com/fprzepio/Blood-Bank-Database/assets/132128402/6064d163-aa23-4e5a-9de6-3d601f3872ab)

Diagram ilustruje proces oddawania krwi. Dawca zgłasza się do banku krwi, gdzie następuje zestawienie pacjenta z dawcą. Następnie pracownik banku krwi przeprowadza wywiad z dawcą oraz pobiera krew. Po pobraniu, krew jest przekazywana do badań. Pracownik wykonuje stwierdzenie zgodności, dotyczy sprawdzenia grupy krwi oraz chorób. Przy potwierdzeniu przydatności krwi, wykonywana jest transakcja. Wyniki procesu są później rejestrowane w systemie.

# 4. Projekt bazy danych

## Diagram przedstawiający schemat bazy danych

![obraz_2024-06-26_193621009](https://github.com/fprzepio/Blood-Bank-Database/assets/132128402/0d3cf26e-aa1a-4869-a6ac-2323e94b5c1a)

## Opis poszczególnych tabel

**PK - Primary Key (Klucz Główny)**
**FK - Foreign Key (Klucz Obcy)**

<br>
Nazwa tabeli: blood_bank
- Opis: Tabela przechowująca dane o Bankach Krwi

| Nazwa atrybutu | Typ          | Opis/Uwagi                 |
| -------------- | ------------ | -------------------------- |
| bank_id        | int          | PK, Numer ID Banku Krwi    |
| bankName       | varchar(100) | Nazwa Banku Krwi           |
| address        | varchar(50)  | Adres Banku                |
| city           | varchar(50)  | Miasto                     |
| postalcode     | varchar(20)  | Numer pocztowy             |
| phone          | varchar(15)  | Numer telefonu organizacji |

<br>

<br>
Nazwa tabeli: employee
- Opis: Tabela przechowująca dane pracowników Banków Krwi

| Nazwa atrybutu | Typ         | Opis/Uwagi                                   |
| -------------- | ----------- | -------------------------------------------- |
| employee_id    | int         | PK, Numer ID pracownika                      |
| bank_id        | int         | FK do tabeli blood_bank, Numer ID Banku Krwi |
| firstName      | varchar(50) | Imie pracownika                              |
| lastName       | varchar(50) | Nazwisko pracownika                          |
| title          | varchar(20) | Tytuł pracownika                             |
| address        | varchar(50) | Adres                                        |
| city           | varchar(50) | Miasto                                       |
| postalcode     | varchar(20) | Numer pocztowy                               |
| phone          | varchar(15) | Numer telefonu                               |

<br>

<br>
Nazwa tabeli: blood_transaction
- Opis: Tabela zawierające transakcje krwi

| Nazwa atrybutu  | Typ          | Opis/Uwagi                                    |
| --------------- | ------------ | --------------------------------------------- |
| transaction_id  | int          | PK, Numer ID transakcji                       |
| patient_id      | int          | FK do tabeli patient, Numer ID pacjenta       |
| donor_id        | int          | FK o tabeli donor, Numer ID dawcy             |
| bank_id         | int          | FK do tabeli blood_bank, Numer ID Banku Krwii |
| transactionDate | date         | Data transakcji krwi                          |
| amount          | decimal(5,2) | Ilość oddanej krwii                           |

<br>

<br>
Nazwa tabeli: patient
- Opis: Tabela zawierające dane pacjentów

| Nazwa atrybutu | Typ         | Opis/Uwagi                                  |
| -------------- | ----------- | ------------------------------------------- |
| patiend_id     | int         | PK, Numer ID pacjenta                       |
| blood_id       | int         | FK o tabeli blood_type, Numer ID grupy krwi |
| firstName      | varchar(50) | Imie pacjenta                               |
| lastName       | varchar(50) | Nazwisko pacjenta                           |
| address        | varchar(50) | Adres                                       |
| city           | varchar(50) | Miasto                                      |
| postalcode     | varchar(20) | Numer pocztowy                              |
| phone          | varchar(15) | Numer telefonu pacjenta                     |

<br>

<br>
Nazwa tabeli: blood_type
- Opis: Tabela z grupami krwi

| Nazwa atrybutu | Typ         | Opis/Uwagi              |
| -------------- | ----------- | ----------------------- |
| blood_id       | int         | PK, Numer ID grupy krwi |
| bloodType      | varchar(10) | Nazwa grupy krwi        |

<br>

<br>
Nazwa tabeli: donor
- Opis: Tabela z danymi dawcy

| Nazwa atrybutu | Typ         | Opis/Uwagi                                   |
| -------------- | ----------- | -------------------------------------------- |
| donor_id       | int         | PK, Numer ID dawcy                           |
| blood_id       | int         | FK do tabeli blood_type, Numer ID grupy krwi |
| firstName      | varchar(50) | Imie dawcy                                   |
| lastName       | varchar(50) | Nazwisko dawcy                               |
| address        | varchar(50) | Adres                                        |
| city           | varchar(50) | Miasto                                       |
| postalcode     | varchar(20) | Numer pocztowy                               |
| phone          | varchar(15) | Numer telefonu dawcy                         |

<br>

<br>
Nazwa tabeli: report
- Opis: Tabela z raportami medycznymi dawców

| Nazwa atrybutu | Typ         | Opis/Uwagi                         |
| -------------- | ----------- | ---------------------------------- |
| report_id      | int         | PK, Numer ID raportu medycznego    |
| donor_id       | int         | FK do tabeli donor, Numer ID dawcy |
| reportDate     | date        | Data wystawienia raportu           |
| disease        | varchar(50) | Nazwa choroby                      |

<br>

<br>
Nazwa tabeli: blood_test
- Opis: Tabela zawierająca badania krwii pod względem chorób

| Nazwa atrybutu | Typ         | Opis/Uwagi                         |
| -------------- | ----------- | ---------------------------------- |
| test_id        | int         | PK, Numer ID badania krwi          |
| donor_id       | int         | FK do tabeli donor, Numer ID dawcy |
| testDate       | date        | Data wykonania badania             |
| testResult     | varchar(50) | Wynik testu krwii                  |

<br>

<br>
Nazwa tabeli: schedule
- Opis: Tabela zawierająca harmonogram przeprowadzania badań

| Nazwa atrybutu  | Typ         | Opis/Uwagi                         |
| --------------- | ----------- | ---------------------------------- |
| schedule_id     | int         | PK, Numer ID harmonogramu          |
| donor_id        | int         | FK do tabeli donor, Numer ID dawcy |
| appointmentDate | date        | Data skierowania na badania        |
| testResult      | varchar(50) | Wynik testu krwii                  |

<br>
