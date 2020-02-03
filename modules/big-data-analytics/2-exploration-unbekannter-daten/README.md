---
description: In diesem Block geht es die Erkundung neuer Datensätze mit SQL.
---

# \#2 Exploration von Daten

> The data may not contain the answer. The combination of some data and an aching desire for an answer does not ensure that a reasonable answer can be extracted from a given body of data.   
> \(John Tukey\)

## 🎯 Lernziele

* 🎯 Ihr kennt Formate, in denen Datensätze häufig gespeichert werden, und wie ihr mit den unterschiedlichen Formaten geeignet verfahren könnt.
* 🎯 Ihr wendet Vorgehen und Tools für die Auswertung von Big Data auf neue Datensätze an.
* 🎯 Ihr erzeugt neue Datensätze und analysiert diese neuen Daten systematisch für die Beantwortung eurer Fragestellungen.
* 🎯 Ihr identifiziert aus einer großen, unstrukturierten Masse an Daten die für eine Fragestellung relevanten Datensätze.

## \*\*\*\*❓ **Fragen**

* ❓ Welche Arten von Datensätzen \(Format, Inhalt, Struktur\) kann man unterscheiden?
* ❓ Welche Informationen zu einem neuen Datensatz sind hilfreich für die weitere Analyse?
* ❓ Wie komme ich an diese Informationen heran?
* ❓ Wie kann ich aus meinen Datensätzen die passenden Datensätze zu einer Fragestellung identifizieren?

## 🏷 Begriffe

* 🏷Structured Query Language \(SQL\)
* 🏷Datentypen
* 🏷JSON
* 🏷Domain \(Wertebereich\)

## 🔑 Key Points

* 🔑 In der Praxis begegnen wir ständig neuen Datensätzen, über die wir nicht viel wissen. Wir haben aber oft die Hoffnung, dass uns die Daten bei der Beantwortung wichtiger Fragen weiterhelfen können. Deshalb wollen wir die Daten analysieren. 
* 🔑 Wir müssen einige Fragen bezüglich des Datensatzes beantworten, bevor wir mit der Analyse beginnen können: 
  * In welchem Format liegen die Daten vor \(z.B. XLS-Datei, JSON, CSV, Parquet, in einer Datenbank\)
  * Welche Größe haben die Daten \(in GB, TB, etc.\)?
  * Welche Struktur haben die Daten bzw. liegt überhaupt eine Struktur vor?
  * Ändern sich die Daten währende der Analyse? 
* 🔑 Ausgehend von den Antworten auf diese Fragen können wir entscheiden, ob und mit welchen Methoden und Werkzeugen wir die Daten analysieren können. Strukturierte Daten, wie sie z.B. in einer relationalen Datenbank, einer Excel-Datei, oder auch einer CSV-Datei in der Regel vorliegen, können wir sehr gut mit SQL analysieren. Bei so genannten semi- oder polystrukturierten Daten, wie es oft beim JSON-Format oder bei Daten in NoSQL-Datenbanken der Fall ist, können wir ebenfalls mit SQL arbeiten, müssen aber bestimmte Dinge beachten. Zum Beispiel sind hier die Dokumente \(oder Datensätze\) oft heterogen in Bezug auf die verfügbaren Attribute.  
* 🔑 Bei komplett **unstrukturierten Daten** wie losen Texten \(z.B. Blogartikel, Twitter, Facebook\) oder Bildern müssen wir uns erst **Gedanken machen, welche Struktur wir auf diese Daten** **projizieren** wollen, bevor wie sie analysieren. Es kann nur systematisch analysiert werden, was auch eine Struktur besitzt. Bei Bildern könnten z.B. die abgebildeten Objekte ein Strukturelement sein, das uns interessiert. Bei Texten könnten es die einzelnen Wörter sein, die wir zählen wollen. 
* 🔑 Wenn die Strukturfrage geklärt ist, können wir weitere Fragen anschließen: 
  * Wie ist die Struktur genau beschaffen? Welche Attribute \(oder Spalten\) gibt es?
  * Welche Datentypen und welchen Wertebereich haben diese Spalten?
  * Was ist der Wertebereich \(🏷Domain\) der Spalte?

## 🔗 Links

Diese Tutorial bietet euch den Einstieg in SQL. Wenn ihr SQL-Neulinge seid müsst ihr mit diesem Tutorial starten:

{% page-ref page="../../../self-learning/sql/einfuehrung-sql/" %}

In diesem Tutorial bekommt ihr einen Überblick, welche Möglichkeiten SQL bietet, um einen neuen Datensatz zu erkunden:

{% page-ref page="../../../self-learning/sql/daten-mit-sql-erkunden.md" %}

Um mit JSON-Daten umgehen zu lernen, schaut euch diese beiden Tutorials an:

{% page-ref page="../../../self-learning/web-development/javascript-fuers-web/einfuehrung-in-json.md" %}

{% page-ref page="../../../self-learning/sql/sql-und-json.md" %}

