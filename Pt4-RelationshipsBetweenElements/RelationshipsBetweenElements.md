Hello and welcome to another Javascript Tutorial. In this tutorial, you will learn about the different relationships between the nodes and how to navigate from one to the other. Without further ado, let’s begin! 

Every node in the DOM tree has some kind of relationship with some other node. These relationships are described using the following terms: parent, child and sibling. Take a look below. This is the HTML code from the previous tutorials. Open it on your browser and inspect it on the DevTools. 

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Javascript Intermediate Tutorial Part 4</title>
  </head>

  <body>

    <h1 id="title">Javascript Tutorial</h1>
    <h3 id="subtitle">We are learning about the DOM</h3>

    <p class="conversation">- Hello there!</p>
    <p class="conversation">- General Kenobi!</p>

    <button id="sidious">Order 66</button>

    <ul>
      <li class="lightsaber-green">Qui-Gon Jinn</li>
      <li class="lightsaber-green">Yoda</li>
      <li class="lightsaber-purple">Mace Windu</li>
    </ul>

  </body>

</html>
```

In this DOM tree, the top node is called 'root node'. In other words, the `<html>` node is the root node of the tree. Each other node can have a parent node (only one!), child nodes and sibling nodes. Notice, that the root node is the only one that has no parent. 

Let’s figure out the different relationships in this tree. The root node (`<html>`) has two children: the `<head>` and the `<body>`. These nodes are siblings. Each of these have their own children. For example the `<head>` has a child: the `<title>`. The <body> node has as children all the nodes that we’ve worked with in the past. Almost all of the nodes inside the `<body>` section of the page, see the `<body>` as their parent. I said 'almost' because the `<li>` nodes are not direct children of the `<body>` node. Their parent is the `<ul>` node. 

By now you should be able to understand each and every relationship between the various nodes. It’s not that hard, is it? 

So, how can we navigate from one node to the other using these relationships? Let’s say that we want to get a reference to the `<html>` node from the `<body>` node. We, surely, know that `<body>` is `<html>`’s child, so we can do:

```javascript
console.log(document.body.parentElement);
```

We can, also, see `<body>`’s children by doing: 

```javascript
console.log(document.body.children);
```

If we need to fetch only the first or the last child of a node we can do the following: 

```javascript
console.log(document.body.firstElementChild);

console.log(document.body.lastElementChild);
```

What about siblings, though? We can 'walk' from one sibling to the other by using the properties below:

```javascript
var li = document.querySelector('li');

console.log(li.nextElementSibling);

var liSecond = document.querySelector('li:nth-child(2)');

console.log(liSecond.previousElementSibling);
```

These are the different properties you will, probably, use in your developer career to navigate inside the DOM. I hope you understood everything, because they can be really handy in a lot of cases. 

Until next time.
