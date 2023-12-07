# คอมโพเนนต์วิว

ส่วนประกอบใน Vue ช่วยให้เราสามารถแบ่งหน้าเว็บของเราออกเป็นชิ้นเล็กๆ ซึ่งง่ายต่อการใช้งาน

เราสามารถทำงานกับคอมโพเนนต์ Vue โดยแยกจากส่วนที่เหลือของเว็บเพจ โดยมีเนื้อหาและตรรกะของตัวเอง

เว็บเพจมักประกอบด้วยคอมโพเนนต์ Vue มากมาย



## คอมโพเนนต์คืออะไร?

ส่วนประกอบต่างๆ เป็นโค้ดที่สามารถนำมาใช้ซ้ำได้และมีอยู่ในตัวเอง ซึ่งห่อหุ้มส่วนเฉพาะของอินเทอร์เฟซผู้ใช้ เพื่อให้เราสามารถสร้างแอปพลิเคชัน Vue ที่สามารถปรับขนาดได้และบำรุงรักษาได้ง่ายขึ้น

เราสามารถสร้างส่วนประกอบใน Vue ได้ด้วยตัวเอง หรือใช้ส่วนประกอบในตัวที่เราจะเรียนรู้ในภายหลัง เช่น <Teleport> หรือ <KeepAlive> ที่นี่เราจะเน้นไปที่ส่วนประกอบที่เราสร้างขึ้นเอง



## การสร้างคอมโพเนนต์

Components ใน Vue เป็นเครื่องมือที่ทรงพลังมากเพราะช่วยให้หน้าเว็บของเราสามารถปรับขนาดได้มากขึ้น และโครงการที่ใหญ่ขึ้นก็จัดการได้ง่ายขึ้น

มาสร้างส่วนประกอบและเพิ่มลงในโปรเจ็กต์ของเรากันดีกว่า

1. สร้างส่วนประกอบโฟลเดอร์ใหม่ภายในโฟลเดอร์ src

2. ภายในโฟลเดอร์ส่วนประกอบ ให้สร้างไฟล์ใหม่ FoodItem.vue เป็นเรื่องปกติที่จะตั้งชื่อส่วนประกอบต่างๆ ด้วยรูปแบบการตั้งชื่อ PascalCase โดยไม่ต้องเว้นวรรค และโดยที่คำใหม่ทั้งหมดขึ้นต้นด้วยตัวพิมพ์ใหญ่ จะเป็นคำแรกด้วย

3. ตรวจสอบให้แน่ใจว่าไฟล์ FoodItem.vue มีลักษณะดังนี้:



##### รหัสภายในองค์ประกอบ FoodItem.vue:

```html
<template>
  <div>
    <h2>{{ name }}</h2>
    <p>{{ message }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: 'Apples',
      message: 'I like apples'
    }
  }
};
</script>

<style></style>
```

ดังที่คุณเห็นในตัวอย่างด้านบน ส่วนประกอบยังประกอบด้วยแท็ก <template>, <script> และ <style> เช่นเดียวกับไฟล์ App.vue หลักของเรา



## การเพิ่มคอมโพเนนต์

โปรดสังเกตว่าแท็ก <script> ในตัวอย่างข้างต้นเริ่มต้นด้วยค่าเริ่มต้นในการส่งออก ซึ่งหมายความว่าสามารถรับหรือนำเข้าออบเจ็กต์ที่มีคุณสมบัติข้อมูลในไฟล์อื่นได้ เราจะใช้สิ่งนี้เพื่อนำคอมโพเนนต์ FoodItem.vue ไปใช้กับโปรเจ็กต์ที่มีอยู่ของเราโดยการนำเข้าด้วยไฟล์ main.js

ขั้นแรก ให้เขียนบรรทัดสุดท้ายใหม่เป็นสองบรรทัดในไฟล์ main.js ดั้งเดิมของคุณ:

##### `main.js`:

```jsx
import { createApp } from 'vue'

import App from './App.vue'

const app = createApp(App)
app.mount('#app')
```

ตอนนี้ เพิ่มคอมโพเนนต์ FoodItem.vue โดยการแทรกบรรทัด 4 และ 7 ลงในไฟล์ main.js ของคุณ:

##### `main.js`:

```jsx
import { createApp } from 'vue'

import App from './App.vue'
import FoodItem from './components/FoodItem.vue'

const app = createApp(App)
app.component('food-item', FoodItem)
app.mount('#app')
```

ในบรรทัดที่ 7 คอมโพเนนต์จะถูกเพิ่มเพื่อให้เราสามารถใช้เป็นแท็กที่กำหนดเอง <food-item/> ภายในแท็ก <template> ในไฟล์ App.vue ของเราดังนี้:

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <food-item/>
  <food-item/>
  <food-item/>
</template>

<script></script>

<style></style>
```

และมาเพิ่มสไตล์ภายในแท็ก <style> ในไฟล์ App.vue ตรวจสอบให้แน่ใจว่าเซิร์ฟเวอร์การพัฒนากำลังทำงานอยู่ และตรวจสอบผลลัพธ์

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <food-item/>
  <food-item/>
  <food-item/>
</template>

<script></script>

<style>
  #app > div {
    border: dashed black 1px;
    display: inline-block;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
</style>
```



โหมดการพัฒนา: เมื่อทำงานกับโปรเจ็กต์ Vue ของคุณ จะมีประโยชน์ที่จะให้โปรเจ็กต์ของคุณอยู่ในโหมดการพัฒนาเสมอโดยการรันบรรทัดโค้ดต่อไปนี้ในเทอร์มินัล:

```
npm run dev
```



##  คอมโพเนนต์ส่วนบุคคล

คุณสมบัติที่มีประโยชน์และทรงพลังมากเมื่อทำงานกับส่วนประกอบต่างๆ ใน Vue คือเราสามารถทำให้ส่วนประกอบเหล่านั้นทำงานเป็นรายบุคคล โดยไม่ต้องทำเครื่องหมายองค์ประกอบด้วย ID เฉพาะ เช่นเดียวกับที่เราต้องทำกับ JavaScript ธรรมดา Vue จะดูแลแต่ละองค์ประกอบแยกกันโดยอัตโนมัติ

มาทำให้องค์ประกอบ <div> นับเมื่อเราคลิกมัน

สิ่งเดียวที่เพิ่มลงในไฟล์แอปพลิเคชันหลักของเรา App.vue คือใน CSS เพื่อให้เคอร์เซอร์ดูเหมือนมือชี้ระหว่างวางเมาส์เหนือ เพื่อบอกเป็นนัยว่ามีฟังก์ชันการคลิกบางประเภท

##### CSS code added to the `<style>` tag in `App.vue`:

```css
#app > div:hover {
  cursor: pointer;
}
```

ในไฟล์ส่วนประกอบ FoodItem.vue เราต้องเพิ่มจำนวนคุณสมบัติข้อมูล ตัวฟังการคลิกให้กับองค์ประกอบ <div> วิธีการทำงานเมื่อมีการคลิกเกิดขึ้นเพื่อเพิ่มตัวนับ และการแก้ไขข้อความ {{}} เพื่อแสดงจำนวน

### Example

##### `FoodItem.vue`:

```html
<template>
  <div v-on:click="countClicks">
    <h2>{{ name }}</h2>  
    <p>{{ message }}</p>
    <p id="red">You have clicked me {{ clicks }} times.</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: 'Apples',
      message: 'I like apples',
      clicks: 0
    }
  },
  methods: {
    countClicks() {
      this.clicks++;
    }
  }
}
</script>

<style>
  #red {
    font-weight: bold ;
    color: rgb(144, 12, 12);
  }
</style>
```

เราไม่จำเป็นต้องกำหนด ID ที่ไม่ซ้ำกันหรือทำงานเพิ่มเติมใดๆ สำหรับ Vue เพื่อจัดการการนับแยกกันสำหรับแต่ละองค์ประกอบ <div> Vue จะทำสิ่งนี้โดยอัตโนมัติ

แต่ยกเว้นค่าตัวนับที่แตกต่างกัน เนื้อหาขององค์ประกอบ <div> ยังคงเหมือนเดิม ในหน้าถัดไป เราจะเรียนรู้เพิ่มเติมเกี่ยวกับส่วนประกอบเพื่อให้เราสามารถใช้ส่วนประกอบในลักษณะที่สมเหตุสมผลมากขึ้น ตัวอย่างเช่น การแสดงอาหารประเภทต่างๆ ในแต่ละองค์ประกอบ <div> จะเหมาะสมกว่า