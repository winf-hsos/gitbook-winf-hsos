---
description: Nützliche SQL Abfragen für die Arbeit mit Twitter-Daten.
---

# Twitter-Daten mit SQL auswerten

## 💡 Datenqualität erhöhen

### 💡 Doppelte Tweets herausfiltern

Durch die Twitter API kann es vorkommen, dass einige Tweets doppelt in den Daten vorhanden sind. Das können wir in SQL beheben:

```sql
-- Auf doppelte Tweets prüfen
select id, count(1) 
from twitter_timelines
group by id 
order by count(1) desc
```

Wir sehen im Ergebnis, dass manche IDs zwei Mal vorkommen. Wir können mit der Window-Funktion `row_number()` innerhalb der gleichen ID jeder Zeile eine Nummer geben. Somit hat keine der beiden ansonsten gleichen Zeilen die gleiche `row_num`.

```sql
-- Zeilenummern generieren innerhalb einer ID-Gruppe
select id
,count(1) over(partition by id) as `occ`
,row_number() over(partition by id order by id) as `row_num`
from twitter_timelines
order by `occ` desc, id
```

Wenn wir jetzt das Ergebnis von oben als Unterabfrage verwenden und auf `row_num = 1` filtern, fallen alle doppelten Zeilen im Ergebnis raus:

```sql
-- Immer nur die erste Zeile selektieren
select * from (
    select * ,row_number() over(partition by id order by id) as `row_num`
    from twitter_timelines
)
where row_num = 1
```

## Informationen aus Tweets extrahieren

### 💡 Extrahieren der Koordinaten eines Tweets

Das Feld coordinates liefert uns die Koordinaten eines Tweets als Längen- und Breitengrad. Die Angabe bezieht sich dabei auf den Ort, von dem aus der Tweet abgeschickt wurde. Dieses Feld ist nur befüllt, wenn die verwendete Applikation diese Information bereitgestellt hat und der User die Freigabe der Koordinaten erteilt hat.

Folgendes SQL Statement ermittelt für einen Tweet die Angaben, die anschließend z.B. in Tableau visualisiert werden können:

```sql
select text
      ,user_location
      ,coordinates.coordinates[0] as `longitude` 
      ,coordinates.coordinates[1] as `latitude` 
from twitter_timelines
where coordinates is not null
```



