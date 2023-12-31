# Zadanie 1

***1. Wyświetl średnią wagę wszystkich wikingów***
```sql
SELECT sum(waga)/sum(rodzaj = 'wiking') FROM kreatura  WHERE rodzaj = 'wiking';

SELECT avg(waga) FROM kreatura WHERE rodzaj = 'wiking'
```
***2. Wyświetl średnią wagę oraz liczbę kreatur dla każdego rodzaju***
```sql
SELECT avg(waga), count(rodzaj) FROM kreatura GROUP BY rodzaj;
```
***3. Wyświetl średni wiek dla każdego rodzaju kreatury***
```sql
SELECT rodzaj ,avg(2023 - year(dataUr)) FROM kreatura GROUP BY rodzaj;
```
*4. Dodatkowe*
```sql
avg(), sum(),min(),max(), 
count(*) = zlicza ilosc wierszy
SELECT sum(waga),count(*),avg(waga) FROM kreatura;
SELECT 2023 - year(dataUr) AS wiek FROM kreatura;
SELECT year(curdate()) - year(dataUr) AS wiek FROM kreatura
SELECT DISTINCT nazwa FROM zasob;
SELECT count(distinct nazwa) FROM zasob;
```
# Zadanie 2
***1. Dla każdego rodzaju zasobu wyświetlić sumę wag tego zasobu.***
```sql
 SELECT rodzaj,sum(waga*ilosc) FROM zasob GROUP BY rodzaj;
```
***2. Dla każdej nazwy zasobu wyświetlić średnią wagę, jeśli ilość jest równa co najmniej 4 oraz jeśli ta suma wag jest większa od 10.***
```sql
SELECT avg(waga) FROM zasob
WHERE ilosc >= 4
GROUP BY rodzaj HAVING sum(waga) > 10;

najpierw odfiltrowanie pozniej agregowanie
```
***3. Wyświetlić ile jest różnych nazw dla każdego rodzaju zasobu, jeśli minimalna liczba zasobu jest większa od 1.***
```sql
SELECT count(distinct nazwa) FROM zasob GROUP BY rodzaj HAVING min(ilosc) > 1;
```
# Zadanie 3 

***1. Wyświetlić dla każdej kreatury ilość zasobów jakie niesie.***
```sql
SELECT nazwa, idZasobu, ilosc FROM kreatura, ekwipunek
WHERE kreatura.idKreatury=ekwipunek.idKreatury;
lub
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k
INNER JOIN ekwipunek e ON k.idKreatury=e.idKreatury;

INNER JOIN - laczy tabelki
```
***2. Wyświetlić dla każdej kreatury nazwy zasobów jakie posiada.***
```sql
SELECT k.nazwa, e.idZasobu, e.ilosc z.nazwa FROM kreatura k
INNER JOIN ekwipunek e ON k.idKreatury=e.idKreatury
INNER JOIN zasob z ON e.idZasobu=z.idZasobu;
```
***3. Wyświetlić kreatury, które nie posiadają żadnego ekwipunku.***
```sql
SELECT k.nazwa, e.idZasobu, e.ilosc FROM kreatura k
LEFT JOIN ekwipunek e ON k.idKreatury = e.idKreatury
WHERE e.idZasobu IS NULL;
```

*DODATEK*
```sql
left join + warunek z null

SELECT k.nazwa FROM kreatura k
LEFT JOIN ekwipunek e ON k.idKreatury = e.idKreatury
WHERE e.idKreatury IS NULL

podzapytanie

SELECT nazwa, idKreatury FROM kreatura
WHERE idKreatury NOT IN (SELECT DISTINCT idKreatury FROM ekwipunek WHERE idKreatury IS NOT NULL);

Natural Join - sam laczy (niewarto uzywac)
```

# Zadanie 4
***1. Wyświetlić nazwy wikingów, którzy urodzili się w latach 70-tych XVII wieku oraz nazwy zasobów, które posiadaają (użyj natural joina jeśli się da)***
```sql
SELECT k.nazwa, z.nazwa FROM kreatura k
JOIN ekwipunek e ON k.idKreatury=e.idKreatury
JOIN zasob z ON e.idZasobu=z.idZasobu
WHERE year(dataUr) BETWEEN 1670 AND 1680;
```
***2. Wyświetlić nazwy 5 najmłodszych kreatur, które w ekwipunku posiadają jedzenie.***
```sql
SELECT k.nazwa, k.dataUr, z.rodzaj FROM kreatura k
INNER JOIN ekwipunek e ON k.idKreatury=e.idKreatury
INNER JOIN zasob z ON e.idZasobu=z.idZasobu.
WHERE z.rodzaj = 'jedzenie' ORDER BY k.dataUr DESC LIMIT 5;
```
***3. Wypisz obok siebie nazwy kreatur, których numer idKreatury różni się o 5 (np. Bjorn - Astrid, Brutal - Ibra itd.)***
```sql
SELECT concat(k1.nazwa, '-',k2.nazwa) FROM kreatura k1 INNER JOIN kreatura k2 ON abs(k1.kreatury-k2.kreatury) = 5;
lub
SELECT concat(k1.nazwa, '-',k2.nazwa) FROM kreatura k1 INNER JOIN kreatura k2 ON k1.kreatury-k2.kreatury = 5;
```

# Zadanie 5
***1. Dla każdego rodzaju kreatury wyświetlić średnią wagę zasobów, jaką posiadają w ekwipunku, jeśli kreatura nie jest małpą ani wężem i ilość ekwipunku jest poniżej 30.***
```sql
SELECT k.rodzaj, avg(e.ilosc * z.waga) FROM kreatura k
INNER JOIN ekwipunek e ON k.idKreatury=e.idKreatury
INNER JOIN zasob z ON e.idZasobu=z.idZasobu
WHERE k.rodzaj NOT IN ('malpa','waz') AND e.ilosc < 30 GROUP BY k.rodzaj; 
```
***2. Dla każdego rodzaju kreatury wyświetlić nazwę, datę urodzenia i rodzaj najmłodszej i najstarszej kreatury.***
```sql
SELECT k.rodzaj, k.nazwa, n.najstarsza, n.najmlodsza FROM (SELECT rodzaj, min(dataUr) najstarsza, max(dataUr) najmlodsza
FROM kreatura group by rodzaj) n, kreatura k
WHERE n.najstarsza = k.dataUr OR n.najmlodsza=k.dataUr; 
```
