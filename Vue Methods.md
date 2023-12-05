# เมธอด Vue

เมธอด Vue คือฟังก์ชันที่เป็นของอินสแตนซ์ Vue ภายใต้คุณสมบัติ 'methods'

เมธอด Vue เหมาะที่จะใช้กับการจัดการเหตุการณ์ (v-on) เพื่อทำสิ่งที่ซับซ้อนมากขึ้น

เมธอด Vue ยังสามารถใช้เพื่อทำสิ่งอื่นนอกเหนือจากการจัดการเหตุการณ์



## The Vue 'methods' Property

เราได้ใช้คุณสมบัติ Vue หนึ่งรายการในบทช่วยสอนนี้ ซึ่งก็คือคุณสมบัติ 'data' ซึ่งเราสามารถจัดเก็บค่าได้

มีคุณสมบัติ Vue อื่นที่เรียกว่า 'methods ซึ่งเราสามารถจัดเก็บฟังก์ชันที่เป็นของอินสแตนซ์ Vue ได้ วิธีการสามารถเก็บไว้ในอินสแตนซ์ Vue ดังนี้:

```javascript
const app = Vue.createApp({
  data() {
    return {
      text: ''
    }
  },
  methods: {
    writeText() {
      this.text = 'Hello Wrold!'
    }
  }
})
```

เคล็ดลับ: เราต้องเขียนสิ่งนี้ เป็นคำนำหน้าเพื่ออ้างถึงคุณสมบัติข้อมูลจากภายในวิธีการ



หากต้องการเรียกใช้เมธอด 'writeText' เมื่อเราคลิกองค์ประกอบ <div> เราสามารถเขียนโค้ดด้านล่างนี้:

```html
<div v-on:click="writeText"></div>
```

ตัวอย่างมีลักษณะดังนี้:

### Example

คำสั่ง v-on ใช้กับองค์ประกอบ <div> เพื่อฟังเหตุการณ์ 'click' เมื่อ event  'click' เกิดขึ้น ระบบจะเรียกเมธอด 'writeText' และข้อความจะเปลี่ยนไป

```html
<div id="app">
  <p>Click on the box below:</p>
  <div v-on:click="writeText">
    {{ text }}
  </div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        text: ''
      }
    },
    methods: {
      writeText() {
        this.text = 'Hello World!'
      }
    }
  })
  app.mount('#app')
</script>
```



## เรียกใช้เมธอดด้วย Event Object

เมื่อมี event เกิดขึ้นจนมีการเรียกเมธอด event object จะถูกส่งผ่านเมธอดตามค่าเริ่มต้น วิธีนี้สะดวกมากเนื่องจาก event object ประกอบด้วยข้อมูลที่เป็นประโยชน์มากมาย เช่น target object, the event type หรือตำแหน่งเมาส์เมื่อมีเหตุการณ์ 'click' หรือ 'mousemove' เกิดขึ้น

### Example

คำสั่ง v-on ใช้กับองค์ประกอบ <div> เพื่อฟัง 'mousemove' event เมื่อ 'mousemove' event เกิดขึ้น เมธอด 'mousePos' จะถูกเรียก และ event object จะถูกส่งพร้อมกับเมธอดตามค่าเริ่มต้น เพื่อให้เราสามารถรับตำแหน่งตัวชี้เมาส์ได้

เราต้องใช้สิ่งนี้ คำนำหน้าเพื่ออ้างถึง "xPos" ภายในคุณสมบัติข้อมูลอินสแตนซ์ Vue จากเมธอด

```html
<div id="app">
  <p>Move the mouse pointer over the box below:</p>
  <div v-on:mousemove="mousePos"></div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        xPos: 0,
        yPos: 0
      }
    },
    methods: {
      mousePos(event) {
        this.xPos = event.offsetX
        this.yPos = event.offsetY
      }
    }
  })
  app.mount('#app')
</script>
```

หากเราขยายตัวอย่างข้างต้นเพียงบรรทัดเดียว เราก็สามารถเปลี่ยนสีพื้นหลังตามตำแหน่งตัวชี้เมาส์ในทิศทาง x ได้ สิ่งเดียวที่เราต้องเพิ่มคือ v-bind เพื่อเปลี่ยนสีพื้นหลังในแอตทริบิวต์ style:

### Example

ความแตกต่างจากตัวอย่างด้านบนคือสีพื้นหลังผูกกับ 'xPos' ด้วย v-bind ดังนั้นค่า hsl 'hue' จะถูกตั้งค่าเท่ากับ 'xPos'

```html
<div
  v-on:mousemove="mousePos"
  v-bind:style="{backgroundColor:'hsl('+xPos+',80%,80%)'}">
</div>
```

ในตัวอย่างด้านล่าง event object จะมีข้อความจากแท็ก <textarea> เพื่อให้ดูเหมือนว่าเรากำลังเขียนอยู่ในสมุดบันทึก

### Example

คำสั่ง v-on ใช้กับแท็ก <textarea> เพื่อฟัง 'input' event ซึ่งเกิดขึ้นเมื่อใดก็ตามที่มีการเปลี่ยนแปลงในข้อความภายในองค์ประกอบ textarea

เมื่อ 'input' event เกิดขึ้น ระบบจะเรียกเมธอด 'writeText' และ event object จะถูกส่งด้วยวิธีดังกล่าวตามค่าเริ่มต้น เพื่อให้เรารับข้อความจากแท็ก <textarea> ได้ คุณสมบัติ 'text' ในอินสแตนซ์ Vue ได้รับการอัพเดตโดยเมธอด 'writeText' ส่วน span element ได้รับการตั้งค่าให้แสดงค่า 'text' ด้วยไวยากรณ์เครื่องหมายปีกกาคู่ และสิ่งนี้ได้รับการอัปเดตโดยอัตโนมัติโดย Vue

```html
<div id="app">
  <textarea v-on:input="writeText" placeholder="Start writing.."></textarea>
  <span>{{ text }}</span>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        text: ''
      }
    },
    methods: {
      writeText(event) {
        this.text = event.target.value
      }
    }
  })
  app.mount('#app')
</script>
```



## Passing Arguments

บางครั้งเราต้องการส่งผ่านข้อโต้แย้งด้วยเมธอดเมื่อมีเหตุการณ์เกิดขึ้น

สมมติว่าคุณทำงานเป็นเจ้าหน้าที่พิทักษ์ป่า และต้องการนับจำนวนการพบเห็นกวางมูส บางครั้งอาจเห็นกวางมูสหนึ่งหรือสองตัว บางครั้งอาจเห็นกวางมูสมากกว่า 10 ตัวในหนึ่งวัน เราเพิ่มปุ่มเพื่อนับการพบเห็น '+1' และ '+5' และปุ่ม '-1' ในกรณีที่เรานับมากเกินไป

ในกรณีนี้ เราสามารถใช้เมธอดเดียวกันสำหรับปุ่มทั้งสามปุ่ม และเพียงเรียกเมธอดที่มีตัวเลขต่างกันเป็นอาร์กิวเมนต์จากปุ่มที่ต่างกัน นี่คือวิธีที่เราสามารถเรียกเมธอดที่มีอาร์กิวเมนต์ได้:

```html
<button v-on:click="addMoose(5)">+5</button>
```

และนี่คือวิธีการ 'addMoose' มีลักษณะดังนี้:

```javascript
methods: {
  addMoose(number) {
    this.count = this.count + number
  }
}
```

มาดูกันว่าการส่งผ่านอาร์กิวเมนต์ด้วย method ทำงานอย่างไรในตัวอย่างเต็ม

### Example

```html
<div id="app">
  <img src="img_moose.jpg">
  <p>{{ "Moose count: " + count }}</p>
  <button v-on:click="addMoose(+1)">+1</button>
  <button v-on:click="addMoose(+5)">+5</button>
  <button v-on:click="addMoose(-1)">-1</button>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        count: 0
      }
    },
    methods: {
      addMoose(number) {
        this.count+=number
      }
    }
  })
 app.mount('#app')
</script>
```



## Passing both an Argument and The Event Object

หากเราต้องการส่งผ่านทั้ง event object และอาร์กิวเมนต์อื่น จะมีชื่อที่สงวนไว้ '$event' เราสามารถใช้ตำแหน่งที่เรียกใช้เมธอดได้ เช่นนี้

```html
<button v-on:click="addAnimal($event, 5)">+5</button>
```

และนี่คือลักษณะวิธีการในอินสแตนซ์ Vue:

```javascript
methods: {
  addAnimal(e, number) {
    if(e.target.parentElement.id==="tigers"){
      this.tigers = this.tigers + number
    }
  }
}
```

ตอนนี้ให้เราดูตัวอย่างเพื่อดูว่าจะส่งผ่านทั้ง event object และอาร์กิวเมนต์อื่นด้วยวิธีการได้อย่างไร

### Example

ในตัวอย่างนี้วิธีการของเราจะรับทั้ง event object และ text

```html
<div id="app">
  <img
    src="img_tiger.jpg"
    id="tiger"
    v-on:click="myMethod($event,'Hello')">
  <p>"{{ msgAndId }}"</p>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        msgAndId: ''
      }
    },
    methods: {
      myMethod(e,msg) {
        this.msgAndId = msg + ', '
        this.msgAndId += e.target.id
      }
    }
  })
 app.mount('#app')
</script>
```



## ตัวอย่างขนาดใหญ่

ในตัวอย่างนี้ เราเห็นว่าเป็นไปได้ที่จะใช้เพียง method เดียวในการนับสัตว์สามตัวที่แตกต่างกันโดยเพิ่มทีละสามตัวสำหรับสัตว์แต่ละตัว เราบรรลุสิ่งนี้ได้โดยส่งทั้ง event object และ increment number:

### Example

ทั้งขนาดที่เพิ่มขึ้นและ event object จะถูกส่งผ่านเป็นอาร์กิวเมนต์ด้วย method เมื่อมีการคลิกปุ่ม คำสงวน '$event' ใช้เพื่อส่งผ่าน event object พร้อมวิธีบอกสัตว์ที่จะนับ

```html
<div id="app">
  <div id="tigers">
    <img src="img_tiger.jpg">
    <button v-on:click="addAnimal($event,1)">+1</button>
    <button v-on:click="addAnimal($event,5)">+5</button>
    <button v-on:click="addAnimal($event,1)">-1</button>
  </div>
  <div id="moose">
    <img src="img_moose.jpg">
    <button v-on:click="addAnimal($event,1)">+1</button>
    <button v-on:click="addAnimal($event,5)">+5</button>
    <button v-on:click="addAnimal($event,1)">-1</button>
  </div>
  <div id="kangaroos">
    <img src="img_kangaroo.jpg">
    <button v-on:click="addAnimal($event,1)">+1</button>
    <button v-on:click="addAnimal($event,5)">+5</button>
    <button v-on:click="addAnimal($event,1)">-1</button>
  </div>
  <ul>
    <li>Tigers: {{ tigers }} </li>
    <li>Moose: {{ moose }} </li>
    <li>Kangaroos: {{ kangaroos }} </li>
  </ul>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        tigers: 0,
        moose: 0,
        kangaroos: 0
      }
    },
    methods: {
      addAnimal(e,number) {
        if(e.target.parentElement.id==="tigers") {
          this.tigers+=number
        }
        else if(e.target.parentElement.id==="moose") {
          this.moose+=number
        }
        else {
          this.kangaroos+=number
        }
      }
    }
  })
 app.mount('#app')
</script>
```

