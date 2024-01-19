***Zadanie 1. Wyświetl nazwę działu i minimalną, maksymalną i średnią wartość pensji w każdym dziale.***
```sql
SELECT d.nazwa, MIN(p.pensja) AS min_pensja, MAX(p.pensja) AS max_pensja,
AVG(p.pensja) AS srednia_pensja FROM dzial AS d LEFT JOIN pracownik AS p
ON d.id_dzialu = p.dzial GROUP BY d.nazwa;
```

***Zadanie 2. Wyświetl pełną nazwę klienta, wartość zamówienia dla 10 najwyższych wartości zamówienia.***
```sql
SELECT k.pelna_nazwa, SUM(p.cena) AS wartosc FROM klient AS k
LEFT JOIN zamowienie AS z ON k.id_klienta = z.klient
LEFT JOIN pozycja_zamowienia AS p ON z.id_zamowienia = p.zamowienie
GROUP BY k.pelna_nazwa ORDER BY SUM(p.cena) DESC LIMIT 10;
```

***Zadanie 3. Wyświetl wartość przychodu dla każdego roku. Dane posortuj malejąco według sumy wartości zamówień.***
```sql
SELECT YEAR(z.data_zamowienia), SUM(p.cena) FROM zamowienie AS z
LEFT JOIN pozycja_zamowienia AS p ON z.id_zamowienia = p.zamowienie
GROUP BY YEAR(z.data_zamowienia) ORDER BY SUM(p.cena) DESC;
```

***Zadanie 4. Wyświetl sumę wartości wszystkich anulowanych zamówień.***
```sql
SELECT SUM(p.cena) FROM pozycja_zamowienia AS p LEFT JOIN zamowienie AS z
ON p.zamowienie = z.id_zamowienia WHERE z.status_zamowienia = 6;
```

***Zadanie 5. Wyświetl liczbę zamówień i sumę zamówień dla każdego miasta z podstawowego adresu klientów.***
```sql
SELECT a.miejscowosc, COUNT(z.id_zamowienia) AS ilosc_zamowien, SUM(p.cena) AS suma_zamowien
FROM pozycja_zamowienia AS p LEFT JOIN zamowienie AS z ON p.zamowienie = z.id_zamowienia
LEFT JOIN adres_klienta AS a ON z.klient = a.klient GROUP BY a.miejscowosc;
```

***Zadanie 6. Wyświetl dotychczasowy dochód firmy biorąc pod uwagę tylko zamówienia zrealizowane.***
```sql
SELECT SUM(p.cena) FROM zamowienie AS z LEFT JOIN pozycja_zamowienia AS p
ON z.id_zamowienia = p.zamowienie WHERE status_zamowienia = 5;
```

***Zadanie 7. Policz i wyświetl dochód (przychód z zamówień i cena zakupu towaru) w każdym roku działalności firmy.***
```sql

```

***Zadanie 8. Wyświetl wartość aktualnego stanu magazynowego z podziałem na kategorię produktów.***
```sql
SELECT k.nazwa_kategori, SUM(s.ilosc) AS wartosc_stanu_mag FROM stan_magazynowy AS s
JOIN towar AS t ON s.towar = t.id_towaru JOIN kategoria AS k ON t.kategoria = k.id_kategori
GROUP BY k.nazwa_kategori;
```

***Zadanie 9. Przygotuj zapytanie, które wyświetli dane w poniższej postaci (policz ilu pracowników urodziło się w danym miesiącu - uwaga na porządek sortowania).***
```sql
SELECT MONTHNAME(data_urodzenia) AS miesiac, COUNT(id_pracownika) AS ilosc_pracownikow
FROM pracownik GROUP BY MONTHNAME(data_urodzenia) ORDER BY FIELD
(miesiac, 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December');
```

***Zadanie 10 * Wyświetl imię i nazwisko pracownika i koszt jaki poniósł pracodawca od momentu jego zatrudnienia.
(Nie aż tak trudne jak poszukać odpowiedniej funkcji operującej na datach.)***
```sql
```
