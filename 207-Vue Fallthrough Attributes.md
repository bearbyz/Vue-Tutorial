# Vue Fallthrough Attributes

สามารถเรียกคอมโพเนนต์ด้วยแอตทริบิวต์ที่ไม่ได้ประกาศเป็นอุปกรณ์ประกอบฉากได้ และคอมโพเนนต์เหล่านั้นก็จะ **fall through** ไปยังองค์ประกอบรูทในส่วนประกอบ

ด้วย **fallthrough attributes** คุณจะได้รับภาพรวมที่ดีขึ้นจากพาเรนต์ที่เป็นผู้สร้างส่วนประกอบ และทำให้โค้ดของเราง่ายขึ้นเนื่องจากเราไม่จำเป็นต้องประกาศแอตทริบิวต์เป็นอุปกรณ์ประกอบฉาก

คุณลักษณะทั่วไปที่ใช้คือ `class`, `style` และ v-on



## Fallthrough Attributes

อาจเป็นการดีที่จะยกตัวอย่างการควบคุมการจัดสไตล์ส่วนประกอบจากพาเรนต์ แทนที่จะซ่อนสไตล์ไว้ภายในส่วนประกอบ

มาสร้างตัวอย่างใหม่ รายการสิ่งที่ต้องทำพื้นฐานใน Vue และดูว่าแอตทริบิวต์ style เกี่ยวข้องกับส่วนประกอบที่แสดงถึงสิ่งที่ต้องทำอย่างไร

ดังนั้น App.vue ของเราควรมีรายการสิ่งที่ต้องทำ และองค์ประกอบ <input> และ <button> เพื่อเพิ่มสิ่งใหม่ๆ ที่ต้องทำ แต่ละรายการเป็นองค์ประกอบ <todo-item />

##### `App.vue`:

```html
<template>
  <h3>Todo List</h3>  
  <ul>
    <todo-item
      v-for="x in items"
      :key="x"
      :item-name="x"
    />
  </ul>
  <input v-model="newItem">
  <button @click="addItem">Add</button>
</template>

<script>
  export default {
    data() {
      return {
        newItem: '',
        items: ['Buy apples','Make pizza','Mow the lawn']
      };
    },
    methods: {
      addItem() {
        this.items.push(this.newItem),
        this.newItem = '';
      }
    }
  }
</script>
```

และ TodoItem.vue เพิ่งได้รับคำอธิบายว่าต้องทำอะไรเป็น prop:

##### `TodoItem.vue`:

```html
<template>
  <li>{{ itemName }}</li>
</template>

<script>
  export default {
    props: ['itemName']
  }
</script>
```

ในการสร้างแอปพลิเคชันของเราอย่างถูกต้อง เราจำเป็นต้องมีการตั้งค่าที่ถูกต้องใน main.js:

##### `main.js`:

```js
import { createApp } from 'vue'
  
import App from './App.vue'
import TodoItem from './components/TodoItem.vue'

const app = createApp(App)
app.component('todo-item', TodoItem)
app.mount('#app')
```

หากต้องการดูประเด็นของส่วนนี้ คุณสมบัตินั้นสามารถตกไปถึงองค์ประกอบรูทภายใน <template> ของส่วนประกอบของเรา เราสามารถกำหนดสไตล์ให้กับรายการรายการจาก App.vue:

### Example

เรากำหนดสไตล์ให้กับองค์ประกอบ <li> ภายในคอมโพเนนต์จาก App.vue:

```html
<template>
  <h3>Todo List</h3>
  <ul>
    <todo-item
      v-for="x in items"
      :key="x"
      :item-name="x"
      style="background-color: lightgreen;"
    />
  </ul>
  <input v-model="newItem">
  <button @click="addItem">Add</button>
</template>
```

เพื่อยืนยันว่าแอตทริบิวต์ style ล้มเหลวจริงๆ เราสามารถคลิกขวาที่องค์ประกอบ <li> ในรายการสิ่งที่ต้องทำของเราในเบราว์เซอร์ เลือก 'Inspect' และเราจะเห็นว่าแอตทริบิวต์ style อยู่ในองค์ประกอบ <li> แล้ว:

![img](https://www.w3schools.com/vue/img_li-fallthru.png)



## Merging 'class' and 'style' Attributes

หากแอตทริบิวต์ 'class' หรือ 'style' ได้รับการตั้งค่าไว้แล้ว และแอตทริบิวต์ 'class' หรือ 'style' ก็มาจากพาเรนต์เป็นแอตทริบิวต์ fallthrough แอตทริบิวต์ดังกล่าวจะถูกรวมเข้าด้วยกัน

### Example

นอกเหนือจากการออกแบบที่มีอยู่จากพาเรนต์แล้ว เรายังเพิ่มระยะขอบให้กับองค์ประกอบ <li> ภายในส่วนประกอบ TodoItem.vue:

```html
<template>
  <li style="margin: 5px 0;">{{ itemName }}</li>
</template>

<script>
  export default {
    props: ['itemName']
  }
</script>
```

หากเราคลิกขวาที่องค์ประกอบ <li> ในเบราว์เซอร์ เราจะเห็นว่าแอตทริบิวต์ถูกรวมเข้าด้วยกัน Margin ถูกตั้งค่าโดยตรงบนองค์ประกอบ <li> ภายในคอมโพเนนต์ และถูกรวมเข้ากับสีพื้นหลังที่ตกมาจากพาเรนต์:

![img](https://www.w3schools.com/vue/img_li-fallthru-merge.png)



## $attrs

หากเรามีมากกว่าหนึ่งองค์ประกอบในระดับรูทขององค์ประกอบ ก็จะไม่ชัดเจนว่าองค์ประกอบใดที่แอตทริบิวต์ควร fall through

เพื่อกำหนดว่าองค์ประกอบรูทใดได้รับคุณลักษณะ Fallthrough เราสามารถทำเครื่องหมายองค์ประกอบด้วยวัตถุ $attrs ในตัวได้ เช่นนี้

### Example

##### `TodoItem.vue`:

```html
<template>
  <div class="pinkBall"></div>
  <li v-bind="$attrs">{{ itemName }}</li>
  <div class="pinkBall"></div>
</template>
```