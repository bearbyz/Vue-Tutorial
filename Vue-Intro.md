# Vue Introduction

Vue is a **JavaScript framework**. It can be added to an HTML page with a <script> tag.

Vue extends HTML attributes with **Directives**, and binds data to HTML with **Expressions**.

## Vue is a JavaScript Framework

Vue is a front-end JavaScript framework written in JavaScript.

Similar frameworks to Vue are React and Angular, but Vue is more lightweight and easier to start with.

Vue is distributed as a JavaScript file, and can be added to a web page with a script tag:

```html
<script
  src="https://unpkg.com/vue@3/dist/vue.global.js">
</script>
```

## Why Learn Vue?

- It is simple and easy to use.
- It is able to handle both simple and complex projects.
- Its growing popularity and open-source community support.
- In normal JavaScript we need to write **HOW** HTML and JavaScript is connected, but in Vue we simply need to make sure that there **IS** a connection and let Vue take care of the rest.
- It allows for a more efficient development process with a template-based syntax, two-way data binding, and a centralized state management.

If some of these points are hard to understand, don't worry, you will understand at the end of the tutorial.

## The Options API

There are two different ways to write code in Vue: The Options API and The Composition API.

The underlying concepts are the same for both the Options API and Composition API, so after learning one, you can easily switch to the other.

The Options API is what is written in this tutorial because it is considered to be more beginner-friendly, with a more recognizable structure.

Take a look at [this page](https://www.w3schools.com/vue/vue_composition-api.php) at the end of this tutorial to learn more about the differences between the Options API and the Composition API.



## My first page

We will now learn how we can create our very first Vue web page, in 5 basic steps:

1. Start with a basic HTML file.
2. Add a `<div>` tag with `id="app"` for Vue to connect with.
3. Tell the browser how to handle Vue code by adding a `<script>` tag with a link to Vue.
4. Add a `<script>` tag with the Vue instance inside.
5. Connect the Vue instance to the `<div id="app">` tag.

These steps are described in detail below, with the full code in a 'Try It Yourself' example in the end.

### Step 1: HTML page

Start with a simple HTML page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My first Vue page</title>
</head>
<body>

</body>
</html>
```

### Step 2: Add a <div>

Vue needs an HTML element on your page to connect to.

Put a `<div>` tag inside the `<body>` tag and give it an id:

```html
<body>
  <div id="app"></div>
</body>
```

### tep 3: Add a link to Vue

To help our browser to interpret our Vue code, add this `<script>` tag:

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```



------

### Step 4: Add the Vue instance

Now we need to add our Vue code.

This is called the **Vue instance** and can contain data and methods and other things, but now it just contains a message.

On the last line in this `<script>` tag our Vue instance is connected to the `<div id="app">` tag:

```html
<div id="app"></div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<script>

  const app = Vue.createApp({
    data() {
      return {
        message: "Hello World!"
      }
    }
  })

 app.mount('#app')

</script>
```



------

### Step 5: Display 'message' with Text Interpolation

Finally, we can use **text interpolation**, a Vue syntax with double curly braces `{{ }}` as a placeholder for data.

```html
<div id="app"> {{ message }} </div>
```

The browser will exchange `{{ message }}` with the text stored in the 'message' property inside the Vue instance.

Here is our very first Vue page:



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My first Vue page</title>
</head>
<body>

  <div id="app">
    {{ message }}
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <script>
    const app = Vue.createApp({
      data() {
        return {
          message: "Hello World!"
        }
      }
    })

   app.mount('#app')

  </script>
</body>
</html>
```

## Text Interpolation

Text interpolation is when text is taken from the Vue instance to show on the web page.

The browser receives the page with this code inside:

```html
<div id="app"> {{ message }} </div>
```

Then the browser finds the text inside the 'message' property of the Vue instance and translates the Vue code into this:

```html
<div id="app">Hello World!</div>
```

## JavaScript in Text Interpolation

Simple **JavaScript expressions** can also be written inside the double curly braces `{{ }}`.

```html
<div id="app">
  {{ message }} <br>
  {{'Random number: ' + Math.ceil(Math.random()*6) }}
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<script>

  const app = Vue.createApp({
    data() {
      return {
        message: "Hello World!"
      }
    }
  })

 app.mount('#app')

</script>
```

