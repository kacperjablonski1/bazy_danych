# Zadanie 1

***1. Skopiuj tabele 'kreatura','zasob','ekwipunek' z bazy 'wikingowie' do swojej bazy.***

```sql
CREATE TABLE kreatura  AS SELECT * FROM wikingowie.kreatura;
CREATE TABLE zasob  AS SELECT * FROM wikingowie.zasob;
CREATE TABLE ekwipunek AS SELECT * FROM wikingowie.ekwipunek;
```

***2. Wypisz wszystkie rekordy z tabeli 'zasob'.***

```sql
SELECT * FROM zasob;
```

***3. Wypisz wszystkie rekordy z tabeli 'zasob' gdzie typ to jedznienie.***

```sql
SELECT * FROM zasob WHERE rodzaj = 'jedzenie';
```

***4. Wypisz 'idZasobu'.'ilosc', dla kreatur o id 1,3,5.***

```sql
SELECT idZasobu  FROM zasob WHERE (SELECT idKreatury FROM kreatura WHERE idKreatury = 5);
SELECT idZasobu, ilosc  FROM zasob WHERE (SELECT idKreatury FROM kreatura WHERE idKreatury = 1);

SELECT idZasobu, ilosc  FROM ekwipunek WHERE idKreatur IN (1,3,5); 
```

# Zadanie 2 
***1. Wyświetl kreatury, które nie są wiedźmą i dźwigają co najmniej 50kg.*** 

```sql
SELECT * FROM kreatura WHERE rodzaj NOT LIKE 'wiedzma' AND udzwig >= 50;

SELECT * FROM kreatura WHERE NOT rodzaj = 'wiedzma' AND udzwig >=50;
```
***2. Wyświetl zasoby, które ważą pomiędzy 2 a 5kg.***

```sql
SELECT * FROM zasob WHERE waga between 2 AND 5;
```

***3. Wyświetl kreatury, których nazwa zawiera 'or' i które dźwigają między 30kg a 70kg.***

```sql
SELECT * FROM kreatura WHERE nazwa = '%or%' AND udzwig between 30 AND 70;
```

# Zadanie 3 

***1. Wyświetl zasoby, które zostały pozyskane w miesiącach lipcu i sierpniu***

```sql
SELECT * FROM zasob WHERE month(dataPozyskania) between 07 AND 08;
```

***2. Wyświetl zasoby, które mają zdefiniowany rodzaj od najlżejszego do najcięższego***

```sql
SELECT * FROM zasob WHERE rodzaj IS NOT NULL ORDER BY waga ASC;

SELECT * FROM zasob ORDER BY rodzaj ASC;
```

***3. Wyświetl 5 najstarszych kreatur****

```sql
SELECT * FROM kreatura order by dataUr DESC LIMIT 5;
```

*DODATKOWE*

```sql
SELECT DISTINCT rodzaj FROM kreatura; - Usuwa powtarzające sie kolumny, wiersze
SELECT nazwa, ilosc,rodzaj FROM zasob WHERE rodzaj = 'jedznie' AND ilosc = 1;
SELECT distinct ilosc,rodzaj FROM zasob WHERE rodzaj = 'jedznie' AND ilosc = 1; = usuwa dublikaty (wartosci powtarzajace sie itp)

SELECT concat('Ala','ma','kota'); - laczenie tego co w srodku
SELECT concat (nazwa. 'to id=', idKreatury) FROM kreatura;
```

# Zadanie 4
***1. Wyświetl unikalne rodzaje zasobów.***

```sql
SELECT DISTINCT rodzaj FROM zasob;
```

***2. Wyświetl jako jedną kolumnę nazwę i rodzaj kreatury (w postaci: nazwa - rodzaj), gdzie rodzaj rozpoczyna się od 'wi'.***

```sql
SELECT concat(nazwa, ' to id=', idKreatury) FROM kreatura WHERE rodzaj LIKE 'wi%';

```

***3. Wyświetl zasoby z całkowitą wagą danego zasobu (ilość * waga) dla zasobów pozyskanych w latach 2000-2007.***

```sql
SELECT nazwa, (ilosc*waga) as calkowitaWaga FROM zasob WHERE year(dataPozyskania) BETWEEN 2000 AND 2007;
```

# Zadanie 5

***1. Zakładając, że każdy rodzaj jedzenia to 30% odpadu, wyświetl masę właściwego jedzenia (netto) oraz wagę odpadków.***

```sql
SELECT nazwa, waga * 0.7 AS masa_netto, waga * 0.3 AS masa_odpadkow FROM zasob WHERE rodzaj = 'jedzenie';
```

***2. Wyświetl zasoby, które nie mają rodzaju.****

```sql
SELECT * FROM zasob WHERE rodzaj IS NULL;
```
***3. Wyświetl wszystkie unikalne rodzaje zasobów, których nazwa zaczyna się od 'Ba' lub kończy się na 'os'. Dane posortuj alfabetycznie.***

```sql
SELECT DISTINCT rodzaj FROM zasob WHERE (nazwa LIKE 'Ba%' OR nazwa LIKE '%os') AND rodzaj IS NOT NULL ORDER BY rodzaj;
```
