---
description: In dieser Lerneinheit geht es die Erkundung eines neuen Datensatzes mit SQL.
---

# Exploration unbekannter Daten

## ❓ Fragen

* Welche Spalten hat der neue Datensatz und welchen Datentyp haben die Spalten?
* Wie viele Zeilen sind in den Datensätzen jeweils enthalten?
* Wie ist die Verteilung der Werte in den einzelnen Spalten des Datensatzes?
* Wie ist es um die Datenqualität beschaffen?
* Wie ist der zeitliche Bezug der Daten?

## 🏷 Begriffe

* 🏷 Datentypen
* 🏷 JSON
* 🏷Domain \(Wertebereich\)

## ▶ Lerneinheit

### 1⃣ Exploration neuer Daten mittels SQL

Führt das folgende Tutorial durch, um wichtige Funktionen für die Erkundung eines neuen Datensatzes kennenzulernen. Wendet die Abfragen auf die Datensätze der Fallstudie an. Nutzt dazu die bereitgestellten [Databricks Notebook Templates im Anhang dieser Veranstaltung](../anhang/#notebook-templates), um die Daten in euren Account zu laden. Beginnt anschließend mit der Erkundung der Daten.

{% page-ref page="../../../../introduction-to-sql/daten-mit-sql-erkunden.md" %}

### 2⃣ Spalten mit einer Baumstruktur \(JSON-Objekte\)

Je nach Datensatz werdet ihr feststellen, dass manche Spalten eine spezielle Struktur aufweisen. Es sind darin keine atomaren Werte wie Zahlen oder Datumswerte gespeichert, sondern ganze Objekte mit einer eigenen Struktur. Diesen Spaltentyp nennen wir ein 🏷JSON-Objekt. In den folgenden beiden Tutorials lernt ihr, was es damit auf sich hat und wie wir diese Spalten mittels SQL abfragen können. 

Wendet die Konzepte auf die entsprechenden Spalten eurer Datensätze an.

{% page-ref page="../../../../javascript-fuers-web/einfuehrung-in-json.md" %}

## 🔗 Links

Unter dem folgenden Link findet ihr eine Zusammenfassung der wichtigsten SQL-Funktionen auf 2 Seiten:

{% page-ref page="../../../../cheatsheet-sql.md" %}

