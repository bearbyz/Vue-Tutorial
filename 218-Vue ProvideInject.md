# Vue Provide/Inject

**Provide/Inject** ใน Vue ใช้เพื่อจัดเตรียมข้อมูลจากคอมโพเนนต์หนึ่งไปยังคอมโพเนนต์อื่น ๆ โดยเฉพาะในโปรเจ็กต์ขนาดใหญ่

**Provide** ทำให้ข้อมูลพร้อมใช้งานสำหรับส่วนประกอบอื่น ๆ

**Inject** ใช้เพื่อรับข้อมูลที่ให้มา

**Provide/Inject** เป็นวิธีหนึ่งในการแบ่งปันข้อมูลเป็นทางเลือกในการส่งข้อมูลโดยใช้อุปกรณ์ประกอบฉาก



## Provide/Inject

ในโปรเจ็กต์ขนาดใหญ่ที่มีส่วนประกอบอยู่ภายในส่วนประกอบ อาจเป็นเรื่องยากที่จะใช้อุปกรณ์ประกอบฉากเพื่อจัดเตรียมข้อมูลจาก "App.vue" ไปยังส่วนประกอบย่อย เนื่องจากต้องมีการกำหนดอุปกรณ์ประกอบฉากในทุกองค์ประกอบที่ข้อมูลส่งผ่าน

หากเราใช้ Provide/Inject แทน Props เราเพียงแต่ต้องกำหนดข้อมูลที่ให้มาในตำแหน่งที่มันถูกจัดเตรียมไว้ และเราจำเป็นต้องกำหนดเฉพาะข้อมูลที่แทรกในตำแหน่งที่มันถูกฉีดเท่านั้น



## Provide Data

เราใช้ตัวเลือกการกำหนดค่า 'provide' เพื่อให้ข้อมูลพร้อมใช้งานสำหรับส่วนประกอบอื่นๆ:

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <div @click="this.activeComp = 'food-about'" class="divBtn">About</div>
  <div @click="this.activeComp = 'food-kinds'" class="divBtn">Kinds</div>
  <div id="divComp">
    <component :is="activeComp"></component>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: 'food-about',
      foods: [
        { name: 'Pizza', imgUrl: '/img_pizza.svg' },
        { name: 'Apple', imgUrl: '/img_apple.svg' },
        { name: 'Cake', imgUrl: '/img_cake.svg' },
        { name: 'Fish', imgUrl: '/img_fish.svg' },
        { name: 'Rice', imgUrl: '/img_rice.svg' }
      ]
    }
  },
  provide() {
    return {
      foods: this.foods
    }
  }
}
</script>
```

ในโค้ดด้านบน ตอนนี้อาร์เรย์ 'foods' ได้รับการจัดเตรียมไว้แล้ว เพื่อให้พร้อมสำหรับการฉีดเข้าไปในส่วนประกอบอื่นๆ ในโครงการของคุณ



## Inject Data

ตอนนี้อาร์เรย์ 'foods' พร้อมใช้งานโดย 'provide' ใน 'App.vue' แล้ว เราก็สามารถรวมไว้ในองค์ประกอบ 'FoodKinds' ได้

ด้วยการฉีดข้อมูล 'foods' ในส่วนประกอบ 'FoodKinds' เราสามารถใช้ข้อมูลจาก App.vue เพื่อแสดงอาหารที่แตกต่างกันในส่วนประกอบ 'FoodKinds':

### Example

##### `FoodKinds.vue`:

```html
<template>
    <h2>Different Kinds of Food</h2>
    <p><mark>In this application, food data is provided in "App.vue", and injected in the "FoodKinds.vue" component so that it can be shown here:</mark></p>
    <div v-for="x in foods">
        <img :src="x.imgUrl">
        <p class="pName">{{ x.name }}</p>
    </div>
</template>

<script>
export default {
    inject: ['foods']
}
</script>

<style scoped>
    div {
        margin: 10px;
        padding: 10px;
        display: inline-block;
        width: 80px;
        background-color: #28e49f47;
        border-radius: 10px;
    }
    .pName {
        text-align: center;
    }
    img {
        width: 100%;
    }
</style>
```