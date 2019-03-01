# Daten mit SQL erkunden

## 🎯 Lernziele

In diesem Tutorial bekommt ihr einen Überblick, mit welchen Vorgehen und zugehörigen SQL-Abfragen ihr euch schnell einen Überblick über einen unbekannten Datensatz verschaffen könnt. Die Konzepte sind allesamt auch im Tutorial [Einführung SQL](einfuehrung-sql/) enthalten, es geht hier um eine gezielte Bündelung der Abfragen, die bei dem **Erkunden von Daten** relevant sind.

## 💡 Datensätze zählen

Meistens interessiert im ersten Schritt der Umfang des Datensatzes, also die Anzahl der Zeilen. Das bekommen wir ganz einfach heraus:

```sql
select count(*) from ted_meta
```

## 💡 Die Spalten einer Tabelle anzeigen

Die Spalten eines Datensatzes beinhalten die Attribute, die wir mittels SQL abfragen können. Es ist daher zunächst wichtig zu wissen, welche Spalten zur Verfügung stehen und welchen Datentyp sie haben:

```sql
describe ted_meta
```

## 💡 Überblick über den Wertebereich einer Spalte bekommen

Der erste Hinweis auf den Wertebereich gibt euch bereits der `describe` Befehl. Er liefert neben dem Namen auch den Datentyp einer Spalte zurück. Um aber ein besseres Bild zu bekommen, welche Werte in einer Spalte enthalten sind, kann man sich z.B. alle eindeutigen Werte sortiert ausgeben lassen:

```sql
select distinct event from ted_meta
```

Eine Alternative mit der zusätzlichen Information über die Häufigkeitsverteilung der einzelnen Werte bietet  eine Gruppierung kombiniert mit `count(1)`:

```sql
select event, count(1) as `Number Occurences`
from ted_meta
group by event
order by `Number Occurences` desc
```

Die häufigsten Werte werden im Ergebnis oben angezeigt.

### 💡 Schnelle Visualisierungen

Databricks bietet die Möglichkeit, tabellarische Ergebnisse mit einem Mausklick in eine visuelle Form zu bringen. Dazu nutzt ihr die Buttonleiste unter der Ergebnisanzeige. Mit Klick auf Chartsymbol bekommt ihr sofort eine Anzeige als Balkendiagramm. Über die den Button "Plot Options..." könnt ihr auch andere Charts auswählen und die Achsen konfigurieren.

![Die Anzahl Talks pro Event als Area-Chart.](../../.gitbook/assets/image%20%288%29.png)



