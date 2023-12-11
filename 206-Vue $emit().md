# Vue $emit() Method

ด้วยเมธอด $emit() ในตัวใน Vue เราสามารถสร้าง event ที่กำหนดเองในองค์ประกอบย่อยที่สามารถบันทึกในองค์ประกอบหลักได้

Props ใช้เพื่อส่งข้อมูลจากองค์ประกอบหลักไปยังองค์ประกอบย่อย และ $emit() ถูกใช้เพื่อทำสิ่งที่ตรงกันข้าม: เพื่อส่งข้อมูลจากองค์ประกอบย่อยไปยังองค์ประกอบหลัก



**วัตถุประสงค์**ของสิ่งที่เราจะทำต่อไปคือการสิ้นสุดด้วยสถานะ 'favorite' ของรายการอาหารที่จะเปลี่ยนแปลงใน App.vue หลัก แทนที่จะเป็นในองค์ประกอบย่อย FoodItem.vue ที่การเปลี่ยนแปลงกำลังเกิดขึ้นอยู่

**เหตุผล**ในการเปลี่ยนสถานะรายการโปรดใน App.vue แทนที่จะเป็น FoodItem.vue ก็คือ App.vue เป็นที่ที่สถานะรายการโปรดถูกจัดเก็บไว้ตั้งแต่แรก ดังนั้นจึงจำเป็นต้องอัปเดต ในโปรเจ็กต์ขนาดใหญ่ ข้อมูลอาจมาจากฐานข้อมูลที่เราเชื่อมต่อใน App.vue และเราต้องการให้การเปลี่ยนแปลงเกิดขึ้นจากส่วนประกอบเพื่อทำการเปลี่ยนแปลงในฐานข้อมูล ดังนั้นเราจึงจำเป็นต้องสื่อสารกลับไปยังพาเรนต์จากคอมโพเนนต์ลูก .



## Emit a Custom Event

มีความจำเป็นต้องส่งข้อมูลจากส่วนประกอบไปยังพาเรนต์ และเราใช้เมธอด $emit() ในตัวเพื่อดำเนินการดังกล่าว

เรามีเมธอด toggleFavorite ภายในส่วนประกอบ FoodItem.vue ที่ทำงานเมื่อมีการคลิกปุ่มสลับแล้ว ตอนนี้เรามาลบบรรทัดที่มีอยู่และเพิ่มบรรทัดเพื่อปล่อยเหตุการณ์ที่กำหนดเองของเรา 'toggle-favorite':

##### `FoodItem.vue`:

```js
methods: {
  toggleFavorite() {
    this.foodIsFavorite = !this.foodIsFavorite;
    this.$emit('toggle-Favorite');
  }
}
```

เราสามารถเลือกชื่อของเหตุการณ์ที่กำหนดเองได้ แต่เป็นเรื่องปกติที่จะใช้ kebab-case เพื่อ emit events



## Receive an Emit Event

ขณะนี้ emit event แบบกำหนดเอง 'toggle-favorite' ถูกปล่อยออกมาจากส่วนประกอบ FoodItem.vue แต่เราต้องฟัง event ในพาเรนต์ของ App.vue และเรียกใช้เมธอดที่ทำบางอย่างเพื่อให้เราเห็นว่า event นั้นเกิดขึ้น

เราฟังเหตุการณ์โดยใช้ shorthand @ แทน v-on: ใน App.vue โดยที่ส่วนประกอบถูกสร้างขึ้น:

### Example

ฟัง event 'toggle-favorite' ใน App.vue:

```html
<food-item
  v-for="x in foods"
  :key="x.name"
  :food-name="x.name"
  :food-desc="x.desc"
  :is-favorite="x.favorite"
  @toggle-favorite="receiveEmit"
/>
```

เมื่อ 'toggle-favorite'  event  แบบกำหนดเองของเราเกิดขึ้น เราจำเป็นต้องสร้างเมธอด 'testEmit' ใน App.vue เพื่อให้เราเห็นว่า event นั้นเกิดขึ้น:

```js
methods: {
  receiveEmit() {
    alert('Hello World!');
  }
}
```



## เปลี่ยนสถานะ 'favorite' ของรายการอาหารใน Parent

ตอนนี้เรามี event ที่แจ้งเตือน App.vue เมื่อมีการคลิกปุ่ม 'Favorite' จากองค์ประกอบย่อย

เราต้องการเปลี่ยนคุณสมบัติ 'รายการโปรด' ในอาร์เรย์ 'อาหาร' ใน App.vue สำหรับรายการอาหารที่ถูกต้องเมื่อมีการคลิกปุ่ม 'รายการโปรด' ในการทำเช่นนั้น เราจะส่งชื่อรายการอาหารจาก FoodItem.vue ไปยัง App.vue เนื่องจากชื่อนั้นไม่ซ้ำกันสำหรับรายการอาหารแต่ละรายการ:

##### `FoodItem.vue`:

```js
methods: {
  toggleFavorite() {
    this.$emit('toggle-favorite', this.foodName);
  }
}
```

ขณะนี้เราสามารถรับชื่อรายการอาหารใน App.vue เป็นอาร์กิวเมนต์ของวิธีการที่เรียกว่าเมื่อ 'toggle-favorite' event เกิดขึ้น เช่นนี้:

### Example

##### `App.vue`:

```js
methods: {
  receiveEmit(foodId) {  
    alert( 'You clicked: ' + foodId );
  }
}
```

ตอนนี้เรารู้แล้วว่ารายการอาหารใดที่ถูกคลิก เราสามารถอัปเดตสถานะ 'favorite' สำหรับรายการอาหารที่ถูกต้องภายในอาร์เรย์ 'foods' ได้:

##### `App.vue`:

```js
methods: {
  receiveEmit(foodId) {
    const foundFood = this.foods.find(
      food => food.name === foodId
    );
    foundFood.favorite = !foundFood.favorite;
  }
}
```

ในโค้ดด้านบน วิธีการอาร์เรย์ 'find' จะผ่านอาร์เรย์ 'foods' และค้นหาวัตถุที่มีคุณสมบัติชื่อเท่ากับรายการอาหารที่เราคลิก และส่งกลับวัตถุนั้นเป็น 'foundFood' หลังจากนั้นเราสามารถตั้งค่า 'foundFood.health' ให้ตรงข้ามกับที่เคยเป็นมา เพื่อที่มันจะสลับระหว่างจริงและเท็จ

xxxxxxxxxx <food-item  v-for="x in foods"  :key="x.name"  :food-name="x.name"  :food-desc="x.desc"  :is-favorite="x.favorite"/>html

เรียนรู้เพิ่มเติมเกี่ยวกับฟังก์ชันลูกศร JavaScript ที่นี่



อาหารที่ถูกต้องในอาร์เรย์ 'foods' จะได้รับการอัปเดตสถานะ 'favorite' แล้ว สิ่งเดียวที่เหลืออยู่คือการอัพเดตรูปภาพที่บ่งบอกถึงอาหารจานโปรด

เนื่องจากส่วนประกอบรายการอาหารถูกสร้างขึ้นแล้วด้วยสถานะ 'favorite' จากอาร์เรย์ 'foods' และส่งเป็นพร็อพ 'is-favorite' จาก App.vue เราเพียงแค่ต้องอ้างอิงถึงพร็อพ 'isFavorite' นี้ใน FoodItem.vue จาก v-show โดยที่องค์ประกอบ <img> ใช้เพื่ออัปเดตรูปภาพ:

```html
<img src="/img_quality.svg" v-show="isFavorite">
```

นอกจากนี้เรายังสามารถลบคุณสมบัติข้อมูล 'foodIsFavorite' ใน FoodItem.vue ได้เนื่องจากไม่ได้ใช้งานอีกต่อไป

### Example

ในโค้ดตัวอย่างสุดท้ายนี้ สถานะรายการโปรดของรายการอาหารสามารถสลับได้ในลักษณะเดียวกันกับเมื่อก่อน แต่ตอนนี้สถานะรายการโปรดได้รับการแก้ไขในตำแหน่งที่ถูกต้องภายใน App.vue

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <p>The toggle button on the component emits an event to the parent "App.vue". The favorite status is modified in "App.vue", and the updated status is sent back to the component so that the image is toggled to reflect the favorite status.</p>
  <p>The result looks exactly like before, but now the favorite staus is modified where it should be in "App.vue" instead of in the "FoodItem.vue" component.</p>
  <div id="wrapper">
    <food-item
      v-for="x in foods"
      :key="x.name"
      :food-name="x.name"
      :food-desc="x.desc"
      :is-favorite="x.favorite"
      @toggle-favorite="receiveEmit"/>
  </div> 
</template>

<script>
export default {
  data() { 
    return {
      foods: [
        { name: 'Apples', desc: 'Apples are a type of fruit that grow on trees.', favorite: true},
        { name: 'Pizza', desc: 'Pizza has a bread base with tomato sauce, cheese, and toppings on top.', favorite: false},
        { name: 'Rice', desc: 'Rice is a type of grain that people like to eat.', favorite: false},
        { name: 'Fish', desc: 'Fish is an animal that lives in water.', favorite: true},
        { name: 'Cake', desc: 'Cake is something sweet that tates good.', favorite: false}
      ]
    };
  },
  methods: {
    receiveEmit(foodId) {
      let foundFood = this.foods.find(
        food => food.name === foodId
      );
      foundFood.favorite = !foundFood.favorite;
    }
  }
}
</script>

<style>
  #wrapper {
    display: flex;
    flex-wrap: wrap;
  }
  #wrapper > div {
    border: dashed black 1px;
    flex-basis: 120px;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
</style>  
```

##### `FoodItem.vue`:

```html
<template>
    <div>
        <h2>
            {{ foodName }}
            <img src="/img_quality.svg" v-show="isFavorite">
        </h2>
        <p>{{ foodDesc }}</p>
        <button @click="toggleFavorite">Favorite</button>
    </div>
</template>

<script>
export default {
    props: ['foodName','foodDesc','isFavorite'],
    methods: {
        toggleFavorite() {
            this.$emit('toggle-favorite', this.foodName);
        }
    }
};
</script>

<style>
    img {
        height: 1.5em;
        float: right;
    }
</style>
```

##### `main.js`:

```jsx
import { createApp } from 'vue'

import App from './App.vue'
import FoodItem from './components/FoodItem.vue'

const app = createApp(App)

app.component('food-item', FoodItem)

app.mount('#app')
                
```



## The 'emits' Option

ในทำนองเดียวกับที่เราประกาศ props ภายในส่วนประกอบ FoodItem.vue เรายังสามารถบันทึกสิ่งที่ส่วนประกอบปล่อยออกมาได้โดยใช้ตัวเลือก Vue 'emits'

จะต้องประกาศ props ในส่วนประกอบ ในขณะที่แนะนำให้จัดทำเอกสารการปล่อยสัญญาณเท่านั้น

นี่คือวิธีที่เราสามารถบันทึกการปล่อยของเราในส่วนประกอบ FoodItem.vue:

```html
<script>
export default {  
  props: ['foodName','foodDesc','isFavorite'],
  emits: ['toggle-favorite'],
  methods: {
    toggleFavorite() {
      this.$emit('toggle-favorite', this.foodName);
    }
  }
};
</script>
```

คอมโพเนนต์จะง่ายขึ้นสำหรับผู้อื่นที่จะใช้เมื่อมีการ emits ได้รับการบันทึกไว้