# Local Components

วิธีที่เรารวมคอมโพเนนต์ต่างๆ จนถึงตอนนี้ทำให้สามารถเข้าถึงได้จากไฟล์ *.vue ทั้งหมดในโปรเจ็กต์

คอมโพเนนต์สามารถทำให้เป็นแบบโลคัลได้ ซึ่งหมายความว่าสามารถเข้าถึงได้ภายในไฟล์ *.vue ที่ระบุเท่านั้น



## Global Components

วิธีที่เราได้รวมคอมโพเนนต์ต่างๆ ไว้ใน main.js ทำให้คอมโพเนนต์ต่างๆ สามารถเข้าถึงได้ภายใน <template> ของไฟล์ *.vue อื่นๆ ทั้งหมดในโปรเจ็กต์นั้น

### Example

เราใช้คอมโพเนนต์ CompOne.vue ภายในทั้ง CompTwo.vue และ App.vue เพื่อแสดงว่าส่วนประกอบต่างๆ สามารถเข้าถึงได้ซึ่งกันและกันด้วยการตั้งค่า main.js ในปัจจุบันของเรา

##### `main.js`:

```js
import { createApp } from 'vue'
 
import App from './App.vue'
import CompOne from './components/CompOne.vue'
import CompTwo from './components/CompTwo.vue'

const app = createApp(App)
app.component('comp-one', CompOne)
app.component('comp-two', CompTwo)
app.mount('#app')
```



## Local Components

เราสามารถรวมคอมโพเนนต์โดยตรงในแท็ก <script> ในไฟล์ *.vue แทนที่จะรวมไว้ใน main.js

หากเรารวมคอมโพเนนต์โดยตรงในไฟล์ *.vue คอมโพเนนต์นั้นจะสามารถเข้าถึงได้เฉพาะในไฟล์นั้นเท่านั้น

### Example

ในการทำให้ CompOne.vue เป็นแบบโลคัลเป็น App.vue และเข้าถึงได้จากที่นั่นเท่านั้น เราจะลบมันออกจาก main.js

##### `main.js`:

![image-20231207215316300](C:\Users\BEARBY\AppData\Roaming\Typora\typora-user-images\image-20231207215316300.png)

และรวม CompOne.vue โดยตรงในแท็ก <script> ของ App.vue แทน

##### `App.vue`:

```html
<template>
  <h3>Local Component</h3>
  <p>The CompOne.vue component is a local component and can only be used inside App.vue.</p>
  <comp-one />
  <comp-two />
</template>

<script> 
  import CompOne from './components/CompOne.vue';

  export default {
    components: {
      'comp-one': CompOne
    }
  }
</script>
```