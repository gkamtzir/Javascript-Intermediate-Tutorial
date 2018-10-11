Hello and welcome to another Javascript tutorial. In the last 5 tutorials, we learned about the DOM and how to work with it. Although, these tutorials had many code samples, they were not so practical. The code snippets were used just to demonstrate how a particular utility worked. Nothing more. In the next 4 tutorials, we will get our hands on a much more practical project. We are going to design a task assigning form. The user, in our case the admin only, will be able to assign tasks to a particular user. A task consist of the following:

*title: The title of the task 
*body: Additional information about the task 
*userID: The assignee’s ID 
*urgent: A boolean value indicating if the task is urgent or not

When we’re finished, a user will be able to fill the corresponding fields and submit the form to a fake API which is called 'JSON: Placeholder' and can be found here. Without further ado, let’s begin! 

In this first tutorial, we will take a closer look at the HTML input elements we need. 

For the title field, we need a text input. This input will have an ID of 'title' and a placeholder with the value of 'Enter task’s title'. We can also restrict the length of that field to maximum 30 characters. To, visually, complete the title field, we have to add a label too.

```html
<div class="form-group">
  <label for="title">Title:</label>
  <input type="text" id="title" maxLength="30" placeholder="Enter task's title"/>
</div>
```

For the body field, we will use a textarea input. Its ID will be 'body'.

```html
<div class="form-group">
  <label for="body">Body:</label>
  <textarea id="body">
  </textarea>
</div>
```

For the userID, we can use some radio buttons. Our users will be predefined and, as we mentioned above, only one user can be assigned to a task. The users are 3 and have IDs from 0 to 2.

```html
<div class="form-group">
  <input type="radio" id="darthVader" name="user" value="0" checked> Darth Vader
  <br />
  <input type="radio" id="darthMaul" name="user" value="1"> Darth Maul
  <br />
  <input type="radio" id="kyloRen" name="user" value="2"> Kylo Ren
</div>
```

For the urgent field, we can use a simple checkbox, just like below: 

```html
<div class="form-group">
  <input type="checkbox" id="urgent" name="urgent" /> Urgent?
</div>
```

Last but not least, we are going to need a submit button. 

```html
<input type="submit" value="Submit" />
```

Don’t forget to include everything we wrote, so far, inside a form element. The final HTML code will look something like this:

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

  </body>

</html>
```

Notice that I added some CSS rules just to make it more appealing, although our goal is not to create a beautiful UI. The CSS file is shown below:

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

That was it people! Our HTML code is ready. In the next tutorial we will see how to fetch the value of each element. 

See you soon.