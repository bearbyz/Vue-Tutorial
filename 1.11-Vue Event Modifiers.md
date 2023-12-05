# ตัวแก้ไขเหตุการณ์ Vue

ตัว Event modifiers ใน Vue จะปรับเปลี่ยนวิธีที่เหตุการณ์ทริกเกอร์การเรียกใช้เมธอด และช่วยให้เราจัดการกับเหตุการณ์ได้อย่างมีประสิทธิภาพและตรงไปตรงมามากขึ้น

ตัวแก้ไขเหตุการณ์จะใช้ร่วมกับคำสั่ง Vue v-on ตัวอย่างเช่น:

- ป้องกันพฤติกรรมการส่งเริ่มต้นของแบบฟอร์ม HTML (v-on:submit.prevent)
- ตรวจสอบให้แน่ใจว่าเหตุการณ์สามารถทำงานได้เพียงครั้งเดียวหลังจากโหลดเพจแล้ว (v-on:click.once)
- ระบุแป้นคีย์บอร์ดที่จะใช้เป็นเหตุการณ์เพื่อเรียกใช้เมธอด (v-on:keyup.enter)



## วิธีการแก้ไข v-on Directive

ตัว Event modifiers ใช้เพื่อกำหนดวิธีการตอบสนองต่อเหตุการณ์โดยละเอียดยิ่งขึ้น

เราใช้ตัว Event modifiers โดยการเชื่อมต่อแท็กเข้ากับ event เหมือนที่เราเคยเห็นมาก่อน:

```html
<button v-on:click="createAlert">Create alert</button>
```

ตอนนี้ เพื่อกำหนดให้เจาะจงยิ่งขึ้นว่าเหตุการณ์การคลิกปุ่มควรเริ่มทำงานเพียงครั้งเดียวหลังจากโหลดเพจแล้ว เราสามารถเพิ่มตัวแก้ไข .once ได้ดังนี้:

```html
<button v-on:click.once="createAlert">Create alert</button>
```

นี่คือตัวอย่างที่มีตัวแก้ไข .once:

### Example

ตัวแก้ไข .once ถูกใช้บนแท็ก <button> เพื่อเรียกใช้เมธอดในครั้งแรกที่เกิดเหตุการณ์ 'click' เท่านั้น

```html
<div id="app">
  <p>Click the button to create an alert:</p>
  <button v-on:click.once="creteAlert">Create Alert</button>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    methods: {
      createAlert() {
        alert("Alert created from button click")
      }
    }
  })
  app.mount('#app')
</script>
```

หมายเหตุ: เป็นไปได้ที่จะจัดการกับเหตุการณ์ภายในวิธีการแทนการใช้ตัวแก้ไขเหตุการณ์ แต่ตัวแก้ไขเหตุการณ์ทำให้ง่ายขึ้นมาก



## ตัวปรับเปลี่ยน v-on ที่แตกต่างกัน

ตัว Event modifiers ใช้ในสถานการณ์ที่แตกต่างกัน เราสามารถใช้ตัว Event modifiers เมื่อเราฟังเหตุการณ์บนคีย์บอร์ด เหตุการณ์การคลิกเมาส์ และเรายังสามารถใช้ตัว Event modifiers ได้อีกด้วย

ตัวแก้ไขเหตุการณ์ .once สามารถใช้ได้หลังจาก keyboard และ mouse click events.



## ตัวแก้ไขเหตุการณ์ Keyboard Key

เรามีประเภทเหตุการณ์แป้นพิมพ์ที่แตกต่างกันสามประเภท การ keydown การ keypress และ การ keyup

สำหรับเหตุการณ์สำคัญแต่ละประเภท เราสามารถระบุได้อย่างชัดเจนว่าคีย์ใดที่จะรับฟังหลังจากเหตุการณ์สำคัญเกิดขึ้น เรามี .space, .enter, .w และ .up เป็นต้น

คุณสามารถเขียน key event ลงในหน้าเว็บหรือลงในคอนโซลด้วย console.log(event.key) เพื่อค้นหาค่าของคีย์ที่ต้องการด้วยตนเอง:

### Example

keydown keyboard event จะทริกเกอร์เมธอด 'getKey' และค่า 'key' จาก event object จะถูกเขียนไปยังคอนโซลและไปยังหน้าเว็บ

```html
<input v-on:keydown="getKey">
<p> {{ keyValue }} </p>
```

```javascript
data() {
  return {
    keyValue = ''
  }
},
methods: {
  getKey(evt) {
    this.keyValue = evt.key
    console.log(evt.key)
  }
}
```

นอกจากนี้เรายังสามารถเลือกที่จะ limit the event ที่จะเกิดขึ้นเฉพาะเมื่อมีการ mouse click หรือ key press เกิดขึ้นร่วมกับคีย์ตัวปรับแต่งระบบ .alt, .ctrl, .shift หรือ .meta คีย์ตัวปรับแต่งระบบ .meta แสดงถึง Windows key บนคอมพิวเตอร์ Windows หรือ command key บนคอมพิวเตอร์ Apple

| Key Modifier             | **Details**                                                  |
| :----------------------- | ------------------------------------------------------------ |
| .[*Vue key alias*]       | คีย์ที่พบบ่อยที่สุดมีนามแฝงของตัวเองใน Vue:   `.enter` `.tab` `.delete` `.esc` `.space` `.up` `.down` `.left` `.right` |
| .[*letter*]              | ระบุตัวอักษรที่มาเมื่อคุณกดปุ่ม ตามตัวอย่าง: ใช้ตัวแก้ไขคีย์ .s เพื่อฟังคีย์ 'S'   |
| .[*system modifier key*] | .alt, .ctrl, .shift หรือ .meta ปุ่มเหล่านี้สามารถใช้ร่วมกับปุ่มอื่นๆ หรือใช้ร่วมกับการคลิกเมาส์ได้ |

### Example

ใช้ตัวแก้ไข .s เพื่อสร้างการแจ้งเตือนเมื่อผู้ใช้เขียน 's' ภายในแท็ก <textarea>

```html
<div id="app">
  <p>Try pressing the 's' key:</p>
  <textarea v-on:keyup.s="createAlert"></textarea>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    methods: {
      createAlert() {
        alert("You pressed the 'S' key!")
      }
    }
  })
  app.mount('#app')
</script>
```



## Combine Keyboard Event Modifiers

ตัวแก้ไขเหตุการณ์ยังสามารถใช้ร่วมกับตัวอื่นๆ ได้ ดังนั้นต้องมีมากกว่าหนึ่งสิ่งเกิดขึ้นพร้อมกันจึงจะเรียกใช้เมธอดได้

### Example

ใช้ตัวแก้ไข .s และ .ctrl ร่วมกันเพื่อสร้างการแจ้งเตือนเมื่อมีการกด 's' และ 'ctrl' พร้อมกันภายในแท็ก <textarea>

```html
<div id="app">
  <p>Try pressing the 's' key:</p>
  <textarea v-on:keydown.ctrl.s="createAlert"></textarea>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    methods: {
      createAlert() {
        alert("You pressed the 'S' and 'Ctrl' keys, in combination!")
      }
    }
  })
  app.mount('#app')
</script>
```



## ตัวแก้ไขปุ่มเมาส์

ในการตอบสนองต่อการคลิกเมาส์ เราสามารถเขียน v-on:click ได้ แต่เพื่อระบุปุ่มเมาส์ที่ถูกคลิก เราสามารถใช้ตัวดัดแปลง .left, .center หรือ .right



**ผู้ใช้แทร็คแพด:** คุณอาจต้องคลิกด้วยสองนิ้ว หรือที่ด้านขวาล่างของแทร็คแพดบนคอมพิวเตอร์ของคุณเพื่อสร้างการคลิกขวา

### Example

เปลี่ยนสีพื้นหลังเมื่อผู้ใช้คลิกขวาที่องค์ประกอบ <div>:

```html
<div id="app">
  <div v-on:click.right="changeColor"
       v-bind:style="{backgroundColor:'hsl('+bgColor+',80%,80%)'}">
    <p>Press right mouse button here.</p>
  </div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        bgColor: 0
      }
    },
    methods: {
      changeColor() {
        this.bgColor+=50
      }
    }
  })
  app.mount('#app')
</script>
```

Mouse button events สามารถทำงานร่วมกับตัวปรับแต่งระบบคีย์ได้

### Example

เปลี่ยนสีพื้นหลังเมื่อผู้ใช้คลิกขวาในองค์ประกอบ <div> ร่วมกับปุ่ม 'ctrl':

```html
<div id="app">
  <div v-on:click.right.ctrl="changeColor"
       v-bind:style="{backgroundColor:'hsl('+bgColor+',80%,80%)'}">
    <p>Press right mouse button here.</p>
  </div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        bgColor: 0
      }
    },
    methods: {
      changeColor() {
        this.bgColor+=50
      }
    }
  })
  app.mount('#app')
</script>
```

ตัวแก้ไขเหตุการณ์ .prevent สามารถใช้เพิ่มเติมจากตัวแก้ไข .right เพื่อป้องกันไม่ให้เมนูดรอปดาวน์เริ่มต้นปรากฏขึ้นเมื่อเราคลิกขวา

### Example

เมนูดรอปดาวน์จะไม่ปรากฏเมื่อคุณคลิกขวาเพื่อเปลี่ยนสีพื้นหลังขององค์ประกอบ <div>:

```html
<div id="app">
  <div v-on:click.right.prevent="changeColor"
       v-bind:style="{backgroundColor:'hsl('+bgColor+',80%,80%)'}">
    <p>Press right mouse button here.</p>
  </div>
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        bgColor: 0
      }
    },
    methods: {
      changeColor() {
        this.bgColor+=50
      }
    }
  })
  app.mount('#app')
</script>
```

อาจเป็นไปได้ที่จะป้องกันไม่ให้เมนูดรอปดาวน์ปรากฏขึ้นหลังจากการคลิกขวาโดยใช้ event.preventDefault() ภายในเมธอด แต่ด้วย Vue .prevent modifier โค้ดจะสามารถอ่านได้ง่ายขึ้นและดูแลรักษาได้ง่ายขึ้น



คุณยังสามารถตอบสนองต่อการคลิกเมาส์ปุ่มซ้ายร่วมกับตัวปรับแต่งอื่นๆ เช่น click.left.shift:

### Example

กดปุ่มคีย์บอร์ด 'shift' ค้างไว้แล้วกดปุ่มซ้ายของเมาส์บนแท็ก <img> เพื่อเปลี่ยนภาพ

```html
<div id="app">
  <p>Hold 'Shift' key and press left mouse button:</p>
  <img v-on:click.left.shift="changeImg" v-bind:src="imgUrl">
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<script>
  const app = Vue.createApp({
    data() {
      return {
        imgUrlIndex: 0,
        imgUrl: 'img_tiger_square.jpeg',
        imgages: [
          'img_tiger_square.jpeg',
          'img_moose_square.jpeg',
          'img_kangaroo_square.jpeg'
        ]
      }
    },
    methods: {
      changeImg() {
        this.imgUrlIndex++
        if(this.imgUrlIndex>=3){
          this.imgUrlIndex=0
        }
        this.imgUrl = this.images[this.imgUrlIndex]
      }
    }
  })
  app.mount('#app')
</script>
```