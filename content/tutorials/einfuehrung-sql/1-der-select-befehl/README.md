# \#1 Der SELECT Befehl

## 🎯 Lernziele

* 🎯 Ihr kennt die Syntax des SELECT Befehls, mit dem Daten aus Tabellen in fast beliebiger Weise abgefragt werden können.
* 🎯 Ihr kennt die unterschiedlichen Komponenten des SELECT Befehls und versteht, wie diese das Ergebnis verändern. 
* 🎯 Ihr könnt einfach Abfragen mithilfe des SELECT Befehls formulieren, um Fragestellungen auf Basis von Daten zu beantworten.

## 🔑 Key Points

🔑 Mit dem SELECT Befehl können **strukturierte Daten** aus einer Datenbank abgefragt werden. Mit strukturierten Daten sind Daten gemeint, die sich in Zeilen einer Tabelle abbilden lassen, wobei die Tabelle aus _1_ bis _n_ Spalten besteht. Stellt euch als Analogie ein Excel-Spreadsheet vor.

🔑 Jede Spalte einer Tabelle enthält genau einen Wert bzw. ein **Attribut** des Datensatzes. Für jedes Attribut ist festgelegt, welchen Wertebereich es annehmen darf \(z.B. eine ganze Zahl, einen beliebigen Text, ein Datum etc.\). Je nach Definition der möglichen Werte besitzt eine Spalte einen bestimmten **Datentyp**.

🔑 In SQL häufig verwendete **Datentypen** sind:

* Ganze Zahlen \(Integer oder `int`\)
* Gleitkommazahlen \(`double` oder `float`\)
* Zeichenketten \(`string`\)
* Datum \(`date`\)
* Zeitstempel \(`timestamp`\)
* Wahrheitswerte \(`boolean`\)

🔑 Während eine Tabelle beliebig viele Spalten haben kann, erlaubt der SELECT Befehl das Auswählen einer Teilmenge der vorhandenen Spalten. Denn häufig benötigt man für die Beantwortung einer Fragestellung nur wenige Spalten. Das Auswählen einer Teilmenge nennt man in der relationalen Algebra auch **Projektion**.

## 

