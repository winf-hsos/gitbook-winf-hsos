# Gruppierungen

## 💡 Gruppieren - so geht’s

Ihr habt gerade gesehen, wie man einfach Aggregationen, wie das Zählen oder Summieren, auf alle Datensätze in der Tabelle anwenden kann. Oftmals möchte man aber **einen Wert pro Gruppe** innerhalb der Daten ermitteln. Das funktioniert mit der `GROUP BY` Klausel.

```sql
select event
      ,avg(duration / 60) as `Durchschnittliche Dauer in Minuten`
from ted_meta
group by event
order by avg(duration /60) desc
```

Die SQL Abfrage oben ermittelt die durchschnittliche Dauer eines Talks in Minuten **pro Event.** Das heißt, es gibt nicht eine Zeile als Ergebnis, sondern eine Zeile pro Event. Zusätzlich wird noch nach der Dauer sortiert, so dass die Events mit den längsten Talks im Durchschnitt oben erscheinen.

Wir können auch nach mehreren Spalten oder Kriterien gruppieren:

```sql
select event
      ,speaker_occupation
      ,avg(duration / 60) as `Durchschnittliche Dauer in Minuten`
from ted_meta
group by event, speaker_occupation
order by avg(duration /60) desc
```

Unsere Gruppen sind nun etwas feiner, d.h. wir bekommen im Ergebnis mehr Spalten. Eine pro Event und Beruf des Speakers.

## Achtung: Beliebte Fehlerquelle

⚠ Ein häufiger Fehler beim Erstellen von SQL-Abfragen ist das Vergessen von Spalten in der Gruppierung. In diesem Fall bekommt man die folgende Fehlermeldung, die immer die gleiche Lösung hat:

![Beliebter Fehler: Vergessen zu gruppieren.](../../../../.gitbook/assets/image%20%2811%29.png)

Im Screenshot oben wurde die Spalte `speaker_occupation` nicht in der Gruppierung aufgeführt, was zu diesem Fehler führt. ☝Als Faustregel gilt: Alle Spalten, auf die keine Aggregationsfunktion angewendet werden, müssen in der `GROUP BY` Klausel auftauchen.

## 🧪 Übungsaufgaben

#### Aufgabe 1.10

{% tabs %}
{% tab title="Aufgabe 1.10" %}
Ermittelt die Anzahl TED Talks pro Jahr. \(Tipp: Das Jahr bekommt ihr mit `year(film_date)`\)
{% endtab %}

{% tab title="Lösung 1.10" %}
```sql
select year(film_date) as `Jahr`
      ,count(1) as `Anzahl Talks`
from ted_meta
group by `Jahr`
order by `Jahr`
```
{% endtab %}
{% endtabs %}

