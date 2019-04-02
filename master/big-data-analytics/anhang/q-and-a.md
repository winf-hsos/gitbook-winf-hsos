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

Durch die API kann es vorkommen, dass einige Tweets doppelt in den Daten vorhanden sind. Das können wir in SQL beheben:

```sql
-- Auf doppelte Tweets prüfen
select id, count(1) 
from twitter_timelines
group by id 
order by count(1) desc
```

Wir sehen dass manchen ID 2x vorkommen. Wir können mit der Window-Funktion `row_number()` innerhalb der gleichen ID jeder Zeile eine Nummer geben. Somit hat keine der beiden ansonsten gleichen Zeilen die gleiche `row_num`.

```sql
-- Zeilenummern generieren innerhalb einer ID-Gruppe
select id
,count(1) over(partition by id) as `occ`
,row_number() over(partition by id order by id) as `row_num`
from twitter_timelines
order by `occ` desc, id
```

Wenn wir jetzt das Ergebnis von oben als Unterabfrage verwenden und auf row\_num = 1 filtern, fallen alle doppelten Zeilen im Ergebnis raus.

```sql
-- Immer nur die erste Zeile selektieren
select * from (
    select * ,row_number() over(partition by id order by id) as `row_num`
    from twitter_timelines
)
where row_num = 1
```

