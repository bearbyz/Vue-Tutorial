# Vue Animations with v-for

ส่วนประกอบ <TransitionGroup> ในตัวใน Vue ช่วยให้เราสร้างภาพเคลื่อนไหวองค์ประกอบที่เพิ่มลงในเพจของเราด้วย v-for



## The <TransitionGroup> Component

คอมโพเนนต์ <TransitionGroup> ถูกใช้รอบๆ องค์ประกอบที่สร้างด้วย v-for เพื่อให้องค์ประกอบเหล่านี้มีภาพเคลื่อนไหวแต่ละรายการเมื่อมีการเพิ่มหรือลบออก

แท็กที่สร้างด้วย v-for ภายในคอมโพเนนต์ <TransitionGroup> จะต้องถูกกำหนดด้วยแอตทริบิวต์คีย์

ส่วนประกอบ <TransitionGroup> จะแสดงผลเป็นแท็ก HTML เท่านั้นหากเรากำหนดให้เป็นแท็กเฉพาะโดยใช้แท็ก prop เช่นนี้

```html
<TransitionGroup tag="ol">
  <li v-for="x in products" :key="x">
    {{ x }}
  </li>
</TransitionGroup>
```

นี่เป็นผลลัพธ์จากโค้ดด้านบน หลังจากที่ Vue แสดงผลแล้ว:

```html
<ol>
  <li>Apple</li>
  <li>Pizza</li>
  <li>Rice</li>
</ol>
```

ขณะนี้เราสามารถเพิ่มโค้ด CSS เพื่อทำให้รายการใหม่เคลื่อนไหวได้เมื่อมีการเพิ่มลงในรายการ:

```html
<style>
  .v-enter-from {
    opacity: 0;
    rotate: 180deg;
  }
  .v-enter-to {
    opacity: 1;
    rotate: 0deg;
  }
  .v-enter-active {
    transition: all 0.7s;
  }
</style>
```

ในตัวอย่างนี้ รายการใหม่จะเคลื่อนไหวได้โดยการเพิ่มลงในอาร์เรย์ 'ผลิตภัณฑ์':

### Example

##### `App.vue`:

```html
<template>
  <h3>The <TransitionGroup> Component</h3>
  <p>New products are given animations using the <TransitionGroup> component.</p>
  <input type="text" v-model="inpName"> 
  <button @click="addEl">Add</button>
  <TransitionGroup tag="ol">
    <li v-for="x in products" :key="x">
      {{ x }}
    </li>
  </TransitionGroup>
</template>

<script>
  export default {
    data() {
      return {
        products: ['Apple','Pizza','Rice'],
        inpName: ''
      }
    },
    methods: {
      addEl() {
        const el = this.inpName;
        this.products.push(el);
        this.inpName = null;
      }
    }
  }
</script>

<style>
  .v-enter-from {
    opacity: 0;
    rotate: 180deg;
  }
  .v-enter-to {
    opacity: 1;
    rotate: 0deg;
  }
  .v-enter-active {
    transition: all 0.7s;
  }
</style>
```



## Add and Remove Elements

เมื่อลบองค์ประกอบที่อยู่ระหว่างองค์ประกอบอื่น องค์ประกอบอื่นๆ จะตกอยู่ในตำแหน่งที่มีองค์ประกอบที่ถูกลบออก ในการสร้างภาพเคลื่อนไหวให้กับรายการที่เหลือเมื่อองค์ประกอบถูกลบออก เราจะใช้คลาส v-move ที่สร้างขึ้นโดยอัตโนมัติ

แต่ก่อนอื่น เรามาดูตัวอย่างที่ไม่มีภาพเคลื่อนไหวว่ารายการอื่นเข้าที่เมื่อองค์ประกอบถูกลบออกอย่างไร:

### Example

#### `App.vue`:

```html
<template>
  <h3>The <TransitionGroup> Component</h3>
  <p>New products are given animations using the <TransitionGroup> component.</p>
  <button @click="addDie">Roll</button>
  <button @click="removeDie">Remove random</button><br>
  <TransitionGroup>
    <div v-for="x in dice" :key="x" class="diceDiv" :style="{ backgroundColor: 'hsl('+x*40+',85%,85%)' }">
      {{ x }}
    </div>
  </TransitionGroup>
</template>

<script>
  export default {
    data() {
      return {
        dice: [],
        inpName: ''
      }
    },
    methods: {
      addDie() {
        const newDie = Math.ceil(Math.random()*6);
        this.dice.push(newDie);
      },
      removeDie() {
        if(this.dice.length>0){
          this.dice.splice(Math.floor(Math.random()*this.dice.length), 1);
        }
      }
    },
    mounted() {
      this.addDie();
      this.addDie();
      this.addDie();
    }
  }
</script>

<style>
.v-enter-from {
  opacity: 0;
  translate: 200px 0;
  rotate: 360deg;
}
.v-enter-to {
  opacity: 1;
  translate: 0 0;
  rotate: 0deg;
}
.v-enter-active,
.v-leave-active {
  transition: all 0.7s;
}
.v-leave-from { opacity: 1; }
.v-leave-to { opacity: 0; }
.diceDiv {
  margin: 10px;
  width: 30px;
  height: 30px;
  line-height: 30px;
  vertical-align: middle;
  text-align: center;
  border: solid black 1px;
  border-radius: 5px;
  display: inline-block;
}
</style>
```

ดังที่คุณเห็นในตัวอย่างด้านบน เมื่อรายการถูกลบออก รายการที่อยู่หลังรายการที่ถูกลบจะกระโดดเข้าสู่ตำแหน่งใหม่ทันที หากต้องการทำให้รายการที่เหลือเคลื่อนไหวเมื่อรายการถูกลบออก เราจะใช้คลาส v-move ที่สร้างขึ้นโดยอัตโนมัติ

คลาส v-move จะทำให้องค์ประกอบอื่นๆ เคลื่อนไหวเมื่อไอเท็มที่ถูกลบออกไป แต่มีปัญหาหนึ่งคือ ไอเท็มที่ถูกลบยังคงมีอยู่และเกิดขึ้นจนกว่าจะถูกลบออก ดังนั้นคลาส v-move จะไม่มีผลกระทบใดๆ เพื่อให้คลาส v-move เคลื่อนไหว เราสามารถกำหนดตำแหน่ง: สัมบูรณ์; ไปที่คลาส v-leave-active เมื่อตำแหน่ง: แน่นอน; ถูกตั้งค่าไว้ในช่วงระยะเวลาการลบออก รายการที่ลบออกยังคงมองเห็นได้ แต่ไม่เกิดขึ้น

ในตัวอย่างนี้ ข้อแตกต่างเพียงอย่างเดียวจากตัวอย่างก่อนหน้านี้คือคลาส CSS ใหม่สองคลาสที่เพิ่มในบรรทัดที่ 14 และ 17:

### Example

##### `App.vue`:

```html
<style>
.v-enter-from {
  opacity: 0;
  translate: 200px 0;
  rotate: 360deg;
}
.v-enter-to {
  opacity: 1;
  translate: 0 0;
  rotate: 0deg;
}
.v-enter-active,
.v-leave-active,
.v-move {
  transition: all 0.7s;
}
.v-leave-active { position: absolute; }
.v-leave-from { opacity: 1; }
.v-leave-to { opacity: 0; }
.diceDiv {
  margin: 10px;
  width: 30px;
  height: 30px;
  line-height: 30px;
  vertical-align: middle;
  text-align: center;
  border: solid black 1px;
  border-radius: 5px;
  display: inline-block;
}
</style>
```



## A Larger Example

ลองใช้ตัวอย่างข้างต้นเป็นพื้นฐานสำหรับตัวอย่างใหม่

ในตัวอย่างนี้ จะยิ่งชัดเจนยิ่งขึ้นว่ารายการทั้งหมดเคลื่อนไหวอย่างไรเมื่อมีการเพิ่มหรือลบรายการใหม่ หรือเมื่อมีการเรียงลำดับทั้งอาร์เรย์

ในตัวอย่างนี้เราสามารถ:

- ลบรายการโดยคลิกที่รายการเหล่านั้น
- จัดเรียงรายการ
- เพิ่มรายการใหม่ในตำแหน่งสุ่มในรายการ

### Example

##### `App.vue`:

```html
<template>
  <h3>The <TransitionGroup> Component</h3>
  <p>Items inside the <TransitionGroup> component are animated when they are created or removed.</p>
  <button @click="addDie">Roll</button>
  <button @click="addDie10">Roll 10 dice</button>
  <button @click="dice.sort(compareFunc)">Sort</button>
  <button @click="dice.sort(shuffleFunc)">Shuffle</button><br>
  <TransitionGroup>
    <div 
    v-for="x in dice" 
    :key="x.keyNmbr" 
    class="diceDiv" 
    :style="{ backgroundColor: 'hsl('+x.dieNmbr*60+',85%,85%)' }"
    @click="removeDie(x.keyNmbr)">
      {{ x.dieNmbr }}
    </div>
  </TransitionGroup>
</template>

<script>
  export default {
    data() {
      return {
        dice: [],
        keyNumber: 0
      }
    },
    methods: {
      addDie() {
        const newDie = {
          dieNmbr: Math.ceil(Math.random()*6),
          keyNmbr: this.keyNumber
        };
        this.dice.splice(Math.floor(Math.random()*this.dice.length),0,newDie);
        this.keyNumber++;
      },
      addDie10() {
        for(let i=0; i<10; i++) {
          this.addDie();
        }
      },
      compareFunc(a,b){
        return a.dieNmbr - b.dieNmbr;
      },
      shuffleFunc(a,b){
        return Math.random()-0.5;
      },
      removeDie(key) {
        const pos = this.dice.map(e => e.keyNmbr).indexOf(key);
        this.dice.splice(pos, 1);
      }
    },
    mounted() {
      this.addDie10();
    }
  }
</script>

<style>
.v-enter-from {
  opacity: 0;
  scale: 0;
  rotate: 360deg;
}
.v-enter-to {
  opacity: 1;
  scale: 1;
  rotate: 0deg;
}
.v-enter-active,
.v-leave-active,
.v-move {
  transition: all 0.7s;
}
.v-leave-active { position: absolute; }
.v-leave-from { opacity: 1; }
.v-leave-to { opacity: 0; }
.diceDiv {
  margin: 10px;
  width: 30px;
  height: 30px;
  line-height: 30px;
  vertical-align: middle;
  text-align: center;
  border: solid black 1px;
  border-radius: 5px;
  display: inline-block;
}
.diceDiv:hover {
  cursor: pointer;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
#app {
  position: relative;
}
</style>
```