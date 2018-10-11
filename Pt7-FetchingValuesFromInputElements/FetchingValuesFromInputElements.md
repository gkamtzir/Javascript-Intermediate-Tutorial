## Fetching Values from Input Elements

![Tutorial image](https://1.bp.blogspot.com/-NZWQpxYpbmU/W31LnZ46IkI/AAAAAAAABFs/tlEOPQ61V3cAHge6zu2nkpfoqRygaMOmgCLcBGAs/s1600/Javascript-Intermediate-7.png)

Hello and welcome to another Javascript tutorial. In today’s post, we will see how to fetch the needed values from the input elements. Let’s get started! 

At the moment, the only file we have is the HTML file shown below: 

```html
<!DOCTYPE html>
<html>

  <head>
    <title>Task Assigner</title>
    <link rel="stylesheet" href="main.css" />
  </head>

  <body>

    <div class="main-content">

      <h2>Assign a User</h2>

      <form>

        <div class="form-group">
          <label for="title">Title:</label>
          <input type="text" id="title" maxLength="30" placeholder="Enter task's title"/>
        </div>

        <br />

        <div class="form-group">
          <label for="body">Body:</label>
          <textarea id="body"></textarea>
        </div>

        <br />

        <div class="form-group">
          <input type="radio" id="darthVader" name="user" value="0" checked> Darth Vader
          <br />
          <input type="radio" id="darthMaul" name="user" value="1"> Darth Maul
          <br />
          <input type="radio" id="kyloRen" name="user" value="2"> Kylo Ren
        </div>

        <br />

        <div class="form-group">
          <input type="checkbox" id="urgent" name="urgent" /> Urgent?
        </div>

        <br />

        <input type="submit" value="Submit" />

      </form>

    </div>

    <script src="./app.js"></script>

  </body>

</html>
```

How do we fetch the value of each input element? Well, the first question we need to answer is not ‘how’ but ‘when’. When do we need to fetch those values? As you probably have guessed, we need to fetch them when the user clicks the 'Submit' button. In other words, we have to set a 'listener' to notify us when the user presses the 'Submit' button. To achieve that we can do:

```javascript
var submit = document.querySelector('input[type=submit]');

submit.addEventListener('click', function() {

  console.log('Submit clicked');

});
```

Notice the way we used the argument in the querySelector() function. Basically, this syntax states that we want to get the first input element which has an attribute named 'type' with the value 'submit'. This element, of course, is our 'Submit' button. So, after attaching this 'listener' to the button we expect to see the 'Submit clicked' message in the console. If you give it a try you’ll immediately realize that the message appears for a fraction of a second and then the page reloads. Let me tell you that this is the default behavior of the 'Submit' button. When the user clicks it, the page automatically reloads. To prevent this, we must utilize the event object by calling the preventDefault() function. This function, as its name indicates, it prevents any default behavior. 

```javascript
submit.addEventListener('click', function(event) {

  event.preventDefault();
  console.log('Submit clicked');

});
```

Cool! 

Now we know when the user clicks on the 'Submit' button. It’s time to fetch the desired values. 

To fetch the title we can do: 

```javascript
var title = document.querySelector('#title').value;
```

To fetch the body, we follow the exact same approach: 

```javascript
var body = document.querySelector('#body').value;
```

To check which of the radio buttons is selected, we can use the 'checked' property:

```javascript
var vader = document.querySelector('#darthVader').checked;

var maul = document.querySelector('#darthMaul').checked;

var kylo = document.querySelector('#kyloRen').checked;
```

Lastly, to see if the task is urgent or not, we should do: 

```javascript
var urgent = document.querySelector('#urgent').checked;
```

Our Javascript files should look something like this:

```javascript
var submit = document.querySelector('input[type=submit]');

submit.addEventListener('click', function(event) {

  event.preventDefault();
  console.log('Submit clicked');

  var title = document.querySelector('#title').value;
  console.log(title);

  var body = document.querySelector('#body').value;
  console.log(body);

  var vader = document.querySelector('#darthVader').checked;
  console.log(vader);

  var maul = document.querySelector('#darthMaul').checked;
  console.log(maul);

  var kylo = document.querySelector('#kyloRen').checked;
  console.log(kylo);

  var urgent = document.querySelector('#urgent').checked;
  console.log(urgent);

});
```

In order to be able to see the values, I’ve added 'console.logs' after each value. 

Pretty cool, right? Now you know how to get a value from an input element. In the next tutorial, you’ll learn to validate those values and print warnings and errors to the user. 

See you there!
