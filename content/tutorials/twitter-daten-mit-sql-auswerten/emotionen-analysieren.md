# Emotionen analysieren

## 💡 Emotionen über Emojis identifizieren

Eine einfache Möglichkeit nach Emojis zu suchen ist die Verwendung des `LIKE` Operators:

```sql
select text, * from twitter_timelines
where text like '%😂%'
```

{% embed url="https://unicode.org/emoji/charts/full-emoji-list.html" %}

{% embed url="http://www.emojitracker.com/" %}



