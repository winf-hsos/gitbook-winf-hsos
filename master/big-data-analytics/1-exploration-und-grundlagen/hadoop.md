---
description: In dieser Session lernen wir Hadoop kennen.
---

# Hadoop

## ❓ Fragen

* Was ist Hadoop und welche Komponenten gehören dazu?
* Warum ist Hadoop eine gute Lösung für die Herausforderungen von Big Data?
* Wie löst HDFS das Problem, große Datenmengen effizient und ausfallsicher zu speichern?
* Wie können mittels MapReduce sehr große Datenmengen in kurzer Zeit verarbeitet werden?
* Welche Nachteile hat MapReduce im Vergleich zu neueren Alternativen?

## 🏷 Begriffe

* 🏷 HDFS
* 🏷 MapReduce
* 🏷 Cluster
* 🏷 Data Node
* 🏷 Worker Node
* 🏷 Name Node

## 🔑 Key Points

🔑 Hadoop ist der Name eines [Apache Open Source Projektes](https://hadoop.apache.org/), dass sich mit der Speicherung und Verarbeitung sehr großer Datenmengen \(Big Data\) befasst.

🔑 Die wichtigsten Bestandteile von Hadoop sind das 🏷HDFS und das 🏷MapReduce Framework. Das HDFS ist ein verteiltes Dateisystem \(_distributed filesystem_\) und kümmert sich um die Speicherung sehr großer Datenmengen. MapReduce ist ein Ansatz für die parallele und verteilte Verarbeitung \(_parallel and distributed processing_\) großer Datenmengen. MapReduce hängt von einem verteilten Dateisystem wie HDFS ab.

🔑 HDFS und MapReduce verwenden für die verteilte Speicherung und die parallel Verarbeitung ein so genanntes Hadoop 🏷Cluster. Ein Cluster ist eine Verbund mehrerer Rechner \(Server\), die sich die Arbeitslast untereinander teilen. Einzelne Rechner in einem Cluster werden Knoten genannt \(_nodes_\). 

🔑 In einem Hadoop Cluster werden drei Arten von Knoten unterschieden: 🏷Data Nodes, 🏷Worker Nodes und der 🏷Name Node. Data Nodes sind Teil des HDFS und speichern Daten. Worker Nodes sind verarbeitende Knoten im Kontext von MapReduce. Dem Name Node kommt eine zentrale Rolle zu: Nur er weiß, auf welchen Knoten welche Blöcke \(Daten\) abgelegt sind und kann auf Anfrage hin die richtigen Blöcke zur ursprünglichen Datei zusammensetzen. Der Name Node als Verwalter sämtlicher Metadaten ist der zentrale Zugang zum Hadoop Cluster.

🔑 Wenn wir eine Datei im 🏷HDFS speichern wird sie zunächst in Blöcke gleicher Größe \(im Standard 128 MB\) zerlegt und jeder Block anschließend auf mindestens 3 Rechnern \(_nodes_\) gespeichert. Durch die redundante Speicherung jedes Blocks wird eine hohe Ausfallsicherheit gewährleistet. Sollte ein Knoten ausfallen, existieren noch 2 weitere Kopien.

🔑 Wenn eine Datei aus dem 🏷HDFS abgerufen wird, fragt zunächst der Name Node die notwendigen Blöcke bei den entsprechenden Rechner, auf denen sie gespeichert wurden, an. Anschließend werden die Blöcke in der richtigen Reihenfolge zur angefragten Datei zusammengefügt und zurückgeliefert.

🔑 Von Außen betrachtet sieht das 🏷HDFS wie ein gewöhnliches Verzeichnissystem aus, wie man es z.B. aus dem Windows-Explorer gewohnt ist. Auch das Verhalten ist gleich. Die Komplexität, die im Hintergrund für die hohe Performanz und die Ausfallsicherheit sorgt, wird vor dem Benutzer versteckt.

## ▶ Session

### 1⃣ HDFS

### 2⃣ MapReduce

## 🔗 Links

* [Webseite von Apache Hadoop](https://hadoop.apache.org/)

