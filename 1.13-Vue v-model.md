# คำสั่ง Vue v-model

เมื่อเปรียบเทียบกับ JavaScript ปกติ จะทำงานกับแบบฟอร์มใน Vue ได้ง่ายกว่าเนื่องจากคำสั่ง v-model เชื่อมต่อกับองค์ประกอบอินพุตทุกประเภทในลักษณะเดียวกัน

v-model สร้างการเชื่อมโยงระหว่างแอตทริบิวต์ค่าองค์ประกอบอินพุตและค่าข้อมูลในอินสแตนซ์ Vue เมื่อคุณเปลี่ยนอินพุต ข้อมูลจะอัปเดต และเมื่อข้อมูลเปลี่ยนแปลง อินพุตจะอัปเดตเช่นกัน (two-way binding)



## Two-way Binding

ดังที่เราได้เห็นแล้วในตัวอย่างรายการช็อปปิ้งในหน้าก่อน v-model ให้การเชื่อมโยงแบบสองทางแก่เรา ซึ่งหมายความว่าองค์ประกอบอินพุตของฟอร์มจะอัปเดตอินสแตนซ์ข้อมูล Vue และการเปลี่ยนแปลงในข้อมูลอินสแตนซ์ Vue จะอัปเดตอินพุต .

ตัวอย่างด้านล่างยังแสดงให้เห็นถึงการเชื่อมโยงแบบสองทางกับ v-model

### Example

การเชื่อมโยงสองทาง: ลองเขียนภายในฟิลด์อินพุตเพื่อดูว่าค่าคุณสมบัติข้อมูล Vue ได้รับการอัพเดต ลองเขียนโค้ดโดยตรงเพื่อเปลี่ยนค่าคุณสมบัติข้อมูล Vue รันโค้ด และดูว่าฟิลด์อินพุตได้รับการอัปเดตอย่างไร

```html
<div id="app">
  <input type="text" v-model="inpText">
  <p> {{ inpText }} </p>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        inpText: 'Initial text'
      }
    }
  })
  app.mount('#app')
</script>
```



หมายเหตุ: ฟังก์ชันการรวมสองทางของ v-model สามารถทำได้จริงด้วยการรวมกันของ v-bind:value และ v-on:input:

- v-bind:value เพื่ออัปเดตองค์ประกอบอินพุตจากข้อมูลอินสแตนซ์ Vue
- และ v-on:input เพื่ออัพเดตข้อมูลอินสแตนซ์ Vue จากอินพุต

แต่ v-model นั้นใช้งานง่ายกว่ามาก นั่นคือสิ่งที่เราจะทำ



## A Dynamic Checkbox

เราเพิ่มช่องทำเครื่องหมายในรายการช็อปปิ้งของเราในหน้าก่อนหน้าเพื่อทำเครื่องหมายว่ารายการนั้นมีความสำคัญหรือไม่

ถัดจากช่องทำเครื่องหมาย เราจะเพิ่มข้อความที่แสดงถึงสถานะ 'important' ในปัจจุบัน โดยจะเปลี่ยนแบบไดนามิกระหว่าง 'true' หรือ 'false'

เราใช้ v-model เพื่อเพิ่มช่องทำเครื่องหมายและข้อความแบบไดนามิกเพื่อปรับปรุงการโต้ตอบของผู้ใช้

พวกเราต้องการ:

- ค่าบูลีนในคุณสมบัติข้อมูลอินสแตนซ์ Vue ที่เรียกว่า 'important'
- ช่องทำเครื่องหมายที่ผู้ใช้สามารถตรวจสอบว่ารายการนั้นมีความสำคัญหรือไม่
- ข้อความตอบรับแบบไดนามิกเพื่อให้ผู้ใช้สามารถดูว่ารายการนั้นมีความสำคัญหรือไม่

ด้านล่างนี้คือลักษณะของฟีเจอร์ 'important' ซึ่งแยกออกจากรายการช็อปปิ้ง

### Example

ข้อความในช่องทำเครื่องหมายถูกสร้างขึ้นแบบไดนามิกเพื่อให้ข้อความสะท้อนถึงค่าอินพุตช่องทำเครื่องหมายปัจจุบัน

```html
<div id="app">
  <form>
    <p>
      Important item?
      <label>
        <input type="checkbox" v-model="important">
        {{ important }}
      </label>
    </p>
  </form>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
       important: false
      }
    }
  })
  app.mount('#app')
</script>
```

มารวมคุณลักษณะแบบไดนามิกนี้ไว้ในตัวอย่างรายการช็อปปิ้งของเรา

### Example

```html
<div id="app">
  <form v-on:submit.prevent="addItem">
    <p>Add item</p>
    <p>Item name: <input type="text" required v-model="itemName"></p>
    <p>How many: <input type="number" v-model="itemNumber"></p>
    <p>
      Important?
      <label>
        <input type="checkbox" v-model="itemImportant">
        {{ important }}
      </label>
    </p>
    <button type="submit">Add item</button>
  </form>
  <hr>
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
        important: false,
        shoppingList: [
          { name: 'Tomatoes', number: 5, important: false }
        ]
      }
    },
    methods: {
      addItem() {
        let item = {
          name: this.itemName,
          number: this.itemNumber
          important: this.itemImportant
        }
        this.shoppingList.push(item)
        this.itemName = null
        this.itemNumber = null
        this.itemImportant = false
      }
    }
  })
  app.mount('#app')
</script>
```



## ทำเครื่องหมายพบสินค้าในรายการช็อปปิ้ง

มาเพิ่มฟังก์ชันการทำงานเพื่อให้สามารถทำเครื่องหมายรายการที่เพิ่มลงในรายการช้อปปิ้งว่าพบแล้ว

พวกเราต้องการ:

- รายการที่จะตอบสนองเมื่อคลิก

- เพื่อเปลี่ยนสถานะของรายการที่ถูกคลิกเป็น 'found' และใช้สิ่งนี้เพื่อย้ายรายการออกไปด้วยสายตาและขีดทับด้วย CSS

เราสร้างหนึ่งรายการที่มีรายการทั้งหมดที่เราจำเป็นต้องค้นหา และอีกหนึ่งรายการด้านล่างที่มีรายการที่พบขีดทับ จริงๆ แล้วเราสามารถวางรายการทั้งหมดไว้ในรายการแรก และรายการทั้งหมดในรายการที่สอง และใช้ v-show กับคุณสมบัติข้อมูล Vue 'found' เพื่อกำหนดว่าจะแสดงรายการในรายการแรกหรือรายการที่สอง

### Example

หลังจากเพิ่มสินค้าลงในรายการช้อปปิ้งแล้ว เราก็สามารถแกล้งทำเป็นไปช้อปปิ้งได้โดยคลิกสินค้าออกไปหลังจากค้นหาแล้ว หากเราคลิกรายการใดรายการหนึ่งโดยไม่ได้ตั้งใจ เราจะสามารถนำรายการนั้นกลับไปยังรายการ 'not found' ได้โดยการคลิกรายการนั้นอีกครั้ง

```html
<div id="app">
  <form v-on:submit.prevent="addItem">
    <p>Add item</p>
    <p>Item name: <input type="text" required v-model="itemName"></p>
    <p>How many: <input type="number" v-model="itemNumber"></p>
    <p>
      Important?
      <label>
        <input type="checkbox" v-model="itemImportant">
        {{ important }}
      </label>
    </p>
    <button type="submit">Add item</button>
  </form>

  <p><strong>Shopping list:</strong></p>
  <ul id="ulToFind">
    <li v-for="item in shoppingList"
        v-bind:class="{ impClass: item.important }"
        v-on:click="item.found=!item.found"
        v-show="!item.found">
          {{ item.name }}, {{ item.number}}
    </li>
  </ul>
  <ul id="ulFound">
    <li v-for="item in shoppingList"
        v-bind:class="{ impClass: item.important }"
        v-on:click="item.found=!item.found"
        v-show="item.found">
          {{ item.name }}, {{ item.number}}
    </li>
  </ul>

</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        itemName: null,
        itemNumber: null,
        important: false,
        shoppingList: [
          { name: 'Tomatoes', number: 5, important: false, found: false }
        ]
      }
    },
    methods: {
      addItem() {
        let item = {
          name: this.itemName,
          number: this.itemNumber,
          important: this.itemImportant,
          found: false
        }
        this.shoppingList.push(item)
        this.itemName = null
        this.itemNumber = null
        this.itemImportant = false
      }
    }
  })
  app.mount('#app')
</script>
```



## ใช้ v-model เพื่อทำให้ฟอร์มเป็นไดนามิก

เราสามารถสร้างแบบฟอร์มที่ลูกค้าสั่งจากเมนูได้ เพื่อให้ง่ายแก่ลูกค้าเราจึงนำเสนอเฉพาะเครื่องดื่มให้เลือกหลังจากที่ลูกค้าเลือกสั่งเครื่องดื่มแล้วเท่านั้น เรียกได้ว่าดีกว่าการนำเสนอลูกค้าด้วยรายการอาหารทั้งหมดในคราวเดียว ในตัวอย่างนี้ เราใช้ v-model และ v-show เพื่อทำให้ฟอร์มเป็นไดนามิก

พวกเราต้องการ:

- แบบฟอร์มพร้อมแท็กอินพุตที่เกี่ยวข้องและปุ่ม 'Order'
- ปุ่มตัวเลือกเพื่อเลือก 'Dinner', 'Drink' หรือ 'Dessert'
- หลังจากเลือกหมวดหมู่แล้ว dropdown menu จะปรากฏขึ้นพร้อมกับรายการทั้งหมดในหมวดหมู่นั้น
- เมื่อเลือกสินค้าแล้วคุณจะเห็นรูปภาพ คุณสามารถเลือกจำนวนและเพิ่มลงในคำสั่งซื้อได้ แบบฟอร์มจะถูกรีเซ็ตเมื่อมีการเพิ่มสินค้าลงในคำสั่งซื้อ

### Example

แบบฟอร์มนี้เป็นแบบไดนามิก มันเปลี่ยนแปลงตามตัวเลือกของผู้ใช้ ผู้ใช้จะต้องเลือกหมวดหมู่ก่อน จากนั้นเลือกผลิตภัณฑ์และจำนวน ก่อนที่จะมองเห็นปุ่มสั่งซื้อและผู้ใช้สามารถสั่งซื้อได้

```html
<!DOCTYPE html>
<html>
<head>
  <title>Restaurant Order</title>
  <style>
    #app {
      border: dashed black 1px;
      display: inline-block;
      padding: 0 20px;
    }
    #app label, #app li {
      padding: 5px;
      border-radius: 5px;
    }
    #app input[type=radio] {
      margin: 8px;
    }
    #app label:hover {
      cursor: pointer;
      background-color: lightgray;
    }
    ul {
      list-style-type: none;
    }
    li {
      margin: 2px;
      width: 17ch;
      height: 35px;
      line-height: 35px;
      text-align: center;
      background-color: rgb(211, 254, 211);
    }
    .impClass {
      background-color: rgb(255, 202, 202);
    }
    #ulFound li {
      text-decoration: line-through;
      background-color: rgb(230,230,230);
    }
    form img {
      width: 50px;
    }
    li img {
      float: right;
      height: 100%;
    }
    h4 {
      margin: 0;
    }
  </style>
</head>
<body>

<h1>Example: Restaurant Order</h1>
<p>Here the user can order food and drinks from a menu. To limit the amount of choices in the drop-down list, the user first filter by chosing between 'Dinner', 'Drink' or 'Dessert'.</p>
<div id="app">
  <form v-on:submit.prevent="addItem">
    <p>
      <h4>Order here:</h4>
    <label>
      <input type="radio" required value="Dinner" v-model="itemType" name="rbgType">Dinner
    </label><br>
    <label>
      <input type="radio" required value="Drink" v-model="itemType" name="rbgType">Drink
    </label><br>
    <label>
      <input type="radio" required value="Dessert" v-model="itemType" name="rbgType">Dessert
    </label>
    </p>
    <p v-show="itemType">
      <label>
        <select required v-model="itemName" v-on:change="newUrl">
          <option value="" selected disabled>Select item</option>
          <option v-for="item in preDefItems" v-bind:value="item.name" v-show="item.type===itemType" v-bind:data-url="item.imgUrl">
            {{ item.name }}
          </option>
        </select>
      </label>
    </p>
    <img v-bind:src="itemUrl">
    <p v-show="itemName">
      <input type="number" placeholder="How many?" v-model="itemNumber" required>
    </p>
    <button type="submit">Order</button>
  </form>
  <br>
  <hr>

  <div>
    <h4>Your order:</h4>
    <ul id="ulToFind">
      <li v-for="item in order">
          {{ item.name }}, {{ item.number}} <img v-bind:src="item.url">
      </li>
    </ul>

    </ul>
  </div>
</div>


<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        itemType: '',
        itemName: '',
        itemUrl: '',
        itemNumber: null,
        preDefItems: [
          { name: 'Burrito', type: 'Dinner', imgUrl: 'img_burrito.svg' },
          { name: 'Pizza', type: 'Dinner', imgUrl: 'img_pizza.svg' },
          { name: 'Pho Soup', type: 'Dinner', imgUrl: 'img_soup.svg' },
          { name: 'Spaghetti', type: 'Dinner', imgUrl: 'img_spaghetti.svg' },
          { name: 'Fish', type: 'Dinner', imgUrl: 'img_fish.svg' },
          { name: 'Cake', type: 'Dessert', imgUrl: 'img_cake.svg' },
          { name: 'Rice', type: 'Dinner', imgUrl: 'img_rice.svg' },
          { name: 'Salad', type: 'Dinner', imgUrl: 'img_salad.svg' },
          { name: 'Coke', type: 'Drink', imgUrl: 'img_soda.svg' },
          { name: 'Green Soda', type: 'Drink', imgUrl: 'img_greenSoda.svg' },
          { name: 'Doughnut', type: 'Dessert', imgUrl: 'img_doughnut.svg' },
          { name: 'Ice Cream', type: 'Dessert', imgUrl: 'img_iceCream.svg' },
          { name: 'Lemonade', type: 'Drink', imgUrl: 'img_lemonade.svg' },
          { name: 'Pancakes', type: 'Dessert', imgUrl: 'img_pancakes.svg' },
          { name: 'Water', type: 'Drink', imgUrl: 'img_water.svg' }
        ],
        order: []
      }
    },
    methods: {
      addItem(){
        let item = {
          name: this.itemName,
          number: this.itemNumber,
          url: this.itemUrl
        }
        this.order.push(item)
        this.itemType = ''
        this.itemName = ''
        this.itemNumber = null  
        this.itemUrl = ''
      },
      newUrl(e) {
        this.itemUrl = e.target.options[e.target.selectedIndex].getAttribute("data-url")
      }
    }
  })
 app.mount('#app')
</script>

</body>
</html>
```

