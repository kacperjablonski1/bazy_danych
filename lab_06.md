# Zadanie 1

***1. Skopiuj tabele 'kreatura','zasob','ekwipunek' z bazy 'wikingowie' do swojej bazy.***

```sql
a)  CREATE TABLE kreatura  AS SELECT * FROM wikingowie.kreatura;
b)  CREATE TABLE zasob  AS SELECT * FROM wikingowie.zasob;
c)  CREATE TABLE ekwipunek AS SELECT * FROM wikingowie.ekwipunek;
```

***2. Wypisz wszystkie rekordy z tabeli 'zasob'.***

```sql
SELECT * FROM zasob;
```

***3. Wypisz wszystkie rekordy z tabeli 'zasob' gdzie typ to jedznienie.

```sql
SELECT * FROM zasob WHERE rodzaj = 'jedzenie';
```

***4. Wypisz 'idZasobu'.'ilosc', dla kreatur o id 1,3,5.

```sql
SELECT idZasobu  FROM zasob WHERE (SELECT idKreatury FROM kreatura WHERE idKreatury = 5);
SELECT idZasobu, ilosc  FROM zasob WHERE (SELECT idKreatury FROM kreatura WHERE idKreatury = 1);

SELECT idZasobu, ilosc  FROM ekwipunek WHERE idKreatu IN (1,3,5); 
```

# Zadanie 2 
***1. Wyświetl kreatury, które nie są wiedźmą i dźwigają co najmniej 50kg.*** 

```sql
SELECT * FROM kreatura WHERE rodzaj NOT LIKE 'wiedzma' AND udzwig >= 50;

SELECT * FROM kreatura WHERE NOT rodzaj = 'wiedzma' AND udzwig >=50;
```

b) SELECT * FROM zasob WHERE waga between 2 AND 5;
c)  SELECT * FROM kreatura WHERE nazwa = '%or%' AND udzwig between 30 AND 70;

Zadanie 3 
a) SELECT * FROM zasob WHERE month(dataPozyskania) between 07 AND 08;
b) SELECT * FROM zasob order by rodzaj;
SELECT DISTINCT rodzaj FROM kreatura;
c) SELECT * FROM kreatura order by dataUr DESC LIMIT 5;

DODATKOWE
SELECT nazwa, ilosc,rodzaj FROM zasob WHERE rodzaj = 'jedznie' AND ilosc = 1;
SELECT distinct ilosc,rodzaj FROM zasob WHERE rodzaj = 'jedznie' AND ilosc = 1; = usuwa dublikaty (wartosci powtarzajace sie itp)

SELECT concat('Ala','ma','kota'); - laczenie tego co w srodku
SELECT concat (nazwa. 'to id=', idKreatury) FROM kreatura;

Zadanie 4
a) select distinct rodzaj FROM zasob;
b) SELECT nazwa, rodzaj FROM kreatura WHERE rodzaj LIKE 'wi%';
c) SELECT ilosc*waga FROM zasob WHERE year(dataPozyskania) BETWEEN 2000 AND 2007;

Zadanie 5
a) SELECT nazwa, waga * 0.7 AS masa_netto, waga * 0.3 AS masa_odpadkow
FROM zasob
WHERE rodzaj = 'jedzenie';
b) select * from zasob where rodzaj is null;
c) SELECT DISTINCT rodzaj FROM zasob WHERE (nazwa LIKE 'Ba%' OR nazwa LIKE '%os') AND rodzaj IS NOT NULL
ORDER BY rodzaj;
