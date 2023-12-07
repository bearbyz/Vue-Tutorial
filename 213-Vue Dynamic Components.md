# Dynamic Components

คอมโพเนนต์แบบไดนามิกสามารถใช้เพื่อพลิกดูหน้าเว็บต่างๆ ภายในหน้าเว็บของคุณได้ เช่น แท็บในเบราว์เซอร์ โดยใช้แอตทริบิวต์ 'is'



## The Component Tag and The 'is' Attribute

ในการสร้างคอมโพเนนต์แบบไดนามิก เราใช้แท็ก <component> เพื่อแสดงคอมโพเนนต์ที่ใช้งานอยู่ แอตทริบิวต์ 'is' เชื่อมโยงกับค่าที่มี v-bind และเราเปลี่ยนค่านั้นเป็นชื่อของคอมโพเนนต์ที่เราต้องการให้ใช้งานอยู่

### Example

ในตัวอย่างนี้ เรามีแท็ก <component> ที่ทำหน้าที่เป็นตัวยึดตำแหน่งสำหรับคอมโพเนนต์ comp-one หรือคอมโพเนนต์ comp-two แอตทริบิวต์ 'is' ถูกตั้งค่าบนแท็ก <component> และฟังค่าที่คำนวณได้ 'activeComp' ที่เก็บ 'comp-one' หรือ 'comp-two' เป็นค่า และเรามีปุ่มที่สลับคุณสมบัติข้อมูลระหว่าง 'จริง' และ 'เท็จ' เพื่อให้ค่าที่คำนวณได้สลับระหว่างส่วนประกอบที่ใช้งานอยู่

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <p>App.vue switches between which component to show.</p>
  <button @click="toggleValue = !toggleValue">
    Switch component
  </button>
  <component :is="activeComp"></component>
</template>

<script>
  export default {
    data() {
      return {
        toggleValue: true
      }
    },
    computed: {
      activeComp() {
        if(this.toggleValue) {
          return 'comp-one'
        }
        else {
          return 'comp-two'
        }
      }
    }
  }
</script>
```



## **<KeepAlive>**

เรียกใช้ตัวอย่างด้านล่าง คุณจะสังเกตเห็นว่าการเปลี่ยนแปลงที่คุณทำในส่วนประกอบหนึ่งจะถูกลืมเมื่อคุณเปลี่ยนกลับไปใช้คอมโพเนนต์นั้น นั่นเป็นเพราะว่าคอมโพเนนต์ถูกถอดออกและติดตั้งอีกครั้ง โดยจะโหลดส่วนประกอบใหม่

### Example

ตัวอย่างนี้เหมือนกับตัวอย่างก่อนหน้า ยกเว้นคอมโพเนนต์จะแตกต่างกัน ใน comp-one คุณสามารถเลือกระหว่าง 'Apple' และ 'Cake' และใน comp-two คุณสามารถเขียนข้อความได้ อินพุตของคุณจะหายไปเมื่อคุณกลับไปที่คอมโพเนนต์

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <p>App.vue switches between which component to show.</p>
  <button @click="toggleValue = !toggleValue">Switch component</button>
  <component :is="activeComp"></component>
</template>

<script>
  export default {
    data () {
      return {
        toggleValue: true
      }
    },
    computed: {
      activeComp() {
        if(this.toggleValue) {
          return 'comp-one'
        }
        else {
          return 'comp-two'
        }
      }
    }
  }
</script>

<style>
  #app {
    width: 350px;
    margin: 10px;
  }
  #app > div {
    border: solid black 2px;
    padding: 10px;
    margin-top: 10px;
  }
  h2 {
    text-decoration: underline;
  }
</style>         
```

##### `CompOne.vue`:

```html
<template>
    <div>
        <img :src="imgSrc">
        <h2>Component One</h2>
        <p>Choose food.</p>
        <label>
            <input type="radio" name="rbgFood" 
            v-model="imgSrc" :value="'img_apple.svg'" /> 
            Apple
        </label>
        <label>
            <input type="radio" name="rbgFood" 
            v-model="imgSrc" :value="'img_cake.svg'" /> 
            Cake
        </label>
    </div>
</template>

<script>
  export default {
    data () {
      return {
        imgSrc: 'img_question.svg'
      }
    }
  }
</script>

<style scoped>
    div {
        background-color: lightgreen;
    }
    img {
        float: right;
        height: 100px;
        margin-top: 20px;
    }
    label:hover {
        cursor: pointer;
    }
</style>                  
```

##### `CompTwo.vue`:

```html
<template>
    <div>
        <h2>Component Two</h2>
        <input type="text" v-model="msg" placeholder="Write something...">
        <p>Your message:</p>
        <p><strong>{{ this.msg }}</strong></p>
    </div>
</template>

<script>
  export default {
    data () {
      return {
        msg: ''
      }
    }
  }
</script>

<style scoped>
    div {
        background-color: lightpink;
    }
    strong {
      background-color: yellow;
      padding: 5px;
    }
</style>                  
```

##### `main.js`:

```jsx
import { createApp } from 'vue'

import App from './App.vue'
import CompOne from './components/CompOne.vue'
import CompTwo from './components/CompTwo.vue'

const app = createApp(App)
app.component('comp-one', CompOne)
app.component('comp-two', CompTwo)
app.mount('#app')
                  
```

เพื่อรักษาสถานะซึ่งเป็นอินพุตก่อนหน้าของคุณ เมื่อกลับไปยังคอมโพเนนต์ เราใช้แท็ก <KeepAlive> รอบๆ แท็ก <component>

### Example

ตอนนี้ส่วนประกอบต่างๆ จดจำอินพุตของผู้ใช้แล้ว

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <p>App.vue switches between which component to show.</p>
  <button @click="toggleValue = !toggleValue">
    Switch component
  </button>
  <KeepAlive>
    <component :is="activeComp"></component>
  </KeepAlive>
</template>
```



## The 'include' and 'exclude' Attributes

คอมโพเนนต์ทั้งหมดภายในแท็ก <KeepAlive> จะถูกเก็บไว้ตามค่าเริ่มต้น

แต่เรายังสามารถกำหนดคอมโพเนนต์บางส่วนเท่านั้นที่จะเก็บไว้ได้โดยใช้แอตทริบิวต์ 'include' หรือ 'exclude' บนแท็ก <KeepAlive>

หากเราใช้แอตทริบิวต์ 'include' หรือ 'exclude' ในแท็ก <KeepAlive> เรายังจำเป็นต้องตั้งชื่อคอมโพเนนต์ด้วยตัวเลือก 'name':

##### `CompOne.vue`:

```html
<script>
  export default {
    name: 'CompOne',
    data() {
      return {
        imgSrc: 'img_question.svg'
      }
    }
  }
</script>
```

### Example

ด้วย <KeepAlive include="CompOne"> เฉพาะคอมโพเนนต์ 'CompOne' เท่านั้นที่จะจดจำสถานะซึ่งเป็นอินพุตก่อนหน้า

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <p>App.vue switches between which component to show.</p>
  <button @click="toggleValue = !toggleValue">
    Switch component
  </button>
  <KeepAlive include="CompOne">
    <component :is="activeComp"></component>
  </KeepAlive>
</template>
```

นอกจากนี้เรายังสามารถใช้ 'exclude' เพื่อเลือกคอมโพเนนต์ที่จะคงอยู่หรือไม่ก็ได้

### Example

ด้วย <KeepAliveไม่รวม="CompOne"> เฉพาะคอมโพเนนต์ 'CompTwo' เท่านั้นที่จะจดจำสถานะของมัน

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <p>App.vue switches between which component to show.</p>
  <button @click="toggleValue = !toggleValue">
    Switch component
  </button>
  <KeepAlive exclude="CompOne">
    <component :is="activeComp"></component>
  </KeepAlive>
</template>
```

ทั้ง 'include' และ 'exclude' สามารถใช้กับองค์ประกอบหลายรายการได้โดยใช้การแยกเครื่องหมายจุลภาค

เพื่อแสดงให้เห็นสิ่งนี้ เราจะเพิ่มส่วนประกอบอีกหนึ่งชิ้นเพื่อรวมส่วนประกอบทั้งหมดสามชิ้น

### Example

ด้วย <KeepAlive include="CompOne, CompThree"> ทั้งคอมโพเนนต์ 'CompOne' และ 'CompThree' จะจดจำสถานะของพวกเขา

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <button @click="compNbr++">
    Next component
  </button>
  <KeepAlive include="CompOne,CompThree">
    <component :is="activeComp"></component>
  </KeepAlive>
</template>
```



## The 'max' Attribute

เราสามารถใช้ 'max' เป็นแอตทริบิวต์ของแท็ก <KeepAlive> เพื่อจำกัดจำนวนคอมโพเนนต์ที่เบราว์เซอร์จำเป็นต้องจดจำสถานะของ

### Example

ด้วย <KeepAlive :max="2"> เบราว์เซอร์จะจดจำเฉพาะการป้อนข้อมูลของผู้ใช้ของคอมโพเนนต์ที่เยี่ยมชมสองรายการล่าสุดเท่านั้น

##### `App.vue`:

```html
<template>
  <h1>Dynamic Components</h1>
  <label><input type="radio" name="rbgComp" v-model="compName" :value="'comp-one'"> One</label>
  <label><input type="radio" name="rbgComp" v-model="compName" :value="'comp-two'"> Two</label>
  <label><input type="radio" name="rbgComp" v-model="compName" :value="'comp-three'"> Three</label>
  <KeepAlive :max="2">
    <component :is="activeComp"></component>
  </KeepAlive>
</template>
```