***Zadanie 1 Wyświetl imię i nazwisko każdego pracownika i jego rok urodzenia.***
```sql
SELECT imie, nazwisko, data_urodzenia FROM pracownik;
```
#zad2
```sql
SELECT imie, nazwisko, 2024 - year(data_urodzenia) as wiek FROM pracownik;
```
#zad3
```sql
SELECT d.nazwa, count(p.id_pracownika)
FROM dzial d INNER JOIN pracownik p
ON d.id_dzialu=p.dzial GROUP BY d.id_dzialu;
```
#zad4
```sql
SELECT k.nazwa_kategori, count(t.id_towaru)
FROM towar t INNER JOIN kategoria k ON
t.kategoria=k.id_kategori;
```
#zad5
```sql
SELECT k.nazwa_kategori, group_concat(t.nazwa_towaru) FROM towar t 
INNER JOIN kategoria k ON t.kategoria=k.id_kategori 
GROUP BY k.id_kategori;
```
#zad6
```sql
SELECT round(avg(pensja), 2) FROM pracownik;
```
#zad7
```sql
SELECT avg(pensja) FROM pracownik WHERE (2024 - year(data_zatrudnienia)) > 5;
SELECT round(avg(pensja), 2) FROM pracownik
WHERE data_zatrudnienia <= '2019-01-11';

#lub

SELECT round(avg(pensja), 2) FROM pracownik
WHERE data_zatrudnienia <= 
subdate(data_zatrudnienia, interval 5 year);
```
#zad8
```sql
SELECT t.nazwa_towaru, p.towar, sum(p.ilosc) FROM towar t INNER JOIN pozycja_zamowienia p
ON t.id_towaru=p.towar GROUP BY p.towar ORDER BY sum(p.ilosc) DESC limit 10;
```
#zad9
```sql
SELECT z.id_zamowienia, z.numer_zamowienia, sum(pz.ilosc*pz.cena)
FROM zamowienie z INNER JOIN pozycja_zamowienia pz ON z.id_zamowienia=pz.zamowienie 
WHERE quarter(z.data_zamowienia)=1 AND year(z.data_zamowienia) = 2017
GROUP BY z.id_zamowienia;
```
#zad10
```sql
SELECT pr.imie, pr.nazwisko, sum(pz.ilosc*pz.cena) as wartosc
FROM zamowienie z INNER JOIN pozycja_zamowienia pz ON z.id_zamowienia=pz.zamowienie 
INNER JOIN pracownik pr ON pr.id_pracownika=z.pracownik_id_pracownika 
GROUP BY pr.id_pracownika ORDER BY wartosc DESC;
```
