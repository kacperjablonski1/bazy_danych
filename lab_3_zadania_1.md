***Zadanie 1. Wyświetl imię i nazwisko każdego pracownika i jego rok urodzenia.***
```sql
SELECT imie, nazwisko, data_urodzenia FROM pracownik;
```

***Zadanie 2. Wyświetl imię i nazwisko pracowników oraz ich wiek w latach (bez uwzględniania miesiąca i dnia urodzenia).***
```sql
SELECT imie, nazwisko, 2024 - year(data_urodzenia) as wiek FROM pracownik;
```

***Zadanie 3. Wyświetl nazwę działu i liczbę pracowników przypisanych do każdego z nich.***
```sql
SELECT d.nazwa, count(p.id_pracownika)
FROM dzial d INNER JOIN pracownik p
ON d.id_dzialu=p.dzial GROUP BY d.id_dzialu;
```

***Zadanie 4. Wyświetl nazwę kategorii oraz liczbę produktów w każdej z nich.***
```sql
SELECT k.nazwa_kategori, count(t.id_towaru)
FROM towar t INNER JOIN kategoria k ON
t.kategoria=k.id_kategori;
```

***Zadanie 5. Wyświetl nazwę kategorii i w kolejnej kolumnie listę wszystkich produktów należącej do każdej z nich.***
```sql
SELECT k.nazwa_kategori, group_concat(t.nazwa_towaru) FROM towar t 
INNER JOIN kategoria k ON t.kategoria=k.id_kategori 
GROUP BY k.id_kategori;
```

***Zadanie 6. Wyświetl średnie zarobki pracowników za zaokrągleniem do 2 miejsc po przecinku.***
```sql
SELECT round(avg(pensja), 2) FROM pracownik;
```

***Zadanie 7. Wyświetl średnie zarobki pracowników, którzy pracują co najmniej od 5 lat.***
```sql
SELECT avg(pensja) FROM pracownik WHERE (2024 - year(data_zatrudnienia)) > 5;
SELECT round(avg(pensja), 2) FROM pracownik
WHERE data_zatrudnienia <= '2019-01-11';

lub

SELECT round(avg(pensja), 2) FROM pracownik
WHERE data_zatrudnienia <= 
subdate(data_zatrudnienia, interval 5 year);
```

***Zadanie 8. Wyświetl 10 najczęściej sprzedawanych produktów.***
```sql
SELECT t.nazwa_towaru, p.towar, sum(p.ilosc) FROM towar t INNER JOIN pozycja_zamowienia p
ON t.id_towaru=p.towar GROUP BY p.towar ORDER BY sum(p.ilosc) DESC limit 10;
```

***Zadanie 9. Wyświetl numer zamówienia, jego wartość (suma wartości wszystkich jego pozycji) zarejestrowanych w pierwszym kwartale 2017 roku.***
```sql
SELECT z.id_zamowienia, z.numer_zamowienia, sum(pz.ilosc*pz.cena)
FROM zamowienie z INNER JOIN pozycja_zamowienia pz ON z.id_zamowienia=pz.zamowienie 
WHERE quarter(z.data_zamowienia)=1 AND year(z.data_zamowienia) = 2017
GROUP BY z.id_zamowienia;
```


***Zadanie 10. Wyświetl imie, nazwisko i sumę wartości zamówień, które dany pracownik dodał. Posortuj malejąco po sumie.***
```sql
SELECT pr.imie, pr.nazwisko, sum(pz.ilosc*pz.cena) AS wartosc
FROM zamowienie z INNER JOIN pozycja_zamowienia pz ON z.id_zamowienia=pz.zamowienie 
INNER JOIN pracownik pr ON pr.id_pracownika=z.pracownik_id_pracownika 
GROUP BY pr.id_pracownika ORDER BY wartosc DESC;
```
