
# HTML & CSS Crash Course

## Basic HTML Structure and Elements and Attributes, Classes and IDs

- Elements, Tags, Attributes, Classes, IDs
- In HTML, some Elements can have attributes. These attributes describe elements.
- For example, consider the following anchor element. **<a href="https://github.com/subhadeep">My Github</a>**. Here href is an attribute of the <a> tag because it defines the link to which the anchor element should point to.
- An **<a>** is also known as an inline element because the text contained within the **<a>** tags are displayed in-line. Contrast this with something like the **<p>** tag where the text is displayed on a different line. Such an element is known as a Block Element.
- Similarly you have the **<img src="https://github.com/subhadeep" alt="">** element. An **img** element does not have a closing tag.
- There are two attributes that we can use on ALL elements. These are class and id. These attributes are used to name the HTML elements so that we can style them using CSS. We also use them to select elements from JS when we are doing DOM Manipulation.
- The difference between classes and ids is that ids are supposed to be unique. That is, you can only use an id ONCE, on a page.
- A **<div>** element is used to draw a box on the HTML page.
- A **<form>** element is used to accept input from the user. **<form>** is just a **<div>** that has been given some semantic meaning to explain to HTML that we intend to take an input from the user.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <link href="style.css" rel="stylesheet" />

    <title>Learning HTML & CSS</title>
  </head>
  <body>
    <h1>JavaScript is fun, but so is HTML & CSS!</h1>
    <p class="first">
      You can learn JavaScript without HTML and CSS, but for DOM manipulation
      it's useful to have some basic ideas of HTML & CSS. You can learn more
      about it
      <a href="https://www.udemy.com/user/jonasschmedtmann/">on Udemy</a>.
    </p>

    <h2>Another heading</h2>
    <p class="second">
      Just another paragraph
    </p>

    <img
      id="course-image"
      src="https://img-a.udemycdn.com/course/480x270/437398_46c3_9.jpg"
    />

    <form id="your-name">
      <h2>Your name here</h2>
      <p class="first">Please fill in this form :)</p>

      <input type="text" placeholder="Your name" />
      <button>OK!</button>
    </form>
  </body>
</html>
```


## Basic Styling with CSS & Introduction to the CSS Box Model

 - According to the box model in CSS, each and every element on a web page can be seen as a rectangular box.
 

## Screenshots

![BoxModel](https://github.com/subhadeeppaul/JavaScript-Notes/blob/main/Images/BoxModel.png)
  
- The CSS file corresponding to the HTML in the section above:
  
  ```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: rgb(255, 247, 201);
  font-family: Arial;
  font-size: 20px;
  padding: 50px;
}

h1 {
  font-size: 35px;
  margin-bottom: 25px;
}

h2 {
  margin-bottom: 20px;
  text-align: center;
}

p {
  margin-bottom: 20px;
}

.first {
  color: red;
}

##your-name {
  background-color: rgb(255, 220, 105);
  border: 5px solid ##444;
  width: 400px;
  padding: 25px;
  margin-top: 30px;
}

input,
button {
  padding: 10px;
  font-size: 16px;
}

a {
  background-color: yellowgreen;
}

##course-image {
  width: 300px;
}

##your-name h2 {
  color: olivedrab;
}
```

