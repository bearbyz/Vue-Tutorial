# Vue v-for Components

คอมโพเนนต์ต่างๆ สามารถนำมาใช้ซ้ำได้ด้วย v-for เพื่อสร้างองค์ประกอบหลายๆ รายการที่เป็นประเภทเดียวกัน

เมื่อสร้างคอมโพเนนต์ด้วย v-for จากคอมโพเนนต์ จะมีประโยชน์มากเช่นกันที่สามารถกำหนดอุปกรณ์ประกอบฉากแบบไดนามิกตามค่าจากอาร์เรย์ได้



## Create Component Elements with v-for

ตอนนี้เราจะสร้างองค์ประกอบคอมโพเนนต์ด้วย v-for ตามอาร์เรย์ที่มีชื่อรายการอาหาร

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <p>Components created with v-for based on an array.</p>
  <div id="wrapper">
    <food-item
      v-for="x in foods"
      v-bind:food-name="x"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        foods: ['Apples','Pizza','Rice','Fish','Cake']
      };
    }
  }
</script>
```

##### `FoodItem.vue`:

```html
<template>
  <div>
    <h2>{{ foodName }}</h2>
  </div>
</template>

<script>
  export default {
    props: ['foodName']
  }
</script>
```



## v-bind Shorthand

ในการผูก props แบบไดนามิก เราใช้ v-bind และเนื่องจากเราจะใช้ v-bind มากกว่าเมื่อก่อนมาก เราจะใช้ v-bind: shorthand **:** ในส่วนที่เหลือของบทช่วยสอนนี้



## The 'key' Attribute

หากเราแก้ไขอาร์เรย์หลังจากสร้างองค์ประกอบด้วย v-for ข้อผิดพลาดอาจเกิดขึ้นได้เนื่องจากวิธีที่ Vue อัปเดตองค์ประกอบดังกล่าวที่สร้างด้วย v-for Vue นำองค์ประกอบกลับมาใช้ใหม่เพื่อเพิ่มประสิทธิภาพ ดังนั้นหากเราลบรายการหนึ่งออก องค์ประกอบที่มีอยู่แล้วจะถูกนำมาใช้ซ้ำแทนที่จะสร้างองค์ประกอบทั้งหมดขึ้นใหม่ และคุณสมบัติขององค์ประกอบอาจไม่ถูกต้องอีกต่อไป

เหตุผลที่องค์ประกอบต่างๆ ถูกนำมาใช้ซ้ำอย่างไม่ถูกต้องก็คือ องค์ประกอบต่างๆ ไม่มีตัวระบุที่ไม่ซ้ำกัน และนั่นคือสิ่งที่เราใช้แอตทริบิวต์คีย์สำหรับ: เพื่อให้ Vue แยกองค์ประกอบต่างๆ

เราจะสร้างพฤติกรรมที่ผิดพลาดโดยไม่มีแอตทริบิวต์หลัก แต่ก่อนอื่นเรามาสร้างหน้าเว็บที่มีอาหารโดยใช้ v-for เพื่อแสดง: ชื่ออาหาร คำอธิบาย รูปภาพของอาหารโปรด และปุ่มเพื่อเปลี่ยนสถานะรายการโปรด

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <p>Food items are generated with v-for from the 'foods' array.</p>
  <div id="wrapper">
    <food-item
      v-for="x in foods"
      :food-name="x.name"
      :food-desc="x.desc"
      :is-favorite="x.favorite"/>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        foods: [
          { name: 'Apples',
            desc: 'Apples are a type of fruit that grow on trees.',
            favorite: true },
          { name: 'Pizza',
            desc: 'Pizza has a bread base with tomato sauce, cheese, and toppings on top.',
            favorite: false },
          { name: 'Rice',
            desc: 'Rice is a type of grain that people like to eat.',
            favorite: false }
          { name: 'Fish',
            desc: 'Fish is an animal that lives in water.',
            favorite: true }
          { name: 'Cake',
            desc: 'Cake is something sweet that tastes good.',
            favorite: false }
        ]
      };
    }
  }
</script>

<style>
  #wrapper {
    display: flex;
    flex-wrap: wrap;
  }
  #wrapper > div {
    border: dashed black 1px;
    flex-basis: 120px;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
</style>
```

##### `FoodItem.vue`:

```html
<template>
  <div>
    <h2>
      {{ foodName }}
      <img src="/img_quality.svg" v-show="foodIsFavorite">
    </h2>
    <p>{{ foodDesc }}</p>
    <button v-on:click="toggleFavorite">Favorite</button>
  </div>
</template>

<script>
  export default {
    props: ['foodName','foodDesc','isFavorite'],
    data() {
      return {
        foodIsFavorite: this.isFavorite
      }
    },
    methods: {
      toggleFavorite() {
        this.foodIsFavorite = !this.foodIsFavorite;
      }
    }
  }
</script>

<style>
  img {
    height: 1.5em;
    float: right;
  }
</style>
```

หากต้องการดูว่าเราต้องการแอตทริบิวต์คีย์ เรามาสร้างปุ่มที่จะลบองค์ประกอบที่สองในอาร์เรย์ เมื่อสิ่งนี้เกิดขึ้น หากไม่มีแอตทริบิวต์หลัก รูปภาพโปรดจะถูกโอนจากองค์ประกอบ 'Fish' ไปยังองค์ประกอบ 'Cake' และนั่นไม่ถูกต้อง:

### Example

ความแตกต่างเพียงอย่างเดียวจากตัวอย่างก่อนหน้านี้คือเราเพิ่มปุ่ม:

```html
<button @click="removeItem">Remove Item</button>
```

และเมธอด:

```js
methods: {
  removeItem() {
    this.foods.splice(1,1);
  }
}
```

ใน App.vue



ดังที่กล่าวไว้ก่อนหน้านี้: ข้อผิดพลาดนี้ ซึ่งรูปภาพโปรดเปลี่ยนจาก 'fish' เป็น 'cake' เมื่อองค์ประกอบถูกลบออก เกี่ยวข้องกับการที่ Vue เพิ่มประสิทธิภาพเพจด้วยการนำองค์ประกอบกลับมาใช้ใหม่ และในขณะเดียวกัน Vue ก็ไม่สามารถแยกองค์ประกอบออกจากกันได้อย่างสมบูรณ์ . นั่นคือเหตุผลที่เราควรรวมแอตทริบิวต์หลักไว้เสมอเพื่อทำเครื่องหมายแต่ละองค์ประกอบโดยไม่ซ้ำกันเมื่อสร้างองค์ประกอบด้วย v-for เมื่อเราใช้แอตทริบิวต์คีย์ เราจะไม่พบปัญหานี้อีกต่อไป

เราไม่ใช้ดัชนีองค์ประกอบอาร์เรย์เป็นค่าแอตทริบิวต์หลักเนื่องจากจะเปลี่ยนแปลงเมื่อองค์ประกอบอาร์เรย์ถูกลบและเพิ่ม เราสามารถสร้างคุณสมบัติข้อมูลใหม่เพื่อเก็บค่าที่ไม่ซ้ำกันสำหรับแต่ละรายการ เช่น หมายเลข ID แต่เนื่องจากรายการอาหารมีชื่อที่ไม่ซ้ำกันอยู่แล้ว เราจึงใช้สิ่งนั้นได้:

### Example

เราจำเป็นต้องเพิ่มหนึ่งบรรทัดใน App.vue เพื่อระบุแต่ละองค์ประกอบที่สร้างด้วย v-for โดยไม่ซ้ำกันและแก้ไขปัญหา:

```html
<food-item
  v-for="x in foods"
  :key="x.name"
  :food-name="x.name"
  :food-desc="x.desc"
  :is-favorite="x.favorite"
/>
```