# Themen in Texten mittels SQL identifizieren

## 💡 Deduktive Themenidentifikation mit SQL

Es gibt grundsätzlich zwei Möglichkeiten, Texte auf Inhalte hin zu analysieren. Der erste weg beinhaltet die **deduktive Bildung von Themenkategorien** mit entsprechenden Schlagwörtern. Das bedeutet, wir überlegen uns **VOR** der Betrachtung der Daten, welche Themen eine Rolle spielen könnten und welche Schlagwörter zu diesen Themen gehören könnten. Unsere Überlegungen dokumentieren wir als Tabelle mit 2 Spalten: Ein Schlagwort, wie z.B. "glyphosat", und ein von uns zugeordnetes Thema, wie z.B. "Insektensterben".

Der andere Weg ist die **induktive Bildung von Themenkategorien**. Hier identifizieren wir Schlagwörter aus den Daten heraus, ordnen den Schlagwörtern Themen zu, indem wir die Daten \(hier z.B.: Tweets\) sehr genau unter die Lupe nehmen, und dokumentieren das Ergebnis wieder als Tabelle mit mindestens zwei Spalten: Das Schlagwort und die Zuordnung zu einem Thema. So eine Tabelle nennen wir auch _Codebuch_.

Da wir für beide Wege iterativ umfangreiche Tabellen erstellen müssen, benötigen wir einen Weg, diese zu pflegen und einfach in Databricks zu laden. Das ist die Voraussetzung, damit wir sie auf unsere Daten anwenden und so die Themen quantifizieren können. Ich stelle nun 2 Wege vor, wobei für die meisten Fälle die Variante der [Google Sheets](themen-in-texten-mittels-sql-identifizieren.md#tabellen-ueber-google-sheets-pflegen-und-laden) am besten funktionieren dürfte.

### 💡 Einfache Erstellung einer Mapping-Tabelle mit Scala

#### Einfache Listen mit Wörtern oder Zahlen

Ihr könnt ganz einfach eine eigene Tabelle erstellen, die ihr später in euren Analysen anstelle eine langen Liste wie bei `WHERE IN (...)` verwenden könnt. Dazu könnt ihr folgenden Scala-Code als Vorlage nutzen:

```scala
// Hier einfach in die Wörter durch eure ersetzen
val list = Seq("organic", "environment", "quality");

// Die einzige Spalte wird hier "word" genannt (gerne umbenennen)
val df = sc.parallelize(list).toDF("word");

// Zum Schluss wird ein temporärer View erzeugt mit dem Namen "myTable"
df.createOrReplaceTempView("myTable");
```

Anschließend könnt ihr den View wie eine Tabelle abfragen und für eure Analysen verwenden:

```sql
select * from myTable
```

#### Eine Tabelle mit 2 oder mehr Spalten

Das Beispiel oben zeigt, wie man eine Liste als Tabelle mit einer Spalte anlegen kann. In einigen Fällen benötigt man aber 2 oder mehr Spalten, wie z.B. beim POS-Tagging. Hier braucht man eine Spalte für das Wort und eine für den Typ des Wortes \(Adjektiv, Substantiv, Nomen etc.\). Auch das geht einfach in Scala:

```scala
// Jetzt sind es Wortpaare, jeweils in eigenen Klammern mit Kommata getrennt
val list = Seq(("feed", "adjective"), ("food", "noun"), ("delicious", "adjective"))

// Nun benötigen wir auch 2 Namen für die Spalten
val df = sc.parallelize(list).toDF("word", "type")

// Und schließlich erzeugen wir wieder einen View
df.createOrReplaceTempView("myPosTable")
```

Wenn wir diesen View abfragen erhalten wir im Ergebnis 2 Spalten.

Das Beispiel ist beliebig erweiterbar. Ab einer zu großen Anzahl Spalten und Zeilen wird aber auch dieses Vorgehen schnell unübersichtlich. Dann ergibt es mehr Sinn, die Daten auszulagern, z.B. in ein Google Spreadsheet, und dieses dann automatisiert in Databricks zu importieren.

### 💡 Tabellen über Google Sheets pflegen und laden

[Google Sheets](https://www.google.com/sheets/about/) ist eine kostenlose Alternative zu dem weit verbreiteten Microsoft Excel. Und weil Google Sheets in der Cloud und damit im Internet verfügbar sind, lassen sie sich wunderbar in Databricks ohne komplizierte Umwege über den eigenen Rechner laden. Den folgenden Code-Block müsst ihr euch in euer Databricks-Notebook kopieren und in den Zeilen 2 und 6 die notwendigen Anpassungen durchführen:

```scala
// Choose a name for your resulting table in Databricks
var tableName = "stopwords"

// Replace this URL with the one from your Google Spreadsheets
// Click on File --> Publish to the Web --> Option CSV and copy the URL
var url = "https://docs.google.com/spreadsheets/d/e/2PACX-1vSWAaX6X1mcF7iCxFXE7dvwQHxb01L4CPlwgGPkmBYDLCsHozvANJBXs_sxlEJ37tAC-jBrZ0c7ADf2/pub?output=csv"

var localpath = "/tmp/" + tableName + ".csv"
dbutils.fs.rm("file:" + localpath)
"wget -O " + localpath + " " + url !!

dbutils.fs.mkdirs("dbfs:/datasets/gsheets")
dbutils.fs.cp("file:" + localpath, "dbfs:/datasets/gsheets")

sqlContext.sql("drop table if exists " + tableName)
var df = spark.read.option("header", "true").option("inferSchema", "true").csv("/datasets/gsheets/" + tableName + ".csv");
df.write.saveAsTable(tableName);
```

In Zeile 2 ersetzt ihr einfach den Wert `"stopwords"` mit dem Namen für eure Tabelle. In Zeile 6 müsst ihr nun noch die öffentliche URL eures Google Sheets einfügen. Wie das geht erkläre ich im Folgenden.

#### Ein Google Sheet als CSV veröffentlichen

Ihr legt in eurem Google Account ganz einfach ein neues Spreadsheet an und pflegt eure Daten in Spalten und Zeilen ein. Eben wie ihr es auch in Excel machen würdet. Wenn ihr dann einen Stand habt, den ihr gerne in Databricks als Tabelle verfügbar laden wollt, geht ihr wie folgt vor:

**Schritt 1:** Ihr klickt auf "Datei" und dann "Im Web veröffentlichen"

![](../../.gitbook/assets/image%20%2827%29.png)

**Schritt 2:** "Gesamtes Dokument" auswählen und im rechten Dropdown-Menü "Kommagetrennte Werte \(CSV\)" ausählen.

![](../../.gitbook/assets/image%20%2816%29.png)

**Schritt 3:** Link kopieren und in Databricks einfügen \(Wert in Zeile 6 ersetzen\).

![Diesen Link in die Zwischenablage kopieren.](../../.gitbook/assets/image%20%2814%29.png)

Nun müsst ihr nur noch den Code-Block ausführen und anschließend sollte die neue Tabelle verfügbar sein. Wenn ihr anschließend Änderungen im Spreadsheet durchführt und den Code zum Laden der Tabelle erneut ausführt, habt ihr alle Änderungen auch in Databricks verfügbar. Das erleichtert den Prozess, gerade wenn man iterativ Tabellen erstellt, die man sehr häufig in Databricks aktualisieren muss.

## 💡 Induktive Themenidentifikation mit SQL

Kommt bald...

