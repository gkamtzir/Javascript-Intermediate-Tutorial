Hello and welcome to our very first Javascript intermediate tutorial. In this particular tutorial you’ll learn about the DOM and how to get HTML elements from it, using Javascript. Sit tight and enjoy! 

So, what exactly is the DOM? DOM stands for Document Object Model and is a programming interface which helps us work with web pages. Essentially, a web page is a document and the DOM is just a representation of that document. I’m sure you’re still confused, but fear not! Keep reading! 

When you write your HTML code and load it on the browser, it is turned into the DOM. You can take a look at the visual representation of the DOM by opening browser’s DevTools. If you do so, you’ll think that that’s exactly what’s in your HTML file. Well, more or less yes. Your HTML code is definitely in there, but there are also extra bits and pieces placed there by the browser. There is also a ton of functionality you can utilize with Javascript! I bet these were not in your HTML file, right? Let’s continue. 

The DOM represents the web page as a tree, consisting of nodes. Each node can have a parent, siblings and children. Let’s create a simple HTML file:

```html
<html>
  <head>
    <title>My title</title>
  </head>
  <body>
    <h1>A heading</h1>
    <a href=”https://programmunity.blogspot.com”>Link text</a>
  </body>
</html>
```

The DOM representation of this particular code can be seen below: 

That’s it. Quite simple, eventually. 

As I mentioned before, with Javascript we can manipulate the web page through the DOM. I’m going to create another simple HTML page which we’ll use in this tutorial:

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Javascript Intermediate Tutorial Part 1</title>
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
Save this code in a file and open it on your browser. Then, open DevTools. Go to the console tab and type: document. Then click on the object that gets returned. It’s page’s code, right? So, we can access the DOM by using the document object. Nice, but what do we do when we need only a part of it, only a node? We use specific functions that are included in the same object to retrieve it. 

There are 5 different functions we can utilize to achieve our goal. The first one is the getElementById() function, which helps us grab an element with a specific id. Let’s grab the `<h1>` element and store it in a variable:

```javascript
var h1 = document.getElementById('title');

console.log(h1);
```

Cool, right? 

The second function is the getElementsByClassName(). This function returns all the elements that have a specific class name. For example:

```javascript
var conversation = document.getElementsByClassName('conversation');

console.log(converstation);
```

Notice, that the returned object is not an Array. It’s a HTMLCollection. That means that if you want to use Array specific functions, first you’ll need to convert the collection to an Array. To do that you can use the following:

```javascript
var conversationArray = Array.from(conversation);

console.log(conversationArray);
```

The third function is the getElementsByTagName(). It returns a HTMLCollection containing all the elements that match the given tag.

```javascript
var jedis = document.getElementsByTagName('li');

console.log(jedis);
```

The fourth and fifth functions are much more flexible compared to the previous ones. These are the querySelector() and the querySelectorAll(). With the querySelector() we can easily fetch only the second `<li>` element:

```javascript
var yoda = document.querySelector('ul li:nth-child(2)');

console.log(yoda);
```

Wow, what’s that nth-child() thing? This is a pseudo element. You can think of them as extra tools that help us construct more sophisticated queries. Let’s see another example:

```javascript
var mace = document.querySelector('ul li.lightsaber-purple')

console.log(mace);
```

Pretty useful, right? The difference between the querySelector() and querySelectorAll() is that the first retrieves only the first element that will match the given criteria, while the second will return all of them. To see that in action, run the following:

```javascript
var paragraph = document.querySelector('p');

console.log(paragraph);

var paragraphs = document.querySelectorAll('p');

console.log(paragraphs);
```

Notice, also, that the querySelectorAll() returns a NodeList. Again, if you need to use Array specific functions then convert it to an Array. 

Today we’ve learned what the heck is the DOM and how can we fetch elements from it. In the next tutorial we will see how to add elements that don’t exist in our HTML file using Javascript code. 

See you there!
