Hello and welcome to the last Javascript intermediate tutorial. In this tutorial, we will complete our web application by displaying warning/error messages to the user and, also, submitting our form to a real API. Let’s get started!

We can check in the console if a specific value is valid, but that’s not user friendly at all. Instead, we should display a beautiful message to the user, explaining what’s right or wrong. For this purpose, we can construct a function: 

```javascript
function displayMessage() {

}
```

The displayMessage() function will receive 3 arguments: the input element which contains invalid data, the message we want to display and the type of the message ('error' or 'success'):

```javascript
function displayMessage(element, errorMessage, type) {

}
```

In the body of the function, we are going to create a new div element. This element will contain our message. 

```javascript
function displayMessage(element, errorMessage, type) {

  var div = document.createElement('div');
  div.setAttribute('class', type);

  var message = document.createTextNode(errorMessage);
 
  div.appendChild(message);

  element.parentElement.appendChild(div);

}
```

Essentially, we create a basic div element. Then we give it an 'error' class and the error message in a text node. Finally, we add the div element as a sibling to the input element (recall the use of parentElement). Simple!

Our click handler, now, looks something like this:

```javascript
submit.addEventListener('click', function(event) {

  event.preventDefault();

  var title = document.querySelector('#title');

  if (!isRequired(title.value)) {

    displayMessage(title, 'The title is required.', 'error');

  }

  if (!isLengthAppropriate(title.value)) {

    displayMessage(title, 'The title mush consist of at least 2 and not more than 30 characters', 'error');

  }

  var body = document.querySelector('#body');

  if (!isRequired(body.value)) {

    displayMessage(body, 'The body is required.', 'error');

  }

  var radioButtons = [];

  var vader = document.querySelector('#darthVader');

  radioButtons.push({
    value: 0,
    checked: vader.checked
  });

  var maul = document.querySelector('#darthMaul');

  radioButtons.push({
    value: 1,
    checked: maul.checked
  });

  var kylo = document.querySelector('#kyloRen');

  radioButtons.push({
    value: 2,
    checked: kylo.checked
  });

  var checkedRadioButton;

  if (!(checkedRadioButton = isRadioButtonChecked(radioButtons))) {

    displayMessage(vader, 'Exactly one radio button must be checked', 'error');

  }

  var urgent = document.querySelector('#urgent').checked;

});
```

Notice, that the variables, now, hold the element reference and not the value. We did this because we, now, need the element reference for the displayMessage() function.

Go ahead and test it. 

Hmm. The messages are quite nice, but they are stuck. Even if you enter a valid input they are still there. Well, we can do something about it. Just add a setTimeout() function. This function takes 2 arguments: a callback function and a number indicating the time (in milliseconds) to wait before executing the given callback. So, in the body of the callback we are going to remove the div element from the DOM after 5 seconds.

```javascript
function displayMessage(element, errorMessage, type) {

  var div = document.createElement('div');
  div.setAttribute('class', type);

  var message = document.createTextNode(errorMessage);
 
  div.appendChild(message);

  element.parentElement.appendChild(div);

  setTimeout(function() {

    div.remove();

  }, 5000);

}
```

There are 2 additional CSS classes in the main.css file. These are: 

```css
.error {
    color: #a94442;
    background-color: #f2dede;
    border-color: #ebccd1;
    border-radius: 3px;
    margin-top: 5px;
    padding: 15px;
}

.success {
    color: #3c763d;
    background-color: #dff0d8;
    border-color: #d6e9c6;
    font-size: 16px;
    padding: 20px;
    text-align: center;
}
```

As you can see, the errors disappear after 5 seconds. Although, this is a good approach, it is not perfect. Ideally, the messages would disappear if and only if the user enters a valid input. For example, the 'appropriate length' message would disappear when the user enters at least 2 characters in the 'title' field. This functionality can be achieved with events. You can monitor the title field by listening for 'onkeydown' events. Try it for homework! 

Now, the user interface informs the user for any invalid data. We can now proceed to the form submission. 

Our ultimate goal is to provide those data to an API. The API stands for Application Programming Interface and it basically is the middleman (the back-end, the server) between the front-end (your browser) and the database (where all the data are stored at). However, APIs, back-end logic and databases are beyond the scope of this tutorial. The only thing that we need to know, for now, is that we have to send our form data to a database through an API. That’s it. 

We usually send data to an API through HTTP protocol. HTTP is a communication protocol that made the world wide web possible. If you don’t know much about it, fear not. We will only need a tiny part of it. That is the POST functionality that provides. HTTP uses a few 'verbs' which help with the communication. For instance, when you type in the URL bar 'google.com' your browser makes a GET request (this is another and the most used HTTP 'verb') in order to get the desired web page. 

To make the long story short, we will make a POST request to the API to send our form data. This API, as I already mentioned in a previous tutorial, is the [JSONPlaceholder](https://jsonplaceholder.typicode.com/). We will send the 'title', the 'body' and the 'user'. Unfortunately, the structure of the data is defined from the API and it doesn’t include an 'urgent' or similar field. So, since the API is not ours, we will dump the 'urgent' field. Tough luck… 

Let’s create our submit function. In this function, we will create a 'XMLHttpRequest' object. This object is going to help us send the POST request. Then we use the open() function to define what kind of request we want to make and where that request is going to end up (to the fake API). After that, we declare that the data will be in JSON form. A JSON form, basically, is a Javascript object with properties and values, with the only difference it’s a string. Nothing less, nothing more. Lastly, we use the send() function to send the request. This function receives as an argument the data in the form of a JSON object. Notice, the use of the stringify() function which converts a Javascript object to a JSON string.

```javascript
function submitData(data) {

  var http = new XMLHttpRequest();

  http.open("POST", "https://jsonplaceholder.typicode.com/posts");
  http.setRequestHeader("Content-Type", "application/json");
  http.send(JSON.stringify(data));

}
```

Nice! How do we know if the API has accepted our request? Well, to do that we have to use the 'onreadystatechange' event handler. This handler provides 2 variables: the 'status' variable and the 'readyState' variable. The ‘status’ contains the status code of the HTTP request. If the status equals 201 it is accepted. If the status is greater or equal to 300 we will assume the opposite. However, this is not entirely true. If you want to learn more about the status codes, do a little research about the HTTP protocol (maybe I can explain them in a future tutorial). The 'readyState' variable contains an integer which represent the current state of the request. When that integer is equal to '4' the request is done and we can display the success or error message to the user.

So, our submit function looks like this: 

```javascript
function submitData(data) {

  var http = new XMLHttpRequest();

  http.onreadystatechange = function() {
 
    console.log('status: ' + this.status);

  }

  http.open("POST", "https://jsonplaceholder.typicode.com/posts");
  http.setRequestHeader("Content-Type", "application/json");
  http.send(JSON.stringify(data));

}
```

Again, if you still don’t understand what’s going on exactly, don’t worry. The goal of this post is to demonstrate that our form data will end up on a database through an API. I’ll try and make a tutorial about APIs, so stay tuned! 

The last thing we have to do is to display an error or success message to the user, after he submits the form: 

```javascript
function submitData(data) {

  var http = new XMLHttpRequest();

  http.onreadystatechange = function() {
 
    if (this.status == 201) {

      displayMessage(document.querySelector('input[type=submit]'), 'Data have been sent.', 'success');

    } else if (this.status >= 300) {

      displayMessage(document.querySelector('input[type=submit]'), 'Could not send data.', 'error');

    }

  }

  http.open("POST", "https://jsonplaceholder.typicode.com/posts");
  http.setRequestHeader("Content-Type", "application/json");
  http.send(JSON.stringify(data));

}
```

At this stage, the user is able to submit the form even with invalid data. To prevent such action, we have to check if there is any invalid input. We can do this by using a variable which will hold a boolean value. If that value is set to 'true' then we can be sure that there are no errors. If it’s set to 'false' then there is at least 1 error. 

```javascript
submit.addEventListener('click', function(event) {

  event.preventDefault();

  var error = false;

  var title = document.querySelector('#title');

  if (!isRequired(title.value)) {

    displayMessage(title, 'The title is required.', 'error');
    error = true;

  }

  if (!isLengthAppropriate(title.value)) {

    displayMessage(title, 'The title mush consist of at least 2 and not more than 30 characters', 'error');
    error = true;

  }

  var body = document.querySelector('#body');

  if (!isRequired(body.value)) {

    displayMessage(body, 'The body is required.', 'error');
    error = true;

  }

  var radioButtons = [];

  var vader = document.querySelector('#darthVader');

  radioButtons.push({
    value: 0,
    checked: vader.checked
  });

  var maul = document.querySelector('#darthMaul');

  radioButtons.push({
    value: 1,
    checked: maul.checked
  });

  var kylo = document.querySelector('#kyloRen');

  radioButtons.push({
    value: 2,
    checked: kylo.checked
  });

  var checkedRadioButton;

  if (!(checkedRadioButton = isRadioButtonChecked(radioButtons))) {

    displayMessage(vader, 'Exactly one radio button must be checked', 'error');
    error = true;

  }

  var urgent = document.querySelector('#urgent').checked;

  if (!error) {

    submitData({
      title: title.value,
      body: body.value,
      userId: checkedRadioButton.value
    });

  }

});
```

That was it! We have a fully functional web page. Amazing, right? 

So, this is the last intermediate tutorial. Be sure that many more will come along the way. I know you’re probably confused with the new stuff, but as I said it’s fine. The purpose of these post are to show you how to construct and manipulate a simple form using Javascript. 

Until the next tutorial series, stay safe!