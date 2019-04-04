# Themen in Texten mittels SQL identifizieren

## 💡 Deduktive Themenidentifikation mit SQL

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

### 💡 Tabellen über Google Spreadsheets pflegen und laden

Kommt bald...

## 💡 Induktive Themenidentifikation mit SQL

Kommt bald...

