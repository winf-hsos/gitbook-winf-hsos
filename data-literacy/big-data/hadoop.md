---
description: In dieser Session lernen wir Hadoop kennen.
---

# Hadoop, Spark & Co.

## Questions

**Apache Hadoop**

* Was ist Hadoop und welche Komponenten gehören dazu?
* Warum ist Hadoop eine gute Lösung für die Herausforderungen von Big Data?
* Wie löst HDFS das Problem, große Datenmengen effizient und ausfallsicher zu speichern?
* Wie funktioniert MapReduce?
* Warum können mittels MapReduce sehr große Datenmengen in kurzer Zeit verarbeitet werden?
* Welche Nachteile hat MapReduce im Vergleich zu neueren Alternativen?
* Was sind Anwendungsbeispiele des MapReduce-Algorithmus?

**Apache Spark**

* Wie funktioniert verteiltes Verarbeiten \(_distributed processing_\) mit Apache Spark?
* Welche Arten von Datenverarbeitung unterstützt Apache Spark?
* Welche Vorteile bietet Apache Spark gegenüber MapReduce?

## Terms

* Verteiltes Dateisystem \(Distributed Filesystem\)
* Verteilte Datenverarbeitung \(Distributed Processing\)
* Cluster
* HDFS
* MapReduce
  * Data Node
  * Worker Node
  * Name Node
* Apache Spark
* Spark _transformations_ vs _actions_
* Resilient Distributed Dataset \(RDD\)
* Dataframe

## HDFS, MapReduce & Apache Spark

{% embed url="https://docs.google.com/presentation/d/1ul2cIIwSN4Ldvzq6IcoBykNM4GrnjDnwm6lqTcrTGsw/preview" %}

## Key Points

### Apache Hadoop

* Hadoop ist der Name eines [Apache Open Source Projektes](https://hadoop.apache.org/), dass sich mit der Speicherung und Verarbeitung sehr großer Datenmengen \(**Big Data**\) befasst. 
* Die wichtigsten Bestandteile von Hadoop sind das **HDFS** und das **MapReduce** Framework. Das HDFS ist ein verteiltes Dateisystem \(_distributed filesystem_\) und kümmert sich um die Speicherung sehr großer Datenmengen. MapReduce ist ein Ansatz für die parallele und verteilte Verarbeitung \(_parallel and distributed processing_\) großer Datenmengen. **MapReduce** hängt von einem verteilten Dateisystem wie HDFS ab. 
* **HDFS** und **MapReduce** verwenden für die verteilte Speicherung und die parallele Verarbeitung ein so genanntes Hadoop **Cluster**. Ein Cluster ist eine Verbund mehrerer Rechner \(Server\), die sich die Arbeitslast untereinander teilen. Einzelne Rechner in einem Cluster werden Knoten genannt \(_nodes_\).  
* In einem Hadoop Cluster werden drei Arten von Knoten unterschieden: **Data Nodes**, **Worker Nodes** und der **Name Node**. Data Nodes sind Teil des **HDFS** und speichern Daten. Worker Nodes sind verarbeitende Knoten im Kontext von MapReduce. Dem Name Node kommt eine zentrale Rolle zu: Nur er weiß, auf welchen Knoten welche Blöcke \(Daten\) abgelegt sind und kann auf Anfrage hin die richtigen Blöcke zur ursprünglichen Datei zusammensetzen. Der Name Node als Verwalter sämtlicher Metadaten ist der zentrale Zugang zum Hadoop **Cluster**. 
* Wenn wir eine Datei im **HDFS** speichern wird sie zunächst in Blöcke gleicher Größe \(im Standard 128 MB\) zerlegt und jeder Block anschließend auf mindestens 3 Rechnern \(_nodes_\) gespeichert. Durch die redundante Speicherung jedes Blocks wird eine hohe Ausfallsicherheit gewährleistet. Sollte ein Knoten ausfallen, existieren noch 2 weitere Kopien. 
* Wenn eine Datei aus dem **HDFS** abgerufen wird, fragt zunächst der Name Node die notwendigen Blöcke bei den entsprechenden Rechner, auf denen sie gespeichert wurden, an. Anschließend werden die Blöcke in der richtigen Reihenfolge zur angefragten Datei zusammengefügt und zurückgeliefert. 
* Von Außen betrachtet sieht das **HDFS** wie ein gewöhnliches Verzeichnissystem aus, wie man es z.B. aus dem Windows-Explorer gewohnt ist. Auch das Verhalten ist gleich. Die Komplexität, die im Hintergrund für die hohe Performanz und die Ausfallsicherheit sorgt, wird vor dem Benutzer versteckt. 
* **MapReduce** ist ein Verfahren für die parallele Verarbeitung großer Datenmengen. Ein großer Datensatz wird dabei in kleinere Teile gesplittet, die parallel und unabhängig voneinander auf unterschiedlichen Rechnern \(w_orker nodes_\) im Cluster verarbeitet werden. Die Ergebnisse der Teilprozesse werden anschließend zum Gesamtergebnis zusammengeführt \(_reduce_\). 
* Ein bekanntes Beispiel für den MapReduce-Algorithmus ist das Word Count Beispiel. Es geht darum, in einem oder vielen Texten das Vorkommen einzelner Wörter zu zählen und als Ergebnis eine \(sortierte\) Liste `<Wort, Anzahl>` auszugeben. Häufig wird dies am Beispiel der Wikipedia Enzyklopädie demonstriert. MapReduce teilt den Text in kleinere Abschnitte, in denen von je einem _Worker Node_ die Wörter gezählt werden. Jeder _Worker Node_ liefert sein Teilergebnis zurück und die Teilergebnisse werden zu dem Gesamtergebnis aggregiert \(_reduce_\).

### Apache Spark

* Apache Spark repräsentiert Daten als 🏷Resilient Distributed Datasets \(RDD\). 
* Ein 🏷RDD ist eine Verkettung von Transformationen \( 🏷transformation\), die nacheinander ausgeführt werden. Ähnlich wie in einem Rezept. Die sequenziell ablaufenden Transformationen werden jedoch solange nicht ausgeführt, bis eine Aktion \( 🏷action\) ausgeführt wird. Ein Beispiel ist die Funktion `count()`, die alle Datensätze nach Anwendung sämtlicher Transformationen zählt und das Ergebnis zurückliefert. 
* Ein RDD besitzt keinerlei Struktur, jeder Datensatz \(oder jede Zeile\) wird als Zeichenkette interpretiert. In vielen Fällen gibt es aber eine Struktur in den Quelldaten, z.B. bei CSV-Dateien. Um diese Struktur in Spark nutzbar zu machen, können 🏷Dataframes verwendet werden. Ein Dataframe ist somit eine Abstraktionsschicht auf einem RDD und fügt die Information hinzu, wie aus einer Zeile Text eine Tabelle mit strukturierten Daten entsteht. Im Beispiel der CSV-Datei wäre das die einfache Regel, nach einem Trennzeichen wie Komma oder Semikolon zu suchen, und jede Zeile anhand dieser Trennzeichen in Spalten aufzuteilen. 
* Weil ein 🏷Dataframe eine Struktur besitzt \(damit meinen wir definierter Spalten und Werte\) können wir SQL verwenden, um die Daten abzufragen. Die Verwendung von SQL eröffnet uns das Potenzial eine mächtige Sprache für die Datenanalyse.

## Links

* [Webseite von Apache Hadoop](https://hadoop.apache.org/)
* [Webseite von Apache Spark](https://spark.apache.org/)

