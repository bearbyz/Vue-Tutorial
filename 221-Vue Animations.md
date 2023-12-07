# Vue Animations

ส่วนประกอบ <Transition> ในตัวใน Vue ช่วยให้เราทำแอนิเมชั่นเมื่อมีการเพิ่มหรือลบองค์ประกอบด้วย v-if, v-show หรือด้วยส่วนประกอบแบบไดนามิก

ไม่มีอะไรผิดปกติกับการใช้การเปลี่ยนภาพและภาพเคลื่อนไหว CSS ธรรมดาในกรณีอื่นๆ



## A Short Introduction to CSS Transition and Animation

บทช่วยสอนในส่วนนี้ต้องการความรู้เกี่ยวกับภาพเคลื่อนไหวและการเปลี่ยน CSS ขั้นพื้นฐาน

แต่ก่อนที่เราจะใช้คอมโพเนนต์ <Transition> ในตัวเฉพาะของ Vue เพื่อสร้างภาพเคลื่อนไหว เรามาดูสองตัวอย่างว่าภาพเคลื่อนไหวและการเปลี่ยนผ่าน CSS แบบธรรมดาสามารถใช้กับ Vue ได้อย่างไร

### Example

##### `App.vue`:

```html
<template>
  <h1>Basic CSS Transition</h1>
  <button @click="this.doesRotate = true">Rotate</button>
  <div :class="{ rotate: doesRotate }"></div>
</template>

<script>
export default {
  data() {
    return {
      doesRotate: false
    }
  }
}
</script>

<style scoped>
  .rotate {
    rotate: 160deg;
    transition: rotate 1s;
  }
  div {
    border: solid black 2px;
    background-color: lightcoral;
    width: 60px;
    height: 60px;
  }
  h1, button, div {
    margin: 10px;
  }
</style>
```

ในตัวอย่างด้านบน เราใช้ v-bind เพื่อกำหนดคลาสให้กับแท็ก <div> เพื่อให้หมุนได้ เหตุผลที่การหมุนใช้เวลา 1 วินาทีก็คือ การหมุนนั้นถูกกำหนดด้วยคุณสมบัติการเปลี่ยนแปลง CSS

ในตัวอย่างด้านล่าง เราจะมาดูกันว่าเราสามารถย้ายวัตถุด้วยคุณสมบัติภาพเคลื่อนไหว CSS ได้อย่างไร

### Example

##### `App.vue`:

```html
<template>
  <h1>Basic CSS Animation</h1>
  <button @click="this.doesMove = true">Start</button>
  <div :class="{ move: doesMove }"></div>
</template>

<script>
export default {
  data() {
    return {
      doesMove: false
    }
  }
}
</script>

<style scoped>
  .move {
    animation: move .5s alternate 4 ease-in-out;
  }
  @keyframes move {
    from {
      translate: 0 0;
    }
    to {
      translate: 70px 0;
    }
  }
  div {
    border: solid black 2px;
    background-color: lightcoral;
    border-radius: 50%;
    width: 60px;
    height: 60px;
  }
  h1, button, div {
    margin: 10px;
  }
</style>
```



## The <Transition> Component

ไม่มีอะไรผิดปกติกับการใช้ทรานซิชั่นและภาพเคลื่อนไหว CSS ธรรมดาเหมือนที่เราทำในสองตัวอย่างข้างต้น

แต่โชคดีที่ Vue มีคอมโพเนนต์ <Transition> ในตัวในกรณีที่เราต้องการทำให้องค์ประกอบเคลื่อนไหวขณะที่มันถูกลบออกหรือเพิ่มลงในแอปพลิเคชันของเราด้วย v-if หรือ v-show เพราะนั่นคงเป็นเรื่องยาก ทำกับภาพเคลื่อนไหว CSS ธรรมดา

ขั้นแรกเรามาสร้างแอปพลิเคชันโดยที่ปุ่มเพิ่มหรือลบแท็ก <p>:

### Example

##### `App.vue`:

```html
<template>
  <h1>Add/Remove <p> Tag</h1>
  <button @click="this.exists = !this.exists">{{btnText}}</button><br>
  <p v-if="exists">Hello World!</p>
</template>

<script>
export default {
  data() {
    return {
      exists: false
    }
  },
  computed: {
    btnText() {
      if(this.exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    }
  }
}
</script>

<style>
  p {
    background-color: lightgreen;
    display: inline-block;
    padding: 10px;
  }
</style>
```

ตอนนี้ เรามาล้อมองค์ประกอบ <Transition> ไว้รอบๆ แท็ก <p> และดูว่าเราสามารถทำให้การลบแท็ก <p> เคลื่อนไหวได้อย่างไร

เมื่อเราใช้คอมโพเนนต์ <การเปลี่ยนผ่าน> เราจะได้คลาส CSS ที่แตกต่างกัน 6 คลาสโดยอัตโนมัติ ซึ่งเราสามารถใช้เพื่อทำให้เคลื่อนไหวเมื่อมีการเพิ่มหรือลบองค์ประกอบ

ในตัวอย่างด้านล่าง เราจะใช้คลาส v-leave-from และ v-leave-to ที่มีอยู่โดยอัตโนมัติเพื่อสร้างภาพเคลื่อนไหวที่จางลงเมื่อแท็ก <p> ถูกลบ:

### Example

##### `App.vue`:

```html
<template>
  <h1>Add/Remove <p> Tag</h1>
  <button @click="this.exists = !this.exists">{{btnText}}</button><br>
  <Transition>
    <p v-if="exists">Hello World!</p>
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      exists: false
    }
  },
  computed: {
    btnText() {
      if(this.exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    }
  }
}
</script>

<style>
  .v-leave-from {
    opacity: 1;
  }
  .v-leave-to {
    opacity: 0;
  }
  p {
    background-color: lightgreen;
    display: inline-block;
    padding: 10px;
    transition: opacity 0.5s;
  }
</style>
```



## The Six <Transition> Classes

มีหกคลาสที่พร้อมใช้งานโดยอัตโนมัติเมื่อเราใช้ส่วนประกอบ <Transition>

เมื่อมีการ**เพิ่ม**องค์ประกอบภายในองค์ประกอบ <Transition> เราสามารถใช้สามคลาสแรกเหล่านี้เพื่อทำให้การเปลี่ยนแปลงนั้นเคลื่อนไหวได้:

1. v-enter-from
2. v-enter-active
3. v-enter-to

และเนื่องจากองค์ประกอบถูก**ลบ**ออกภายในองค์ประกอบ <Transition> เราจึงสามารถใช้คลาสสามคลาสถัดไปได้ :

1. v-leave-from
2. v-leave-active
3. v-leave-to

หมายเหตุ: สามารถมีได้เพียงองค์ประกอบเดียวในระดับรากขององค์ประกอบ <Transition>



ตอนนี้ ลองใช้สี่คลาสเหล่านี้เพื่อให้เราสามารถเคลื่อนไหวทั้งเมื่อมีการเพิ่มแท็ก <p> และเมื่อถูกลบออก

### Example

##### `App.vue`:

```html
<template>
  <h1>Add/Remove <p> Tag</h1>
  <button @click="this.exists = !this.exists">{{btnText}}</button><br>
  <Transition>
    <p v-if="exists">Hello World!</p>
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      exists: false
    }
  },
  computed: {
    btnText() {
      if(this.exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    }
  }
}
</script>

<style>
  .v-enter-from {
    opacity: 0;
    translate: -100px 0;
  }
  .v-enter-to {
    opacity: 1;
    translate: 0 0;
  }
  .v-leave-from {
    opacity: 1;
    translate: 0 0;
  }
  .v-leave-to {
    opacity: 0;
    translate: 100px 0;
  }
  p {
    background-color: lightgreen;
    display: inline-block;
    padding: 10px;
    transition: all 0.5s;
  }
</style>
```

นอกจากนี้เรายังสามารถใช้ v-enter-active และ v-leave-active เพื่อตั้งค่าสไตล์หรือภาพเคลื่อนไหวระหว่างการเพิ่มหรือระหว่างการลบองค์ประกอบ:

### Example

##### `App.vue`:

```html
<template>
  <h1>Add/Remove <p> Tag</h1>
  <button @click="this.exists = !this.exists">{{btnText}}</button><br>
  <Transition>
    <p v-if="exists">Hello World!</p>
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      exists: false
    }
  },
  computed: {
    btnText() {
      if(this.exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    }
  }
}
</script>

<style>
  .v-enter-active {
    background-color: lightgreen;
    animation: added 1s;
  }
  .v-leave-active {
    background-color: lightcoral;
    animation: added 1s reverse;
  }
  @keyframes added {
    from {
      opacity: 0;
      translate: -100px 0;
    }
    to {
      opacity: 1;
      translate: 0 0;
    }
  }
  p {
    display: inline-block;
    padding: 10px;
    border: dashed black 1px;
  }
</style>
```



## The Transition 'name' Prop

ในกรณีที่คุณมีส่วนประกอบ <Transition> หลายรายการ แต่คุณต้องการให้ส่วนประกอบ <Transition> อย่างน้อยหนึ่งรายการมีภาพเคลื่อนไหวที่แตกต่างกัน คุณต้องมีชื่อที่แตกต่างกันสำหรับส่วนประกอบ <Transition> เพื่อแยกความแตกต่าง

เราสามารถเลือกชื่อของส่วนประกอบ <Transition> ด้วยชื่อ prop และนั่นจะเปลี่ยนชื่อของคลาสการเปลี่ยนแปลงด้วยเช่นกัน เพื่อให้เราสามารถตั้งค่ากฎภาพเคลื่อนไหว CSS ที่แตกต่างกันสำหรับส่วนประกอบนั้นได้

```html
<Transition name="swirl">
```

หากค่า prop ชื่อการเปลี่ยนแปลงถูกตั้งค่าเป็น 'swirl' คลาสที่มีอยู่โดยอัตโนมัติจะเริ่มต้นด้วย 'swirl-' แทนที่จะเป็น 'v-':

1. **swirl**-enter-from
2. **swirl**-enter-active
3. **swirl**-enter-to
4. **swirl**-leave-from
5. **swirl**-leave-active
6. **swirl**-leave-to

ในตัวอย่างด้านล่าง เราใช้ชื่อ prop เพื่อให้ส่วนประกอบ <Transition> มีภาพเคลื่อนไหวที่แตกต่างกัน คอมโพเนนต์ <Transition> หนึ่งรายการไม่ได้รับการตั้งชื่อ ดังนั้นจึงได้รับแอนิเมชันโดยใช้คลาส CSS ที่สร้างขึ้นโดยอัตโนมัติโดยขึ้นต้นด้วย 'v-' ส่วนประกอบ <Transition> อื่นๆ ได้รับการตั้งชื่อว่า 'swirl' เพื่อให้สามารถกำหนดกฎสำหรับภาพเคลื่อนไหวด้วยคลาส CSS ที่สร้างขึ้นโดยอัตโนมัติโดยเริ่มต้นด้วย 'swirl-'

### Example

##### `App.vue`:

```html
<template>
  <h1>Add/Remove <p> Tag</h1>
  <p>The second transition in this example has the name prop "swirl", so that we can keep the transitions apart with different class names.</p>
  <hr>
  <button @click="this.p1Exists = !this.p1Exists">{{btn1Text}}</button><br>
  <Transition>
    <p v-if="p1Exists" id="p1">Hello World!</p>
  </Transition>
  <hr>
  <button @click="this.p2Exists = !this.p2Exists">{{btn2Text}}</button><br>
  <Transition name="swirl">
    <p v-if="p2Exists" id="p2">Hello World!</p>
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      p1Exists: false,
      p2Exists: false
    }
  },
  computed: {
    btn1Text() {
      if(this.p1Exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    },
    btn2Text() {
      if(this.p2Exists) {
        return 'Remove';
      }
      else {
        return 'Add';
      }
    }
  }
}
</script>

<style>
  .v-enter-active {
    background-color: lightgreen;
    animation: added 1s;
  }
  .v-leave-active {
    background-color: lightcoral;
    animation: added 1s reverse;
  }
  @keyframes added {
    from {
      opacity: 0;
      translate: -100px 0;
    }
    to {
      opacity: 1;
      translate: 0 0;
    }
  }
  .swirl-enter-active {
    animation: swirlAdded 1s;
  }
  .swirl-leave-active {
    animation: swirlAdded 1s reverse;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 360deg;
      scale: 1;
    }
  }
  #p1, #p2 {
    display: inline-block;
    padding: 10px;
    border: dashed black 1px;
  }
  #p2 {
    background-color: lightcoral;
  }
</style>
```



## JavaScript Transition Hooks

คลาส Transition ทุกคลาสดังที่กล่าวไปนั้นสอดคล้องกับเหตุการณ์ที่เราสามารถเชื่อมต่อเพื่อรันโค้ด JavaScript ได้

| Transition Class | JavaScript Event                              |
| ---------------- | --------------------------------------------- |
| v-enter-from     | `before-enter`                                |
| v-enter-active   | `enter`                                       |
| v-enter-to       | `after-enter` `enter-cancelled`               |
| v-leave-from     | `before-leave`                                |
| v-leave-active   | `leave`                                       |
| v-leave-to       | `after-leave` `leave-cancelled` (v-show only) |

เมื่อเหตุการณ์ after-enter เกิดขึ้นในตัวอย่างด้านล่าง วิธีการจะทำงานโดยแสดงองค์ประกอบ <div> สีแดง

### Example

##### `App.vue`:

```html
<template>
  <h1>JavaScript Transition Hooks</h1>
  <p>This code hooks into "after-enter" so that after the initial animation is done, a method runs that displays a red div.</p>
  <button @click="pVisible=true">Create p-tag!</button><br>
  <Transition @after-enter="onAfterEnter">
    <p v-show="pVisible" id="p1">Hello World!</p>
  </Transition>
  <br>
  <div v-show="divVisible">This appears after the "enter-active" phase of the transition.</div>
</template>

<script>
export default {
  data() {
    return {
      pVisible: false,
      divVisible: false
    }
  },
  methods: {
    onAfterEnter() {
      this.divVisible = true;
    }
  }
}
</script>

<style scoped>
  .v-enter-active {
    animation: swirlAdded 1s;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 360deg;
      scale: 1;
    }
  }
  #p1, div {
    display: inline-block;
    padding: 10px;
    border: dashed black 1px;
  }
  #p1 {
    background-color: lightgreen;
  }
  div {
    background-color: lightcoral;
  }
</style>
```

คุณสามารถใช้ปุ่ม "สลับ" ในตัวอย่างด้านล่างเพื่อขัดจังหวะระยะการเปลี่ยนผ่านขององค์ประกอบ <p> เพื่อให้เหตุการณ์ที่ยกเลิกการป้อนถูกทริกเกอร์:

### Example

##### `App.vue`:

```html
<template>
  <h1>The 'enter-cancelled' Event</h1>
  <p>Click the toggle button again before the enter animation is finished to trigger the 'enter-cancelled' event.</p>
  <button @click="pVisible=!pVisible">Toggle</button><br>
  <Transition @enter-cancelled="onEnterCancelled">
    <p v-if="pVisible" id="p1">Hello World!</p>
  </Transition>
  <br>
  <div v-if="divVisible">You interrupted the "enter-active" transition.</div>
</template>

<script>
export default {
  data() {
    return {
      pVisible: false,
      divVisible: false
    }
  },
  methods: {
    onEnterCancelled() {
      this.divVisible = true;
    }
  }
}
</script>

<style scoped>
  .v-enter-active {
    animation: swirlAdded 2s;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 720deg;
      scale: 1;
    }
  }
  #p1, div {
    display: inline-block;
    padding: 10px;
    border: dashed black 1px;
  }
  #p1 {
    background-color: lightgreen;
  }
  div {
    background-color: lightcoral;
  }
</style>
```



## The 'appear' Prop

หากเรามีองค์ประกอบที่เราต้องการทำให้เคลื่อนไหวเมื่อโหลดหน้า เราจำเป็นต้องใช้เสาปรากฏบนองค์ประกอบ <การเปลี่ยน>

```html
<Transition appear>
  ...
</Transition>
```

ในตัวอย่างนี้ปรากฏเสาเริ่มภาพเคลื่อนไหวเมื่อโหลดหน้าเป็นครั้งแรก:

### Example

##### `App.vue`:

```html
<template>
  <h1>The 'appear' Prop</h1>
  <p>The 'appear' prop starts the animation when the p tag below is rendered for the first time as the page opens. Without the 'appear' prop, this example would have had no animation.</p>
  <Transition appear>
    <p id="p1">Hello World!</p>
  </Transition>
</template>

<style>
  .v-enter-active {
    animation: swirlAdded 1s;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 360deg;
      scale: 1;
    }
  }
  #p1 {
    display: inline-block;
    padding: 10px;
    border: dashed black 1px;
    background-color: lightgreen;
  }
</style>
```



## Transition Between Elements

ส่วนประกอบ <Transition> ยังสามารถใช้เพื่อสลับระหว่างหลายองค์ประกอบได้ ตราบใดที่เราตรวจสอบให้แน่ใจว่าจะแสดงเพียงองค์ประกอบเดียวในแต่ละครั้งโดยใช้ <v-if> และ <v-else-if>:

### Example

##### `App.vue`:

```html
<template>
  <h1>Transition Between Elements</h1>
  <p>Click the button to get a new image.</p>
  <p>The new image is added before the previous is removed. We will fix this in the next example with mode="out-in".</p>
  <button @click="newImg">Next image</button><br>
  <Transition>
    <img src="/img_pizza.svg" v-if="imgActive === 'pizza'">
    <img src="/img_apple.svg" v-else-if="imgActive === 'apple'">
    <img src="/img_cake.svg" v-else-if="imgActive === 'cake'">
    <img src="/img_fish.svg" v-else-if="imgActive === 'fish'">
    <img src="/img_rice.svg" v-else-if="imgActive === 'rice'">
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      imgActive: 'pizza',
      imgs: ['pizza', 'apple', 'cake', 'fish', 'rice'],
      indexNbr: 0
    }
  },
  methods: {
    newImg() {
      this.indexNbr++;
      if(this.indexNbr >= this.imgs.length) {
        this.indexNbr = 0;
      }
      this.imgActive = this.imgs[this.indexNbr];
    }
  }
}
</script>

<style>
  .v-enter-active {
    animation: swirlAdded 1s;
  }
  .v-leave-active {
    animation: swirlAdded 1s reverse;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 360deg;
      scale: 1;
    }
  }
  img {
    width: 100px;
    margin: 20px;
  }
  img:hover {
    cursor: pointer;
  }
</style>
```



## mode="out-in"

ในตัวอย่างด้านบน รูปภาพถัดไปจะถูกเพิ่มก่อนที่รูปภาพก่อนหน้าจะถูกลบออก

เราใช้ mode="out-in" prop และค่า prop บนส่วนประกอบ <Transition> เพื่อให้การลบองค์ประกอบเสร็จสิ้นก่อนที่จะเพิ่มองค์ประกอบถัดไป

### Example

นอกจาก mode="out-in" แล้ว ตัวอย่างนี้ยังใช้ค่าที่คำนวณได้ 'imgActive' แทนเมธอด 'newImg' ที่เราใช้ในตัวอย่างก่อนหน้านี้

##### `App.vue`:

```html
<template>
  <h1>mode="out-in"</h1>
  <p>Click the button to get a new image.</p>
  <p>With mode="out-in", the next image is not added until the current image is removed. Another difference from the previous example, is that here we use computed prop instead of a method.</p>
  <button @click="indexNbr++">Next image</button><br>
  <Transition mode="out-in">
    <img src="/img_pizza.svg" v-if="imgActive === 'pizza'">
    <img src="/img_apple.svg" v-else-if="imgActive === 'apple'">
    <img src="/img_cake.svg" v-else-if="imgActive === 'cake'">
    <img src="/img_fish.svg" v-else-if="imgActive === 'fish'">
    <img src="/img_rice.svg" v-else-if="imgActive === 'rice'">
  </Transition>
</template>

<script>
export default {
  data() {
    return {
      imgs: ['pizza', 'apple', 'cake', 'fish', 'rice'],
      indexNbr: 0
    }
  },
  computed: {
    imgActive() {
      if(this.indexNbr >= this.imgs.length) {
        this.indexNbr = 0;
      }
      return this.imgs[this.indexNbr];
    }
  }
}
</script>

<style>
  .v-enter-active {
    animation: swirlAdded 0.7s;
  }
  .v-leave-active {
    animation: swirlAdded 0.7s reverse;
  }
  @keyframes swirlAdded {
    from {
      opacity: 0;
      rotate: 0;
      scale: 0.1;
    }
    to {
      opacity: 1;
      rotate: 360deg;
      scale: 1;
    }
  }
  img {
    width: 100px;
    margin: 20px;
  }
  img:hover {
    cursor: pointer;
  }
</style>
```



## Transition with Dynamic Components

นอกจากนี้เรายังสามารถใช้ส่วนประกอบ <Transition> เพื่อเคลื่อนไหวการสลับระหว่างส่วนประกอบไดนามิก:

### Example

##### `App.vue`:

```html
<template>
  <h1>Transition with Dynamic Components</h1>
  <p>The Transition component wraps around the dynamic component so that the switching can be animated.</p>
  <button @click="toggleValue = !toggleValue">Switch component</button>
  <Transition mode="out-in">
    <component :is="activeComp"></component>
  </Transition>
</template>

<script>
  export default {
    data () {
      return {
        toggleValue: true
      }
    },
    computed: {
      activeComp() {
        if(this.toggleValue) {
          return 'comp-one'
        }
        else {
          return 'comp-two'
        }
      }
    }
  }
</script>

<style>
  .v-enter-active {
    animation: slideIn 0.5s;
  }
  @keyframes slideIn {
    from {
      translate: -200px 0;
      opacity: 0;
    }
    to {
      translate: 0 0;
      opacity: 1;
    }
  }
  .v-leave-active {
    animation: slideOut 0.5s;
  }
  @keyframes slideOut {
    from {
      translate: 0 0;
      opacity: 1;
    }
    to {
      translate: 200px 0;
      opacity: 0;
    }
  }
  #app {
    width: 350px;
    margin: 10px;
  }
  #app > div {
    border: solid black 2px;
    padding: 10px;
    margin-top: 10px;
  }
</style>
```