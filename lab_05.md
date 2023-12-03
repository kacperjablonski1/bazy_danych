# Zadanie 1

***a) Uśmierć dwóch najstarszych wikingów, ale to nie moze byc Bjorn (DELETE z WHERE)***

```sql
DELETE FROM postac
WHERE rodzaj = 'wiking' AND nazwa NOT LIKE 'Bjorn'
ORDER BY wiek DESC
LIMIT 2;
```

***b) Usuń klucz glówny z tabeli postać - może być potrzebnych kilka komend (np. odtaczenie kluczy obcych)***

```sql
ALTER TABLE postac DROP PRIMARY KEY - aby to to najpierw to zadziałało

#1 - usuneicie auto_increment - jesli jest

ALTER TABLE postac CHANGE id_postaci id_postaci int;
ALTER TABLE postac MODIFY id_postaci int; - usuniecie auto_increment

#2 - usuniecie kluczy obcy

ALTER TABLE walizka DROP FOREIGN KEY walizka_ibfk_1; 
```

# Zadanie 2

***a) Do tabeli postać dodaj pole pesel składające się z 11 znaków i ustaw to pole na klucz główny***

```sql
ALTER TABLE postac ADD COLUMN pesel char(11) PRIMARY KEY first; (żeby to zadziałało, to trzeba ustawić coś w tabeli)

UPTADE postac SET pesel = '98434534592' + id_postaci;

ALTER TABLE postac ADD PRIMARY KEY (pesel);
```

***b) W tabeli postać zmień pole rodzaj, tak, aby możliwe było dodanie syreny. (ENUM dodaj syrene)***

```sql
ALTER TABLE postac MODIFY  rodzaj enum('(Trzeba wszystko wypisac jeszcze raz + coś nowego)')
```

***c) Wstaw do tabeli syrene o nazwie Gertruda Nieszczera***

```sql
INSERT INTO postac (pesel,id_postaci,nazwa,rodzaj,data_ur,wiek)  VALUES ('23423423423',5,'Gertruda Nieszczera', 'syrena', '2023-11-23',125);
````

*DODATEK (WYSWIETLANIE)*

```sql
# % - dowolny ciag znakow, _ - dokladnie jeden znak
SELECT nazwa FROM postac WHERE nazwa like '_r%';
select nazwa from postac WHERE nazwa like '__-__';
select nazwa from postac where nazwa regexp '%a%';
```

# Zadanie 3 

***a) Wszystkie postacie, które mają w swojej nazwie 'a', wsadź na statek Bjorna***

```sql
UPDATE postac SET statek = 'Czarna Perla' WHERE nazwa LIKE '%a%'
```

***b) Zmniejsz ladowność wszystkim statkom o 30%, których data wodowania była w XX wieku***

```sql
Update statek set max_ladownosc = max_ladownosc * 0.7 where year(data_wodowania) between 1701 and 2001;
```

*DODATEK (SORTOWANIE)*

```sql
SELECT * FROM statek WHERE data_wodowania >='1901-01-01' AND data_wodowania <= '2003-10-02';
SELECT * FROM statek WHERE data_wodowania BETWEEN '1903-94-23' AND '2009-12-31';
SELECT data_wodowania FROM statek;
SELECT year/day/month (data_wodowania) FROM statek;
SELECT * FROM statek WHERE year (data_wodoowania) BETWEEN 1901 AND 2000;
```

***c) Ustaw warunek sprawdzajacy czy wiek postaci nie jest większy od 1000***

```sql
ALTER TABLE postac ADD CHECK (wiek <= 1000); - jesli teraz byśmy chcieli cos zmienic w tabeli to musi to spelniać to.
```

# Zadanie 4

***a) Do postaci dodaj węza Loko, tylko nie wsadzaj go na statek.***

```sql
najpierw enum

ALTER TABLE postac MODIFY rodzaj enum('wiking','ptak','kobieta','syrena','waz');

teraz waz Loko

INSERT INTO postac (pesel,id_postaci,nazwa,rodzaj,data_ur,wiek,funkcja) VALUES ('12345678910','6','Loko','waz','2023-11-20',12,'waz');
```

***b) Stwórz nowa tabele na podstawie tabeli Postacie (doktadnie takie same pola), 
nazwij ja Marynarz - wrzuć do tej tabeli wszystkie postacie które maja zdefiniowany statek***

```sql
1 sposób

CREATE TABLE marynarz LIKE postac; (nie kopiuje kluczy obcych)

INSERT INTO  marynarz SELECT * FROM postac WHERE id_statku IS NOT NULL;

2 - sposób czyli przy stworzeniu tabeli aby odrazu dodal ale tu nie kopiuje klucza glownego i obcego.

CREATE TABLE marynarz3 AS SELECT * FROM postac WHERE statek IS NOT NULL;
```

***c) dostosuj odpowiednio klucze glowne i obce***

```sql
My używając pierwszego sposobu musimy tylko klucz obcy dostosować ponieważ juz mamy juz głowny.

ALTER TABLE marynarz ADD FOREIGN KEY (id_statku) REFERENCES statek(nazwa_statku);
```

# Zadanie 5

***a) wysadz wszystkich ze statku***

```sql
UPDATE marynarz SET id_statku = NULL WHERE id_postaci IN (5,3,4,5,7);
```

***b) usmierc jednego wikinga***

```sql
DELETE FROM marynarz WHERE nazwa = 'Barbarosa';
```

***c) zniszcz wszystkie statki***

```sql
Najpierw trzeba usunac klucze obce ktore sie odwoluja do tych statkow.

ALTER TABLE postac DROP FOREIGN KEY postac_ibfk_1;

Teraz usuwamy statki

DELETE FROM statek WHERE max_ladownosc = 560;
DELETE FROM statek WHERE max_ladownosc = 200;

```

***d) Usuń tabele statek***

```sql
najpierw klucz

ALTER TABLE marynarz DROP FOREIGN KEY marynarz_ibfk_1;

# Potem tabelka.

DROP TABLE statek;
```

***e) stwórz tabele zwierz z polami id - klucz gtowny samo zwiekszajacy sie, nazwa - ciag znakow, wiek - liczba***

```sql
CREATE TABLE zwierz ( id_zwierz INT AUTO_INCREMENT PRIMARY KEY, nazwa TEXT, wiek INT );
```

***f) przekopiuj z tabeli postać wszystkie zwierzaki***

```sql
INSERT INTO zwierz (id_zwierz,nazwa,wiek) SELECT id_postaci,nazwa,wiek FROM  postac WHERE rodzaj IN ('waz','ptak');
```
