# Case Study Phase 1

### Fallstudie Phase 1: Exploration der Datensätze

Im weiteren Verlauf der Fallstudie werdet ihr mit zwei Datensätzen arbeiten und auf dieser Grundlage versuchen, Antworten auf Fragen der Geschäftsführung zu finden. Die Datensätze könnt ihr hier herunterladen \(Quelle der Daten: [Webseite Julian McAuley - UCSD](http://jmcauley.ucsd.edu/data/amazon/)\):

* [Amazon Reviews for Grocery and Fine Foods \(220 MB\)](https://s3.amazonaws.com/nicolas.meseth/amazon_reviews/reviews_Grocery_and_Gourmet_Food.json.gz)
* [Metadata for Grocery and Fine Foods \(52 MB\)](https://s3.amazonaws.com/nicolas.meseth/amazon_reviews/meta_Grocery_and_Gourmet_Food.json.gz)

Für die Beantwortung der Fragen müssen die Daten in geeigneter Weise analysiert werden. Hierzu wird im Rahmen des Seminars die Sofware _Apache Spark_ verwendet. Um Spark kostenlos verwenden zu können meldet euch bitte für die [Databricks Community Edition](https://community.cloud.databricks.com) an \(falls noch nicht geschehen\).

Der erste Schritt bei der Analyse eines neuen Datensatzes ist die Erforschung oder _Exploration_ der Daten: Worum handelt es sich bei dem Datensatz? Welche Informationen sind enthalten? In welcher Form liegen die Daten vor? Wie ist die Qualität der Daten?

Bitte versucht die folgenden Fragen mittels Spark und SQL zu beantworten. Nutzt für die Ergebissicherung die Databricks Notebooks. Hier könnt ihr interaktiv Spark-Kommandos eingeben und ausführen. Gleichzeitig könnt ihr die Kommandos in Blöcke aufteilen und jedem Block einen Namen \(Titel\) geben. Verwendet als Titel jedes Blocks die Frage und schreibt den zugehörigen Code für die Antwort in diesen Block. Beispiel:

![Beispiel Notebook](/content/exercises/exercise-spark-sql-fallstudie-phase-1/example_notebook.png)

Damit wäre die erste Frage unten bereits beantwortet :-\)

**Hinweis**: Um eine bessere Nachvollziehbarkeit der Lösungen zu schaffen bietet es sich an, dass alle Gruppen die Ausgangsvariablen für die DataFrames und die temporären SQL Tabellen gleich bennennt. So wird der Austausch über Slack auch deutlich vereinfacht. Bitte fügt also alle zu Beginn eures Notebooks den folgenden Codeblock ein \(ersetzt den Dateipfad entsprechend\):

```java
val dfReviews = spark.read.json("/FileStore/tables/b8ant8h71491818520570/reviews_Grocery_and_Gourmet_Food_json-7a595.gz")
val dfMeta = spark.read.json("/FileStore/tables/7jy387mw1492069611940/meta_Grocery_and_Gourmet_Food_json-536c0.gz")

dfReviews.createOrReplaceTempView("reviews")
dfMeta.createOrReplaceTempView("products")
```

**Fragen zur Exploration des Reviewdatensatzes**

1. Wie viele Reviews enthält der Datensatz? \(●\)
2. Welche Felder enthält der Datensatz und was ist in den Feldern inhaltlich abgebildet? \(●\)
3. Untersucht das Feld `asin` genauer!
   * Gibt es Datensätze ohne ASIN? \(●\)
   * Was ist der Wertebereich des Feldes? \(●\)
4. Untersucht das Feld `helpful` genauer!
   * Welchen Datentyp hat das Feld? \(●\)
   * Wie sind die Werte zu interpretieren? \(●\)
5. Was ist der Wertebereich der Reviewtexte?
   * Wie lang ist der längste und der kürzeste Text? \(●\)
   * Gibt es leere Reviews? \(●\)
   * Wie lang ist der durchschnittliche Text, wenn man leere Reviews ausnimmt? \(●●●\)
6. Gibt es doppelte Reviewdatensätze? \(●\)
7. Aus welchem Zeitraum stammen die Reviews? \(●●●\)
8. Wie ist die Verteilung der Reviews über Jahre? \(●●●\)
9. Wer hat die meisten Reviews geschrieben und wie viele? \(●\)
10. Wie viele Reviewer haben keinen Namen? \(●\)

**Fragen zur Exploration der Produktmetadaten**

1. Wie viele Produkte enthält der Datensatz? \(●\)
2. Analysiert das Feld `categories` genauer!
   * Wie ist es aufgebaut? \(●\)
   * Wie sind die Werte zu interpretieren? \(●\)
3. Wie viele eindeutige Kategorien sind in den Produkten enthalten? \(●●●\)
4. Wie viele Level hat die tiefste Kategorie? \(●\)
5. Welche Brands haben die meisten Produkte im Datensatz? \(●\)
6. Was sind die Top 5 Produkte gemäß dem Verkaufsrang in der Kategorie _Grocery & Gourmet Food_? \(●\)
7. Welche Produkte haben die meisten Reviews? \(●\)
8. Gibt es Produkte ohne Reviews? \(●\)
9. Wie lang ist der längste Titel eines Produkts? \(●\)
10. Welche Marke hat durchschnittlich die teuersten Produkte? \(●●●\)

### Legende

● = diese Frage kann entweder korrekt \(100%\) oder ungenügend \(0%\) beantwortet werden

●●● = diese Frage wird in 3 Abstufungen bewertet: 100%, 75%, 50% \(oder 0%\).

●●●●● = diese Frage wird in 5 Abstufungen bewertet: 100%, 90%, 75%, 60%, 50% \(oder 0%\).

Diese Angabe hat nichts mit der Gewichtung der Fragen zu tun. Alle Fragen sind gleich gewichtet.

### LINKS

* [Spark SQL Functions Documentation](https://spark.apache.org/docs/latest/api/java/org/apache/spark/sql/functions.html)
* [Spark SQL Reference](https://docs.databricks.com/spark/latest/spark-sql/index.html)
* [Introdcution to DataFrames - Scala](https://docs.databricks.com/spark/latest/dataframes-datasets/introduction-to-dataframes-scala.html)
* [Apache Spark 2.1.0 Quick Start](http://spark.apache.org/docs/latest/quick-start.html)
* [Apache Spark 2.1.0 SQL and DataFrames](http://spark.apache.org/docs/latest/sql-programming-guide.html)

