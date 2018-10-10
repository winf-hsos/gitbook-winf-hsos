# \#02 - My Task App

In this exercise, you're going to build a simple task app with HTML, CSS and JavaScript.

{% hint style="info" %}
To get started, you can fork this [CodePen](https://codepen.io/winf-hsos/pen/VEpNrg)
{% endhint %}

## Add the structure with HTML

Let's start by adding the neccessary HTML to our app:

1. An a heading `<h1>` that gives your app an appropriate title.
2. Add an **unordered list** with 2 items that should serve as our first example tasks
3. Under the list, place a **button** and name it "Add Task". This button should later be implemented to actually add a new task to our list.
4. Add another button and name it "Clear Lists". This button should later clear all items from the list.

![Not really pretty!](../../../.gitbook/assets/image%20%285%29.png)

## Style the list with CSS

The list looks quite unattractive so far. Let's improve upon that:

1. For the whole app, set the font to **Roboto** and the font color to **\#262626**
2. Give the tasks element \(`<li>`\) a nice rounded border. Add a background color \(e.g. **\#B3D2B2 with opacity of 60%**\). Now, adjust the margin and padding values so that there is enough space between task items and between the border and the task name. Finally, make each list item **300 pixels** wide.
3. Remove the bullets from the list items \(`list-style: none`\) and remove the indendation of the items \(`padding-left`\).
4. When we move the mouse over a task item, change the background color so that it gets highlighted \(e.g. change the opacity to 100%\).
5. Make the mouse pointer turn into a pointer when we hover over a task item \(`cursor: pointer`\)
6. Give the two buttons rounded corners and adjust the spacing so that is looks good. Set the text color for the buttons to the same color as for the whole app.

![Looks better! Not perfect, but good enough.](../../../.gitbook/assets/image%20%283%29.png)

## Add the functionality with JavaScript

It's now time to make the whole thing work:

1. Implement the logic of the "Clear List" button, so that it removes all items from the list.
2. Implement the logic of the "Add Task" button, so that it prompts the user for a task name, and then adds a new task with that name. Make sure the last task is always **on top of the list**.
3. When the user clicks a task in the list, make the text appear ~~striked through~~ \(`text-decoration: line-through`\) and set the background to gray \(**\#757575**\), the hover color to another gray \(**\#C0C0C0**\), and the text color to white. Additionally, move the task to the end of the list.
4. When the user clicks on a completed task, the task should become undone and the styling changed back to what it was before. Also, the task should appear at the beginning of the list.

![A functional todo app!](../../../.gitbook/assets/image%20%289%29.png)

