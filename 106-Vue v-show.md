# คำสั่ง Vue `v-show`

เรียนรู้วิธีทำให้องค์ประกอบมองเห็นหรือไม่เห็นด้วย v-show

v-show ใช้งานง่ายเนื่องจากมีการเขียนเงื่อนไขลงในแอตทริบิวต์แท็ก HTML อย่างถูกต้อง



##  การมองเห็นแบบมีเงื่อนไข

คำสั่ง v-show ซ่อนองค์ประกอบเมื่อเงื่อนไขเป็น 'false' โดยการตั้งค่าคุณสมบัติ CSS 'แสดง' เป็น 'none'

หลังจากเขียน v-show เป็นแอตทริบิวต์ HTML แล้ว เราจะต้องกำหนดเงื่อนไขในการตัดสินใจว่าจะมองเห็นแท็กหรือไม่

### **Syntax**

```html
<div v-show="showDiv">This div tag can be hidden</div>
```

ในโค้ดด้านบน 'showDiv' แสดงถึงคุณสมบัติข้อมูลบูลีน Vue ที่มีค่าคุณสมบัติ 'true' หรือ 'false' หาก 'showDiv' เป็น 'true' แท็ก div จะปรากฏขึ้น และหากเป็น 'false' แท็กจะไม่แสดง

### Example

แสดงองค์ประกอบ <div> เฉพาะเมื่อคุณสมบัติ showDiv ถูกตั้งค่าเป็น 'true'

```html
<div id="app">
  <div v-show="showDiv">This div tag can be hidden</div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        showDiv: true
      }
    }
  })
  app.mount('#app')
</script>
```



## `v-show` vs. `v-if`

ความแตกต่างระหว่าง v-show และ v-if คือ v-if สร้าง (เรนเดอร์) องค์ประกอบขึ้นอยู่กับเงื่อนไข แต่ด้วย v-show องค์ประกอบนั้นถูกสร้างขึ้นแล้ว v-show จะเปลี่ยนการมองเห็นเท่านั้น

ดังนั้นจึงเป็นการดีกว่าที่จะใช้ v-show เมื่อเปลี่ยนการมองเห็นของวัตถุ เนื่องจากเบราว์เซอร์ทำได้ง่ายกว่า และอาจนำไปสู่การตอบสนองที่เร็วขึ้นและประสบการณ์ผู้ใช้ที่ดีขึ้น

เหตุผลในการใช้ v-if แทน v-show คือ v-if สามารถใช้กับ v-else-if และ v-else ได้

ในตัวอย่างด้านล่าง v-show และ v-if จะใช้แยกกันในองค์ประกอบ <div> ที่แตกต่างกันสององค์ประกอบ แต่ขึ้นอยู่กับคุณสมบัติ Vue เดียวกัน คุณสามารถเปิดตัวอย่างและตรวจสอบโค้ดเพื่อดูว่า v-show เก็บองค์ประกอบ <div> และตั้งค่าคุณสมบัติการแสดงผล CSS เป็น 'none' เท่านั้น แต่ v-if จะทำลายองค์ประกอบ <div> จริงๆ

### Example

แสดงสององค์ประกอบ <div> เฉพาะในกรณีที่คุณสมบัติ showDiv ถูกตั้งค่าเป็น 'true' หากคุณสมบัติ showDiv ถูกตั้งค่าเป็น 'false' และเราตรวจสอบหน้าตัวอย่างด้วยเบราว์เซอร์ เราจะเห็นว่าองค์ประกอบ <div> ที่มี v-if ถูกทำลาย แต่องค์ประกอบ <div> ที่มี v-show มีเพียงคุณสมบัติการแสดงผล CSS ตั้งค่าเป็น 'none'

```html
<div id="app">
  <div v-show="showDiv">Div tag with v-show</div>
  <div v-if="showDiv">Div tag with v-if</div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        showDiv: true
      }
    }
  })
  app.mount('#app')
</script>
```
