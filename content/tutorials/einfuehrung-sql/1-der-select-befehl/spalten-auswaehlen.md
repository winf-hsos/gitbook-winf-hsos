# Spalten auswählen

## 💡 Spalten auswählen - so geht’s

Mit SQL lassen sich einzelne Spalten einer Tabelle auswählen. Das folgende Statement wählt nur den Titel und die Beschreibung eines TED-Talks aus der Tabelle `ted_meta` aus.

```sql
select title, description 
from ted_meta
```

Die Syntax ist einfach: Zu selektierende Spalten \(oder allgemein Ausdrücke\) werden mit Kommata getrennt hinter dem SELECT Schlüsselwort aufgezählt:

```sql
-- Allgemeine Syntax für das Auswählen von Spalten
select <spalte 1>, <spalte 2>, ..., <spalte n>
from <tabellenname>
```

✔ Im Code-Block oben stellt die erste Zeile einen 🏷**Kommentar** dar. Kommentare beginnen mit einem Doppelminus \(`--`\) und werden nicht als SQL interpretiert und somit auch nicht ausgeführt. Kommentare erlauben uns somit, für andere Menschen verständliche Hinweis zu unseren SQL Abfragen zu formulieren 😎. 

Es ist immer eine gute Idee, genau die Spalten auszuwählen, die für die Beantwortung der Frage benötigt werden. In manchen Fällen möchte man aber vielleicht alle Spalten einer Tabelle auswählen, weil man z.B. die Spaltennamen noch nicht kennt. Für diesen Fall gibt es den so genannten Wildcard-Selektor `*`. Das folgende SQL Statement gibt **alle Spalten** der Tabelle `ted_meta` zurück:

```sql
select * from ted_meta
```

## 🧪 Übungsaufgaben

Wechselt zu Databricks und öffnet das Notebook 🗒\#1 Der SELECT Befehl. Versucht dort die unten stehenden Aufgaben mit passenden SQL Statements zu lösen.

#### Aufgabe 1.2

{% tabs %}
{% tab title="Aufgabe 1.2" %}
Schreibe eine SQL Abfrage, die für einen TED-Talk die Anzahl Kommentare und die Anzahl Views ermittelt. Gebt den Titel des Talks aus!
{% endtab %}

{% tab title="Lösung 1.2" %}
```sql
select title, comments, views
from ted_meta
```
{% endtab %}
{% endtabs %}

#### Aufgabe 1.3

{% tabs %}
{% tab title="Aufgabe 1.3" %}
Gib nur die Texte aller TED-Talks aus!
{% endtab %}

{% tab title="Lösung 1.3" %}
```sql
select text 
from ted_text
```
{% endtab %}
{% endtabs %}

## 💡 

