# Vue v-slot

เราต้องการคำสั่ง v-slot เพื่ออ้างถึงช่องที่มีชื่อ

ช่องที่มีชื่อช่วยให้สามารถควบคุมตำแหน่งเนื้อหาที่วางไว้ภายในเทมเพลตของคอมโพเนนต์ย่อยได้มากขึ้น

ช่องที่มีชื่อสามารถใช้เพื่อสร้างส่วนประกอบที่ยืดหยุ่นและนำกลับมาใช้ใหม่ได้มากขึ้น



ก่อนที่จะใช้ v-slot และ name slots เรามาดูกันว่าเกิดอะไรขึ้นถ้าเราใช้สอง slot ในส่วนประกอบ:

### Example

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp>'Hello!'</slot-comp>
```

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot></slot>
</div>
<div>
  <slot></slot>
</div>
```

ด้วย slots สองช่องในหนึ่งคอมโพเนนต์ เราจะเห็นว่าเนื้อหาปรากฏทั้งสองที่เท่านั้น



## v-slot and Named Slots

หากเรามี <slot> มากกว่าหนึ่งรายการในองค์ประกอบ แต่เราต้องการควบคุมว่าเนื้อหาควรปรากฏที่ใด เราจำเป็นต้องตั้งชื่อช่องและใช้ v-slot เพื่อส่งเนื้อหาไปยังตำแหน่งที่ถูกต้อง

### Example

เพื่อให้สามารถแยกแยะความแตกต่างของสล็อตได้ เราจึงตั้งชื่อสล็อตให้แตกต่างกัน

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot name="topSlot"></slot>
</div>
<div>
  <slot name="bottomSlot"></slot>
</div>
```

และตอนนี้เราสามารถใช้ v-slot ใน App.vue เพื่อนำเนื้อหาไปยังช่องที่ถูกต้องได้

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp v-slot:bottomSlot>'Hello!'</slot-comp>
```



## Default Slots

หากคุณมี <slot> ที่ไม่มีชื่อ <slot> นั้นจะเป็นค่าเริ่มต้นสำหรับคอมโพเนนต์ที่มีเครื่องหมาย v-slot:default หรือคอมโพเนนต์ที่ไม่ได้ทำเครื่องหมายด้วย v-slot

หากต้องการดูวิธีการทำงาน เราเพียงแค่ต้องทำการเปลี่ยนแปลงเล็กๆ น้อยๆ สองครั้งในตัวอย่างก่อนหน้านี้:

### Example

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot name="topSlot"></slot>
</div>
<div>
  <slot name="bottomSlot"></slot>
</div>
```

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp v-slot:bottomSlot>'Hello!'</slot-comp>
```

ดังที่กล่าวไปแล้ว เราสามารถทำเครื่องหมายเนื้อหาด้วยค่าเริ่มต้น v-slot:default เพื่อให้ชัดเจนยิ่งขึ้นว่าเนื้อหาเป็นของช่องเริ่มต้น

### Example

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot></slot>
</div>
<div>
  <slot name="bottomSlot"></slot>
</div>
```

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp v-slot:default>'Default slot'</slot-comp>
```



## v-slot in <template>

ดังที่คุณเห็นแล้วว่าคำสั่ง v-slot สามารถใช้เป็นแอตทริบิวต์ในแท็กส่วนประกอบได้

v-slot ยังสามารถนำมาใช้ในแท็ก <template> เพื่อนำเนื้อหาส่วนใหญ่ไปยัง <slot> ที่ต้องการ

### Example

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp>
  <template v-slot:bottomSlot>
    <h4>To the bottom slot!</h4>
    <p>This p tag and the h4 tag above are directed to the bottom slot with the v-slot directive used on the template tag.</p>
  </template>
  <p>This goes into the default slot</p>
</slot-comp>
```

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot></slot>
</div>
<div>
  <slot name="bottomSlot"></slot>
</div>
```

เราใช้แท็ก <template> เพื่อนำเนื้อหาบางส่วนไปยัง <slot> เนื่องจากแท็ก <template> ไม่ได้แสดงผล แต่เป็นเพียงตัวยึดตำแหน่งสำหรับเนื้อหา คุณสามารถดูสิ่งนี้ได้โดยตรวจสอบเพจที่สร้างขึ้น: คุณจะไม่พบแท็กเทมเพลตที่นั่น



## v-slot Shorthand #

อักษรย่อสำหรับ v-slot: คือ #

ซึ่งหมายความว่า:

```html
<slot-comp v-slot:topSlot>'Hello!'</slot-comp>
```

สามารถเขียนเป็น:

```html
<slot-comp #topSlot>'Hello!'</slot-comp>
```

### Example

##### `App.vue`:

```html
<h1>App.vue</h1>
<p>The component has two div tags with one slot in each.</p>
<slot-comp #topSlot>'Hello!'</slot-comp>
```

##### `SlotComp.vue`:

```html
<h3>Component</h3>
<div>
  <slot name="topSlot"></slot>
</div>
<div>
  <slot name="bottomSlot"></slot>
</div>
```