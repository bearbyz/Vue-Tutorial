# Vue Computed Properties

**Computed properties** ก็เหมือนกับคุณสมบัติของข้อมูล ยกเว้นว่าจะขึ้นอยู่กับคุณสมบัติอื่นๆ

**Computed properties** นั้นเขียนเหมือนกับวิธีการ แต่ไม่ยอมรับอาร์กิวเมนต์อินพุตใดๆ

**Computed properties** จะได้รับการอัปเดตโดยอัตโนมัติเมื่อการขึ้นต่อกันเปลี่ยนแปลง ในขณะที่มีการเรียกใช้เมธอดเมื่อมีบางสิ่งเกิดขึ้น เช่น การจัดการเหตุการณ์ เป็นต้น

**Computed properties** จะใช้เมื่อส่งออกสิ่งที่ขึ้นอยู่กับสิ่งอื่น



## Computed Properties เป็นแบบไดนามิก

ข้อได้เปรียบที่สำคัญของ computed property คือเป็นแบบไดนามิก ซึ่งหมายความว่าคุณสมบัติดังกล่าวจะเปลี่ยนแปลงไปขึ้นอยู่กับตัวอย่างค่าของคุณสมบัติข้อมูลหนึ่งรายการขึ้นไป

  computed properties  เป็นตัวเลือกการกำหนดค่าที่สามในอินสแตนซ์ Vue ที่เราจะเรียนรู้ ตัวเลือกการกำหนดค่าสองตัวแรกที่เราได้ดูไปแล้วคือ 'data' และ 'methods'

เช่นเดียวกับ computed properties 'data' และ 'methods' ยังมีชื่อที่สงวนไว้ในอินสแตนซ์ Vue: 'computed'

### Syntax

```javascript
const app = Vue.createApp({
  data() {
    ...
  },
  computed: {
    ...
  },
  methods: {
    ...
  }
})
```



## Computed Property 'yes' or 'no'

สมมติว่าเราต้องการแบบฟอร์มเพื่อสร้างรายการในรายการช็อปปิ้ง และเราต้องการทำเครื่องหมายว่ารายการใหม่มีความสำคัญหรือไม่ เราสามารถเพิ่มความคิดเห็นที่ 'true' หรือ 'false' เมื่อช่องทำเครื่องหมายถูกทำเครื่องหมาย เหมือนกับที่เราเคยทำในตัวอย่างก่อนหน้านี้:

### Example

input element ถูกสร้างขึ้นแบบไดนามิกเพื่อให้ข้อความสะท้อนถึงสถานะ

```html
<input type="checkbox" v-model="chbxVal"> {{ chbxVal }}
```

```javascript
data() {
  return {
    chbxVal: false
  }
}
```

อย่างไรก็ตาม หากคุณถามใครสักคนว่ามีบางสิ่งที่สำคัญหรือไม่ พวกเขามักจะตอบว่า 'yes' หรือ 'no' แทนที่จะเป็น 'true' หรือ 'false' ดังนั้น เพื่อให้แบบฟอร์มของเราเหมาะสมกับภาษาปกติมากขึ้น (ใช้สัญชาตญาณมากขึ้น) เราควรมี 'yes' หรือ 'no' เป็นความคิดเห็นในช่องทำเครื่องหมาย แทนที่จะเป็น 'true' หรือ 'false'

ลองเดาดู  computed property แล้วเป็นเครื่องมือที่สมบูรณ์แบบที่ช่วยเราในเรื่องนั้น

### Example

ด้วย computed property แล้ว 'isImportant' เราสามารถปรับแต่งข้อความตอบกลับให้กับผู้ใช้ได้เมื่อเปิดหรือปิดช่องทำเครื่องหมาย

```html
<input type="checkbox" v-model="chbxVal"> {{ isImportant }}
```

```javascript
data() {
  return {
    chbxVal: false
  }
},
computed: {
  isImportant() {
    if(this.chbxVal){
      return 'yes'
    }
    else {
      return 'no'
  }
}
```



## Computed Properties vs. Methods

methods และ Computed properties ถูกเขียนเป็นฟังก์ชัน แต่จะต่างกัน:

Methods เมื่อมีการเรียกจาก HTML แต่ computed properties จะอัปเดตโดยอัตโนมัติเมื่อการเปลี่ยนแปลงการขึ้นต่อกัน
computed properties จะใช้ในลักษณะเดียวกับที่เราใช้ data properties แต่เป็นแบบไดนามิก