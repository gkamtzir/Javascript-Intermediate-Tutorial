## Altering the Attributes of Elements

![Tutorial image](https://2.bp.blogspot.com/-aBD12Ruas4U/W27kUe26THI/AAAAAAAABD0/1UPJlFSDlFkGUZwXPC-rk2LlZCH8Vf1XgCLcBGAs/s1600/Javascript-Intermediate-3.png)

Hello and welcome to another Javascript tutorial. Today, you will learn how to add, delete and alter the attributes of a HTML element. In the previous tutorial, we built the structure of a HTML page. It is time to add the appropriate classes and ids. 

Below is the HTML code that we created dynamically using Javascript. The structure is, now, hardcoded because we want to avoid the extra Javascript code (from the last tutorial) for clarity reasons. 

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Javascript Intermediate Tutorial Part 3</title>  
  </head>

  <body>

    <h1>Javascript Tutorial</h1>
    <h3>We are learning about the DOM</h3>

    <p>- Hello there!</p>
    <p>- General Kenobi!</p>

    <button>Order 66</button>

    <ul>
      <li>Qui-Gon Jinn</li>
      <li>Yoda</li>
      <li>Mace Windu</li>
    </ul>

    <script src="./app.js"></script>
  </body>

</html>
```

To add an attribute to an existing element, you have to use the setAttribute() function. This function accepts 2 arguments: the first is the name of the attribute to be added and the second is the value of that attribute. So, to add an id of 'title' to the `<h1>` tag we should do: 

```javascript
var h1 = document.querySelector('h1');

h1.setAttribute('id', 'title');
```

We can also retrieve the value of a specific attribute by using the getAttribute() function. This function accepts 1 argument: the name of the attribute. To get the id value of `<h1>`’s tag we can do: 

```javascript
console.log(h1.getAttribute('id'));
```

If we need to check the existence of a particular attribute we can use the hasAttribute() function. It accepts the attribute name as an argument and returns 'true' if it exists. Otherwise, it returns 'false'.

```javascript
console.log(h1.hasAttribute('id'));
console.log(h1.hasAttribute('class'));
```

If we want to remove an attribute we use the removeAttribute() function. It takes the attribute name as an argument. Let’s remove button’s id attribute: 

```javascript
h1.removeAttribute('id');
```
I’m going to create some basic CSS rules for the classes and ids we want to use in our HTML file. 

```css
#title {
  border: 2px solid #ff0000;
}

#subtitle {
  border: 1px dashed #00ff00;
}

.conversation {
  font-weight: bold;
  color: #123456;
}

#sidious {
  background: #551a8b;
}

.lightsaber-green {
  color: #008000;
}

.lightsaber-purple {
  color: #a020f0;
}
```

Don’t forget to link this CSS file to our HTML file by adding the following line just before the closing `<head>` tag.

```html
<link rel="stylesheet" href="main.css" />
```

Let’s start adding the desired attributes to our HTML elements. 

```javascript
var h1 = document.querySelector('h1');
var h3 = document.querySelector('h3');

var p = Array.from(document.querySelectorAll('p'));

var button = document.querySelector('button');

var li = Array.from(document.querySelectorAll('li'));

h1.setAttribute('id', 'title');
h3.setAttribute('id', 'subtitle');

for (var i = 0; i < p.length; i++) {

  p[i].setAttribute('class', 'conversation');

}

button.setAttribute('id', 'sidious');

li[0].setAttribute('class', 'lightsaber-green');
li[1].setAttribute('class', 'lightsaber-green');
li[2].setAttribute('class', 'lightsaber-purple');
```

Voilà! Each element has the proper attribute and the CSS styling is working. Pretty good! 

Because it’s quite lame in 2k18 to use a for-loop like that, I’m going to show you a much better option. When we want to iterate over an Array we can use a forEach loop. It works very similar to the filter, map and reduce functions. It takes a function as an argument. That function accepts a parameter which is the actual item of the Array. So, if we want to iterate the p Array and set the attributes, we should do:  

```javascript
p.forEach(function(p) {
 
  p.setAttribute('class', 'converstation');

});
```

From now on, I’ll be using only the forEach loop. 

But, what happens when we need to change the style of a specific element without having a predefined CSS rule? Well, in that case we can use the style property of the element. The style property gives us access to every single styling property (for example: background, margin etc). So, if for some reason we need to change button’s background, we can do: 

```javascript
button.style.background = 'red';
```

For the style properties which contain ‘-’, we remove the dash and capitalize the first letter of the second word. For example, to change button’s font-size, we do:

```javascript
button.style.fontSize = '20px';
```

Now, you know how to add, remove and alter the attributes of an element. You are, also, able to change the style of elements, without having a predefined CSS rule. In the next tutorial, we are going to learn about the relation between the different nodes (elements) of the DOM. 

See you!
