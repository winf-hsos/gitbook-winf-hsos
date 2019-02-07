# Zeilen filtern

## 💡 Zeilen Filtern - so geht’s

### Strings \(oder Zeichenketten\)

#### Der `=` Operator

Im vorigen Schritt haben wir gesehen, wie wir die Menge der **Spalten** im Ergebnis einschränken können. Häufig müssen wir für die Beantwortung einer Frage auch nur bestimmte die **Zeilen** auswählen. Auch das geht mit SQL, und zwar mit der `WHERE` Klausel. Das folgende SQL Statement gibt nur Zeilen zurück, in denen die Spalte `main_speaker` dem Wert "Al Gore" entspricht:

```sql
select * from ted_meta
where main_speaker = 'Al Gore'
```

Im Beispiel oben verwenden wir die `WHERE` Klausel, um ein Feld vom Datentyp `string` zu filtern. Genauer gesagt wird für alle Datensätze der Wert in der Spalte `main_speaker` mit dem Wert 'Al Gore' verglichen. Es werden nur die Datensätze im Ergebnis behalten, bei denen der Vergleich wahr \(`true`\) zurückliefert. 

💡 Bei Vergleichen zweier Zeichenketten \(oder _Strings_\) müssen wir immer **einfache Anführungszeichen** verwenden. Weil Strings auch Leerzeichen oder andere Sonderzeichen enthalten können, wäre sonst nicht klar, wo das Ende des Strings ist.

#### Der `LIKE` Operator

Neben dem `=` Operator für Stringvergleiche gibt es mit dem `LIKE` Operator eine weitere wirkungsvolle Weise, um Vergleiche aus Zeichenketten durchzuführen. Der LIKE Operator erlaubt es uns, Strings mit Teilstrings zu vergleichen. Das folgende SQL Statement liefert alle TED Talks zurück, bei denen im Titel das Wort 'food' vorkommt:

```sql
select * from ted_meta
where title like '%food%'
```

⚠ Bitte beachtet, dass SQL _case sensitive_ ist. Was heißt das? Es ist ein Unterschied, ob wir nach '**f**ood' oder '**F**ood' im Titel suchen. Groß- und Kleinschreibung wird unterschieden. Das obige SQL Statement würde somit einen Titel wie 'Food is important' nicht im Ergebnis enthalten. Um das zu umgehen, wird häufig die zu vergleichende Spalte mit der Funktion `lower()` in Kleinbuchstaben umgewandelt:

```sql
select * from ted_meta
where lower(title) like '%food%'
```

Das `%` Zeichen in den obigen Statements ist so zu lesen: Es ist egal was vor oder nach dem Wort 'food' kommt, wichtig ist nur, dass das Wort _irgendwo_ vorkommt. Wir können das `%` Zeichen auch so setzen, dass wir z.B. nur Titel mit 'food' am Anfang im Ergebnis haben:

```sql
select * from ted_meta
where lower(title) like 'food%'
```

Jetzt muss 'food' am Anfang der Spalte title stehen, und es ist egal was danach kommt. Genauso können wir auch nach 'food' am Ende suchen:

```sql
select * from ted_meta
where lower(title) like '%food'
```

Wir können die `%` Zeichen auch beliebig setzen, um nach dem Vorkommen unterschiedlicher Wörter zu suchen:

```sql
select * from ted_meta
where lower(title) like '%food%smart'
```

Das obige Statement liefert TED Talks zurück, deren Titel die Wörter 'food' und 'smart' in genau dieser Reihenfolge beinhalten. Ihr seht schon, der `LIKE` Operator kann sehr mächtig sein. Ein letztes Beispiel: Ihr wollt sicherstellen, dass vor dem Wort 'food' nicht noch ein anderes Wort steht, wie z.B. in 'seafood'. Das könnt ihr z.B. so lösen:

```sql
select * from ted_meta
where lower(title) like '% food%'
```

Seht ihr den Unterschied? Es wurde vor 'food' ein Leerzeichen gesetzt, also ' food'. Das Wort 'seafood' würde somit nicht von diesem Vergleich gefunden werden. Allerdings wäre so auch ein Titel mit 'food' am  Anfang außen vor, weil ein Titel nie mit einem Leerzeichen beginnt. Um das zu lösen, müssen wir **mehrere** `WHERE` **Bedingungen miteinander verknüpfen**:

```sql
select * from ted_meta
where lower(title) like '% food'
or lower(title) like 'food%'
```

### Verknüpfung mehrerer Bedingungen \(`AND` / `OR`\)

Wie oben gezeigt können wir mit `WHERE` die erste Filterbedingung definieren und anschließend weitere mit den logischen Verknüpfungen `OR` oder `AND` hinzufügen. Auf diese Weise können wir beliebig viele Bedingungen definieren. Dabei können sich Bedingungen auf jede beliebige Spalte beziehen:

```sql
select * from ted_meta
where title like '%food%'
and event = 'TED2010'
```

Bei der Anwendung der Bedingungen gelten grundsätzlich die Regeln der Logik. Das bedeutet wir können auch Klammern verwenden, um Gruppen von Bedingungen zu bilden und diese miteinander zu verknüpfen.

### Zahlenwerte

Beim Filtern auf numerischen Spalten haben wir sämtliche Möglichkeiten, die uns die Arithmetik bereitstellt, um Zahlen miteinander zu vergleichen:

* `=` : 2 Zahlen müssen exakt gleich sein.
* `>` bzw. `>=`: die erste Zahl muss größer bzw. größer gleich der zweiten Zahl sein.
* `<` bzw. `<=`: die erste Zahl muss kleiner bzw. kleiner gleich der zweiten Zahl sein.
* `<>`: 2 Zahlen müssen ungleich sein.

Im einfachsten Fall nutzen wir den `=` Operator, um einen TED Talk mit einer bestimmten ID zu finden:

```sql
select * from ted_meta 
where id = 1
```

#### Der `IN` Operator

Angenommen wir wollen nun nicht nur den Talk mit der ID = 1, sondern auch den mit der ID = 100 selektieren. Wir können hier auf die bereits bekannte Verknüpfung von Bedingungen zurückgreifen:

```sql
select * from ted_meta
where id = 
or id = 100
```

Hätten wir nun eine Liste mit 5 IDs könnten wir entsprechend 3 weitere Bedingungen mit `OR` verknüpfen. Glücklicherweise gibt es eine einfachere Möglichkeit:

```sql
select * from ted_meta
where id IN (1, 100, 101, 102, 200)
```

Mit dem IN Operator können wir den Wert einer Spalte auf die Zugehörigkeit zu einer Menge, die wir mit Komma getrennt in Klammern definieren, überprüfen. Wenn der Wert sich in der Menge befinden wir die Bedingung wahr.

#### Größer \(gleich\) und kleiner \(gleich\)

Das nächste Beispiel fragt nach allen TED Talks, die länger als 20 Minuten sind \(das Feld `duration` enthält die Länge in Sekunden\):

```sql
select * from ted_meta 
where duration > 60 * 20
```

💡 Wie ihr an dem Beispiel oben erkennt, können wir auf beiden Seiten der Gleichung nicht nur atomare Werte wie Zahlen oder Spaltennamen verwenden, sondern wir können auch **Ausdrücke** für Bedingungen verwenden☝. Im Beispiel oben ist der rechte Teil `60 * 20` ein Ausdruck, der die beiden Zahlen miteinander multipliziert und das Ergebnis `1200` mit dem Wert der Spalte `duration` vergleicht.

Ein weiteres Beispiel zeigt, wie auch Zahlenvergleiche kombiniert werden können, um in diesem Fall alle TED Talks mit mindestens 5 Minuten Länge UND maximal 10 Minuten Länge zu erfragen:

```sql
select * from ted_meta
where duration >= 5 * 60 
and duration <= 10 * 60
```

#### Der `BETWEEN` Operator

Das selbe Ergebnis kann in diesem Fall mit dem `BETWEEN` Operator erzielt werden:

```sql
select * from ted_meta
where duration between 5 * 60 and 10 * 60
```

⚠ Der `BETWEEN` Operator schließt immer die angegebenen Grenzen mit in das Ergebnis ein \(_inclusive_\).

#### Der `NOT` Operator

Um das Ergebnis des letzten Beispiels umzukehren, also alle Talks zu finden, deren Länge außerhalb der Spanne 5 - 10 Minuten liegen, können wir den `NOT` Operator verwenden. Dieser negiert eine Bedingung in ihr Gegenteil ✋:

```sql
select * from ted_meta
where duration not between 5 * 60 and 10 * 60
```

### Bool'sche Werte

Für Spalten vom Datentyp `boolean` kommen in den meisten fällen nur die Operatoren `=` und `<>` in Frage. Angenommen die Tabelle `ted_meta` hätte Spalte `best_talk` vom Typ `boolean`, dann könnten wir alle Talks, die für ihre jeweiliges Event zum besten Talk gewählt wurden, mit folgenden SQL Statement ermitteln:

```sql
select * from ted_meta
where best_talk = true
```

### Datums- und Zeitwerte

Der Vergleich von Datums- und Zeitwerten funktioniert rudimentär über die arithmetischen Vergleichsoperatoren `<`, `<=`, `>`, `>=`, `=` und `<>`. Häufig brauchen wir aber Vergleiche, die über diese einfachen Operationen hinaus gehen, wie z.B.:

* Alle Talks des Jahres 2010
* Alle Events die in den Monaten Juni, Juli und August stattfanden
* Alle Talks, die nicht mehr als 3 Jahre zurückliegen

Für diese Anwendungen verweise ich auf den Abschnitt [\#8 Datum und Zeit](../8-datum-und-zeit.md), in dem spezielle Funktionen für den Umgang mit Datums- und Zeitwerten eingeführt werden.

## 🧪 Übungsaufgaben

Wechselt zu Databricks und öffnet das Notebook 🗒\#1 Der SELECT Befehl. Versucht dort die unten stehenden Aufgaben mit passenden SQL Statements zu lösen.

#### Aufgabe 1.3

{% tabs %}
{% tab title="Aufgabe" %}
Ermittele den Titel und die Anzahl Viewer für alle TED Talks des offiziellen TED 2005 Events.
{% endtab %}

{% tab title="Lösung" %}
```sql
select title, views
from ted_meta
where event = 'TED2005'
```
{% endtab %}
{% endtabs %}

#### Aufgabe 1.4

{% tabs %}
{% tab title="Aufgabe" %}
Gib eine Liste der Talks von Sam Harris, Steven Pinker und Amy Cuddy aus.
{% endtab %}

{% tab title="Lösung" %}
```sql
select * from ted_meta
where main_speaker IN ('Sam Harris', 'Steven Pinker', 'Amy Cuddy')
```
{% endtab %}
{% endtabs %}

#### Aufgabe 1.5

{% tabs %}
{% tab title="Aufgabe" %}

{% endtab %}
{% endtabs %}

## Anhang

Die Tabelle gibt eine Übersicht über die gängigsten Vergleichsoperatoren.

| Operator | Beschreibung | Anwendbar auf... |
| :--- | :--- | :--- |
| `=` | Prüft, ob zwei Werte exakt gleich sind. | Alle Datentypen. |
| `>`, `<`, `>=`, `<=` | Prüft, ob der erste Wert größer/kleiner/größer gleich/kleiner gleich als der zweite ist. | Vorrangig verwendet für numerische Spalten wie `int`, `double`, `float`, aber auch für `string`, `date`, `timestamp` und `boolean` anwendbar. |
| `<>` | Prüft, ob zwei Werte ungleich sind. | Alle Datentypen. |
| `NOT` | Negiert eine Bedingung. | Alle Bedingungen. |
| `LIKE` | Prüft, ob eine Zeichenkette einen oder mehrer Bestandteile besitzt. | `string` |
| `BETWEEN` | Prüft, ob ein Wert sich innerhalb einer bestimmten Spanne befindet. | Vorrangig verwendet für numerische Spalten wie `int`, `double`, `float`, aber auch für `string`, `date`, `timestamp` und `boolean` anwendbar. |
| `IN` | Prüft, ob ein Wert in einer bestimmten Menge enthalten ist. | Alle Datentypen. |

