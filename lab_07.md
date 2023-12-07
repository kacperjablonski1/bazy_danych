# Zadanie 1

1. Wyświetl średnią wagę wszystkich wikingów
```sql
SELECT sum(waga)/ sum(rodzaj = 'wiking') FROM kreatura  WHERE rodzaj = 'wiking';
2 sposob
SELECT avg(waga) FROM kreatura WHERE rodzaj = 'wiking'
```
2. Wyświetl średnią wagę oraz liczbę kreatur dla każdego rodzaju
```sql
SELECT avg(waga), count(rodzaj) FROM kreatura GROUP BY rodzaj;

SELECT count(*) FROM kreatura GROUP BY rodzaj;
```
3. Wyświetl średni wiek dla każdego rodzaju kreatury
```sql
SELECT rodzaj ,avg(2023 - year(dataUr)) FROM kreatura GROUP BY rodzaj;
```
4. Dodatkowe
```sql
avg(), sum(),min(),max(), 
count(*) = zlicza ilosc wierszy
select sum(waga),count(*),avg(waga) from kreatura;
select 2023 - year(dataUr) as wiek from kreatura;
select year(curdate()) - year(dataUr) as wiek from kreatura
select distinct nazwa FROM zasob;
select count(distinct nazwa) FROM zasob;
```
# Zadanie 2
1. Dla każdego rodzaju zasobu wyświetlić sumę wag tego zasobu.
```sql
 SELECT rodzaj,sum(waga) from zasob GROUP BY rodzaj;
```
2. Dla każdej nazwy zasobu wyświetlić średnią wagę, jeśli ilość jest równa co najmniej 4 oraz jeśli ta suma wag jest większa od 10. 
```sql
SELECT sum(waga) FROM zasob WHERE ilosc > 4 GROUP BY rodzaj HAVING sum(waga) > 5;
najpierw odfiltrowanie pozniej agregowanie
```
3. Wyświetlić ile jest różnych nazw dla każdego rodzaju zasobu, jeśli minimalna liczba zasobu jest większa od 1.
```sql
SELECT count(distinct nazwa) FROM zasob GROUP BY rodzaj HAVING min(ilosc) > 1;
SELECT count(distinct nazwa) from zasob GROUP BY rodzaj HAVING min(ilosc) > 1;
```
# Zadanie 3 

1. Wyświetlić dla każdej kreatury ilość zasobów jakie niesie.
```sql
SELECT * FROM kreatura, ekwipunek WHERE kreatura.idKreatury = ekwipunek.idKreatury;

2 sposob

SELECT * FROM kreatura k INNER JOIN ekwipunek e ON k.idKreatury = e.idKreatury;

DODATEK (INNER JOIN - laczy tabelki)
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k INNER JOIN ekwipunek e ON k.idKreatury = e.idKreatury INNER JOIN zasob z ON e.idZasobu = z.idZasobu;
```
2. Wyświetlić dla każdej kreatury nazwy zasobów jakie posiada.
```sql

```
3. Wyświetlić kreatury, które nie posiadają żadnego ekwipunku.
```sql
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k LEFT JOIN ekwipunek e ON k.idKreatury = e.idKreatury WHERE e.kreatury IS NULL;
```

Dodatek
```sql
left join + warunek z null

SELECT k.nazwa FROM kreatura k LEFT JOIN ekwipunek e ON k.idKreatury = e.idKreatury WHERE e.idKreatury IS NULL

podzapytanie

SELECT nazwa, idKreatury FROM kreatura WHERE idKreatury not in (SELECT DISTINCT idKreatury FROM ekwipunek WHERE idKreatury IS NOT NULL);
```
