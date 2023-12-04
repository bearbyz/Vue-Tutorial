# Vue Directives

Vue directives are special HTML attributes with the prefix `v-` that give the HTML tag extra functionality.

Vue directives connect to the Vue instance to create dynamic and reactive user interfaces.

With Vue, creating responsive pages is much easier and requires less code compared to traditional JavaScript methods.

## Different Vue Directives

The different Vue directives we use in this tutorial are listed below.

| **Directive**                                          | **Details**                                                  |
| ------------------------------------------------------ | ------------------------------------------------------------ |
| [v-bind](https://www.w3schools.com/vue/vue_v-bind.php) | Connects an attribute in an HTML tag to a data variable inside the Vue instance. |
|                                                        |                                                              |
|                                                        |                                                              |
|                                                        |                                                              |
|                                                        |                                                              |
|                                                        |                                                              |

### Example: The `v-bind` Directive

The browser finds what class to connect the <div> element to from the Vue instance.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .pinkBG {
      background-color: lightpink;
    }
  </style>
</head>
<body>

  <div id="app">
    <div v-bind:class="vueClass"></div>
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          vueClass: "pinkBG"
        }
      }
    })
    app.mount('#app')
  </script>
</body>
</html>
```

