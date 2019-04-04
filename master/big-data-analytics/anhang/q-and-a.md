---
description: >-
  Hier findet ihr die Fragen und Antworten, die während des Semesters gestellt
  wurden.
---

# Q & A

## Wie wandelt man einen String in eine Zahl um?

In manchen Fällen wissen wir, dass eine Spalte zwar Zahlen _enthält,_ der Datentyp ist aber trotzdem ein String. Das kann z.B. am Import der Daten liegen. Um trotzdem mit dieser Spalte rechnen zu können und um diese Spalte numerisch sortieren zu können, müssen wir sie in eine Zahl umwandeln. Das funktioniert in SQL mit der `cast`-Funktion.

```sql
-- Spalten und Datentypen ausgeben
describe organic_uk
```

Wir sehen als Ergebnis, dass die Spalte `HEADLINE` vom Typ String ist, wir wissen aber, das dort nur Zahlen enthalten sind. Daher wandeln wir um:

```sql
select HEADLINE
      ,cast(COMMENT_COUNT as int) as `Anzahl Kommentare`
from organic_uk
order by `Anzahl Kommentare` desc
```

## Wie extrahiert man Strings aus einem Array?

Zu diesem Thema verweise ich auf das Tutorial unten. Diese Frage wird konkret an [dieser Stelle](../../../content/tutorials/json-felder-mit-sql-verarbeiten.md#arrays-mit-sql-abfragen) beantwortet:

{% page-ref page="../../../content/tutorials/json-felder-mit-sql-verarbeiten.md" %}

## Wie entfernt man doppelte Tweets aus dem Datensatz?

Die Frage ist im Tutorial [Twitter-Daten mit SQL auswerten](../../../content/tutorials/twitter-daten-mit-sql-auswerten/#doppelte-tweets-herausfiltern) adressiert.

{% page-ref page="../../../content/tutorials/twitter-daten-mit-sql-auswerten/" %}

