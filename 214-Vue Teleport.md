# Vue Teleport

แท็ก Vue <Teleport> ใช้เพื่อย้ายเนื้อหาไปยังตำแหน่งอื่นในโครงสร้าง DOM



## <Teleport> and The 'to' Attribute

ในการย้ายเนื้อหาบางส่วนไปยังตำแหน่งอื่นในโครงสร้าง DOM เราใช้แท็ก Vue <Teleport> รอบเนื้อหาและแอตทริบิวต์ 'to' เพื่อกำหนดตำแหน่งที่จะย้ายเนื้อหา

```html
<Teleport to="body">
  <p>Hello!</p>
</Teleport>
```

ค่าแอตทริบิวต์ 'to' ถูกกำหนดเป็นรูปแบบ CSS ดังนั้นหากเราต้องการส่งเนื้อหาบางส่วนไปยังแท็ก body เช่นเดียวกับในโค้ดด้านบน เราก็เพียงเขียน <Teleport to="body">

เราจะเห็นว่าเนื้อหาถูกย้ายไปยังแท็ก body โดยการตรวจสอบหน้าเว็บหลังจากโหลดแล้ว

### Example

##### `CompOne.vue`:

```html
<template>
  <div>
    <h2>Component</h2>
    <p>This is the inside of the component.</p>
    <Teleport to="body">
      <div id="redDiv">Hello!</div>
    </Teleport>
  </div>
</template>
```

If we right-click our page and choose 'Inspect', we can see that the red `<div>` element is moved out of the component and to the end of the `<body>` tag.

![img](https://www.w3schools.com/vue/img_teleport-DOM.png)

ตัวอย่างเช่น เราอาจมีแท็กที่มี id <div id="receivingDiv"> และเทเลพอร์ตเนื้อหาบางส่วนไปยัง <div> นั้นโดยใช้ <Teleport to="#receivingDiv"> รอบๆ เนื้อหาที่เราต้องการเทเลพอร์ต/ย้าย



## Script and Style of Teleported Elements

แม้ว่าเนื้อหาบางส่วนจะถูกย้ายออกจากส่วนประกอบด้วยแท็ก <Teleport> แต่โค้ดที่เกี่ยวข้องภายในส่วนประกอบในแท็ก <script> และ <style> ยังคงใช้งานได้สำหรับเนื้อหาที่ถูกย้าย

### Example

โค้ดที่เกี่ยวข้องจากแท็ก <style> และ <script> ยังคงใช้งานได้สำหรับแท็ก <div> ที่เคลื่อนย้ายได้ แม้ว่าจะไม่ได้อยู่ในส่วนประกอบอีกต่อไปหลังจากการคอมไพล์แล้ว

##### `CompOne.vue`:

```html
<template>
  <div>
    <h2>Component</h2>
    <p>This is the inside of the component.</p>
    <Teleport to="body">
      <div 
        id="redDiv" 
        @click="toggleVal = !toggleVal" 
        :style="{ backgroundColor: bgColor }"
      >
        Hello!<br>
        Click me!
      </div>
    </Teleport>
  </div>
</template>

<script>
export default {
  data() {
    return {
      toggleVal: true
    }
  },
  computed: {
    bgColor() {
      if (this.toggleVal) {
        return 'lightpink'
      }
      else {
        return 'lightgreen'
      }
    }
  }
}
</script>

<style scoped>
#redDiv {
  margin: 10px;
  padding: 10px;
  display: inline-block;
}

#redDiv:hover {
  cursor: pointer;
}
</style>
```