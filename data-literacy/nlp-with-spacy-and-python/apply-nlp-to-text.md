---
description: >-
  Um Texte besser analysieren zu können zerlegen wir sie im ersten Schritt in so
  genannte Tokens. Ein Token ist z.B. ein Wort oder ein Satzzeichen. spaCy hilft
  uns dabei.
---

# Apply NLP

## Anwenden der NLP Pipeline

Nachdem wir spaCy installiert und ein passendes Modell \(hier: Englisch - klein\) geladen haben können wir uns eine erste einfache Anwendung anschauen:

```python
import spacy

# Load English model
nlp = spacy.load("en_core_web_sm")

# Define the text and store it on a variable
text = "I am looking forward to learning about NLP with spaCy!"

# Run NLP pipeline
doc = nlp(text)
```

Zunächst müssen wir das Modul mit dem `import` Befehl in unserem Programm bekannt machen. Anschließend definieren wir eine Variable `nlp` und laden eines der zuvor heruntergeladenen Sprachmodelle, um es danach auf einen Beispieltext anwenden zu können. Das erreichen wir, indem wie `nlp(text)` aufrufen, wobei die Variable `text` den zu analysierenden Text beinhalten muss. Im Hintergrund wird nun eine Abfolge von Schritten durchlaufen, die wir auch _Pipeline_ nennen. In jedem Schritt wird der Text weiter verarbeitet oder mit Informationen angereichert. Am Ende steht das Ergebnis des NLP-Prozesses, das wir im Beispiel oben auf der Variable `doc` speichern. Diese Variable erlaubt es uns nun, auf jedes Teilergebnis zuzugreifen.

![Quelle: https://course.spacy.io/](../../.gitbook/assets/spacy_pipeline.png)

## Zugriff auf die Ergebnisse

### Token

spaCy führt, wie oben gezeigt, beim Ausführen der `nlp()` Funktion unterschiedliche Operationen auf den Texten standardmäßig nacheinander aus. Der erste Schritt ist der t_okenizer_. Das Wort _tokenize_ bedeutet so viel wie den Text in einzelne kleine Blöcke zu unterteilen. Damit sind zum einen die Wörter gemeint, aber auch Satzzeichen oder Zahlen können ein Token sein. Die Trennung erfolgt ganz einfach anhand des Trennzeichens, was im Standard das Leerzeichen ist.

Das Ergebnis des _tokenizers_ liegt nach Ausführen der `nlp()` Funktion im Ergebnisobjekt `doc` vor:

```python
import spacy

# Load English model
nlp = spacy.load("en_core_web_sm")

# Define the text and store it on a variable
text = "I am looking forward to learning about NLP with spaCy!"

# Run the NLP process pipeline and save result on variable 'doc'
doc = nlp(text)

# Iterate over the tokens
for token in doc:
    # Print the text for each token
    print(token.text)
```

Im Codebeispiel oben wird ab Zeile 13 in einer Schleife Schritt für Schritt der Wert jedes Tokens ausgegeben. Wir können auf den Wert \(oder den Text\) des Tokens über `token.text` zugreifen.  

![Ausgabe des Codebeispiels oben in einem Databricks Python Notebook.](../../.gitbook/assets/image%20%2821%29.png)

### POS-Tags

### Benannte Entitäten

### Syntaktische Abhängigkeiten

