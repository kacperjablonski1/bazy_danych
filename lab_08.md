# Zadanie 1
1. Przekopiuj jeszcze raz z bazy wikingowie rekordy z tabeli kreatura, przekopiuj dodatkowo tabele: uczestynicy, etapy_wyprawy, sektor, wyprawa, wraz z danymi.
```sql
CREATE TABLE uczestnicy AS SELECT * FROM wikingowie.uczestnicy;
CREATE TABLE etapy_wyprawy AS SELECT * FROM wikingowie.etapy_wyprawy;
CREATE TABLE sektor AS SELECT * FROM wikingowie.sektor;
CREATE TABLE wyprawa AS SELECT * FROM wikingowie.wyprawa;
```
2. Wypisz nazwy kreatur, które nie uczestniczyły w wyprawie.
```sql
SELECT k.nazwa FROM kreatura k left join uczestnicy u on k.idKreatury=u.id_uczestnika WHERE u.id_wyprawy IS NULL;
```
3. Dla każdej wyprawy wypisać jej nazwę oraz sumę ilości ekwipunku, jaka została zabrana przez uczestników tej wyprawy.
```sql
SELECT max(w.nazwa),sum(e.ilosc) FROM wyprawa w inner join uczestnicy u on w.id_wyprawy=u.id_wyprawy inner join kreatura k on u.id_uczestnika=k.idKreatury inner join ekwipunek e on k.idKreatury=e.idKreatury group by w.id_wyprawy;
```
# Zadanie 2
1. Dla każdej wyprawy wypisz jej nazwę, liczbę uczestników, oraz tych uczestników w jednej linii.
```sql

```
2. Wypisz kolejne etaty wszystkich wypraw wraz z nazwami sektorów, sortując najpierw według daty początku wyprawy, a następnie według kolejności występowania etapów. W każdym etapie określ nazwę kierownika danej wyprawy.
```sql

```
# Zadanie 3
1. Wypisać ile razy dany sektor był odwiedzany podczas wszystkich wypraw (nazwa sektora, ilośćc odwiedzin). Jeśli nie był odwiedzony ani razu, wypisz zero.
```sql

```
2. W zależności od ilości wypraw, w jakich brała udział dana kreatura wypisz: nazwa kreatury,
'brał udział w wyprawie' - gdy liczba > 0, 'nie brał udziału w wyprawie', gdy równa zero.
```sql

```
# Zadania 4
1. Dla każdej wyprawy wypisz jej nazwę oraz sumę liczby znaków, które zostały użyte przy pisaniu dziennika, jeśli ta liczba znaków jest mniejsza od 400.
```sql
```
2. Dla każdej wyrawy podaj średnią wagę zasobów, jakie były niesione przez uczestników tej wyprawy.
```sql
```
# Zadanie 5
1. Wypisać nazwę kreatury oraz ile miała dni (wiek w dniach) w momencie rozpoczęcia wyprawy, dla wypraw, które przechodziły przez chatkę dziadka.
```sql
```
