# Zadanie 1

***a) Uśmierć dwóch najstarszych wikingów, ale to nie moze byc Bjorn (DELETE z WHERE)***

```sql
DELETE FROM postac
WHERE rodzaj = 'wiking' AND nazwa NOT LIKE 'Bjorn'
ORDER BY wiek DESC
LIMIT 2;
```

***b) Usuń klucz glówny z tabeli postać - może być potrzebnych kilka komend (np. odtaczenie kluczy obcych)

```sql
ALTER TABLE postac DROP PRIMARY KEY - aby to to najpierw to zadziałało

#1 - usuneicie auto_increment - jesli jest

ALTER TABLE postac CHANGE id_postaci id_postaci int;
ALTER TABLE postac MODIFY id_postaci int; - usuniecie auto_increment

#2 - usuniecie kluczy obcy

ALTER TABLE walizka DROP FOREIGN KEY walizka_ibfk_1; 
```
