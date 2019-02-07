# Ergebnisse sortieren

## 💡 Sortieren - so geht’s

Einfach, aber sehr mächtig: Das 🔤Sortieren der Ergebnisse erlaubt es uns, Ranglisten zu erstellen und durch Auf- oder Abwärtssortierung schnell den kleinsten oder größten Wert in einer Liste zu identifizieren.

Das erste Beispiel erzeugt eine Liste der TED Talks sortiert nach der Anzahl Views, wobei der Talk mit den wenigsten Views oben in der Ergebnisliste erscheint:

```sql
select * from ted_meta
order by views
```

### 💡 Aufsteigend oder absteigend?

Wollen wir lieber den Talk mit den meisten Views oben, drehen wir das Ergebnis einfach um, indem wir die Sortierungsrichtung ändern:

```sql
select * from ted_meta
order by views desc
```

![](../../../../.gitbook/assets/image%20%285%29.png)

⚠ Die Zusatzangabe `DESC` steht für _descending_ und bedeutet übersetzt absteigend. Das bedeutet, größere Werte erscheinen oben. Ohne das Schlüsselwort `DESC` wird standardmäßig aufsteigend sortiert, was explizit auch mit dem Schlüsselwortpendant `ASC` erreicht werden kann.

### 💡 Sortieren nach mehrerern Spalten

Wir haben die Möglichkeit, mehr als ein Sortierungskriterium anzugeben. Die Reihenfolge ist entscheidend: Es wird zuerst nach dem ersten und dann nach den nachfolgenden Kriterien sortiert. Wir wollen als Beispiel alle TED Talks nach ihrem Event sortieren, und innerhalb eines Events nach der Dauer. Dabei sollen die längeren Talks oben stehen \(absteigende Sortierung\):

```sql
select * from ted_meta
order by event asc, duration desc
```

⚠ Das Schlüsselwort `ASC` wäre hier nicht notwendig, da auch standardmäßig aufsteigend sortiert würde.

## 🧪 Übungsaufgaben

