---
description: In dieser Session lernen wir Hadoop kennen.
---

# Hadoop

## ❓ Fragen

* Wie funktioniert verteiltes Verarbeiten \(_distributed processing_\) mit Apache Spark?
* Welche Arten von Datenverarbeitung unterstützt Apache Spark?
* Welche Vorteile bietet 🏷Spark gegenüber 🏷MapReduce?

## 🔑 Key Points

🔑 Wenn wir eine Datei im 🏷HDFS speichern wird sie zunächst in Blöcke gleicher Größe \(im Standard 128 MB\) zerlegt und jeder Block anschließend auf mindestens 3 Rechner \(_nodes_\) verteilt. Durch die redundante Speicherung jedes Blocks wird eine hohe Ausfallsicherheit gewährleistet. Sollte ein Knoten ausfallen existieren noch 2 weitere Kopien.

🔑 Wenn eine Datei aus dem 🏷HDFS abgerufen wird, fragt zunächst der _Name Node_ die notwendigen Blöcke bei den entsprechenden Rechner, auf denen sie gespeichert wurden, an. Anschließend werden die Blöcke in der richtigen Reihenfolge zur angefragten Datei zusammen gefügt und zurück geliefert.

🔑 Von Außen betrachtet sieht das 🏷HDFS wie ein gewöhnliches Verzeichnissystem aus, wie man es z.B. aus dem Windows-Explorer gewohnt ist. Auch das Verhalten ist gleich. Die Komplexität, die im Hintergrund für die hohe Performanz und die Ausfallsicherheit sorgt, wird vor dem Benutzer versteckt.

## ▶ Session

### 1⃣ HDFS

### 2⃣ MapReduce

