# Zeilen filtern

## 💡 Zeilen Filtern - so geht’s

Im vorigen Schritt haben wir gesehen, wie die Menge der **Spalten** im Ergebnis eingeschränkt werden können. Häufig müssen aber für die Beantwortung einer Frage auch nur bestimmte **Zeilen** im Ergebnis vorhanden sein. Auch das geht mit SQL, und zwar mit der `WHERE` Klausel. Das folgende SQL Statement gibt nur Zeilen zurück, in denen die Spalte `main_speaker` dem Wert "Al Gore" entspricht:

```sql
select * from ted_meta
where main_speaker = 'Al Gore'
```

Das Beispiel oben verwendet die `WHERE` Klausel, um ein Feld vom Datentyp `string` zu filtern. Genauer gesagt wird für alle Datensätze der Wert in der Spalte `main_speaker` mit dem Wert "Al Gore" verglichen, und es es werden nur die Datensätze im Ergebnis behalten, bei denen der Vergleich wahr \(`true`\) zurückliefert. 

💡 Bei Vergleichen zweier Zeichenketten \(oder _Strings_\) müssen wir immer Anführungszeichen verwenden. Weil Strings auch Leerzeichen oder andere Sonderzeichen enthalten können wäre sonst nicht klar, wo das Ende des Strings ist.

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

