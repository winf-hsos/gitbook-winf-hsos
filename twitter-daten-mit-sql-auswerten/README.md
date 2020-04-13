---
description: Nützliche SQL Abfragen für die Arbeit mit Twitter-Daten.
---

# Twitter Data

## 💡 Datenqualität erhöhen

### 💡 Doppelte Tweets herausfiltern

Durch die Twitter API kann es vorkommen, dass einige Tweets doppelt in den Daten vorhanden sind. Das können wir in SQL beheben:

```sql
-- Auf doppelte Tweets prüfen
select id, count(1) 
from twitter_timelines
group by id 
order by count(1) desc
```

Wir sehen im Ergebnis, dass manche IDs zwei Mal vorkommen. Wir können mit der Window-Funktion `row_number()` innerhalb der gleichen ID jeder Zeile eine Nummer geben. Somit hat keine der beiden ansonsten gleichen Zeilen die gleiche `row_num`.

```sql
-- Zeilenummern generieren innerhalb einer ID-Gruppe
select id
,count(1) over(partition by id) as `occ`
,row_number() over(partition by id order by id) as `row_num`
from twitter_timelines
order by `occ` desc, id
```

Wenn wir jetzt das Ergebnis von oben als Unterabfrage verwenden und auf `row_num = 1` filtern, fallen alle doppelten Zeilen im Ergebnis raus:

```sql
-- Immer nur die erste Zeile selektieren
select * from (
    select * ,row_number() over(partition by id order by id) as `row_num`
    from twitter_timelines
)
where row_num = 1
```

## 💡 Informationen aus Tweets extrahieren

### 💡 Was bedeuten all die Felder?

Der Twitter-Datensatz besteht aus 2 Tabellen:

* `twitter_followers`
* `twitter_timelines`

Jede Tabelle hat eine breite Anzahl von Spalten. Die Benennung der Spalten ist analog zu dem Namen in der offiziellen Twitter API. Daher eignet sich die Dokumentation dieser API für beide Tabellen:

* [Dokumentation eines User-Objekts bei Twitter \(twitter\_followers\)](https://developer.twitter.com/en/docs/tweets/data-dictionary/overview/user-object)
* [Dokumentation eines Tweet-Objekts bei Twitter \(twitter\_timelines\)](https://developer.twitter.com/en/docs/tweets/data-dictionary/overview/tweet-object.html)

{% hint style="info" %}
Eine Ausnahme ist das Feld `follower_of` in der Tabelle `twitter_followers`. Dieses Feld existiert so nicht in der Twitter API. Es gibt an, wem der aktuelle Account folgt. Wenn ihr die Daten über das Helper Tool generiert habt, dann ist in `follower_of` der Screen Name gespeichert, den ihr in das Tool eingegeben habt. So könnt ihr später zuordnen, über welchen Screen Name ihr welche Follower bekommen habt.
{% endhint %}

### 💡 Extrahieren der Koordinaten eines Tweets

Das Feld coordinates liefert uns die Koordinaten eines Tweets als Längen- und Breitengrad. Die Angabe bezieht sich dabei auf den Ort, von dem aus der Tweet abgeschickt wurde. Dieses Feld ist nur befüllt, wenn die verwendete Applikation diese Information bereitgestellt hat und der User die Freigabe der Koordinaten erteilt hat.

Folgendes SQL Statement ermittelt für einen Tweet die Angaben, die anschließend z.B. in Tableau visualisiert werden können:

```sql
select text
      ,user_location
      ,coordinates.coordinates[0] as `longitude` 
      ,coordinates.coordinates[1] as `latitude` 
from twitter_timelines
where coordinates is not null
```

### 💡 Extrahieren von URLs oder Foto-URLs

Die URLs und Fotos sind in den Feldern `urls` und `photos` gespeichert. Beide Spalten sind vom Typ Array, was bedeutet, dass ein Tweet mehrere URLs bzw. mehrere Fotos haben kann. Der generelle Umgang mit Array wird im Tutorial [JSON-Felder mit SQL verarbeiten](../json-and-sql.md#arrays-abfragen) erklärt. Hier eine Abfrage, die jeweils die erste URL / Foto eines Tweets in einer eigenen Spalte anzeigt:

```sql
select urls[0].clean_url as `First URL in Tweet`
      ,photos[0].media_url_https as `First photo URL in Tweet`
from twitter_timelines
where size(urls) > 0
or size(photos) > 0
```

## Verwandte Themen

{% page-ref page="../nlp-mit-sql/texte-mit-sql-auswerten/" %}

{% page-ref page="../json-and-sql.md" %}

{% page-ref page="twitter-netzwerke-mit-sql-auswerten.md" %}

