## Form Validation

![Tutorial image](https://4.bp.blogspot.com/-314U39S3noM/W4J3T9vb8mI/AAAAAAAABF8/bAnX5714ooc_wj6fEDPpUJbjhH3QaKU9ACLcBGAs/s1600/Javascript-Intermediate-8.png)

Hello and welcome to another Javascript Tutorial. Today, we are going to take a look at data validation. Let’s get started! 

In the previous posts, we’ve managed to build the following codebase: 

HTML: 

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
          <input type="text" id="title" maxLength="30" placeholder="Enter task's title" />
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

CSS:

```css
body {
  width: 20%;
  margin: auto;
  background: #eddbb7;
}

.main-content {
  text-align: center;
}

.form-group {
  text-align: left;
}

#body {
  padding-top: 30px;
}
```

Javascript: 

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

Now, our goal is to properly validate the given data. Users tend to provide data in all sorts of shapes and forms (not web forms :P). We, as developers, need to make sure the given data match our criteria. So, after the user submits the data, we have to validate them and inform him for any invalid data. 

Important: in this post, we will see how to validate a form on the front-end. It is crucial to validate the data again on the back-end, because a form can be altered in a lot of different ways.

First of all, let’s figure out the rules our data must follow: 

*Every single text input is required. 
*The title must consist of at least 2 characters and at maximum 30 characters. 
*Only one radio button must be checked. 

Based on the these rules, we will have to create a set of functions which will check for any invalid data. 

Rule #1: 

```javascript
function isRequired(value) {

  return value != null && value.trim() != '' ? true : false;

}
```

In this function, we check for 2 things: if the value is null or undefined and if the value is an empty string. We accomplish the first one by checking if the value is not equal to null. Notice, that we use 1 'equal sign' and not 2. This allows us to check for both null and undefined data. To make sure the given string is not empty, we simply trim the given value (using the trim() function) and then we check if it’s equal to an empty string. 

Rule #2: 

```javascript
function isLengthAppropriate(value) {
 
  return value != null && value.length > 1 && value.length < 31 ? true : false;

}
```

In this one, we just check if the given value exists and has more than 1 and less than 31 characters. If it does, we return true. Otherwise, we return false. 

Rule #3: 

```javascript
function isRadioButtonChecked(radioButtons) {

  var checkedRadioButton = null;
  var moreThanOne = null;
  
  if (radioButtons != null) {
  
  
  radioButtons.some(function(radioButton) {

      if (radioButton.checked) {

        if (checkedRadioButton) {

          moreThanOne = true;
          return true;  

        } else {

          checkedRadioButton = radioButton;

        }

      }

    });

    if (checkedRadioButton && !moreThanOne) {
 
      return checkedRadioButton;

    } else {

      return false;

    }

  }

}
```

This one is the toughest one. This function, takes as argument an array of objects. These objects have 2 properties: the value of the radio button and a boolean indicating if the radio button is checked or not. In the body of the function, we initialize 2 variables. The checkedRadioButton stores the checked radio button. The moreThanOne is a boolean value which is true if there are more than 1 radio buttons checked. We iterate over the array using the some() function. The some() function works just like the forEach() function, but allows us to stop the iterations at any point. Imagine that we have 100 radio buttons and the first 2 are checked. By the second iteration we would know that the data are invalid, so the next 98 iterations would be pointless. With some() we can stop the iteration process by returning false at some stage. That’s what we do when we find out that more than 1 radio buttons are checked. Pretty damn cool! When the iteration ends, we check if there is a checked radio button and, of course, if it’s the only one. If it is we return that radio button. Otherwise, we return false. 

Overall, our codebase looks like this:

```javascript
var submit = document.querySelector('input[type=submit]');

submit.addEventListener('click', function(event) {

  event.preventDefault();

  var title = document.querySelector('#title').value;
  console.log('Title: ' + title);
  console.log('Is empty?: ' + isRequired(title));
  console.log('Is length appropriate?: ' + isLengthAppropriate(title));

  console.log('-----------------------');

  var body = document.querySelector('#body').value;
  console.log('Body: ' + body);
  console.log('Is empty?: ' + isRequired(body));

  console.log('-----------------------');

  var radioButtons = [];

  var vader = document.querySelector('#darthVader').checked;

  radioButtons.push({
    value: 0,
    checked: vader
  });

  var maul = document.querySelector('#darthMaul').checked;

  radioButtons.push({
    value: 1,
    checked: maul
  });

  var kylo = document.querySelector('#kyloRen').checked;

  radioButtons.push({
    value: 2,
    checked: kylo
  });
  console.log(isRadioButtonChecked(radioButtons));

  var urgent = document.querySelector('#urgent').checked;
  console.log(urgent);

});

function isRequired(value) {

  return value != null && value.trim() != '' ? true : false;

}

function isLengthAppropriate(value) {
 
  return value != null && value.length > 1 && value.length < 31 ? true : false;

}

function isRadioButtonChecked(radioButtons) {

  var checkedRadioButton = null;
  var moreThanOne = null;
  
  if (radioButtons != null) {
  
  
  radioButtons.some(function(radioButton) {

      if (radioButton.checked) {

        if (checkedRadioButton) {

          moreThanOne = true;
          return true;  

        } else {

          checkedRadioButton = radioButton;

        }

      }

    });

    if (checkedRadioButton && !moreThanOne) {
 
      return checkedRadioButton;

    } else {

      return false;

    }

  }

}
```

Play around with the form. Submit data and check the console to see if the data are valid or not. In the next tutorial, we will see how to print useful messages to the user about the data he provides and how to submit the form to an actual API. 

See you there!
