# Daten mit SQL erkunden

### Datensätze zählen

Meistens interessiert im ersten Schritt der Umfang des Datensatzes, also die Anzahl der Zeilen. Das bekommen wir ganz einfach heraus:

```sql
select count(*) from ted_meta
```

### Die Spalten einer Tabelle anzeigen

Die Spalten eines Datensatzes beinhalten die Attribute, die wir mittels SQL abfragen können. Es ist daher zunächst wichtig zu wissen, welche Spalten zur Verfügung stehen und welchen Datentyp sie haben:

```sql
describe ted_meta
```



