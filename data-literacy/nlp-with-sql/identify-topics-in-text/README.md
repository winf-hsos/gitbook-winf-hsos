# Identify Topics

## 💡 Zwei Herangehensweisen: Deduktiv und induktiv

Es gibt grundsätzlich zwei Möglichkeiten, Themen in Texten zu identifizieren. Der erste Weg ist die **deduktive Bildung von Themenkategorien** mit entsprechenden Schlagwörtern. Das bedeutet, wir überlegen uns **vor der Betrachtung der Daten**, welche Themen eine Rolle spielen könnten und welche Schlagwörter zu diesen Themen gehören könnten. Unsere Überlegungen können wir als Tabelle mit 2 Spalten dokumentieren: Ein Schlagwort, wie z.B. "glyphosat", und ein von uns zugeordnetes Thema, wie z.B. "Insektensterben".

{% hint style="info" %}
Das Schlagwort "glyphosat" wurde bewusst klein geschrieben, weil wir in der [Vorbereitung der Texte](../prepare-text-with-sql/2-texte-bereinigen-und-normalisieren.md) alle Wörter in Kleinschreibung überführt haben. So können wir einfache nach Schlagwörtern suchen und müssen uns um Groß- und Kleinschreibung keine Gedanken machen.
{% endhint %}

Der andere Weg ist die **induktive Bildung von Themenkategorien**. Hier identifizieren wir Schlagwörter aus den Daten heraus, ordnen den Schlagwörtern Themen zu, indem wir die Daten \(hier z.B.: Tweets\) sehr genau unter die Lupe nehmen, und dokumentieren das Ergebnis wieder als Tabelle mit mindestens zwei Spalten: Das Schlagwort und die Zuordnung zu einem Thema. So eine Tabelle nennen wir auch _Codebuch_.

Da wir für beide Wege iterativ umfangreiche Tabellen erstellen müssen, benötigen wir einen Weg, diese zu pflegen und einfach in Databricks zu laden. Das ist die Voraussetzung, damit wir sie auf unsere Daten anwenden und so die Themen quantifizieren können. Ich stelle nun 2 Wege vor, wobei für die meisten Fälle die Variante der [Google Sheets](mapping-tables-with-sql.md#tabellen-ueber-google-sheets-pflegen-und-laden) am besten funktionieren dürfte.

{% page-ref page="mapping-tables-with-sql.md" %}

{% page-ref page="2-deduktive-themenanalyse.md" %}

{% page-ref page="3-induktive-themenanalyse.md" %}

