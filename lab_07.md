# Zadanie 1

1. 
```sql
SELECT sum(waga)/ sum(rodzaj = 'wiking') from kreatura  where rodzaj = 'wiking';
2 sposob
SELECT avg(waga) FROM kreatura WHERE rodzaj = 'wiking'
```
2.
```sql
SELECT count(*) FROM kreatura GROUP BY rodzaj;
```
3.
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
1.
```sql
SELECT * FROM zasob;
```
3.
```sql
SELECT sum(waga) from zasob WHERE ilosc > 4 GROUP BY rodzaj HAVING sum(waga) > 5;
najpierw odfiltrowanie pozniej agregowanie
```
5.
```sql
Select count(distinct nazwa) FROM zasob;
```
