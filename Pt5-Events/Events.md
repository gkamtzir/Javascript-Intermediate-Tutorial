Hello and welcome to another Javascript tutorial. Today, we will take a look at the different events that we can bind (and unbind) to any HTML element. Let’s begin! 

Until now, we were able to create web pages using Javascript. We learned how to fetch, add and remove elements. We, also, understood the relationships between the various elements (nodes) and how to navigate from one to the other. But, as you probably have realized our web pages are not interactive. They are, just, simple ‘vanilla’ pages. 

How can we make them interactive? Of course, Javascript is here to help! The DOM provides a wide range of events that Javascript can utilize, in order to produce user interfaces that are both interactive and very responsive. 

How do they work, though? As I mentioned above, the DOM provides many events. You can see every one of them ‘here’. With Javascript we can add a 'listener' to an element to watch for a particular event. When this event gets triggered we can react accordingly. That 'reacting process' usually comes in the form of a 'handler'. A handler is, basically, a callback function that gets executed when the corresponding event gets triggered. 

So, let’s say that we want to print in the console a simple message when the button 'Order 66' gets clicked: 

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Javascript Intermediate Tutorial Part 5</title>
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

The first thing we have to do is to bind a 'listener' to it. We can bind a listener with the addEventListener() function. It takes 2 parameters: the event type and a handler. 

```javascript
var button = document.getElementById('sidious');

function executeOrder66() {

  console.log('Execute order 66...');

}

button.addEventListener('click', executeOrder66);
```

As we can see, this listener listens (you don’t say) for click events and when someone clicks the button the handler gets called. Dead simple, right? 

With Javascript, we are able to unbind an event, too. Let’s say that we want to remove the previous listener. The only thing we have to do is to use the removeEventListener() function. This function receives 2 arguments: the event type and the handler. If we want to remove the listener that listens for 'click' events and executes the handler executeOrder66(), we should do: 

```javascript
button.removeEventListener('click', executeOrder66);
```

That’s how we bind and unbind events. Because practice makes perfect, let’s add a 'mouseover' event to a `<li>` element: 

```javascript
var mace = document.querySelector('li:nth-child(3)');

function maceWindu() {

  console.log('Be mindful of your feelings.');

}

mace.addEventListener('mouseover', maceWindu);
```

Wow, wait a second. Why do we get 2 messages in the console? We only hovered once! Don’t worry, that was expected. In Javascript, when an event gets triggered it 'bubbles' from bottom to top. In other words, from the children to the parent. When you mouse over the 'Mace Windu' <li> a 'mouseover' event travels to the <ul> element. That’s why the message appears twice. We can prevent that from happening by using the preventPropagation() function on the 'event' object. The 'event' object is the first parameter of any event handler. Either you use it or not, it’s there. So if we want to fix the previous issue, we have to update the maceWindu() function to something like:

```javascript
function maceWindu(event) {

  event.stopPropagation();
  console.log('Be mindful of your feelings.');

}
```

Cool! It works like a charm! 

In this tutorial we’ve learned how to bind and unbind events. We also learned how to prevent the propagation of events (also known as bubbling) from the child nodes to the parent node. This is the last tutorial dedicated to the DOM. The next 4 will be 'form' oriented and, let me add, much more practical and fun! 

See you there!