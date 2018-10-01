---
description: >-
  In this lesson, you'll write your first SQL statements and start querying some
  data.
---

# Basic Queries

## Summary

SQL is the standard language to query database. In this section, we introduce the select command and see how we can use it to get the right columns and rows from a table.

For motivation and intro, watch this short video from the Khan Academy online course ["Intro to SQL: Querying and Managing Data"](https://www.khanacademy.org/computing/computer-programming/sql):

{% embed data="{\"url\":\"https://www.youtube.com/watch?v=IXycPq7MnwE\",\"type\":\"video\",\"title\":\"Welcome to SQL \| Intro to SQL: Querying and managing data \| Computer programming \| Khan Academy\",\"description\":\"SQL is useful for creating and querying relational databases. Learn how to use SQL with this interactive course!\\n\\nWatch the next lesson: https://www.khanacademy.org/computing/computer-programming/sql/sql-basics/v/s-q-l-or-sequel?utm\_source=YT&utm\_medium=Desc&utm\_campaign=computerprogramming \\n\\nMissed the previous lesson? https://www.khanacademy.org/computing/computer-programming/html-css/html-css-further-learning/v/html-validation?utm\_source=YT&utm\_medium=Desc&utm\_campaign=computerprogramming \\n\\nComputer Programming  on Khan Academy: Learn how to program drawings, animations, and games using JavaScript & ProcessingJS, or learn how to create webpages with HTML & CSS. You can share whatever you create, explore what others have created and learn from each other!\\n\\nAbout Khan Academy: Khan Academy offers practice exercises, instructional videos, and a personalized learning dashboard that empower learners to study at their own pace in and outside of the classroom. We tackle math, science, computer programming, history, art history, economics, and more. Our math missions guide learners from kindergarten to calculus using state-of-the-art, adaptive technology that identifies strengths and learning gaps. We\'ve also partnered with institutions like NASA, The Museum of Modern Art, The California Academy of Sciences, and MIT to offer specialized content.\\n\\nFor free. For everyone. Forever. \#YouCanLearnAnything\\n\\nSubscribe to Khan Academy’s Computer Programming  channel: https://www.youtube.com/channel/UCzYDKG5mmfPPIosXuQ1PvEA?sub\_confirmation=1\\nSubscribe to Khan Academy: https://www.youtube.com/subscription\_center?add\_user=khanacademy\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\n\\\"\",\"icon\":{\"type\":\"icon\",\"url\":\"https://www.youtube.com/yts/img/favicon\_144-vfliLAfaB.png\",\"width\":144,\"height\":144,\"aspectRatio\":1},\"thumbnail\":{\"type\":\"thumbnail\",\"url\":\"https://i.ytimg.com/vi/IXycPq7MnwE/maxresdefault.jpg\",\"width\":1280,\"height\":720,\"aspectRatio\":0.5625},\"embed\":{\"type\":\"player\",\"url\":\"https://www.youtube.com/embed/IXycPq7MnwE?rel=0&showinfo=0\",\"html\":\"<div style=\\\"left: 0; width: 100%; height: 0; position: relative; padding-bottom: 56.2493%;\\\"><iframe src=\\\"https://www.youtube.com/embed/IXycPq7MnwE?rel=0&amp;showinfo=0\\\" style=\\\"border: 0; top: 0; left: 0; width: 100%; height: 100%; position: absolute;\\\" allowfullscreen scrolling=\\\"no\\\"></iframe></div>\",\"aspectRatio\":1.7778}}" %}



