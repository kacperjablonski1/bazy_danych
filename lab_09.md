# Zadanie 1
***1. Napisz wyzwalacz, który przed wstawieniem lub modyfikacją tabeli kreatura sprawdzi czy waga jest większa od zera.***
```sql
DELIMITER //
CREATE TRIGGER kreatura_before_insert
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
  IF NEW.waga <= 0
  THEN
    SET NEW.waga = 1;
  END IF;
END
//
DELIMITER;

NEW -> INSERT, UPDATE
OLD -> UPDATE, DELETE
````

# Zadanie 2
***1. Stwórz tabelę archiwum_wypraw z polami id_wyprawy, nazwa, data_rozpoczecia, data_zakonczenia, kierwonik (varchar), do której będą wstawiane rekordy po usunięciu z tabeli wyprawa. Do kolumny kierwonik wstawiane jest nazwa kreatury na podstawie usuwanego id_kreatury***
```sql

CREATE TABLE archiwum_wypraw(
id_wyprawy int primary key auto_increment,
nazwa varchar(55),
data_rozpoczecia date,
data_zakonczenia date,
kierownik varchar(55));

DELIMITER //
CREATE TRIGGER wyprawa_before_delete
BEFORE DELETE ON wyprawa
FOR EACH ROW
BEGIN
  INSERT INTO archiwum_wypraw
  SELECT w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa FROM wyprawa w
  INNER JOIN kreatura k ON k.idKreatury=w.kierownik
  WHERE id_wyprawy=OLD.id_wyprawy;
END
//
DELIMITER;
```
*DODATKOWE*
```sql
SHOW TRIGGERS;
SHOW CREATE TRIGGER nazwa;
DROP TRIGGER nazwa;
```
# Zadanie 3
***1. Napisz procedurę o nazwie "eliksir_sily", która bedzie podnosiła wartość pola udzwig z tabeli kreatura o 20% na podstawie id_kreatury przekazywanego jako parametr.***
```sql
DELIMITER $$
CREATE PROCEDURE premia(in id int)
BEGIN
  UPDATE kreatura
  SET udzwig = 1.2 * udzwig
  WHERE id_pracownika = id;
END
$$
DELIMITER;
```
***2. Napisz funkcję, która będzie pobierała tekst i zwracała go z wielkich liter***
```sql
```
# Zadanie 4
***1. Stwórz tabele "system_alarmowy" z polami, id_alarmu, wiadomosc***
```sql
```
***2. Dodaj wyzwalacz, który będzie sprawdzał czy w tabeli wyprawy pojawiła się misja, w której bierze udział teściowa oraz czy jednym z sektorów misji jest domek dziadka. Jeżeli w/w zaistnieje wyzwalacz wstawi rekord do tabeli "system_alarmowy" z treścią "Teściowa nadchodzi !!!"***
```sql
```

# Zadanie 5
***1. Napisz procedurę mającą jako parametry wyjściowe średnią, sumę i maks udźwigu z tabeli kreatura.***
```sql
```
***2. Napisz procedurę, która jako parametr wyjściowy przyjmuje id_wyprawy a na wyjściu numer sektora (np. A1, B3 itd.) oraz nazwę sektora posortowane wg kolejności w jakiej występują w danej wyprawie.***
```sql
````
