# Vue Routing

**Routing** ใน Vue ใช้เพื่อนำทางแอปพลิเคชัน Vue และเกิดขึ้นบนฝั่งไคลเอ็นต์ (ในเบราว์เซอร์) โดยไม่ต้องโหลดหน้าเต็ม ซึ่งส่งผลให้ประสบการณ์ผู้ใช้เร็วขึ้น

**Routing** เป็นวิธีการนำทาง คล้ายกับวิธีที่เราใช้ส่วนประกอบแบบไดนามิกก่อนหน้านี้

ด้วย **Routing** เราสามารถใช้ที่อยู่ URL เพื่อนำผู้อื่นไปยังสถานที่เฉพาะในแอปพลิเคชัน Vue ของเรา



## Navigate Using a Dynamic Component

เพื่อทำความเข้าใจการกำหนดเส้นทางใน Vue ก่อนอื่นเรามาดูที่แอปพลิเคชันที่ใช้ส่วนประกอบแบบไดนามิกเพื่อสลับระหว่างสองส่วนประกอบ

เราสามารถสลับระหว่างส่วนประกอบต่างๆ ได้โดยใช้ปุ่ม:

### Example

##### `FoodItems.vue`:

```html
<template>
    <h1>Food!</h1>
    <p>I like most types of food.</p>
</template>
```

##### `AnimalCollection.vue`:

```html
<template>
    <h1>Animals!</h1>
    <p>I want to learn about at least one new animal every year.</p>
</template>
```

##### `App.vue`:

```html
<template>
  <p>Choose what part of this page you want to see:</p>
  <button @click="activeComp = 'animal-collection'">Animals</button>
  <button @click="activeComp = 'food-items'">Food</button><br>
  <div>
    <component :is="activeComp"></component>
  </div>
</template>

<script>
export default {
  data() {
      return {
        activeComp: ''
      }
    }
}
</script>

<style scoped>
  button {
    padding: 5px;
    margin: 10px;
  }
  div {
    border: dashed black 1px;
    padding: 20px;
    margin: 10px;
    display: inline-block;
  }
</style>
```



## From Dynamic Component to Routing

เราสร้าง SPAs (แอปพลิเคชันหน้าเดียว) ด้วย Vue ซึ่งหมายความว่าแอปพลิเคชันของเรามีไฟล์ *.html เพียงไฟล์เดียวเท่านั้น และนั่นหมายความว่าเราไม่สามารถนำผู้อื่นไปยังไฟล์ *.html อื่นเพื่อแสดงเนื้อหาที่แตกต่างกันบนเพจของเราได้

ในตัวอย่างด้านบน เราสามารถนำทางไปมาระหว่างเนื้อหาต่างๆ บนเพจได้ แต่เราไม่สามารถให้ที่อยู่ของเพจแก่ผู้อื่น เพื่อให้พวกเขามาที่ส่วนเกี่ยวกับอาหารได้โดยตรง แต่ด้วยการกำหนดเส้นทางที่เราสามารถทำได้

ด้วยการตั้งค่าการกำหนดเส้นทางอย่างเหมาะสม หากคุณเปิดแอปพลิเคชัน Vue ที่มีส่วนขยายไปยังที่อยู่ URL เช่น "/food-items" คุณจะมาถึงส่วนที่มีเนื้อหาอาหารโดยตรง



## Install The Vue Router Library

หากต้องการใช้การกำหนดเส้นทางใน Vue บนเครื่องของคุณ ให้ติดตั้งไลบรารี Vue Router ในโฟลเดอร์โปรเจ็กต์ของคุณโดยใช้เทอร์มินัล:

```
npm install vue-router@4
```



### Update main.js

หากต้องการใช้การกำหนดเส้นทาง เราจะต้องสร้างเราเตอร์ และเราทำสิ่งนั้นในไฟล์ main.js

##### `main.js`:

```js
import { createApp } from 'vue'
import { createRouter, createWebHistory } from 'vue-router'

import App from './App.vue'
import FoodItems from './components/FoodItems.vue'
import AnimalCollection from './components/AnimalCollection.vue'

const router = createRouter({
    history: createWebHistory(),
    routes: [
        { path: '/animals', component: AnimalCollection },
        { path: '/food', component: FoodItems },
    ]
});

const app = createApp(App)

app.use(router);
app.component('food-items', FoodItems);
app.component('animal-collection', AnimalCollection);

app.mount('#app')
```

มีการเพิ่มบรรทัดที่ 2, 8-14 และ 18 เพื่อเพิ่มฟังก์ชันการทำงานของเราเตอร์

บรรทัดที่ 19-20 จะถูกลบออกเนื่องจากส่วนประกอบต่างๆ ได้รับการรวมไว้แล้วผ่านทางเราเตอร์ในบรรทัดที่ 11-12



ตอนนี้เราได้สร้างเราเตอร์ที่สามารถเปิดส่วนประกอบ 'AnimalCollection' ได้หากมีการเพิ่ม '/animals' ต่อท้ายที่อยู่ URL เดิม แต่จะไม่ทำงานจนกว่าจะถึงส่วนถัดไปเมื่อเราเพิ่ม <router-view > ส่วนประกอบ เราเตอร์ยังติดตามประวัติเว็บเพื่อให้คุณสามารถย้อนกลับและส่งต่อในประวัติโดยมักจะอยู่ที่มุมซ้ายบนในเว็บเบราว์เซอร์ถัดจาก URL



### Use The <router-view> Component

หากต้องการเปลี่ยนเนื้อหาบนเพจของเราด้วยเราเตอร์ใหม่ เราจำเป็นต้องลบส่วนประกอบไดนามิกในตัวอย่างก่อนหน้านี้ และใช้ส่วนประกอบ <router-view> แทน

##### `App.vue`:

```html
<template>
  <p>Choose what part of this page you want to see:</p>
  <button @click="activeComp = 'animal-collection'">Animals</button>
  <button @click="activeComp = 'food-items'">Food</button><br>
  <div>
    <router-view></router-view>
    <component :is="activeComp"></component>
  </div>
</template>
```

หากคุณได้ทำการเปลี่ยนแปลงข้างต้นบนคอมพิวเตอร์ของคุณ คุณสามารถเพิ่ม '/food' ลงในที่อยู่ URL ของหน้าโครงการของคุณในเบราว์เซอร์ได้ และหน้าควรอัปเดตเพื่อแสดงเนื้อหาอาหาร เช่นนี้

![img](https://www.w3schools.com/vue/img_screenshot_router.png)

### Use The <router-link> Component

เราสามารถแทนที่ปุ่มต่างๆ ด้วยส่วนประกอบ <router-link> ได้เนื่องจากจะทำงานได้ดีกับเราเตอร์

เราไม่จำเป็นต้องใช้คุณสมบัติข้อมูล 'activeComp' อีกต่อไป ดังนั้นเราจึงสามารถลบมันได้ และเราสามารถลบแท็ก <script> ทั้งหมดได้จริง ๆ เพราะมันว่างเปล่า

##### `App.vue`:

![image-20231208000641005](C:\Users\BEARBY\AppData\Roaming\Typora\typora-user-images\image-20231208000641005.png)



### Style to The <router-link> Component

องค์ประกอบ <router-link> แสดงผลเป็นแท็ก <a> เราจะเห็นได้ว่าหากเราคลิกขวาที่องค์ประกอบในเบราว์เซอร์และตรวจสอบ:

![img](https://www.w3schools.com/vue/img_router-link-render.png)

ดังที่คุณเห็นในภาพหน้าจอด้านบน Vue ยังคอยติดตามว่าส่วนประกอบใดที่ใช้งานอยู่ และจัดเตรียมคลาส 'router-link-active' ให้กับส่วนประกอบ <router-link> ที่ใช้งานอยู่ (ซึ่งตอนนี้แสดงผลเป็น <a > แท็ก)

เราสามารถใช้ข้อมูลด้านบนเพื่อกำหนดสไตล์เพื่อเน้นว่าส่วนประกอบ <router-link> ใดที่ใช้งานอยู่:

### Example

##### `App.vue`:

```html
<template>
  <p>Choose what part of this page you want to see:</p>
  <router-link to="/animals">Animals</router-link>
  <router-link to="/food">Food</router-link><br>
  <div>
    <router-view></router-view>
  </div>
</template>

<style scoped>
  a {
    display: inline-block;
    background-color: black;
    border: solid 1px black;
    color: white;
    padding: 5px;
    margin: 10px;
  }
  a:hover,
  a.router-link-active {
    background-color: rgb(110, 79, 13);
  }
  div {
    border: dashed black 1px;
    padding: 20px;
    margin: 10px;
    display: inline-block;
  }
</style>
```

หมายเหตุ: ในตัวอย่างข้างต้น ที่อยู่ URL จะไม่อัปเดต แต่ถ้าคุณดำเนินการนี้ในเครื่องของคุณเอง ที่อยู่ URL จะได้รับการอัปเดต ตัวอย่างด้านบนใช้งานได้แม้ว่าจะไม่ได้อัปเดตที่อยู่ URL เนื่องจากเราเตอร์ใน Vue ดูแลเส้นทางภายใน