# Scoped Slots

ช่องที่กำหนดขอบเขตจะให้ข้อมูลในเครื่องจากคอมโพเนนต์เพื่อให้พาเรนต์สามารถเลือกวิธีแสดงผลได้



## Send Data to Parent

เราใช้ v-bind ในช่องคอมโพเนนต์เพื่อส่งข้อมูลในตัวเครื่องไปยังพาเรนต์:

##### `SlotComp.vue`:

```html
<template>
  <slot v-bind:lclData="data"></slot>
</template>

<script>
  export default {
    data() {
      return {
        data: 'This is local data'
      }
    }
  }
</script>
```

ข้อมูลภายในคอมโพเนนต์สามารถเรียกได้ว่าเป็น 'ท้องถิ่น' เพราะไม่สามารถเข้าถึงได้โดยผู้ปกครองเว้นแต่จะถูกส่งถึงผู้ปกครองเหมือนที่เราทำที่นี่ด้วย v-bind



## Receive Data from Scoped Slot

ข้อมูลในเครื่องในคอมโพเนนต์จะถูกส่งด้วย v-bind และสามารถรับได้ในพาเรนต์ด้วย v-slot:

### Example

##### `App.vue`:

```html
<slot-comp v-slot:"dataFromSlot">
  <h2>{{ dataFromSlot.lclData }}</h2>
</slot-comp>
```

ในตัวอย่างด้านบน 'dataFromSlot' เป็นเพียงชื่อที่เราสามารถเลือกเองเพื่อแสดงออบเจ็กต์ข้อมูลที่เราได้รับจากช่องที่กำหนดขอบเขต เราได้รับสตริงข้อความจากช่องโดยใช้คุณสมบัติ 'lclData' และเราใช้การแก้ไขเพื่อแสดงข้อความในแท็ก <h2> ในที่สุด



## Scoped Slot with an Array

ช่องที่กำหนดขอบเขตสามารถส่งข้อมูลจากอาร์เรย์ได้โดยใช้ v-for แต่โค้ดใน App.vue โดยพื้นฐานแล้วจะเหมือนกัน:

### Example

##### `SlotComp.vue`:

```html
<template>
  <slot
    v-for="x in foods"
    :key="x"
    :foodName="x"
  ></slot>
</template>

<script>
  export default {
    data() {
      return {
        foods: ['Apple','Pizza','Rice','Fish','Cake']
      }
    }
  }
</script>
```

##### `App.vue`:

```html
<slot-comp v-slot="food">
  <h2>{{ food.foodName }}</h2>
</slot-comp>
```



## Scoped Slot with an Array of Objects

ช่องที่กำหนดขอบเขตสามารถส่งข้อมูลจากอาร์เรย์ของวัตถุได้โดยใช้ v-for:

### Example

##### `SlotComp.vue`:

```html
<template>
  <slot
    v-for="x in foods"
    :key="x.name"
    :foodName="x.name"
    :foodDesc="x.desc"
    :foodUrl="x.url"
  ></slot>
</template>

<script>
  export default {
    data() {
      return {
        foods: [
          { name: 'Apple', desc: 'Apples are a type of fruit that grow on trees.', url: 'img_apple.svg' },
          { name: 'Pizza', desc: 'Pizza has a bread base with tomato sauce, cheese, and toppings on top.', url: 'img_pizza.svg' },
          { name: 'Rice', desc: 'Rice is a type of grain that people like to eat.', url: 'img_rice.svg' },
          { name: 'Fish', desc: 'Fish is an animal that lives in water.', url: 'img_fish.svg' },
          { name: 'Cake', desc: 'Cake is something sweet that tastes good but is not considered healthy.', url: 'img_cake.svg' }
       ]
      }
    }
  }
</script>
```

##### `App.vue`:

```html
<slot-comp v-slot="food">
  <hr>
  <h2>{{ food.foodName }}<img :src=food.foodUrl></h2>
  <p>{{ food.foodDesc }}</p>
</slot-comp>
```



## Static Data from a Scoped Slot

scoped slot ยังสามารถส่งข้อมูลคงที่ ซึ่งเป็นข้อมูลที่ไม่ได้อยู่ในคุณสมบัติข้อมูลของอินสแตนซ์ Vue

เมื่อส่งข้อมูลคงที่ เราจะไม่ใช้ v-bind

ในตัวอย่างด้านล่าง เราส่งข้อความคงที่หนึ่งข้อความ และข้อความหนึ่งเชื่อมโยงกับอินสแตนซ์ข้อมูลแบบไดนามิก เพื่อให้เราได้เห็นความแตกต่าง

### Example

##### `SlotComp.vue`:

```html
<template>
  <slot
    staticText="This text is static"
    :dynamicText="text"
  ></slot>
</template>

<script>
  export default {
    data() {
      return {
        text: 'This text is from the data property'
      }
    }
  }
</script>
```

##### `App.vue`:

```html
<slot-comp v-slot="texts">
  <h2>{{ texts.staticText }}</h2>
  <p>{{ texts.dynamicText }}</p>
</slot-comp>
```



## Named Scoped Slots

สามารถตั้งชื่อ Scoped slots ได้

หากต้องการใช้ชื่อ Scoped slots เราจำเป็นต้องตั้งชื่อ slots ภายในส่วนประกอบด้วยแอตทริบิวต์ 'name'

และในการรับข้อมูลจาก slots ที่มีชื่อ เราจำเป็นต้องอ้างอิงถึงชื่อนั้นในพาเรนต์ที่เราใช้ส่วนประกอบ โดยมีคำสั่ง v-slot หรือตัวย่อ #

### Example

ในตัวอย่างนี้ คอมโพเนนต์จะถูกสร้างขึ้นหนึ่งครั้งโดยอ้างอิงถึงช่อง "leftSlot" และอีกครั้งอ้างอิงถึงช่อง "rightSlot"

##### `SlotComp.vue`:

```html
<template>
  <slot
    name="leftSlot"
    :text="leftText"
  ></slot>
  <slot
    name="rightSlot"
    :text="rightText"
  ></slot>
</template>

<script>
  export default {
    data() {
      return {
        leftText: 'This text belongs to the LEFT slot.',
        rightText: 'This text belongs to the RIGHT slot.'
      }
    }
  }
</script>
```

##### `App.vue`:

```html
<slot-comp #leftSlot="leftProps">
  <div>{{ leftProps.text }}</div>
</slot-comp>
<slot-comp #rightSlot="rightProps">
  <div>{{ rightProps.text }}</div>
</slot-comp>
```

อีกทางหนึ่ง เราสามารถสร้างคอมโพเนนต์ได้ครั้งเดียวโดยใช้แท็ก "เทมเพลต" สองแท็กที่แตกต่างกัน โดยแต่ละแท็ก "เทมเพลต" อ้างอิงถึงช่องที่แตกต่างกัน

### Example

ในตัวอย่างนี้ คอมโพเนนต์ถูกสร้างขึ้นเพียงครั้งเดียว แต่มีแท็ก "เทมเพลต" สองแท็ก โดยแต่ละแท็กอ้างอิงถึงช่องที่แตกต่างกัน

SlotComp.vue เหมือนกับในตัวอย่างก่อนหน้านี้ทุกประการ

##### `App.vue`:

```html
<slot-comp>

  <template #leftSlot="leftProps">
    <div>{{ leftProps.text }}</div>
  </template>

  <template #rightSlot="rightProps">
    <div>{{ rightProps.text }}</div>
  </template>

</slot-comp>
```