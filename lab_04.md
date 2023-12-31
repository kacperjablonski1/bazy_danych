# Zadanie 1

***1. Stwórz tabele postac z nastepujacymi polami:***
* *a. id_postaci kl. gtówny, liczba samozwiekszajaca sie*
* *b. nazwa - ciag znaków max 40*
* *c. rodzaj - typ wyliczeniowy (wiking, ptak, kobieta)*
* *d. data_ur - typ daty*
* *e. wiek - liczba nieujemna.*


```sql
CREATE TABLE postac (
    id_postaci INT AUTO_INCREMENT PRIMARY KEY,
    nazwa VARCHAR(40),
    rodzaj ENUM('wiking', 'ptak', 'kobieta'),
    data_ur DATE,
    wiek INT UNSIGNED
);
```
***2. Do tabeli postac dodaj rekordy, gdzie kolumna naza to Bjorn, Drozd, Tesciowa (w pozostare pola wisz w miare sensowne dane).***

```sql
-- Dodanie rekordu dla Bjorna
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek)
VALUES ('Bjorn', 'wiking', '1990-05-15', 33);

-- Dodanie rekordu dla Drozda
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek)
VALUES ('Drozd', 'ptak', '2015-02-20', 8);

-- Dodanie rekordu dla Tesciowej
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek)
VALUES ('Tesciowa', 'kobieta', '1935-12-10', 87);
```

***3. Zmodyfikuj wiek tesciowej na 88 lat.***

```sql
UPDATE postac
SET wiek = 88
WHERE nazwa = 'Tesciowa';
```

# Zadanie 2 

***1. Stwórz tabele walizka:***
* *a. id_walizki - liczba samozwiekszajaca sie, klucz growny*
* *b. pojemnosc - liczba nieujemna*
* *c. kolor - typ wyliczeniowy (rózowy, czerwony, teczowy, zótty)*
* *d. id_wlasciciela - klucz obcy odwotujacy sie do tabeli postac, ustawione kaskadowe usuwanie.*

```sql
CREATE TABLE walizka (
    id_walizki INT AUTO_INCREMENT PRIMARY KEY,
    pojemnosc INT UNSIGNED,
    kolor ENUM('rózowy', 'czerwony', 'teczowy', 'żółty') ,
    id_wlasciciela INT,
    FOREIGN KEY (id_wlasciciela) REFERENCES postac(id_postaci) ON DELETE CASCADE
);
```

***2. Dodaj do pola kolor wartosc domyslna - rózowy.***

```sql
ALTER TABLE walizka
ALTER COLUMN kolor SET DEFAULT 'rózowy';
```

***3. Dodaj jedna walizke dla Bjorna i jedna walizke, dla tesciowej.***

```sql
-- Dodanie walizki dla Bjorna
INSERT INTO walizka (pojemnosc, id_wlasciciela)
VALUES (30, (SELECT id_postaci FROM postac WHERE nazwa = 'Bjorn'));

-- Dodanie walizki dla teściowej
INSERT INTO walizka (pojemnosc, id_wlasciciela)
VALUES (25, (SELECT id_postaci FROM postac WHERE nazwa = 'Tesciowa'));
```

# Zadanie 3 

***1 Stwórz tabele izba z polami:***
* *a. adres_budynku - czesc klucza gtównego*
* *b. nazwa_izby - czesc klucza gtównego*
* *c. metraz - liczba nieujemna*
* *d. wlasciciel - klucz obcy do tabeli postac, ustaw null w razie usuniecia.*

```sql
CREATE TABLE izba (
    adres_budynku INT,
    nazwa_izby VARCHAR(50),
    metraz INT UNSIGNED,
    wlasciciel INT,
    PRIMARY KEY (adres_budynku, nazwa_izby),
    FOREIGN KEY (wlasciciel) REFERENCES postac(id_postaci) ON DELETE SET NULL
);
```

***2. Za pomoca odazielnego polecenia dodaj pole kolor izby po polu metraz. Ustaw domysiny kolor na czarny.***

```sql
ALTER TABLE izba
ADD COLUMN kolor VARCHAR(20) DEFAULT 'czarny' AFTER metraz;
```

***3. Stworz izbe spizarnia.***

```sql
INSERT INTO izba (adres_budynku, nazwa_izby, metraz, kolor, wlasciciel)
VALUES (1, 'spizarnia', 15, 'zielony', NULL);
```

# Zadanie 4 

***1. Stwórz tabele pretwory z polami:***
* *a. Id _przetworu - Klucz growny*
* *b. rok_produkji - typ roku, domyslnie 1654*
* *c. id_wykonawcy - klucz obcy do tabeli postac*
* *d. zawartosc - ciag znaków*
* *e. dodatek - ciag znaków - domyslnie papryczka chilli*
* *f. id_konsumenta - klucz obcy do tabeli postac*

```sql
CREATE TABLE przetwory (
    Id_przetworu INT AUTO_INCREMENT PRIMARY KEY,
    rok_produkcji YEAR DEFAULT 1654,
    id_wykonawcy INT,
    zawartosc TEXT,
    dodatek VARCHAR(50) DEFAULT 'papryczka chilli',
    id_konsumenta INT,
    FOREIGN KEY (id_wykonawcy) REFERENCES postac(id_postaci),
    FOREIGN KEY (id_konsumenta) REFERENCES postac(id_postaci)
);
```

***2. Wstaw bigos z papryczka chilli do tabeli przetwory.***

*Załóżmy, że ID wykonawcy i ID konsumenta dla bigosu to odpowiednio 1 i 2 (dla przykładu)*

```sql
INSERT INTO przetwory (rok_produkcji, id_wykonawcy, zawartosc, id_konsumenta)
VALUES (2022, 1, 'bigos', 'papryczka chilli', 2);
```

# Zadanie 5

***1. Wstaw 5 wikingów do tabeli postaci.***

```sql
INSERT INTO postac (nazwa, rodzaj, data_ur, wiek)
VALUES 
    ('Jack Sparrow', 'wiking', '1980-01-01', 35),
    ('Barbarosa', 'wiking', '1985-03-15', 30),
    ('Lord Voldemort', 'wiking', '1990-05-20', 25),
    ('Eivor Varinsdottir', 'wiking', '1995-08-10', 20),
    ('Yoda', 'wiking', '2000-12-25', 15);
```

***2. Stworz tabele statek z polami:***
* *a. nazwa statku - klucz gtówny*
* *b. rodzaj statku - typ wyliczeniowy*
* *c. data wodowania - typ daty*
* *d. max_ladownosc - liczba dodatnia*

```sql
CREATE TABLE statek (
    nazwa_statku VARCHAR(50) PRIMARY KEY,
    rodzaj_statku ENUM('żaglowiec', 'okręt wojenny', 'statek handlowy'),
    data_wodowania DATE,
    max_ladownosc INT UNSIGNED
);
```

***3. Dodaj dwa statki do tabeli.***

```sql
INSERT INTO statek (nazwa_statku, rodzaj_statku, data_wodowania, max_ladownosc)
VALUES 
    ('HMS Victory', 'okręt wojenny', '1765-09-01', 800),
    ('Czarna Perła', 'żaglowiec', '1688-07-10', 500);
```

***4. Dodaj pola do tabeli postac:***
* *a. funkcja - ciag znakow.*

```sql
ALTER TABLE postac
ADD COLUMN funkcja VARCHAR(50);
```

***5. Zmien funkcje u Bjorna na kapitan.***

```sql
UPDATE postac
SET funkcja = 'kapitan'
WHERE nazwa = 'Bjorn';
```

***6. Dodaj klucz obcy w tabeli postac odwotujacy sie do statku.***

```sql
ALTER TABLE postac
ADD COLUMN id_statku VARCHAR(50),
ADD FOREIGN KEY (id_statku) REFERENCES statek(nazwa_statku);
```

***7. Powsadzaj wikingów oraz drozda na statki.***

*Załóżmy, że Jack Sparrow, Lord Voldemort, Drozd idą na statek Czarna Perła*

```sql
UPDATE postac
SET id_statku = 'Czarna Perła'
WHERE nazwa IN ('Jack Sparrow', 'Lord Voldemort', 'Drozd');
```

*Załóżmy, że Barbarosa, Eivor Varinsdottir, Yoda idą na statek HMS Victory*

```sql
UPDATE postac
SET id_statku = 'HMS Victory'
WHERE nazwa IN ('Barbarosa', 'Eivor Varinsdottir', 'Yoda');
```

***8. Usun izbe spizarnia z tabell izba.***

```sql
DELETE FROM izba WHERE nazwa_izby = 'spizarnia';
```

***9. Usun tabele izba.***

```sql
DROP TABLE izba;
```
