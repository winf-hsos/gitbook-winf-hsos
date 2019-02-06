# \#1 Der SELECT Befehl

## 🎯 Lernziele

* 🎯 Ihr kennt die Syntax des SELECT Befehls, mit dem Daten aus Tabellen in beliebiger Weise abgefragt werden können.
* 🎯 Ihr kennt die unterschiedlichen Komponenten des SELECT Befehls und versteht, wie diese das Ergebnis verändern. 
* 🎯 Ihr könnt einfach Abfragen mithilfe des SELECT Befehls formulieren, um Fragestellungen auf Basis von Daten zu beantworten.

## 🔑 Key Points

🔑 Mit dem SELECT Befehl können **strukturierte Daten** aus einer Datenbank abgefragt werden. Mit strukturierten Daten sind Daten gemeint, die sich in Zeilen einer Tabelle abbilden lassen, wobei die Tabelle aus _1_ bis _n_ Spalten besteht. Stellt euch als Analogie ein Excel-Spreadsheet vor.

🔑 Jede Spalte einer Tabelle enthält genau einen Wert bzw. ein **Attribut** des Datensatzes. Für jedes Attribut ist festgelegt, welchen Wertebereich es annehmen darf \(z.B. eine ganze Zahl, einen beliebigen Text, ein Datum etc.\). Je nach Definition der möglichen Werte besitzt eine Spalte einen bestimmten **Datentyp**.

🔑 In SQL häufig verwendete **Datentypen** sind:

* Ganze Zahlen \(Integer oder `int`\)
* Gleitkommazahlen \(`double` oder `float`\)
* Zeichenketten \(`string`\)
* Datum \(`date`\)
* Zeitstempel \(`timestamp`\)
* Wahrheitswerte \(`boolean`\)

🔑 Während eine Tabelle beliebig viele Spalten haben kann, erlaubt der SELECT Befehl das Auswählen einer Teilmenge der vorhandenen Spalten. Denn häufig benötigt man für die Beantwortung einer Fragestellung nur wenige Spalten. Das Auswählen einer Teilmenge nennt man in der relationalen Algebra auch **Projektion**.

## ✅ Metadaten sichten \(`DESCRIBE`\)

Bevor wir mit dem SELECT Befehl Daten abfragen stellen wir uns zunächst die Frage, welche Daten haben wir überhaupt vorliegen? Für die Verwendung von SQL müssen wir nämlich die **Struktur der Daten** - und damit sind die Tabellen, Spalten und Datentypen gemeint - möglichst gut kennen. Wie verschaffen wir uns also ein Bild darüber? Der Befehl DESCRIBE hilft uns dabei:

```sql
describe ted_meta
```

Das Ergebnis ist eine Tabelle mit 3 Spalten und in diesem Fall 14 Spalten. Die erste Spalte `col_name` beinhaltet den Namen der Spalte in der Tabelle `ted_meta`. Die zweite Spalte `data_type` gibt den **Datentyp** der Spalte an. Die letzte Spalte enthält einen Kommentar zu der Spalte, wenn dieser denn gepflegt wäre \(in diesem Fall gibt es keine Kommentare\).

![Das Ergebnis des DESCRIBE Befehls hat 3 Spalten.](../../../.gitbook/assets/image%20%2811%29.png)

Diese Art von Informationen nennen wir **Metainformationen** \(oder Metadaten\). Sie beschreiben die Daten selbst, sind also Daten über Daten.

## ✅ Spalten auswählen \(`SELECT` / `FROM`\)

### 💡 So geht's

Mit SQL lassen sich einzelne Spalten einer Tabelle auswählen. Das folgende Statement wählt nur den Titel und die Beschreibung eines TED-Talks aus der Tabelle `ted_meta` aus.

```sql
select title, description 
from ted_meta
```

Die Syntax ist einfach: Zu selektierende Spalten \(oder allgemein Ausdrücke\) werden mit Kommata getrennt hinter dem SELECT Schlüsselwort aufgezählt.

### 🤔 Übungsaufgaben

#### Aufgabe 1.1

{% tabs %}
{% tab title="Aufgabe" %}
Schreibt eine SQL Abfrage, die für einen TED-Talk die Anzahl Kommentare und die Anzahl Views ermittelt. Gebt den Titel des Talks aus!
{% endtab %}

{% tab title="Lösung" %}
```sql
select title, comments, views
from ted_meta
```
{% endtab %}
{% endtabs %}

#### Aufgabe 1.2

{% tabs %}
{% tab title="Aufgabe" %}
Gebt nur die Texte aller TED-Talks aus!
{% endtab %}

{% tab title="Lösung" %}
```sql
select text 
from ted_text
```
{% endtab %}
{% endtabs %}



