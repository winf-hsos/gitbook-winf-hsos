# Metadaten sichten

## 💡 Metadaten sichten - so geht’s

Bevor wir mit dem SELECT Befehl Daten abfragen stellen wir uns zunächst die Frage, welche Daten haben wir überhaupt vorliegen? Für die Verwendung von SQL müssen wir nämlich die 🏷**Struktur der Daten** - und damit sind die 🏷**Tabellen**, 🏷**Spalten** und 🏷**Datentypen** gemeint - möglichst gut kennen. Wie verschaffen wir uns also ein Bild darüber? Der Befehl `describe` hilft uns dabei:

```sql
describe ted_meta
```

Das Ergebnis ist eine Tabelle mit 3 Spalten und in diesem Fall 14 Zeilen, pro Spalte in der Zieltabelle eine Zeile. Die erste Spalte `col_name` beinhaltet den Namen der Spalte in der Tabelle `ted_meta`. Die zweite Spalte `data_type` gibt den 🏷**Datentyp** der Spalte an. Die letzte Spalte enthält einen Kommentar zu der Spalte, wenn dieser gepflegt wäre \(in diesem Fall gibt es keine Kommentare\).

![Das Ergebnis des DESCRIBE Befehls hat 3 Spalten.](../../../../.gitbook/assets/image%20%2814%29.png)

Diese Art von Informationen nennen wir 🏷**Metainformationen** \(oder Metadaten\). Sie beschreiben die Daten selbst, sind also Daten über Daten.

## 🏷 Datentypen

Eine Metainformation, die wir mit `describe` ermitteln können, ist der 🏷**Datentyp** einer Spalte. Der Datentyp gibt uns einen Hinweis, um welche Art von Information es sich bei der Spalte handelt. Genauer gesagt schränkt der Datentyp den 🏷**Wertebereich** \(oder Domäne\) ****der Spalte ein. Was heißt das konkret?

Nehmen wir die erste Spalte `id`. Diese hat laut der Tabelle oben den Datentyp `int`. Das wiederum steht für das Englische Wort 🏷**Integer**, was auf Deutsch gesagt eine Ganzzahl ist. Werte in der Spalte `id` müssen demnach ganze Zahlen sein \(1, 2, 3, usw.\). Dezimalzahlen mit Nachkommastellen sind nicht erlaubt. Genauso wenig sind Buchstaben erlaubt.

Jeder Datentyp in SQL sagt etwas darüber aus, welche Werte in der Spalten stehen dürfen. Einen Überblick über die wichtigsten Datentypen und deren Wertebereich gibt die folgende Tabelle:

| Datentyp | Bezeichnung | Beispielwerte |
| :--- | :--- | :--- |
| `int` | Integer oder Ganzzahl | -1, 0, 1, 2, 3 |
| `double` / `float` | Gleitkommazahlen | 1.5, 0.6666, -25.12  |
| `string` | Zeichenkette | "Hallo Welt", "me@mail.de" |
| `date` | Datum | 01.01.2019 |
| `timestamp` | Zeitstempel \(Sekunden seit dem 01.01.1970\) | 1549470029 |
| `boolean` | Wahrheitswert | true, false |

## 🧪 Übungsaufgaben

Wechselt zu Databricks und öffnet das Notebook 🗒\#1 Der SELECT Befehl. Versucht dort die unten stehenden Aufgaben mit passenden SQL Statements zu lösen.

#### Aufgabe 1.1

{% tabs %}
{% tab title="Aufgabe" %}
Ermittelt alle Spalten und Datentypen für die 3 anderen Tabellen `ted_text`, `ted_ratings` und `ted_tags.`
{% endtab %}

{% tab title="Lösung" %}
```sql
describe ted_text
describe ted_ratings
describe ted_tags
```
{% endtab %}
{% endtabs %}

