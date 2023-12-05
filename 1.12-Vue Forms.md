# Vue Forms

Vue ช่วยให้เราสามารถปรับปรุงประสบการณ์ผู้ใช้ด้วยแบบฟอร์มได้อย่างง่ายดายโดยการเพิ่มฟังก์ชันพิเศษ เช่น responsiveness และ form validation

Vue ใช้คำสั่ง v-model เมื่อจัดการแบบฟอร์ม



## แบบฟอร์มแรกของเรากับ Vue

เริ่มต้นด้วยตัวอย่างรายการช็อปปิ้งง่ายๆ เพื่อดูว่า Vue สามารถใช้เมื่อสร้างแบบฟอร์มได้อย่างไร

สำหรับข้อมูลเพิ่มเติมเกี่ยวกับแบบฟอร์มใน HTML พร้อมแท็กและแอตทริบิวต์ที่เกี่ยวข้อง โปรดดูบทช่วยสอนแบบฟอร์ม HTML ของเรา



##### 1. เพิ่ม  standard HTML form elements:

```html
<form>
  <p>Add item</p>
  <p>Item name: <input type="text" required></p>
  <p>How many: <input type="number"></p>
  <button type="submit">Add item</button>
</form>
```

##### 2. สร้างอินสแตนซ์ Vue ด้วยชื่อรายการปัจจุบัน หมายเลข และรายการช็อปปิ้ง และใช้ `v-model` เพื่อเชื่อมต่ออินพุตของเราเข้ากับมัน

```html
<div id="app">
  <form>
    <p>Add item</p>
    <p>Item name: <input type="text" required v-model="itemName"></p>
    <p>How many: <input type="number" v-model="itemNumber"></p>
    <button type="submit">Add item</button>
  </form>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        itemName: null,
        itemNumber: null,
        shoppingList: [
          { name: 'Tomatoes', number: 5 }
        ]
      }
    }
  })
  app.mount('#app')
</script>
```

##### 3. เรียกใช้วิธีการเพิ่มรายการลงในรายการช็อปปิ้ง และป้องกันการรีเฟรชเบราว์เซอร์เริ่มต้นเมื่อส่ง

```html
<form v-on:submit.prevent="addItem">
```

##### 4. สร้างวิธีการที่เพิ่มสินค้าลงในรายการช็อปปิ้ง และล้างแบบฟอร์ม:

```javascript
methods: {
  addItem() {
    let item = {
      name: this.itemName,
      number: this.itemNumber
      }
    this.shoppingList.push(item);
    this.itemName = null
    this.itemNumber = null
  }
}
```

##### 5. ใช้ v-for เพื่อแสดงรายการช้อปปิ้งที่อัปเดตอัตโนมัติด้านล่างแบบฟอร์ม:

```html
<p>Shopping list:</p>
<ul>
  <li v-for="item in shoppingList">{{item.name}}, {{item.number}}</li>
</ul>
```

ด้านล่างนี้เป็นโค้ดสุดท้ายสำหรับฟอร์ม Vue แรกของเรา

### Example

ในตัวอย่างนี้ เราสามารถเพิ่มสินค้าใหม่ลงในรายการช้อปปิ้งได้

```html
<div id="app">
  <form v-on:submit.prevent="addItem">
    <p>Add item</p>
    <p>Item name: <input type="text" required v-model="itemName"></p>
    <p>How many: <input type="number" v-model="itemNumber"></p>
    <button type="submit">Add item</button>
  </form>

  <p>Shopping list:</p>
  <ul>
    <li v-for="item in shoppingList">{{item.name}}, {{item.number}}</li>
  </ul>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        itemName: null,
        itemNumber: null,
        shoppingList: [
          { name: 'Tomatoes', number: 5 }
        ]
      }
    },
    methods: {
      addItem() {
        let item = {
          name: this.itemName,
          number: this.itemNumber
        }
        this.shoppingList.push(item)
        this.itemName = null
        this.itemNumber = null
      }
    }
  })
  app.mount('#app')
</script>
```

โปรดสังเกตว่า v-model การเชื่อมโยงแบบสองทางมีให้ในตัวอย่างด้านบน:

- v-model อัพเดตข้อมูลอินสแตนซ์ Vue เมื่ออินพุต HTML เปลี่ยนแปลง
- v-model ยังอัพเดตอินพุต HTML เมื่อข้อมูลอินสแตนซ์ Vue เปลี่ยนแปลง

หากต้องการเรียนรู้เพิ่มเติมเกี่ยวกับ v-model และดูตัวอย่างแบบฟอร์มเพิ่มเติม คลิก 'Next'