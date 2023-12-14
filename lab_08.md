# Zadanie 1
1. Przekopiuj jeszcze raz z bazy wikingowie rekordy z tabeli kreatura, przekopiuj dodatkowo tabele: uczestynicy, etapy_wyprawy, sektor, wyprawa, wraz z danymi.
```sql
CREATE TABLE uczestnicy AS SELECT * FROM wikingowie.uczestnicy;
CREATE TABLE etapy_wyprawy AS SELECT * FROM wikingowie.etapy_wyprawy;
CREATE TABLE sektor AS SELECT * FROM wikingowie.sektor;
CREATE TABLE wyprawa AS SELECT * FROM wikingowie.wyprawa;
```
2. 
```sql
SELECT k.nazwa FROM kreatura k left join uczestnicy u on k.idKreatury=u.id_uczestnika WHERE u.id_wyprawy IS NULL;
```
