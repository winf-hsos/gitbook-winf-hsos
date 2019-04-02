# Texte für die Analyse mit SQL vorbereiten

## 🎯 Lernziele

Um Texte mit SQL sinnvoll analysieren zu können, müssen wir sie erst in eine andere Form bringen. Konkret müssen wir eine Struktur auf die unstrukturierten Textdaten projizieren. Wir lernen in diesem Tutorial, wie wir Texte in einzelne Token \(Wörter\) zerlegen und irrelevante Inhalte entfernen.

## 🌟 Daten für das Tutorial

Für dieses Tutorial verwenden wir Twitter Daten als Beispiel, wie sie im Modul Big Data Analytics erhoben werden.

{% hint style="info" %}
Ich stelle bald ein Template mit einem Twitter-Datensatz bereit, so dass jeder dieses Tutorial nutzen kann.
{% endhint %}

## 💡 In fünf Schritten zum Ziel

Texte sind unstrukturierte Daten in dem Sinn, dass es keine Struktur wie Spalten mit atomaren Daten und Datentypen gibt, auf denen wir z.B. mittels der `WHERE` Bedingung Filter definieren oder die wie in einer sinnvollen Form aggregieren können. Daher müssen wir zunächst eine Struktur auf die Texte projizieren, auf der wir anschließend mit SQL Analysen durchführen können. Eine Möglichkeit ist das Zerlegen der Texte in einzelne Wörter \(_Tokens_\).

{% embed url="https://docs.google.com/presentation/d/1ucTdKscyjA7QNfnbkXQZTDqtnTUkpntGbTWjeZVsv0A/edit?usp=sharing" %}

### Schritt 1: Zeilen filtern

Bevor wir mit dem Zerlegen der Texte beginnen ist es ratsam, die Datenmenge wenn möglich einzuschränken. Häufig wissen wir, das nur eine Untermenge der gesamten Daten für unsere Fragestellungen relevant ist. Für das Beispiel Tweets können Untermengen z.B. sein:

* Nur Tweets einer bestimmten Menge Nutzer
* Nur Tweets, in denen bestimmte Hashtags vorkommen
* Nur Tweets aus einem bestimmten Zeitraum

Das a priori Einschränken der Daten hat zur Folge, dass die anschließenden, sehr rechenintensiven Operationen der folgenden Schritte weniger Daten verarbeiten müssen. 

Um das Ergebnis aus jeden Schritt getrennt prüfen zu können definieren wir jeweils für jeden Schritt einen eigenen View:

```sql
-- View enthält im Ergebnis nur Tweets mit dem Hashtag #organic
create or replace view tweets_prep_step_1 as
  select user
      ,text
      ,created_at
  from twitter_timelines
  where array_contains(hashtags, 'organic')
```

Wir können nun diesen neu definierten View wie eine Tabelle abfragen:

```sql
select * from tweets_prep_step_1
```

### Schritt 2: Texte säubern und normalisieren

Im zweiten Schritt ist es sinnvoll, bestimmte Zeichen aus den Texte zu entfernen:

* Sonderzeichen wie @, %, & usw., die für eine Analyse keine Bedeutung haben.
* Satzzeichen

Es kann sinnvoll sein, diese Zeichen bestehen zu lassen. Wenn wir allerdings - wie hier - die Texte für die Analyse von Wortvorkommnissen und der Aggregation auf Wortbasis vorbereiten wollen, benötigen wir diese Zeichen nicht. Im Gegenteil, sie stören uns nur.

Neben dem Entfernen von Satz- und Sonderzeichen transformieren wir in diesem Schritt alle Buchstaben in Kleinbuchstaben. Das erlaubt es uns später, mögliche Fehler der Nutzer bei der Groß- und Kleinschreibung zu ignorieren.

```sql
create or replace view tweets_prep_step_2 as
  select user
      ,created_at
      -- Remove two or more subsequent white spaces
      ,regexp_replace(
        -- Remove special characters
        regexp_replace(
          -- Make all text lower case
          lower(
            -- Replace line breaks (2 different types)
            regexp_replace(
              regexp_replace(text, '\n', ' '), '\r', ' ')), '[^a-zA-ZäöüÄÖÜß]', ' '), '\ {2,}', ' ') as `text`
  from tweets_prep_step_1
```

Das Statement sieht auf den ersten Blick kompliziert aus. Daher schauen wir es uns im Detail an.

Wie in Zeile 13 zu sehen basiert der neue View auf dem aus dem ersten Schritt. Die Schritte bauen immer auf dem Ergebnis des vorigen Schrittes auf. Ansonsten selektieren wir in Zeile 2 und 3 die beiden Spalten `user` und `created_at`. 

#### Zeilenumbrüche `\n` durch Leerzeichen ersetzen

Spannend wird es ab der Zeile 5: Hier folgen nun verschachtelte Aufrufe von 5 Funktionen hintereinander. Die Aufrufe erfolgen von innen nach außen:

```sql
-- 1. Funktion
regexp_replace(text, '\n', ' ')
```

Die Funktion `regexp_replace` ersetzt das Vorkommen eines bestimmten Zeichens \(oder Muster von Zeichen, wie weiter untern zu sehen\) mit etwas anderen. Das erste Argument gibt die Spalte an, in der ersetzt werden soll \(hier: `text`\). Das zweite Argument ist das Zeichen \(oder Muster\), das ersetzt werden soll. Die Angabe `\n` ist ein Sonderzeichen und stellt einen Zeilenumbruch dar. Das dritte Argument ist das Zeichen, dass statt des gesuchten Zeichens eingesetzt werden soll. Hier soll ein Leerzeichen verwendet werden. Kurz gesagt: **Ersetze alle Zeilenumbrüche durch Leerzeichen**!

#### Zeilenumbrüche `\r` durch Leerzeichen ersetzen

Leider gibt es noch weitere Symbole für Zeilenumbrüche, die häufig auch in Kombination auftreten. Um sicherzugehen, ersetzen wir auch das oft verwendete Symbol `\r` mit einem Leerzeichen:

```sql
-- 2. Funktion
regexp_replace( ... , '\r', ' ')
```

Die drei Punkte, an deren Stelle wir eine Spalte erwarten, stehen hier für den Ausdruck aus der 1. Funktion. Das Ergebnis einer Funktion ist wie der Wert einer neuen Spalte zu interpretieren.

#### Buchstaben in Kleinschreibung umwandeln

Die Buchstaben können wir wie folgt in kleine Buchstaben umwandeln:

```sql
-- 3. Funktion (Zeile 9)
lower( ... )
```

#### Sonderzeichen und Satzzeichen entfernen

Wir haben oben gesehen wie wir mit regexp\_replace einzelne Zeichen wie \n oder \r suchen und ersetzen können. Die Funktion ist aber noch deutlich mächtiger: Mit ihr können wir bestimmten Mengen oder Mustern von Zeichen suchen:

```sql
-- 4. Funktion (Zeile 7)
regexp_replace( ... , '[^a-zA-ZäöüÄÖÜß]', ' ')
```

Anstatt als zweites Argument ein einzelnes Zeichen anzugeben nutzen wir einen [regulären Ausdruck](https://de.wikipedia.org/wiki/Regul%C3%A4rer_Ausdruck), um gleich mehrere Zeichen zu suchen. Diese etwas kryptische Angabe ist wie folgt zu lesen: Suche alle Zeichen außer die angegebenen a - z, A - Z, ä, ö, ü, Ä, Ö, Ü, und ß und ersetze sie mit einem Leerzeichen. Das Symbol `^` steht dabei für die Verneinung.

#### Überflüssige Leerzeichen aufräumen

Weil wir alle Sonderzeichen, Satzzeichen und Zeilenumbrüche mit Leerzeichen ersetzen haben wir im Ergebnis wahrscheinlich häufig eine Serie von Leerzeichen hintereinander. Diese Serien von Leerzeichen wollen wir im letzten Schritt auf jeweils nur ein Leerzeichen reduzieren:

```sql
-- 5. Funktion (Zeile 5)
regexp_replace( ... , '\ {2,}', ' ')
```

Auch hier nutzen wir einen regulären Ausdruck. Der ist so zu lesen: Suche nach mindestens 2 oder mehr Leerzeichen und ersetze sie mit einem Leerzeichen.

### Schritt 3: In Wörter splitten \(_Tokenize_\)

Der View aus dem Schritt 2 gibt uns eine bereinigte und normalisierte Form des Ursprungs-Tweets. Aus:

```text
RT @pugandcat: Whisker licking good food from @lilyskitchen
```

wird:

```text
rt pugandcat whisker licking good food from lilyskitchen
```

Nun wird es Zeit, aus dem zusammenhängenden Text einzelne Wörter zu machen. Dabei hilft uns die Funktion `split()`:

```sql
create or replace view tweets_prep_step_3 as
  select user
        ,created_at
        ,split(text, " ") as `words`
  from tweets_prep_step_2
```

Das `split(text, " ")` in Zeile 4 hat zur Folge, dass wir in der neuen Spalte `words` dieses Ergebnis sehen:

```text
["rt","pugandcat","whisker","licking","good","food","from","lilyskitchen"]
```

Komme euch das bekannt vor? Richtig, es handelt sich um ein Array, was wir an den eckigen Klammern außen erkennen können. Array können wir mit `explode()` in seine Einzelteile zerlegen, so dass wir jedes Element in einer eigenen Zeile vorliegen haben:

```sql
-- Array von Wörtern in Zeilen zerlegen
select explode(words) as `word` from tweets_prep_step_3
```

Wenn wir nun beide Funktionen verschachtelt anwenden haben wir unseren finalen View für Schritt 3:

```sql
create or replace view tweets_prep_step_3 as
  select user
        ,created_at
        ,explode(split(text, " ")) as `word`
  from tweets_prep_step_2
```

### Schritt 4: Stopwörter filtern

Wir haben nun jeweils ein Wort pro Zeile in der Spalte `word`.  Das ermöglicht es uns nun theoretisch, Analysen auf den Texten mittels SQL durchzuführen. Wir könnten z.B. zählen, welches Wort in allen Tweets am häufigsten vorkommt:

```sql
select word, count(1) as `Anzahl`
from tweets_prep_step_3
group by word
order by `Anzahl` desc
```

Je nach Datensatz wird bei euch nun das Wort organic weit oben stehe. Das ist nicht verwunderlich, da wir oben nach diesem Wort die Tweets gefiltert haben. Sehr weit oben stehen aber auch ziemlich sicher Wörter wie "a", "the", "is", "to", "rt" usw. Das sind alles Wörter, die in der Englischen Sprache häufig vorkommen, uns aber wenige Aufschluss in der Analyse geben. Deshalb sind sie unerwünscht, und wir nennen sie auch **Stopwörter**.

Wir könnten nun eine Liste von Stopwörtern erstellen und diese aus der Menge mittels WHERE Bedingung ausschließen:

```sql
select word, count(1) as `Anzahl`
from tweets_prep_step_3
-- Ausschluss bestimmter Füllwörter
where word not in ('to', 'the', 'rt', 'a')
group by word
order by `Anzahl` desc
```

Wenn wir die Liste für alle Stopwörter erweitern wird diese sehr lang und das SQL Statement sehr unübersichtlich. Zudem dauert das eine Weile. Glücklicherweise sind wir nicht die ersten mit diesem Problem, und kluge Leute haben Listen für verschiedene Sprachen veröffentlicht, wie z.B. [diese hier](https://gist.github.com/sebleier/554280).

Angenommen wir haben diese Liste als neue Tabelle `stopwords` in Databricks importiert. Wir können nun eine Unterabfrage statt der manuellen Liste nutzen:

```sql
select word, count(1) as `Anzahl`
from tweets_prep_step_3
-- Eine Tabelle statt manueller Liste
where word not in (select word from stopwords)
group by word
order by `Anzahl` desc
```

Das Ergebnis aus Schritt 4 als View sähe demnach so aus:

```sql
create or replace view tweets_prep_step_4 as
  select user
      ,created_at
      ,word
  from tweets_prep_step_3
  where word not in (select word from stopwords)
```

{% hint style="info" %}
Eine noch bessere und flexiblere Lösung ist das Lesen der Stopwords-Tabelle aus einem Google Spreadsheet direkt aus Databricks heraus. Das ermöglicht es uns, die Liste einfach zu erweitern und die Tabelle auf Knopfdruck neu zu laden. Die Infos dazu gibt es in der Veranstaltung.
{% endhint %}

### Schritt 5: POS Tagging

Mit den Daten aus Schritt 4 können wir schon gut arbeiten. Es geht aber immer noch besser. Zum Beispiel könnten wir die Wörter nun mit weiteren Metainformationen anreichern, was uns wiederum bessere Analysemöglichkeiten eröffnet. Metadaten können sein:

* Handelt es sich um ein Verb, Adjektiv, oder Substantiv?
* Wie lautet der Wortstamm?
* Aus welcher Sprache stammt das Wort?
* Ist das Wort positiv oder negativ?

Beim _POS Tagging_ geht um den ersten Punkt. Wir wollen für jedes Wort die Information ergänzen, um welche Art von Wort es sich handelt. Ein naiver Ansatz ist es, ähnlich wie bei den Stopwörtern auf eine Liste aus dem Internet zurückzugreifen. Nehmen wir also an wir haben eine neue Tabelle `pos` mit zwei Spalten `word` und `type`. Die Spalte type enthält Werte wie adjective, noun, verb usw. Wir können die beiden Tabellen nun zusammen joinen, um die Daten anzureichern:

```sql
select t.word, p.type
from tweets_prep_step_4 t
left join pos p
  on p.word = t.word
```

Im Ergebnis bekommen wir nun zu jedem Wort die Information, ob es sich um ein Verb, Adverb, Adjektiv oder Substantiv handelt. Wenn das Wort nicht in der Tabelle `pos` vorhanden ist, dann ist der Wert der Spalte `type` gleich `null`. 

{% hint style="info" %}
**Achtung**: Ein Wort wie "organic" ist in der POS-Liste als Substantiv _und_ Adjektiv gelistet, was korrekt ist. Wir bekommen in solchen Fällen im Ergebnis 2 Zeilen.
{% endhint %}

Wenn wir auch den letzten Schritt als View definieren sind wir am Ziel:

```sql
create or replace view tweets_tweets_prep_step_5 as
  select t.word, p.type
  from tweets_prep_step_4 t
  left join pos p
    on p.word = t.word
```

{% hint style="info" %}
Auch bei der POS-Liste ist das Auslagern in ein Google Spreadsheet sinnvoll, um die Liste flexibel erweitern zu können. Die Infos dazu bekommt ihr in der Veranstaltung.
{% endhint %}

