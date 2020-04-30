# Simple Aggregations

## Einfache Aggregationen - so geht’s

Bisher entsprach jede Zeile im Ergebnis eines SQL Statements auch immer einer Zeile im Datensatz. Die Daten wurden bisher nicht verdichtet. Das wollen wir jetzt ändern.

Gerade bei großen Datenmengen interessieren wir uns oft nicht für einzelne Zeilen, sondern für **berechnete Größen auf Basis vieler Zeilen**. Hier kommen die 🏷**Aggregationsfunktionen** ins Spiel, die in der folgenden Tabelle aufgelistet sind.

| Aggregationsfunktion | Beschreibung |
| :--- | :--- |
| `COUNT` | Zählt die Datensätze. |
| `SUM` | Bildet die Summe über eine Spalte. |
| `AVG` | Bildet den Durchschnittswert \(arithmetisches Mittel\) einer Spalte. |
| `MIN` | Ermittelt den kleinsten Wert über eine Spalte hinweg. |
| `MAX` | Ermittelt den größten Wert über eine Spalte hinweg. |
| `DISTINCT` | Ermittelt eindeutige Werte innerhalb einer Spalte, entfernt also doppelte Werte. |

Nehmen wir an, wir wollen alle TED Talks zählen:

```sql
select count(*) as `Anzahl Talks` from ted_meta
```

### Spalten im Ergebnis umbenennen

Im obigen Beispiel wird ein Ergebnis mit einer Spalte zurückgeliefert, das die Anzahl der Datensätze in der Tabelle `ted_meta` enthält. Wie ihr dem Screenshot unten entnehmen könnt, hat die Spalte den Namen 'Anzahl Talks'. Diesen Namen haben wir oben im SQL Statement mithilfe des `as` Schlüsselwortes definiert. Bei genauem Hinschauen sieht man, dass der Name in _accents graves_ gesetzt wurde. Das ist nur dann zwingend notwendig, wenn der Name Leerzeichen enthält oder selbst ein SQL Schlüsselwort ist. Um Fehler zu vermeiden ist es eine gute Angewohnheit, diese Konvention von Anfang an beizubehalten.

Auf diese Weise können sämtliche Spalten eines SQL Statements umbenannt werden. Für eine schönere und lesbare Ausgabe ist das häufig ratsam.

![](../../.gitbook/assets/image%20%2849%29.png)

Die anderen Aggregationsfunktionen machen das, was man intuitiv erwartet. 

Wie viele Views hatten alle Talks des TED 2010 Events?

```sql
select sum(views) as `Summe der Views`
from ted_meta
where event = 'TED2010'
```

Was ist die durchschnittliche Länge eines TED-Talks?

```sql
select avg(duration / 60) as `Durchschnittliche Länge in Minuten`
from ted_meta
```

Wie lang ist der längste und kürzeste TED Talk?

```sql
select max(duration / 60) as `Dauer des längsten Talks in Minuten`
      ,min(duration / 60) as `Dauer des kürzesten Talks in Minuten`
from ted_meta
```

Welche Sprecher haben einen TED-Talk gehalten \(doppelte Speaker entfernt\):

```sql
select distinct main_speaker
from ted_meta
```

Wie viele Speaker waren das insgesamt?

```sql
select count(distinct main_speaker) as `Anzahl unterschiedliche Speaker`
from ted_meta
```

## Übungsaufgaben

#### Aufgabe 1.8

{% tabs %}
{% tab title="Aufgabe 1.8" %}
Wie viele Kommentare gab es über alle Talks hinweg?
{% endtab %}

{% tab title="Lösung 1.8" %}
```sql
select sum(comments) as `Anzahl Kommentare`
from ted_meta
```
{% endtab %}
{% endtabs %}

#### Aufgabe 1.9

{% tabs %}
{% tab title="Aufgabe 1.9" %}
Von wann ist der neueste und älteste TED Talk im Datensatz?
{% endtab %}

{% tab title="Lösung 1.9" %}
```sql
select min(film_date) as `Ältester Talk`
      ,max(film_date) as `Neuester Talk`
from ted_meta
```
{% endtab %}
{% endtabs %}

