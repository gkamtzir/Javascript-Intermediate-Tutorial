Hello and welcome to another Javascript Tutorial. In this one, you will learn how to create elements and append them to the DOM with the help of Javascript. That’s right, we will structure our web page’s body without writing HTML code. Sounds awesome! Let’s begin! 

The first step in this tutorial is to create a simple HTML file, with an empty body tag: 

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Javascript Intermediate Tutorial Part 2</title>
  </head>

  <body>

    <script src="./app.js"></script>
  </body>

</html>
```

Pay attention to the script tag that I added just before the closing <body> tag. This script tag links our Javascript code to that HTML file. At this point out Javascript file looks like this: 

```javascript
console.log('It works!');
```

Open the HTML file on your browser and check the console. There will be a ‘It works!’ message. If there’s not, make sure that both HTML and Javascript files are in the same folder and have the correct names. 

So, how exactly can we add elements from our Javascript file? To do that we can use the createElement() function on the document object. This basic form of this function takes a single parameter, which is a string that specifies the type of the element to be created. For example, if we want to create a button element we’ll do:

```javascript
document.createElement('button');
```

If you enter this into the console, you’ll see that a button is returned. But our page, still, does not have any button. Well, in order to add the button to our page, first we have to append it to a node. Remember from the last tutorial, that a node is basically an element in our HTML page. That being said, if we want to add a button inside our <body> tag we should do something like that: 

```javascript
var button = document.createElement('button');

document.body.appendChild(button);
```

Notice, that we’ve stored the newly created button in a variable called button and then we called the appendChild() function with the button variable as an argument. Essentially, the appendChild() function is applied on a node and takes as an argument the element that we want to add to that particular node. Dead simple, right? 

Hmm, the button has no text though. To add text to a node you can use the createTextNode() function on the document object. This one takes as an argument the desired text and returns a reference to that text node. If you want to add that text to the button element, you need to call the appendChild() on the button element, providing the text node as an argument: 

```javascript
var button = document.createElement('button');

var buttonText = document.createTextNode('Click me!');

button.appendChild(buttonText);
document.body.appendChild(button);
```

You can remove an element too. If you want to remove the button from the DOM, you have to use the remove() function. This function takes no arguments and gets called on the node you want to be removed. To remove the button element you do:

```javascript
button.remove();
```

Let’s go ahead and create the HTML of the previous tutorial by using only Javascript. We are going to write our code in the Javascript file that’s linked to the HTML file.

```javascript
//Headers
var h1 = document.createElement('h1');
var h3 = document.createElement('h3');

var h1Text = document.createTextNode('Javascript Tutorial');
var h3Text = document.createTextNode('We are learning about the DOM');

h1.appendChild(h1Text);
h3.appendChild(h3Text);

document.body.appendChild(h1);
document.body.appendChild(h3);

//Paragraphs
var p1 = document.createElement('p');
var p2 = document.createElement('p');

var p1Text = document.createTextNode('- Hello there!');
var p2Text = document.createTextNode('- General Kenobi!');

p1.appendChild(p1Text);
p2.appendChild(p2Text);

document.body.appendChild(p1);
document.body.appendChild(p2);

//Button
var button = document.createElement('button');

var buttonText = document.createTextNode('Order 66');

button.appendChild(buttonText);
document.body.appendChild(button);

//List
var ul = document.createElement('ul');
var jedis = [
  'Qui-Gon Jinn',
  'Yoda',
  'Mace Windu'
];
var li = [];
var liText = [];
for (var i = 0; i < jedis.length; i++) {

  li[i] = document.createElement('li');
  liText[i] = document.createTextNode(jedis[i]);
  li[i].appendChild(liText[i]);
  ul.appendChild(li[i]);

}

document.body.appendChild(ul);
```

The <ul> part of the script is much more concise, so make sure you fully understand it. We just use a for loop and 3 Arrays to create the unordered list. 

We managed to create an HTML page by writing Javascript code. If you inspect the page in the DevTools you’ll realize that it’s not exactly the same with the one we wrote in the last tutorial. All the ids and class name’s are missing. That’s what we are going to do in the next tutorial. 

To summarize, today you learned how to create different HTML elements and add them to the DOM. You learned how to make use of the createElement(), createTextNode() and appendChild() functions. In the next tutorial, you will learn how to add classes, ids and every other attribute to an element. Stay tuned! 

I’ll see you there!