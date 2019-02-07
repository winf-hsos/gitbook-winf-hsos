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

⚠ Bitte beachtet, dass SQL _case sensitive_ ist. Was heißt das? Es macht einen Unterschied, ob wir nach '**f**ood' oder '**F**ood' im Titel suchen. Groß- und Kleinschreibung wird unterschieden. Das obige SQL Statement würde somit einen Titel wie 'Food is important' nicht im Ergebnis enthalten. Um das zu umgehen, wird häufig die zu vergleichende Spalte mit der Funktion `lower()` in Kleinbuchstaben umgewandelt:

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

### Verknüpfung mehrere Bedingungen

Wie oben gezeigt können wir mit `WHERE` die erste Filterbedingung definieren und anschließend weitere mit den logischen Verknüpfungen `OR` oder `AND` hinzufügen. Auf diese Weise können wir beliebig viele Bedingungen definieren. Dabei können sich Bedingungen auf jede beliebige Spalte beziehen:

```sql
select * from ted_meta
where title like '%food%'
and event = 'TED2010'
```

Bei der Anwendung der Bedingungen gelten grundsätzlich die Regeln der Logik. Das bedeutet wir können auch Klammern verwenden, um Gruppen von Bedingungen zu bilden und diese miteinander zu verknüpfen:



### Zahlenwerte



## 🧪 Übungsaufgaben

Wechselt zu Databricks und öffnet das Notebook 🗒\#1 Der SELECT Befehl. Versucht dort die unten stehenden Aufgaben mit passenden SQL Statements zu lösen.

#### Aufgabe 1.3

{% tabs %}
{% tab title="Aufgabe" %}

{% endtab %}

{% tab title="Lösung" %}

{% endtab %}
{% endtabs %}

#### Aufgabe 1.4

{% tabs %}
{% tab title="Aufgabe" %}

{% endtab %}

{% tab title="Lösung" %}

{% endtab %}
{% endtabs %}

#### Aufgabe 1.5

{% tabs %}
{% tab title="Aufgabe" %}

{% endtab %}
{% endtabs %}

