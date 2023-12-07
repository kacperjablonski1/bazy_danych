# zadanie 1

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

4. Dodatkowe
avg(), sum(),min(),max(), 
count(*) = zlicza ilosc wierszy
select sum(waga),count(*),avg(waga) from kreatura;
select 2023 - year(dataUr) as wiek from kreatura;
select year(curdate()) - year(dataUr) as wiek from kreatura
