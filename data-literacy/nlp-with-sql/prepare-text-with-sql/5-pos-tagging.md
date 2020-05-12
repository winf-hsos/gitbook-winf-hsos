# POS Tagging

## 💡 Wörter mit weiteren Informationen anreichern

Mit den Daten aus [Schritt 4](4-stopwoerter-filtern.md) können wir schon gut arbeiten. Es geht aber immer noch besser. Zum Beispiel könnten wir die Wörter nun mit weiteren Metainformationen anreichern, was uns wiederum bessere Analysemöglichkeiten eröffnet. Metadaten können sein:

* Handelt es sich um ein Verb, Adjektiv, oder Substantiv?
* Wie lautet der Wortstamm?
* Aus welcher Sprache stammt das Wort?
* Ist das Wort positiv oder negativ?

Beim _POS Tagging_ geht um den ersten Punkt. Wir wollen für jedes Wort die Information ergänzen, um welche Art von Wort es sich handelt. Ein naiver Ansatz ist es, ähnlich wie bei den Stopwörtern auf eine Liste aus dem Internet zurückzugreifen. Nehmen wir also an wir haben eine neue Tabelle `pos` mit zwei Spalten `word` und `type`. Die Spalte type enthält Werte wie adjective, noun, verb usw. Wir können die beiden Tabellen nun zusammen joinen, um die Daten anzureichern:

```sql
select t.word, p.type
from tweets_stop t
left join pos p
  on p.word = t.word
```

Im Ergebnis bekommen wir nun zu jedem Wort die Information, ob es sich um ein Verb, Adverb, Adjektiv oder Substantiv handelt. Wenn das Wort nicht in der Tabelle `pos` vorhanden ist, dann ist der Wert der Spalte `type` gleich `null`. 

{% hint style="info" %}
**Achtung**: Ein Wort wie "organic" ist in der POS-Liste als Substantiv _und_ Adjektiv gelistet, was korrekt ist. Wir bekommen in solchen Fällen im Ergebnis 2 Zeilen.
{% endhint %}

Wenn wir auch den letzten Schritt als View definieren sind wir am Ziel:

```sql
create or replace view tweets_pos as
  select t.word, p.type
  from tweets_stop t
  left join pos p
    on p.word = t.word
```

{% hint style="info" %}
Auch bei der POS-Liste ist das [Auslagern in ein Google Spreadsheet](../identify-topics-in-text/mapping-tables-with-sql.md) sinnvoll, um die Liste flexibel erweitern zu können. Die Infos dazu bekommt ihr in der Veranstaltung.
{% endhint %}

