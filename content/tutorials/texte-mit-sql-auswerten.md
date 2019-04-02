# Texte mit SQL auswerten

## 💡 Texte für die Analyse vorbereiten

Texte sind unstrukturierte Daten in dem Sinne, dass es keine Struktur wie Spalten mit atomaren Daten und Datentypen gibt, auf denen wir z.B. mittels der `WHERE` Bedingung Filter definieren oder die wie in einer sinnvollen Form aggregieren können. Daher müssen wir zunächst eine Struktur auf die Texte projizieren, auf der wir anschließend mit SQL Analysen durchführen können. Eine Möglichkeit ist das Zerlegen der Texte in einzelne Wörter \(_Tokens_\).

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
        ,split(text, " ")
  from tweets_prep_step_2
```

Das `split(text, " ")` in Zeile 4 hat zur Folge, dass wir dieses Ergebnis sehen:

```text
["rt","pugandcat","whisker","licking","good","food","from","lilyskitchen"]
```

Das kommt uns bekannt vor! Richtig, es handelt sich um ein Array, was wir an den eckigen Klammern außen erkennen können.

### Schritt 4: Stopwörter filtern

