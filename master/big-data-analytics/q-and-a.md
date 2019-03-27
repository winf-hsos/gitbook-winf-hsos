---
description: >-
  Hier findet ihr die Fragen und Antworten, die während des Semesters gestellt
  wurden.
---

# Q & A

## Wie wandelt man einen String in eine Zahl um?

In manchen Fällen wissen wir, dass eine Spalte zur Zahlen enthält. Der Datentyp ist aber trotzdem ein String. Um damit rechnen zu können und um diese Spalte numerisch sortieren zu können, müssen wir diese Spalte in eine Zahl umwandeln. Das funktioniert in SQL mit der `cast`-Funktion.

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

Das Thema Arrays wird im Tutorial behandelt:

{% page-ref page="../../content/tutorials/json-felder-mit-sql-verarbeiten.md" %}



