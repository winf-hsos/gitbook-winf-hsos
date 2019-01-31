---
description: In dieser Session lernen wir Apache Spark kennen.
---

# Spark

## ❓ Fragen

* Wie funktioniert verteiltes Verarbeiten \(_distributed processing_\) mit Apache Spark?
* Welche Arten von Datenverarbeitung unterstützt Apache Spark?
* Welche Vorteile bietet 🏷Spark gegenüber 🏷MapReduce?

## 🏷 Begriffe

* 🏷 Spark _transformations_ vs _actions_
* 🏷 Resilient Distributed Dataset \(RDD\)
* 🏷 Dataframe

## 🔑 Key Points

🔑 Apache Spark repräsentiert Daten als 🏷Resilient Distributed Datasets \(RDD\).

🔑 Ein 🏷RDD ist eine Verkettung von Transformationen \( 🏷transformation\), die nacheinander ausgeführt werden. Ähnlich wie in einem Rezept. Die sequenziell ablaufenden Transformationen werden jedoch solange nicht ausgeführt, bis eine Aktion \( 🏷action\) ausgeführt wird. Ein Beispiel ist die Funktion `count()`, die alle Datensätze nach Anwendung sämtlicher Transformationen zählt und das Ergebnis zurückliefert.

🔑 Ein RDD besitzt keinerlei Struktur, jeder Datensatz \(oder jede Zeile\) wird als Zeichenkette interpretiert. In vielen Fällen gibt es aber eine Struktur in den Quelldaten, z.B. bei CSV-Dateien. Um diese Struktur in Spark nutzbar zu machen, können 🏷Dataframes verwendet werden. Ein Dataframe ist somit eine Abstraktionsschicht auf einem RDD und fügt die Information hinzu, wie aus einer Zeile Text eine Tabelle mit strukturierten Daten entsteht. Im Beispiel der CSV-Datei wäre das die einfache Regel, nach einem Trennzeichen wie Komma oder Semikolon zu suchen, und jede Zeile anhand dieser Trennzeichen in Spalten aufzuteilen.

## ▶ Session

### 1⃣ Übersicht Apache Spark

### 2⃣ Spark RDDs

### 3⃣ Spark Dataframes



