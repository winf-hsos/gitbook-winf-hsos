---
description: >-
  In diesem Abschnitt lernt ihr eine Möglichkeit kennen, mittels einer eigenen
  Funktion in Texten nach mehr als einem Wort zu suchen. Eine schnelle
  Alternative zum Tokenizing.
---

# In Texten nach Wörtern suchen

Mit dem like Operator kann man in Texten nach einzelnen Wörtern suchen. Möchte man einen Text nach mehr als nur einem Wort durchsuchen, können wir mehrere like Operatoren mit dem OR-Operator verknüpfen. Diese Vorgehensweise wird aber schnell unübersichtlich.

Eine Alternative ist das Zerlegen der Texte in einzelne Wörter. Das bietet sich an, wenn man tiefer gehende Analysen der Texte durchführen möchte. 

Will man lediglich auf die Schnelle nach mehr als einem Wort suchen gibt es dennoch eine Möglichkeit. Über eine **User Defined Function \(UDF\)** kann zunächst die Funktion abgebildet werden, innerhalb einer Spalte nach einer anderen Spalte \(enthält gesuchtes Wort\) zu suchen:

```scala
def strContains(s: String, k: String): Boolean = {
  val str = Option(s).getOrElse(return false)
  val keyword = Option(k).getOrElse(return false)
  return keyword.r.findAllIn(str).length > 0
}

val strContainsUDF = udf[Boolean, String, String](strContains)
spark.udf.register("strContains", strContainsUDF)
```

Diese UDF kann man nun innerhalb eines SQL Statements aufrufen. Die Tabelle `keywords` enthält dabei die gesuchten Suchbegriffe in der Spalte `word`. Die Tabelle kann beispielsweise in [Google Sheets gepflegt und anschließend geladen werden](../themen-in-texten-mittels-sql-identifizieren/1-arbeiten-mit-mappingstabellen.md#tabellen-ueber-google-sheets-pflegen-und-laden):

```sql
select t.text
      ,k.keyword
from twitter_timelines t
left join keywords k
      on strContains(t.text, k.keyword)
-- Nur Treffer im Ergebnis behalten
where k.keyword is not null
```

Wollt ihr nun jeden Text nur einmal im Ergebnis haben, sortiert nach der Anzahl gefundener Schlüsselwörter, dann verwendet das folgende SQL:

```sql
select id
      ,text
      ,collect_list(word) as hits
      ,count(word) as num_hits
from twitter_timelines
left join test 
  on strContains(lower(text), word)
where word is not null
group by id, text
order by num_hits desc
```

Die Funktion `collect_list` in Zeile 3 aggregiert die Keywords, die zuvor auf mehrere Zeilen verteilt waren, in eine Spalte vom Typ Array. Gleichzeitig zählen wir mit `count(word)` die Treffer und gruppieren die restlichen Spalten. Euch ist vielleicht aufgefallen, dass ein Tweet, in dem 3 Mal das Wort _organic_ vorkommt, nun auch 3 Treffer für dieses Wort gut geschrieben wird. Möchte man jedes Wort nur einmal zählen, egal wie häufig es vorkommt, so verwendet diese Variante:

```sql
select id
      ,text
      ,collect_set(word) as hits
      ,count(distinct word) as num_hits
from twitter_timelines
left join test 
  on strContains(lower(text), word)
where word is not null
group by id, text
order by num_hits desc
```

Der Unterschied ist in den Zeilen 3 und 4 zu erkennen. Die Funktion `collect_set` erstellt eine Liste ohne doppelte Elemente \(im Gegensatz zu `collect_list`\), und `count(distinct word)` zählt jedes Wort nur einmal, egal wie häufig es vorkommt. 

{% hint style="info" %}
Bei größeren Tabellen kann die Verwendung der UDF langsamer sein, als wenn die Texte in einzelne Wörter zerlegt wurden. Daher sollte bei komplexen Textanalysen die Variante des Tokenizing verwendet werden.
{% endhint %}

Beachtet dass ihr mit eigenen UDFs **keine persistenten Views** mittels `create or replace view` erstellen könnt. Verwendet stattdessen `create or replace temporary view`. Ihr müsst bei Verwendung eines neuen Clusters den View dann erst erneut erstellen.

