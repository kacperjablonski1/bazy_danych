# Zadanie 1

***a) usmierc dwóch najstarszych wikingów, ale to nie moze byc Bjorn (DELETE z WHERE)***

```sql
DELETE FROM postac
WHERE rodzaj = 'wiking' AND nazwa NOT LIKE 'Bjorn'
ORDER BY wiek DESC
LIMIT 2;
```
