# Vue Props

Props คือตัวเลือกการกำหนดค่าใน Vue

ด้วย props เราสามารถส่งข้อมูลไปยังส่วนประกอบต่างๆ ผ่านแอตทริบิวต์ที่กำหนดเองไปยังแท็กส่วนประกอบได้



## ส่งข้อมูลไปยังคอมโพเนนต์

คุณจำตัวอย่างในหน้าก่อนๆ ที่คอมโพเนนต์ทั้งสามพูดว่า 'Apple' ได้ไหม ด้วย props  ตอนนี้เราสามารถส่งข้อมูลไปยังคอมโพเนนต์ของเราเพื่อให้เนื้อหาที่แตกต่างกันและทำให้พวกมันดูแตกต่างออกไป

มาสร้างหน้าง่ายๆ เพื่อแสดง 'แอปเปิ้ล' 'พิซซ่า' และ 'ข้าว'

ในไฟล์แอปพลิเคชันหลัก App.vue เราสร้างแอตทริบิวต์ 'food-name' ของเราเองเพื่อส่งผ่าน prop ด้วยแท็กส่วนประกอบ <food-item/>:

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <food-item food-name="Apples"/>
  <food-item food-name="Pizza"/>
  <food-item food-name="Rice"/>
</template>

<script></script>

<style>
  #app > div {
    border: dashed black 1px;
    display: inline-block;
    width: 120px;
    margin: 10px;
    padding: 10px;
    background-color: lightgreen;
  }
</style>
```



## รับข้อมูลภายในคอมโพเนนต์

ในการรับข้อมูลที่ส่งผ่านแอตทริบิวต์ 'รายการอาหาร' จาก App.vue เราใช้ตัวเลือกการกำหนดค่า 'props ' ใหม่นี้ เราแสดงรายการแอตทริบิวต์ที่ได้รับเพื่อให้ไฟล์คอมโพเนนต์ *.vue ของเราทราบ และตอนนี้เราสามารถใช้ props ได้ทุกที่ที่เราต้องการในลักษณะเดียวกับที่เราใช้คุณสมบัติข้อมูล

##### `FoodItem.vue`:

```html
<script>
  export default {
    props: [
      'foodName'
    ]
  }
</script>
```



คุณลักษณะ props จะเขียนด้วยเครื่องหมายขีดกลาง - เพื่อแยกคำ (kebab-case) ในแท็ก <template> แต่ kebab-case ไม่ถูกกฎหมายใน JavaScript ดังนั้นเราจึงต้องเขียนชื่อแอตทริบิวต์เป็น CamelCase ใน JavaScript แทน และ Vue จะเข้าใจสิ่งนี้โดยอัตโนมัติ!



ในที่สุด ตัวอย่างของเราที่มีองค์ประกอบ <div> สำหรับ 'Apples', 'Pizza' และ 'Rice' มีลักษณะดังนี้:

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <food-item food-name="Apples"/>
  <food-item food-name="Pizza"/>
  <food-item food-name="Rice"/>
</template>
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
    props: [
      'foodName'
    ]
  }
</script>

<style></style>
```

เร็วๆ นี้ เราจะเห็นวิธีการส่งผ่านประเภทข้อมูลที่แตกต่างกันเป็นคุณลักษณะของ props ไปยังคอมโพเนนต์ต่างๆ แต่ก่อนที่เราจะทำเช่นนั้น เรามาขยายโค้ดของเราด้วยคำอธิบายของอาหารแต่ละประเภท และใส่องค์ประกอบ food <div> ไว้ในกระดาษห่อ Flexbox

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <div id="wrapper">
    <food-item
      food-name="Apples"
      food-desc="Apples are a type of fruit that grow on trees."/>
    <food-item
      food-name="Pizza"
      food-desc="Pizza has a bread base with tomato sauce, cheese, and toppings on top."/>
    <food-item
      food-name="Rice"
      food-desc="Rice is a type of grain that people like to eat."/>
  </div>
</template>

<script></script>

<style>
  #wrapper {
    display: flex;
    flex-wrap: wrap;
  }
  #wrapper > div {
    border: dashed black 1px;
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
    <h2>{{ foodName }}</h2>
    <p>{{ foodDesc }}</p>
  </div>
</template>

<script>
  export default {
    props: [
      'foodName',
      'foodDesc'
    ]
  }
</script>

<style></style>
```



## Boolean Props

เราสามารถบรรลุฟังก์ชันการทำงานที่แตกต่างกันได้โดยการส่ง props ประเภทข้อมูลที่แตกต่างกัน และเราสามารถกำหนดกฎสำหรับวิธีการให้แอตทริบิวต์เมื่อส่วนประกอบถูกสร้างขึ้นจาก App.vue

มาเพิ่มเสาใหม่ 'isFavorite' นี่ควรเป็นเสาบูลีนที่มีค่าเป็น true หรือ false เพื่อให้เราสามารถใช้มันโดยตรงกับ v-show เพื่อแสดงแท็ก <img> รายการโปรด หากอาหารนั้นถือเป็นรายการโปรด

หากต้องการส่งผ่าน props ที่มีประเภทข้อมูลแตกต่างจาก String เราต้องเขียน v-bind: ไว้หน้าแอตทริบิวต์ที่เราต้องการส่ง

นี่คือวิธีที่เราส่ง prop 'isFavorite' แบบบูลีนจาก App.vue เป็นแอตทริบิวต์ 'is-favorite':

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <p>My favorite food has a diploma image attached to it.</p>
  <div id="wrapper">
    <food-item
      food-name="Apples"
      food-desc="Apples are a type of fruit that grow on trees."
      v-bind:is-favorite="true"/>
    <food-item
      food-name="Pizza"
      food-desc="Pizza has a bread base with tomato sauce, cheese, and toppings on top."
      v-bind:is-favorite="false"/>
    <food-item
      food-name="Rice"
      food-desc="Rice is a type of grain that people like to eat."
      v-bind:is-favorite="false"/>
  </div>
</template>
```

เราได้รับ boolean 'isFavorite' prop ภายใน FoodItem.vue และแสดงตราประทับรายการโปรดหากอาหารนั้นถือเป็นรายการโปรด:

### Example

##### `FoodItem.vue`:

```html
<template>
  <div>
    <h2>
      {{ foodName }}
      <img src="/img_quality.svg" v-show="isFavorite">
    </h2>
    <p>{{ foodDesc }}</p>
  </div>
</template>

<script>
  export default {
      props: ['foodName','foodDesc','isFavorite']
  }
</script>

<style>
  img {
    height: 1.5em;
    float: right;
  }
</style>
```



รูปภาพ: หากต้องการให้รูปภาพในตัวอย่างด้านบนทำงานในโปรเจ็กต์บนเครื่องของคุณ ให้เปิดตัวอย่างด้านบน คลิกขวาที่รูปภาพ เลือก "บันทึกรูปภาพเป็น..." และบันทึกไว้ในโฟลเดอร์ "สาธารณะ" ในโฟลเดอร์ของคุณ โครงการ.

![img](https://www.w3schools.com/vue/img_save_img_as.png)

![img](https://www.w3schools.com/vue/img_image_path.png)



## Props Interface

ในตัวอย่างข้างต้น จากโค้ดภายใน FoodItem.vue เราไม่สามารถทราบได้อย่างแน่ชัดว่าเราได้รับ Prop 'isFavorite' และเราไม่สามารถทราบได้อย่างแน่ชัดว่าเป็นค่าบูลีนหรือไม่ เพื่อช่วยเราในเรื่องนี้ เราสามารถกำหนดประเภทข้อมูลของ props ที่เราได้รับ เราสามารถตั้งค่า props ที่ต้องการได้ และเรายังสามารถสร้างฟังก์ชันการตรวจสอบความถูกต้องเพื่อตรวจสอบ props ที่เราได้รับได้อีกด้วย

การกำหนด props ที่เราได้รับทำหน้าที่เป็นเอกสารสำหรับบุคคลอื่นหากเราทำงานเป็นทีม และจะให้คำเตือนแก่เราในคอนโซลหากกฎที่เรากำหนดไว้นั้นฝ่าฝืน



## Props as an Object

ใน FoodItem.vue เราจะแสดงความคิดเห็นว่าเรากำหนด props ในอาร์เรย์เพื่อใช้เป็นข้อมูลอ้างอิงได้อย่างไร และกำหนด props ในวัตถุแทน นอกจากนี้เรายังสามารถกำหนดประเภทข้อมูลของแต่ละพร็อพนอกเหนือจากชื่อพร็อพได้ ดังนี้:

##### `FoodItem.vue`:

```html
<script>
  export default {
    // props: ['foodName','foodDesc','isFavorite']
    props: {
      foodName: String,
      foodDesc: String,
      isFavorite: Boolean
    }
  }
</script>
```

ด้วย props ที่กำหนดในลักษณะนี้ บุคคลอื่นจึงสามารถดูภายใน FoodItem.vue และดูว่าคอมโพเนนต์คาดหวังอะไรได้อย่างง่ายดาย

หากคอมโพเนนต์ถูกสร้างขึ้นจากองค์ประกอบหลัก (ในกรณีของเรา App.vue) และกำหนด prop ด้วยประเภทข้อมูลที่ไม่ถูกต้อง คุณจะได้รับคำเตือนในคอนโซล เช่นนี้:

![Screenshot of wrong data type prop warning](https://www.w3schools.com/vue/img_propType.png)

คำเตือนดังกล่าวมีประโยชน์ในการแจ้งให้เราและผู้อื่นทราบว่าส่วนประกอบไม่ได้ใช้อย่างที่ควรจะเป็น และเพื่อบอกว่ามีอะไรผิดปกติเพื่อที่เราจะได้แก้ไขข้อผิดพลาดได้



## Required Props

เพื่อบอก Vue ว่าจำเป็นต้องใช้ prop เราจำเป็นต้องกำหนด prop ให้เป็นวัตถุ มาทำให้พร็อพ 'foodName' จำเป็น แบบนี้:

##### `FoodItem.vue`:

```html
<script>
  export default {
    // props: ['foodName','foodDesc','isFavorite']
    props: {
      foodName: {
        type: String,
        required: true
      },
      foodDesc: String,
      isFavorite: Boolean
    }
  }
</script>
```

หากส่วนประกอบถูกสร้างขึ้นจากองค์ประกอบหลัก (ในกรณีของเรา App.vue) และไม่ได้กำหนด prop ที่ต้องการ คุณจะได้รับคำเตือนในคอนโซล เช่นนี้:

![Screenshot of required prop warning](https://www.w3schools.com/vue/img_propRequired.png)

คำเตือนดังกล่าวมีประโยชน์ในการแจ้งให้เราและผู้อื่นทราบว่าคอมโพเนนต์ไม่ได้ใช้อย่างที่ควรจะเป็น และเพื่อบอกว่ามีอะไรผิดปกติเพื่อที่เราจะได้แก้ไขข้อผิดพลาดได้



## Default Value

เราสามารถตั้งค่าเริ่มต้นสำหรับ prop ได้

มาสร้างค่าเริ่มต้นสำหรับ 'foodDesc' prop ในส่วนประกอบ 'FoodItem' จากนั้นสร้างรายการดังกล่าวสำหรับข้าวโดยไม่ต้องกำหนด 'foodDesc'  prop:

### Example

##### `App.vue`:

```html
<template>
  <h1>Food</h1>
  <p>My favorite food has a diploma image attached to it.</p>
  <div id="wrapper">
    <food-item
      food-name="Apples"
      food-desc="Apples are a type of fruit that grow on trees."
      v-bind:is-favorite="true"/>
    <food-item
      food-name="Pizza"
      food-desc="Pizza has a bread base with tomato sauce, cheese, and toppings on top."
      v-bind:is-favorite="false"/>
    <food-item
      food-name="Rice"
      food-desc="Rice is a type of grain that people like to eat." 
      v-bind:is-favorite="false"/>
  </div>
</template>
```

##### `FoodItem.vue`:

```html
<script>
  export default {
    props: {
      foodName: {
        type: String,
        required: true
      },
      foodDesc: {
        type: String,
        required: false,
        default: 'This is the default description.'
      }
      isFavorite: {
        type: Boolean,
        required: false,
        default: false
      }
    }
  }
</script>
```



## Props Validator Function

นอกจากนี้เรายังสามารถกำหนดฟังก์ชันตรวจสอบความถูกต้องที่จะตัดสินว่าค่า prop นั้นถูกต้องหรือไม่

ฟังก์ชันเครื่องมือตรวจสอบความถูกต้องดังกล่าวจะต้องส่งคืนค่าจริงหรือเท็จ เมื่อเครื่องมือตรวจสอบส่งคืนค่าเท็จ แสดงว่าค่า prop ไม่ถูกต้อง ค่า Prop ที่ไม่ถูกต้องจะสร้างคำเตือนในคอนโซลของเบราว์เซอร์เมื่อเราเรียกใช้เพจในโหมดนักพัฒนาซอฟต์แวร์ และคำเตือนดังกล่าวเป็นคำแนะนำที่มีประโยชน์เพื่อให้แน่ใจว่าส่วนประกอบต่างๆ ถูกใช้ตามที่ตั้งใจไว้

สมมติว่าเราต้องการให้คำอธิบายอาหารมีความยาวระหว่าง 20 ถึง 50 อักขระ เราสามารถเพิ่มฟังก์ชันเครื่องมือตรวจสอบเพื่อให้แน่ใจว่าคำอธิบายอาหารที่ให้มานั้นมีความยาวที่ถูกต้อง

##### `FoodItem.vue`:

```html
<script>
  export default {
    props: {
      foodName: {
        type: String,
        required: true
      },
      foodDesc: {
        type: String,
        required: false,
        default: 'This is the default description.',
        validator: function(value) {
          if( 20<value.length && value.length<50 ) {
            return true;
          }
          else {
            return false;
          }
        }
      }
      isFavorite: {
        type: Boolean,
        required: false,
        default: false
      }
    }
  }
</script>
```

หมายเหตุ: หากคุณเพิ่มโค้ดเครื่องมือตรวจสอบด้านบนให้กับโปรเจ็กต์ในพื้นที่ของคุณ คุณจะได้รับคำเตือนในโหมดการพัฒนาเนื่องจากคำอธิบายอาหารสำหรับพิซซ่ามีความยาว 65 อักขระ ซึ่งยาวกว่าที่ฟังก์ชันเครื่องมือตรวจสอบอนุญาตจะมีความยาว 15 อักขระ

![img](https://www.w3schools.com/vue/img_validator_warning.png)



## Modify Props

เมื่อส่วนประกอบถูกสร้างขึ้นในองค์ประกอบหลัก เราจะไม่ได้รับอนุญาตให้เปลี่ยนค่าของ Prop ที่ได้รับในองค์ประกอบลูก ดังนั้นภายใน FoodItem.vue เราไม่สามารถเปลี่ยนค่าของ 'isFavorite' Prop ที่เราได้รับจาก App.vue ได้ Prop เป็นแบบอ่านอย่างเดียวจากพาเรนต์ ซึ่งก็คือ App.vue ในกรณีของเรา

แต่สมมติว่าเราต้องการให้ผู้ใช้สามารถเปลี่ยนอาหารที่ถือว่าเป็นอาหารจานโปรดได้ด้วยการคลิกปุ่ม ขณะนี้มีความจำเป็นต้องเปลี่ยน 'isFavorite' Prop แต่เราไม่สามารถทำได้เนื่องจากเป็นแบบอ่านอย่างเดียว



เราไม่ได้รับอนุญาตให้เปลี่ยน 'isFavorite' สิ่งนี้จะทำให้เกิดข้อผิดพลาด

```js
methods: {
  toggleFavorite() { 
    this.isFavorite = !this.isFavorite;
  }
}
```

เพื่อแก้ไขปัญหานี้ เราสามารถใช้ prop เพื่อเริ่มต้นค่าข้อมูลใหม่ 'foodIsFavorite' ภายใน FoodItem.vue เช่นนี้

```js
data() {
  return { 
    foodIsFavorite: this.isFavorite
  }
}
```

และตอนนี้เราสามารถเพิ่มวิธีการเพื่อให้ผู้ใช้สามารถสลับค่าข้อมูลใหม่นี้ได้:

```js
methods: {
  toggleFavorite() { 
    this.foodIsFavorite = !this.foodIsFavorite;
  }
}
```

เรายังต้องเพิ่มปุ่มสลับให้กับรายการอาหารแต่ละรายการ และเปลี่ยน v-show ในแท็ก <img> ให้ขึ้นอยู่กับคุณสมบัติข้อมูลใหม่ 'foodIsFavorite' และเพื่อทำให้ตัวอย่างของเราง่ายขึ้น เรายังลดขนาดการประกาศ Props ให้เหลือเพียงอาร์เรย์ด้วย

### Example

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