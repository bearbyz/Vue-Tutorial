# คำสั่ง Vue `v-if`

การสร้างองค์ประกอบ HTML นั้นง่ายกว่ามากโดยขึ้นอยู่กับเงื่อนไขใน Vue ด้วยคำสั่ง v-if มากกว่าการใช้ JavaScript ธรรมดา

ด้วย Vue คุณเพียงแค่เขียนคำสั่ง if-state โดยตรงในองค์ประกอบ HTML ที่คุณต้องการสร้างแบบมีเงื่อนไข มันง่ายมาก



##  การเรนเดอร์แบบมีเงื่อนไขใน Vue

**การเรนเดอร์แบบมีเงื่อนไข** ใน Vue ทำได้โดยใช้คำสั่ง v-if, v-else-if และ v-else

การแสดงผลแบบมีเงื่อนไขคือเมื่อมีการสร้างองค์ประกอบ HTML เฉพาะในกรณีที่เงื่อนไขเป็นจริง เช่น สร้างข้อความ "มีสินค้าในสต็อก" หากตัวแปรเป็น "**true**" หรือ "ไม่มีในสต็อก" หากตัวแปรนั้นเป็น "**false**"

### Example

เขียนข้อความที่แตกต่างกันขึ้นอยู่กับว่ามี อยู่ในสต็อกหรือไม่:

```html
<p v-if="typewritersInStock">
  in stock
</p>

<p v-else>
  not in stock
</p>
```



## เงื่อนไขใน Vue

เงื่อนไขหรือ "คำสั่ง if" คือสิ่งที่เป็น **true** หรือ **false**

เงื่อนไขมักจะเป็นการตรวจสอบเปรียบเทียบระหว่างสองค่าดังตัวอย่างด้านบนเพื่อดูว่าค่าหนึ่งมากกว่าอีกค่าหนึ่งหรือไม่

- เราใช้ **ตัวดำเนินการเปรียบเทียบ** เช่น <, >= หรือ !== เพื่อทำการตรวจสอบดังกล่าว
- การตรวจสอบเปรียบเทียบยังสามารถใช้ร่วมกับ **ตัวดำเนินการเชิงตรรกะ** เช่น && หรือ || ได้อีกด้วย
- ไปที่หน้าบทช่วยสอน JavaScript ของเราเพื่อดูข้อมูลเพิ่มเติมเกี่ยวกับการเปรียบเทียบ JavaScript

เราสามารถใช้จำนวนเครื่องพิมพ์ดีดในการจัดเก็บพร้อมการตรวจสอบเปรียบเทียบเพื่อตัดสินใจว่ามีอยู่ในสต็อกหรือไม่:

### Example

ใช้การตรวจสอบเปรียบเทียบเพื่อตัดสินใจว่าจะเขียนว่า "มีในสต็อก" หรือ "ไม่มีในสต็อก" ขึ้นอยู่กับจำนวนเครื่องพิมพ์ดีดในการจัดเก็บ 

```html
<p v-if="typewriterCount > 0">
  in stock
</p>

<p v-else>
  not in stock
</p>
```



## คำสั่งสำหรับการแสดงผลแบบมีเงื่อนไข

ภาพรวมนี้อธิบายวิธีการใช้คำสั่ง Vue ต่างๆ ที่ใช้สำหรับการแสดงผลแบบมีเงื่อนไขร่วมกัน

| **Directive** | **Details**                                                  |
| ------------- | ------------------------------------------------------------ |
| v-if          | สามารถใช้เดี่ยวๆ หรือใช้ร่วมกับ v-else-if และ/หรือ v-else หากเงื่อนไขภายใน v-if เป็น 'จริง' จะไม่พิจารณา v-else-if หรือ v-else |
| v-else-if     | ต้องใช้หลัง v-if หรือ v-else-if อื่น หากเงื่อนไขภายใน v-else-if เป็น 'จริง' จะไม่พิจารณา v-else-if หรือ v-else ที่ตามมา |
| v-else        | ส่วนนี้จะเกิดขึ้นหากส่วนแรกของคำสั่ง if เป็นเท็จ ต้องวางไว้ที่ส่วนท้ายสุดของคำสั่ง if หลังจาก v-if และ v-else-if |

หากต้องการดูตัวอย่างที่มีทั้งสามคำสั่งที่แสดงด้านบน เราสามารถขยายตัวอย่างก่อนหน้าด้วย v-else-if เพื่อให้ผู้ใช้เห็น 'มีสินค้าในสต็อก', 'เหลือน้อยมาก!' หรือ 'สินค้าหมด':

### Example

ใช้การตรวจสอบเปรียบเทียบเพื่อตัดสินใจว่าจะเขียนว่า "มีสินค้าในสต็อก" หรือ "เหลือน้อยมาก!" หรือ "ไม่มีในสต็อก" ขึ้นอยู่กับจำนวนเครื่องพิมพ์ดีดที่จัดเก็บ

```html
<p v-if="typewriterCount>3">
  In stock
</p>

<p v-else-if="typewriterCount>0">
  Very few left!
</p>

<p v-else>
  Not in stock
</p>
```



## ใช้ค่าที่ส่งคืนจากฟังก์ชัน

แทนที่จะใช้การตรวจสอบเปรียบเทียบกับคำสั่ง v-if เราสามารถใช้ค่าที่ส่งคืน 'true' หรือ 'false' จากฟังก์ชันได้:

### Example

หากข้อความใดมีคำว่า 'พิซซ่า' ให้สร้างแท็ก <p> พร้อมข้อความที่เหมาะสม วิธีการ 'includes()' เป็นวิธี JavaScript ดั้งเดิมที่ตรวจสอบว่าข้อความมีคำบางคำหรือไม่

```html
<div id="app">
  <p v-if="text.includes('pizza')">The text includes the word 'pizza'</p>
  <p v-else>The word 'pizza' is not found in the text</p>
</div>
```

```html
data() {
  return {
    text: 'I like taco, pizza, Thai beef salad, pho soup and tagine.'
  }
}
```

ตัวอย่างข้างต้นสามารถขยายได้เพื่อแสดงให้เห็นว่า v-if ยังสามารถสร้างแท็กอื่นๆ เช่น แท็ก <div> และ <img> ได้:

### Example

หากข้อความบางข้อความมีคำว่า 'pizza' ให้สร้างแท็ก <div> พร้อมรูปภาพพิซซ่า และแท็ก <p> พร้อมข้อความ วิธีการ 'includes()' เป็นวิธี JavaScript ดั้งเดิมที่ตรวจสอบว่าข้อความมีคำบางคำหรือไม่

```html
<div id="app">
  <div v-if="text.includes('pizza')">
    <p>The text includes the word 'pizza'</p>
    <img src="img_pizza.svg">
  </div>
  <p v-else>The word 'pizza' is not found in the text</p>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        text: 'I like taco, pizza, Thai beef salad, pho soup and tagine.'
      }
    }
  })
  app.mount('#app')
</script>
```

ด้านล่างมีการขยายตัวอย่างเพิ่มเติมอีก

### Example

หากข้อความบางข้อความมีคำว่า 'พิซซ่า' หรือ 'เบอร์ริโต' หรือไม่มีคำเหล่านี้เลย รูปภาพและข้อความที่แตกต่างกันจะถูกสร้างขึ้น

```html
<div id="app">
  <div v-if="text.includes('pizza')">
    <p>The text includes the word 'pizza'</p>
    <img src="img_pizza.svg">
  </div>
  <div v-else-if="text.includes('burrito')">
    <p>The text includes the word 'burrito', but not 'pizza'</p>
    <img src="img_burrito.svg">
  </div>
  <p v-else>The words 'pizza' or 'burrito' are not found in the text</p>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        text: 'I like taco, pizza, Thai beef salad, pho soup and tagine.'
      }
    }
  })
  app.mount('#app')
</script>
```

ด้วย Vue เราสามารถเขียนโค้ดที่สร้างองค์ประกอบภายใต้เงื่อนไขบางประการได้ง่ายกว่า JavaScript แบบเดิมมาก
