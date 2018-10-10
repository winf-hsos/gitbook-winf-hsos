# \#02 - My Task App

In this exercise, you're going to build a simple task app with HTML, CSS and JavaScript.

{% hint style="info" %}
To get started, you can fork this [CodePen](https://codepen.io/winf-hsos/pen/VEpNrg)
{% endhint %}

## Add the structure with HTML

Let's start with by adding the neccessary HTML to our template:

1. An a heading `<h1>` that gives your app an appropriate title.
2. Add an **unordered list** with 2 items that should serve as our first example tasks
3. Under the list, place a **button** and name it "Add Task". This button should later be implemented to actually add a new task to our list.
4. Add another button and name it "Clear Lists". This button should later clear all items from the list.

![We can do better than that.](../../../.gitbook/assets/image%20%281%29.png)

## Style the list with CSS

The list looks quite unattractive so far. Let's improve upon that:

1. For the whole app, set the font to **Roboto** and the font color to **\#262626**
2. Give the tasks element \(`<li>`\) a nice rounded border. Add a background color \(e.g. **\#B3D2B2**\). Now, adjust the margin and padding values so that there is enough space between task items and between the border and the task name. Finally, make each list item **300 pixels** wide.
3. Remove the bullets from the list items \(`list-style: none`\) and remove the indendation of the items \(`padding-left`\).
4. When we move the mouse over a task item, change the background color so that it gets highlighted.
5. Give the two buttons rounded corners and adjust the spacing so that is looks good.

![An improvement, but not perfect. Good enough though.](../../../.gitbook/assets/image%20%286%29.png)

## Add the functionality with JavaScript

It's now time to make the whole thing work:

1. Implement the logic of the "Clear List" button so that it removes all items from the list.
2. Implement the logic of the "Add Task" button so that it prompts the user for a task name and then adds a new task with that name to end of the list.
3. When the user clicks a task in the list, make the text appear striked through. Additionally, move the task to the end of the list.



