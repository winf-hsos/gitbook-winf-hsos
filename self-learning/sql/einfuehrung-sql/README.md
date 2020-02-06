# Einführung SQL

Das folgende Tutorial führt SQL als Abfragesprache für strukturierte Daten ein. Als Beispieldatensatz verwenden wir einen aus 4 Tabellen bestehenden Datensatz zu TED-Talks. [Der Originaldatensatz wurde auf Kaggle.com veröffentlicht](https://www.kaggle.com/goweiting/ted-talks-transcript) und wurde für dieses Tutorial geringfügig angepasst.

{% hint style="info" %}
Aktuell sind nur die Teile \#0 und \#1 fertig. Der Rest folgt bald 👷♀.
{% endhint %}

## Übersicht

* 0⃣ [Workspace Setup](0-workspace-setup.md) 💻 
  * [Databricks-Account erstellen](0-workspace-setup.md#databricks-account-erstellen)
  * [Notebook-Templates importieren](0-workspace-setup.md#notebook-templates-importieren)
  * [Daten anlegen](0-workspace-setup.md#daten-anlegen) 
* 1⃣ [Der SELECT Befehl](1-der-select-befehl/)
  * [Metadaten sichten](1-der-select-befehl/metadaten-sichten.md) \(`DESCRIBE`\)
  * [Spalten auswählen](1-der-select-befehl/spalten-auswaehlen.md) \(`SELECT` / `FROM`\)
  * [Zeilen filtern](1-der-select-befehl/zeilen-filtern.md) \(`WHERE`\)
  * [Ergebnisse sortieren](1-der-select-befehl/ergebnisse-sortieren.md) \(`ORDER BY`\)
  * [Einfache Aggregationen](1-der-select-befehl/einfache-aggregationen.md) \(`COUNT`, `SUM`, `AVG`, `MAX`, `MIN`\)
  * [Gruppierungen](1-der-select-befehl/gruppierungen.md) \(`GROUP BY`\)
  * [Gruppierte Daten filtern](1-der-select-befehl/gruppierte-daten-filtern.md) \(`HAVING`\) 
* 2⃣ [Mehrere Tabellen](2-mehrere-tabellen.md)
  * `INNER`-Join
  * `LEFT` und `RIGHT`-Join
  * `OUTER`-Join
  * `CROSS`-Join 
* 3⃣ Mengenoperationen

  * Vereinigungsmengen bilden \(`UNION`\)
  * Schnittmengen bilden \(`INTERSECT`\)
  * Mengen subtrahieren \(`EXCEPT`\)

* 4⃣ Unterabfragen
  * Einwertige Unterabfragen
  * Unterabfragen als Mengen 
* 5⃣ Window-Funktionen
* 6⃣ Texte
* 7⃣ Statistische Funktionen
* 8⃣ Datum und Zeit

## 🔗 Links

### Cheatsheet

Unter dem folgenden Link findet ihr eine 2-seitige Zusammenfassung der wichtigsten SQL-Befehle: 

{% page-ref page="../cheatsheet-sql.md" %}

### Online-Kurse

Auf der Plattform Datacamp gibt es gute kostenlose Kurse zur Einführung in SQL:

* [SQL for Data Science](https://campus.datacamp.com/courses/intro-to-sql-for-data-science)
* [SQL for Exploratory Analysis](https://campus.datacamp.com/courses/sql-for-exploratory-data-analysis/)

Beide Kurse empfehle ich in der Reihenfolge, um die Kenntnisse zu vertiefen und einen anderen Blick auf das Thema zu bekommen.

