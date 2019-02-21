# Einfache Aggregationen

## 💡 Einfache Aggregationen - so geht’s

Bisher entsprach jede Zeile im Ergebnis eines SQL Statements auch immer einer Zeile im Datensatz. Die Daten wurden bisher nicht verdichtet. Das wollen wir jetzt ändern.

Gerade bei großen Datenmengen interessieren wir uns oft nicht für einzelne Zeilen, sondern für **berechnete Größen auf Basis vieler Zeilen**. Hier kommen die Aggregationsfunktionen ins Spiel, die in der folgenden Tabelle aufgelistet sind.

| Aggregationsfunktion | Beschreibung |
| :--- | :--- |
| `COUNT` | Zählt die Datensätze. |
| `SUM` | Bildet die Summe über eine Spalte. |
| `AVG` | Bildet den Durchschnittswert \(arithmetisches Mittel\) einer Spalte. |
| `MIN` | Ermittelt den kleinsten Wert über eine Spalte hinweg. |
| `MAX` | Ermittelt den größten Wert über eine Spalte hinweg. |
| `DISTINCT` | Ermittelt eindeutige Werte innerhalb einer Spalte, entfernt also doppelte Werte. |

Nehmen wir an, wir wollen alle TED Talks zählen:

```sql
select count(*) as `Anzahl Talks` from ted_meta
```

### 💡 Spalten im Ergebnis umbenennen

Im obigen Beispiel wird ein Ergebnis mit einer Spalte zurückgeliefert, das die Anzahl der Datensätze in der Tabelle `ted_meta` enthält. Wie ihr dem Screenshot unten entnehmen könnt, hat die Spalte den Namen 'Anzahl Talks'. Diesen Namen haben wir oben im SQL Statement mithilfe des `as` Schlüsselwortes definiert. Bei genauem Hinschauen sieht man, dass der Name in _accents graves_ gesetzt wurde. Das ist nur dann zwingend notwendig, wenn der Name Leerzeichen enthält oder selbst ein SQL Schlüsselwort ist. Um Fehler zu vermeiden ist es eine gute Angewohnheit, diese Konvention von Anfang an beizubehalten.

Auf diese Weise können sämtliche Spalten eines SQL Statements umbenannt werden. Für eine schönere und lesbare Ausgabe ist das häufig ratsam.

![](../../../../.gitbook/assets/image%20%2815%29.png)

## 🧪 Übungsaufgaben

