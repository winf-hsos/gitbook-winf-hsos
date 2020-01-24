---
description: >-
  Natural Language Processing - oder NLP - beschreibt den Versuch, mittels
  Algorithmen den Inhalt von Sprache und speziell Texten zu verstehen. Wir
  lernen spaCy kennen, ein Python-Modul für NLP.
---

# NLP mit Python

## Problem

Texte sind unstrukturierte Daten, die wir nicht ohne Weiteres analysieren können. In vielen Anwendungsfällen geht es aber gerade darum, automatisiert bestimmte Dinge aus Texten zu extrahieren:

* Wichtige Objekte wie Marken, Produkte, Personen, Ereignisse oder Orte, über die gesprochen wird.
* Stimmungen \(_sentiments_\) in einem Text: Ist ein Text positiv oder negativ in Bezug auf den Sachverhalt oder Gegenstand?
* Themen, über die gesprochen wird und _wie_ darüber gesprochen wird.
* Klassifizierung von Texten: Handelt es sich um einen Newsbeitrag oder einen wissenschaftlichen Aufsatz? Ist der Text eher pro oder contra in Bezug einer bestimmten These?
* Viele Anwendungen, die wir täglich nutzen, basieren auf Techniken des NLP: Suchmaschinen, Sprachassistenten, Chatbots, Übersetzungssoftware \(Quelle: [Recent Advancements in NLP](https://medium.com/swlh/recent-advancements-in-nlp-1-2-192ac7eefe3c)\).

{% hint style="info" %}
**Wie können wir Texte aufbereiten oder vorbereiten, um sie automatisch und quantifizierbar analysieren zu können? Welche Verfahren können wir anwenden, um Informationen aus Texten zu extrahieren?**
{% endhint %}

Bedeutung in Texten zu erkennen ist keine leichte Aufgabe für Maschinen:

> _“John saw the man on the mountain with a telescope”_ Who is on the mountain? John, the man, or both? Who has the telescope? John, the man, or the mountain? \([Recent Advancements in NLP](https://medium.com/swlh/recent-advancements-in-nlp-1-2-192ac7eefe3c)\)

## Lernpfad

Zuerst installieren wir das Pyton-Modul [spaCy](https://spacy.io/), um es in unserer gewohnten Databricks-Umgebung verwenden zu können:

{% page-ref page="spacy-installieren.md" %}

Anschließend können wir NLP auf Texte anwenden und die Teilergebnisse begutachten:

{% page-ref page="nlp-auf-texte-anwenden.md" %}



## Links

{% embed url="https://spacy.io/" %}

{% embed url="https://course.spacy.io/" %}

{% file src="../../../.gitbook/assets/spacy-cheatsheet.pdf" caption="spaCy Cheatsheet" %}

