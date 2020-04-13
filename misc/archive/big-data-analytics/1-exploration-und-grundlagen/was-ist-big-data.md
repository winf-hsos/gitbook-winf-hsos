---
description: In dieser Session lernen wir die Grundlagen von Big Data.
---

# Was ist Big Data?

## ❓ Fragen

* Was charakterisiert Big Data?
* Vor welche Herausforderungen stellt uns Big Data?
* Welche Lösungsansätze gibt es, um diesen Herausforderungen zu begegnen?

## 🏷 Begriffe

* 🏷 Die 3 Vs
  * 🏷 ​Volume
  * 🏷 Variety
  * 🏷 Velocity
* 🏷Polystrukturierte Daten

## ▶ Lerneinheit

### 1⃣ Was ist Big Data?

#### Slides

{% embed url="https://docs.google.com/presentation/d/16IASPSzF1lomsqm84KOUZK7slZhU3VwfrHbO2tqIYUQ/preview" %}

#### Video

Diese Slides gibt es auch als Video auf YouTube:

{% embed url="https://www.youtube.com/watch?v=\_dflzZgFtoo" %}



## ⏭ Nachbereitung

Lest bitte als Nachbereitung der Sitzung den folgenden Textausschnitt aus Hansen et al \(2015\). Die Texte werden über OSCA bzw. Slack bereitgestellt.

| Titel | Seiten |
| :--- | :--- |
| BDA-01 - Skalierbare Datenspeicherung und Big Data - Wirtschaftsinformatik 🇩🇪  | 7 |

## 🔑 Key Points

* Wir können Big Data über die 3 Vs von herkömmlichen Daten abgrenzen. Jedes V steht für eine Eigenschaft, die auf Big Data zutreffen _kann_, aber nicht muss. Es reicht tendenziell aus, wenn eines der 3 Vs erfüllt ist, um von Big Data zu sprechen. 
  * **Volume** = Das Datenvolumen gemessen in Bytes überschreitet eine Zahl, die einzelne Rechner bei der Speicherung und Verarbeitung vor Probleme stellen. Typischerweise spricht man hier ab dem hohen Gigabyte oder Terabyte-Bereich von Big Data. 
  * **Velocity** = Die Geschwindigkeit \(Frequenz\) der Datenerzeugung ist sehr hoch und stellt einzelne Rechner vor Probleme. Ein Beispiel sind Sensordaten, die in der Industrie von sehr vielen Geräten im Millisekunden-Takt erzeugt werden. Die Herausforderung entsteht dadurch, dass Anwendungen eine möglichst zeitnahe Analyse dieser hochfrequenten Daten erfordern. Oft dürfen zwischen dem Entstehen der Daten und dem Analyseergebnis nur Millisekunden oder wenige Sekunden vergehen. 
  * **Variety** = Die Vielfalt der Daten ist sehr hoch im Vergleich zu traditionellen Daten in Spreadsheets oder relationalen Datenbanken. Im Big Data Umfeld finden wir häufig von Anwendern erzeugte mediale Daten wie Bilder, Videos, Audiofiles oder Texte. Diese besitzen keine Struktur im Sinne von Spalten und Werten und stellen deshalb eine Herausforderung für traditionelle relationale Datenbanken dar. 
* Um der rasanten Entwicklung der Rechenleistung Rechnung zu tragen, schlagen Hansen et al. eine sehr weit gefasste Definition von Big Data vor. Im Kern sagt die Definition aus, dass Daten dann als Big Data bezeichnet werden müssen, wenn sie **die Fähigkeit einzelner Rechnersysteme übersteigen, diese zu verarbeiten**. Diese Definition lässt sich gut mit den 3 Vs vereinbaren, da speziell bei Volume und Velocity die Rechnerleistung eine entscheidende Rolle spielt.

