# zadanie 1

1. 
'''sql
SELECT sum(waga)/ sum(rodzaj = 'wiking') from kreatura  where rodzaj = 'wiking';
2 sposob
SELECT avg(waga) FROM kreatura WHERE rodzaj = 'wiking'
'''
3.
'''sql
SELECT count(*) FROM kreatura GROUP BY rodzaj;
'''
4. Dodatkowe
avg(), sum(),min(),max(), 
count(*) = zlicza ilosc wierszy
select sum(waga),count(*),avg(waga) from kreatura;
