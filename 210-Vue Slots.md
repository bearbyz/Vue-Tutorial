# Vue Slots

Slots เป็นคุณสมบัติที่ทรงพลังใน Vue ที่ช่วยให้ส่วนประกอบมีความยืดหยุ่นและนำกลับมาใช้ใหม่ได้มากขึ้น

เราใช้ช่องใน Vue เพื่อส่งเนื้อหาจากพาเรนต์ไปยัง <template> ของคอมโพเนนต์ลูก



## Slots

จนถึงตอนนี้ เราเพิ่งใช้ส่วนประกอบภายใน <template> เป็นแท็กปิดตัวเองดังนี้:

##### `App.vue`:

```html
<template>
  <slot-comp />
</template>
```

แต่เราสามารถใช้แท็กเปิดและปิด และใส่เนื้อหาบางส่วนไว้ข้างในได้ เช่น ข้อความ:

##### `App.vue`:

```html
<template>
  <slot-comp>Hello World!</slot-comp>
</template>
```

แต่จะได้รับ 'Hello World!' ภายในคอมโพเนนต์และแสดงบนหน้าของเรา เราจำเป็นต้องใช้แท็ก <slot> ภายในคอมโพเนนต์ แท็ก <slot> ทำหน้าที่เป็นตัวยึดตำแหน่งสำหรับเนื้อหา ดังนั้นหลังจากสร้างแอปพลิเคชันแล้ว <slot> จะถูกแทนที่ด้วยเนื้อหาที่ส่งไป

### Example

##### `SlotComp.vue`:

```html
<template>
  <div>  
    <p>SlotComp.vue</p>
    <slot></slot>
  </div>
</template>
```



## Slots as Cards

Slots ยังสามารถใช้เพื่อพันเนื้อหา HTML ไดนามิกขนาดใหญ่เพื่อให้มีลักษณะเหมือนการ์ด

ก่อนหน้านี้เราได้ส่งข้อมูลเป็น props เพื่อสร้างเนื้อหาภายในคอมโพเนนต์ ตอนนี้เราสามารถส่งเนื้อหา HTML ได้โดยตรงภายในแท็ก <slot> เหมือนเดิม

### Example

##### `App.vue`:

```html
<template>
  <h3>Slots in Vue</h3>  
  <p>We create card-like div boxes from the foods array.</p>
  <div id="wrapper">
    <slot-comp v-for="x in foods">
      <img v-bind:src="x.url">
      <h4>{{x.name}}</h4>
      <p>{{x.desc}}</p>
    </slot-comp>
  </div>
</template>
```

เมื่อเนื้อหาเข้าสู่องค์ประกอบที่มี <slot> อยู่ เราจะใช้ div รอบ <slot> และจัดรูปแบบ <div> ในเครื่องเพื่อสร้างลักษณะที่เหมือนการ์ดรอบๆ เนื้อหา โดยไม่ส่งผลกระทบต่อ div อื่นๆ ในแอปพลิเคชันของเรา

##### `SlotComp.vue`:

```html
<template>
  <div> <!-- This div makes the card-like appearance -->
    <slot></slot>
  </div>
</template>

<script></script>

<style scoped>
  div {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    border-radius: 10px;
    margin: 10px;
  }
</style>
```

คอมโพเนนต์ที่สร้างกรอบคล้ายการ์ดรอบๆ เนื้อหาสามารถนำมาใช้ซ้ำเพื่อสร้างคอมโพเนนต์ต่างๆ ได้ แต่มีกรอบเหมือนการ์ดเดียวกันรอบๆ

ในตัวอย่างนี้ เราใช้คอมโพเนนต์เดียวกันกับรายการอาหารเพื่อสร้างส่วนท้าย

### Example

##### `App.vue`:

```html
<template>
  <h3>Reusable Slot Cards</h3>
  <p>We create card-like div boxes from the foods array.</p>
  <p>We also create a card-like footer by reusing the same component.</p>
  <div id="wrapper">
    <slot-comp v-for="x in foods">
      <img v-bind:src="x.url">
      <h4>{{x.name}}</h4>
    </slot-comp>
  </div>
  <footer>
    <slot-comp>
      <h4>Footer</h4>
    </slot-comp>
  </footer>
</template>
```



## Fallback Content

หากคอมโพเนนต์ถูกสร้างขึ้นโดยไม่มีเนื้อหา เราสามารถมีเนื้อหาทางเลือกใน <slot>

### Example

ส่วนประกอบแรกในแอปพลิเคชันนี้ไม่มีเนื้อหาที่ให้ไว้ ดังนั้นจึงมีการแสดงผลเนื้อหาทางเลือก

##### `App.vue`:

```html
<template>
  <h3>Slots Fallback Content</h3>
  <p>A component without content provided can have fallback content in the slot tag.</p>
  <slot-comp>
    <!-- Empty -->
  </slot-comp>
  <slot-comp>
    <h4>This content is provided from App.vue</h4>
  </slot-comp>
</template>
```

##### `SlotComp.vue`:

```html
<template>
  <div>
    <slot>
      <h4>This is fallback content</h4>
    </slot>
  </div>
</template>
```