# คำสั่ง Vue `v-bind`

คุณคงทราบแล้วว่าการตั้งค่า Vue พื้นฐานประกอบด้วย Vue instance และเราสามารถเข้าถึงได้จากแท็ก <div id="app"> ด้วย {{ }} หรือคำสั่ง v-bind

ในหน้านี้ เราจะอธิบายคำสั่ง v-bind โดยละเอียดเพิ่มเติม



##  คำสั่ง `v-bind`

คำสั่ง v-bind ช่วยให้เราสามารถผูกแอตทริบิวต์ HTML กับข้อมูลในอินสแตนซ์ Vue ทำให้ง่ายต่อการเปลี่ยนค่าแอตทริบิวต์แบบไดนามิก

### **Syntax**

```html
<div v-bind:[attribute]="[Vue data]"></div>
```

### Example

ค่าแอตทริบิวต์ src ของแท็ก <img> นำมาจากคุณสมบัติข้อมูลอินสแตนซ์ Vue 'url':

```html
<img v-bind:src="url">
```



## CSS Binding

เราสามารถใช้คำสั่ง v-bind เพื่อจัดสไตล์อินไลน์และแก้ไขคลาสแบบไดนามิก เราจะแสดงให้คุณเห็นโดยย่อถึงวิธีการดังกล่าวในส่วนนี้ และต่อไปในบทช่วยสอนนี้ ในหน้า CSS Binding เราจะอธิบายรายละเอียดเพิ่มเติม



## Bind style

การกำหนดสไตล์อินไลน์ด้วย Vue ทำได้โดยการผูกแอ็ตทริบิวต์ style กับ Vue ด้วย v-bind

ในฐานะที่เป็นค่าของคำสั่ง v-bind เราสามารถเขียนวัตถุ JavaScript ด้วย CSS property และ value:

### Example

ขนาดฟอนต์ขึ้นอยู่กับ Vue data property 'size' 

```html
<div v-bind:style="{ fontSize: size }">
  Text example
</div>
```

นอกจากนี้เรายังสามารถแยกค่าตัวเลขขนาดตัวอักษรออกจากหน่วยขนาดตัวอักษรได้หากต้องการ เช่นนี้:

### Example

ค่าหมายเลขขนาดแบบอักษรจะถูกจัดเก็บใน Vue data property 'size'

```html
<div v-bind:style="{ fontSize: size + 'px' }">
  Text example
</div>
```

นอกจากนี้เรายังสามารถเขียนชื่อ CSS property ด้วย CSS syntax (kebab-case) ด้วยเครื่องหมายขีดกลางได้ แต่ไม่แนะนำ:

### Example

CSS property fontSize เรียกว่า 'font-size'

```html
<div v-bind:style="{ 'font-size': size + 'px' }">
  Text example
</div>
```

### Example

สีพื้นหลังขึ้นอยู่กับ data property value 'bgVal' ภายในอินสแตนซ์ Vue

```html
<div v-bind:style="{ backgroundColor: 'hsl('+bgVal+',80%,80%)' }">
  Notice the background color on this div tag.
</div>
```

### Example

สีพื้นหลังถูกตั้งค่าด้วยนิพจน์แบบมีเงื่อนไขของ JavaScript (แบบไตรภาค) ขึ้นอยู่กับว่าค่าคุณสมบัติข้อมูล 'isImportant' เป็น 'จริง' หรือ 'เท็จ'

```html
<div v-bind:style="{ backgroundColor: isImportant ? 'lightcoral' : 'lightgray' }">
  Conditional background color
</div>
```



## Bind class

เราสามารถใช้ v-bind เพื่อเปลี่ยนแอตทริบิวต์คลาส

ค่าของ v-bind:class สามารถเป็นตัวแปรได้:

### Example

ชื่อคลาสนำมาจาก 'className' Vue data property:

```html
<div v-bind:class="className">
  The class is set with Vue
</div>
```

ค่าของ v-bind:class ยังสามารถเป็น object ได้ โดยที่ชื่อคลาสจะมีผลเฉพาะเมื่อตั้งค่าเป็น 'จริง':

### Example

คุณลักษณะคลาสถูกกำหนดหรือไม่ขึ้นอยู่กับว่าคลาส 'myClass' ถูกตั้งค่าเป็น 'true' หรือ 'false':

```html
<div v-bind:class="{ myClass: true }">
  The class is set conditionally to change the background color
</div>
```

เมื่อค่าของ v-bind:class เป็นอ็อบเจ็กต์ คลาสสามารถถูกกำหนดได้ขึ้นอยู่กับคุณสมบัติ Vue:

### Example

แอตทริบิวต์คลาสถูกกำหนดขึ้นอยู่กับคุณสมบัติ 'isImportant' หากเป็น 'true' หรือ 'false':

```html
<div v-bind:class="{ myClass: isImportant }">
  The class is set conditionally to change the background color
</div>
```



## อักษรย่อสำหรับ v-bind

อักษรย่อสำหรับ 'v-bind:' เป็นเพียง ':' (โคลอน)

### Example

ที่นี่เราแค่เขียน ':' แทน 'v-bind:':

```html
<div :class="{ impClass: isImportant }">
  The class is set conditionally to change the background color
</div>
```

เราจะใช้ไวยากรณ์ v-bind: ในบทช่วยสอนนี้ต่อไปเพื่อหลีกเลี่ยงความสับสน
