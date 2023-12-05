# Vue Watchers

**watcher** เป็น method ที่เฝ้าดู data property ที่มีชื่อเดียวกัน

**watcher** จะทำงานทุกครั้งที่ค่า data property เปลี่ยนแปลง

ใช้ **watcher** หาก data property บางอย่างต้องมีการดำเนินการ



## The Watcher Concept

Watchers เป็นตัวเลือกการกำหนดค่าที่สี่ในอินสแตนซ์ Vue ที่เราจะเรียนรู้ ตัวเลือกการกำหนดค่าสามตัวแรกที่เราได้ดูไปแล้วคือ 'data' 'methods' และ 'computed'

เช่นเดียวกับ 'data', 'methods' และ 'computed' watchers ยังมีชื่อที่สงวนไว้ในอินสแตนซ์ Vue: '**watch**'

### Syntax

```javascript
const app = Vue.createApp({
  data() {
    ...
  },
  watch: {
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

ตามที่กล่าวไว้ในพื้นที่สีเขียวด้านบน watcher จะตรวจสอบ data property ที่มีชื่อเดียวกัน

เราไม่เคยเรียก watcher  method  จะถูกเรียกโดยอัตโนมัติเมื่อ property value เปลี่ยนแปลงเท่านั้น

 property value ใหม่จะพร้อมใช้งานเป็นอาร์กิวเมนต์อินพุตของ watcher method เสมอ และค่าเก่าก็เช่นกัน

### Example

องค์ประกอบ <input type="range"> ใช้เพื่อเปลี่ยนค่า 'rangeVal' watcher ใช้เพื่อป้องกันไม่ให้ผู้ใช้เลือกค่าระหว่าง 20 ถึง 60 ที่ถือว่าผิดกฎหมาย

```html
<input type="range" v-model="rangeVal">
<p>{{ rangeVal }}</p>
```

```javascript
const app = Vue.createApp({
  data() {
    rangeVal: 70
  },
  watch: {
    rangeVal(val){
      if( val>20 && val<60) {
        if(val<40){
          this.rangeVal = 20;
        }
        else {
          this.rangeVal = 60;
        }
      }
    }
  }
})
```



## Watcher ด้วย New และ Old Values

นอกเหนือจาก new property value แล้ว previous property value ยังพร้อมใช้งานโดยอัตโนมัติเป็นอาร์กิวเมนต์อินพุตสำหรับ watcher methods

### Example

เราตั้งค่า click event บนองค์ประกอบ <div> เพื่อบันทึกตัวชี้เมาส์ตำแหน่ง x 'xPos' ด้วยวิธีการ 'updatePos' watcher จะคำนวณความแตกต่างในพิกเซลระหว่างตำแหน่ง x ใหม่และตำแหน่งก่อนหน้าโดยใช้อาร์กิวเมนต์อินพุตเก่าและใหม่กับ watcher method

```html
<div v-on:click="updatePos"></div>
<p>{{ xDiff }}</p>
```

```javascript
const app = Vue.createApp({
  data() {
    xPos: 0,
    xDiff: 0
  },
  watch: {
    xPos(newVal,oldVal){
      this.xDiff = newVal-oldVal
    }
  },
  methods: {
    updatePos(evt) {
      this.xPos = evt.offsetX
    }
  }
})
```

นอกจากนี้เรายังสามารถใช้ new and old values พื่อให้ข้อเสนอแนะแก่ผู้ใช้ทันทีที่อินพุตเปลี่ยนจาก invalid เป็น valid:

### Example

ค่าจากองค์ประกอบ <input> เชื่อมต่อกับ watcher หากค่ามี '@' จะถือว่าเป็นที่อยู่อีเมลที่ถูกต้อง ผู้ใช้จะได้รับข้อความตอบกลับเพื่อแจ้งว่าอินพุตนั้น valid, invalid หรือเพิ่ง valid เมื่อกดแป้นพิมพ์ครั้งล่าสุด

```html
<input v-type="email" v-model="inpAddress">
<p v-bind:class="myClass">{{ feedbackText }}</p>
```

```javascript
const app = Vue.createApp({
  data() {
    inpAddress: '',
    feedbackText: '',
    myClass: 'invalid'
  },
  watch: {
    inpAddress(newVal,oldVal) {
      if( !newVal.includes('@') ) {
        this.feedbackText = 'The e-mail address is NOT valid';
        this.myClass = 'invalid';
      }
      else if( !oldVal.includes('@') && newVal.includes('@') ) {
        this.feedbackText = 'Perfect! You fixed it!';
        this.myClass = 'valid';
      }
      else {
        this.feedbackText = 'The e-mail address is valid :)';
      }
    }
  }
})
```



## Watchers vs. Methods

ทั้ง Watchers และ Methods ถูกเขียนเป็นฟังก์ชัน แต่มีข้อแตกต่างหลายประการ:

- **Methods** ถูกเรียกจาก HTML
- มักเรียก **Methods** เมื่อมีเหตุการณ์เกิดขึ้น
- **Methods** รับวัตถุเหตุการณ์เป็นอินพุตโดยอัตโนมัติ
- นอกจากนี้เรายังสามารถส่งค่าอื่น ๆ ที่เราเลือกเป็นอินพุตไปยัง **Methods** ได้
- **Watchers** จะถูกเรียกเมื่อ data property value ที่ watched เปลี่ยนแปลงเท่านั้น และสิ่งนี้จะเกิดขึ้นโดยอัตโนมัติ
- **Watchers** จะได้รับค่าใหม่และค่าเก่าจาก watched property โดยอัตโนมัติ
- เราไม่สามารถเลือกที่จะส่งค่าอื่นใดโดยให้ **watcher** เป็นอินพุตได้



## Watchers vs. Computed Properties

Watchers และ computed properties ต่างก็เขียนเป็นฟังก์ชัน

Watchers และ computed properties จะถูกเรียกโดยอัตโนมัติเมื่อการเปลี่ยนแปลงการขึ้นต่อกัน และไม่เคยถูกเรียกจาก HTML

ต่อไปนี้เป็นข้อแตกต่างบางประการระหว่างคุณสมบัติที่คำนวณและผู้เฝ้าดู:

- **Watchers** จะขึ้นอยู่กับทรัพย์สินเพียงแห่งเดียวเท่านั้น นั่นคือทรัพย์สินที่พวกเขาตั้งค่าไว้เพื่อดู
- **Computed properties** สามารถขึ้นอยู่กับคุณสมบัติหลายอย่าง
- **Computed properties** ถูกใช้เหมือนกับ data properties ยกเว้นคุณสมบัติที่เป็นไดนามิก
- **Watchers** ไม่ได้อ้างอิงจาก HTML

