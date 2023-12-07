# Vue Composition API

**Composition API** เป็นอีกวิธีหนึ่งในการเขียนแอปพลิเคชัน Vue ไปยัง Options API ที่ใช้ในที่อื่นในบทช่วยสอนนี้

ใน Composition API เราสามารถเขียนโค้ดได้อย่างอิสระมากขึ้น แต่ต้องใช้ความเข้าใจที่ลึกซึ้งยิ่งขึ้น และถือว่าเป็นมิตรกับผู้เริ่มต้นน้อยกว่า



## The Composition API

ด้วย Composition API ตรรกะจะถูกเขียนโดยใช้ฟังก์ชัน Vue ที่นำเข้า แทนที่จะใช้โครงสร้างอินสแตนซ์ Vue ที่เราคุ้นเคยจาก Options API

นี่คือวิธีที่ Composition API สามารถใช้เขียนแอปพลิเคชัน Vue ซึ่งจะลดจำนวนเครื่องพิมพ์ดีดในพื้นที่จัดเก็บด้วยปุ่ม:

### Example

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <img src="/img_typewriter.jpeg" alt="Typewriter">
  <p>Typewriters left in storage: {{ typeWriters }}</p>
  <button @click="remove">Remove one</button>
  <p style="font-style: italic;">"{{ storageComment }}"</p>
</template>

<script setup>
  import { ref, computed } from 'vue'

  const typeWriters = ref(10);

  function remove(){
    if(typeWriters.value>0){
      typeWriters.value--;
    }
  }

  const storageComment = computed(
    function(){
      if(typeWriters.value > 5) {
        return "Many left"
      }
      else if(typeWriters.value > 0){
        return "Very few left"
      }
      else {
        return "No typewriters left"
      }
    }
  )
</script>
```

**ในบรรทัดที่ 9** ในตัวอย่างด้านบน แอตทริบิวต์การตั้งค่าช่วยให้ใช้ Composition API ได้ง่ายขึ้น ตัวอย่างเช่น โดยใช้แอตทริบิวต์การตั้งค่า ตัวแปรและฟังก์ชันจะสามารถใช้ได้โดยตรงภายใน <เทมเพลต>

**ในบรรทัดที่ 10** ต้องนำเข้าการอ้างอิงและการคำนวณก่อนจึงจะสามารถใช้งานได้ ใน Options API เราไม่จำเป็นต้องนำเข้าสิ่งใดๆ เพื่อประกาศตัวแปรที่มีปฏิกิริยาหรือใช้คุณสมบัติที่คำนวณ

**ในบรรทัดที่ 12** การอ้างอิงใช้เพื่อประกาศคุณสมบัติ 'เครื่องพิมพ์ดีด' ว่ามีปฏิกิริยาโดยที่ '10' เป็นค่าเริ่มต้น

หากต้องการประกาศคุณสมบัติ 'เครื่องพิมพ์ดีด' เป็นแบบโต้ตอบ หมายความว่าบรรทัด {{ typewriters }} ใน <template> จะถูกสร้างขึ้นใหม่โดยอัตโนมัติเพื่อแสดงค่าที่อัปเดตเมื่อค่าคุณสมบัติ 'เครื่องพิมพ์ดีด' มีการเปลี่ยนแปลง ด้วย Option API คุณสมบัติข้อมูลจะกลายเป็นแบบโต้ตอบหากจำเป็นเมื่อสร้างแอปพลิเคชัน ไม่จำเป็นต้องประกาศอย่างชัดเจนว่าเป็นแบบโต้ตอบ

ฟังก์ชัน 'remove()' ที่ประกาศ**ในบรรทัด 14** จะถูกประกาศภายใต้ 'วิธีการ' ของคุณสมบัติ Vue หากตัวอย่างถูกเขียนใน Options API

คุณสมบัติที่คำนวณ 'storageComment' **ในบรรทัด 20** จะถูกประกาศภายใต้คุณสมบัติ Vue 'คำนวณ' หากตัวอย่างถูกเขียนใน Options API



## The Options API

Options API คือสิ่งที่ใช้ในที่อื่นๆ ในบทช่วยสอนนี้

Options API ถูกเลือกสำหรับบทช่วยสอนนี้เนื่องจากมีโครงสร้างที่จดจำได้และถือว่าเริ่มต้นได้ง่ายกว่าสำหรับผู้เริ่มต้น

ตามตัวอย่าง โครงสร้างใน Options API มีคุณสมบัติข้อมูล วิธีการ และคุณสมบัติที่คำนวณทั้งหมดวางไว้ในส่วนต่างๆ ของอินสแตนซ์ Vue โดยแยกออกจากกันอย่างชัดเจน

นี่คือตัวอย่างด้านบนที่เขียนด้วย Options API:

### Example

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <img src="/img_typewriter.jpeg" alt="Typewriter">
  <p>Typewriters left in storage: {{ typeWriters }}</p>
  <button @click="remove">Remove one</button>
  <p style="font-style: italic;">"{{ storageComment }}"</p>
</template>

<script>
export default {
  data() { 
    return {
      typeWriters: 10
    };
  },
  methods: {
    remove(){
      if(this.typeWriters>0){
        this.typeWriters--;
      }
    }
  },
  computed: {
    storageComment(){
      if(this.typeWriters > 5) {
        return "Many left"
      }
      else if(this.typeWriters > 0){
        return "Very few left"
      }
      else {
        return "No typewriters left"
      }
    }
  }
}
</script>
```