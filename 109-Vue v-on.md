# คำสั่ง Vue `v-on`

เช่นเดียวกับการ event handling ใน JavaScript ธรรมดา คำสั่ง v-on ใน Vue จะบอกเบราว์เซอร์:

1. event ใดที่จะฟัง ('คลิก', 'keydown', 'mouseover' ฯลฯ )
2. จะทำอย่างไรเมื่อมี event นั้นเกิดขึ้น



## ตัวอย่างการใช้ `v-on`

ลองมาดูตัวอย่างบางส่วนเพื่อดูว่า v-on สามารถใช้กับ event ต่างๆ ได้อย่างไร และโค้ดต่างๆ ในการทำงานเมื่อ event เหล่านี้เกิดขึ้น

หมายเหตุ: หากต้องการรันโค้ดขั้นสูงเมื่อมี event เกิดขึ้น เราจำเป็นต้องแนะนำ Vue methods เรียนรู้เกี่ยวกับVue methods ในหน้าถัดไปในบทช่วยสอนนี้



## onclick Event

คำสั่ง v-on ช่วยให้เราสามารถดำเนินการตาม event ที่ระบุได้

ใช้ v-on:click เพื่อดำเนินการเมื่อมีการคลิกองค์ประกอบ

### Example

คำสั่ง v-on ใช้กับแท็ก <button> เพื่อฟัง event  'click' เมื่อ event  'click' เกิดขึ้น คุณสมบัติข้อมูล 'lightOn' จะถูกสลับระหว่าง 'true' และ 'false' ทำให้ <div> สีเหลืองด้านหลังหลอดไฟมองเห็น/ซ่อนได้

```html
<div id="app">
  <div id="lightDiv">
    <div v-show="lightOn"></div>
    <img src="img_lightBulb.svg">
  </div>
  <button v-on:click="lightOn = !lightOn">Switch light</button>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        lightOn: false
      }
    }
  })
  app.mount('#app')
</script>
```



## oninput Event

ใช้ v-on:input เพื่อดำเนินการเมื่อองค์ประกอบได้รับอินพุต เช่น การกดแป้นพิมพ์ภายในช่องข้อความ

### Example

นับจำนวนการกดแป้นพิมพ์สำหรับช่องข้อความอินพุต:

```html
<div id="app">
  <input v-on:input="inpCount++">
  <p>{{ 'Input events occured: ' + inpCount }}</p>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        inpCount: 0
      }
    }
  })
  app.mount('#app')
</script>
```



## mousemove Event

ใช้ v-on:mousemove เพื่อดำเนินการเมื่อตัวชี้เมาส์เลื่อนไปเหนือองค์ประกอบ

### Example

เปลี่ยนสีพื้นหลังของ <div> องค์ประกอบเมื่อใดก็ตามที่ตัวชี้เมาส์เลื่อนไป:

```html
<div id="app">
  <p>Move the mouse pointer over the box below</p>
  <div v-on:mousemove="colorVal=Math.floor(Math.random()*360)"
       v-bind:style="{backgroundColor:'hsl('+colorVal+',80%,80%)'}">
  </div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        colorVal: 50
      }
    }
  })
  app.mount('#app')
</script>
```



## ใช้ v-on ใน v-for Loop

คุณยังสามารถใช้คำสั่ง v-on ภายใน v-for loop ได้

รายการของอาร์เรย์พร้อมใช้งานสำหรับการวนซ้ำแต่ละครั้งภายในค่า v-on

### Example

แสดงรายการตามอาร์เรย์อาหาร และเพิ่ม event การคลิกสำหรับแต่ละรายการซึ่งจะใช้ค่าจากรายการอาร์เรย์เพื่อเปลี่ยนแหล่งที่มาของรูปภาพ

```html
<div id="app">
  <img v-bind:src="imgUrl">
  <ol>
    <li v-for="food in manyFoods" v-on:click="imgUrl=food.url">
      {{ food.name }}
    </li>
  </ol>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        imgUrl: 'img_salad.svg',
        manyFoods: [
          {name: 'Burrito', url: 'img_burrito.svg'},
          {name: 'Salad', url: 'img_salad.svg'},
          {name: 'Cake', url: 'img_cake.svg'},
          {name: 'Soup', url: 'img_soup.svg'}
        ]
      }
    }
  })
  app.mount('#app')
</script>
```



## อักษรย่อของ `v-on`

ตัวย่อของ 'v-on' คือ '@'

### Example

ที่นี่เราแค่เขียน '@' แทน 'v-on':

```html
<button @:click="lightOn = !lightOn">Switch light</button>
```

เราจะเริ่มใช้ไวยากรณ์ @ ในภายหลังเล็กน้อยในบทช่วยสอนนี้
