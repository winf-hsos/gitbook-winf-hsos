# Texte für die Analyse mit SQL vorbereiten

## 🎯 Lernziele

Um Texte mit SQL sinnvoll analysieren zu können, müssen wir sie erst in eine andere Form bringen. Konkret müssen wir eine Struktur auf die unstrukturierten Textdaten projizieren. Wir lernen in diesem Tutorial, wie wir Texte in einzelne Token \(Wörter\) zerlegen und irrelevante Inhalte entfernen.

## 🌟 Daten für das Tutorial

Für dieses Tutorial verwenden wir Twitter Daten als Beispiel, wie sie im Modul Big Data Analytics erhoben werden.

{% hint style="info" %}
Ich stelle bald ein Template mit einem ausgewählten Twitter-Datensatz bereit, so dass jeder dieses Tutorial nutzen kann.
{% endhint %}

## 💡 In fünf Schritten ans Ziel

Texte sind unstrukturierte Daten in dem Sinn, dass es keine Struktur wie Spalten mit atomaren Daten und Datentypen gibt, auf denen wir z.B. mittels der `WHERE` Bedingung Filter definieren oder die wie in einer sinnvollen Form aggregieren können. Daher müssen wir zunächst eine Struktur auf die Texte projizieren, auf der wir anschließend mit SQL Analysen durchführen können. Eine Möglichkeit ist das Zerlegen der Texte in einzelne Wörter \(_Tokens_\).

Im Prozess, die Texte in einzelne Wörter zu zerlegen, müssen wir unterschiedliche Schritte durchführen:

{% page-ref page="1-zeilen-filtern.md" %}

{% page-ref page="2-texte-bereinigen-und-normalisieren.md" %}

{% page-ref page="3-texte-in-woerter-zerlegen.md" %}

{% page-ref page="4-stopwoerter-filtern.md" %}

{% page-ref page="5-pos-tagging.md" %}

Die Zusammenfassung der 5 Schritte gibt es auch als Foliensatz:

{% embed url="https://docs.google.com/presentation/d/1ucTdKscyjA7QNfnbkXQZTDqtnTUkpntGbTWjeZVsv0A/edit?usp=sharing" %}

### 

