### Zadanie 1


**1. Stwórz tabele postac z nastepujacymi polami:**
* a) id_postaci kl. gtówny, liczba samozwiekszajaca sie
* b) nazwa - ciag znaków max 40
* c) rodzaj - typ wyliczeniowy (wiking, ptak, kobieta)
* d) data_ur - typ daty
* e) wiek - liczba nieujemna.


```
CREATE TABLE postac (
    id_postaci INT AUTO_INCREMENT PRIMARY KEY,
    nazwa VARCHAR(40),
    rodzaj ENUM('wiking', 'ptak', 'kobieta'),
    data_ur DATE,
    wiek INT UNSIGNED
);
```
