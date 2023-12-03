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
