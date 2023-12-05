# Vue CSS Binding

เรียนรู้เพิ่มเติมเกี่ยวกับวิธีใช้ v-bind เพื่อแก้ไข CSS ด้วยแอตทริบิวต์สไตล์และคลาส

แม้ว่าแนวคิดในการเปลี่ยนสไตล์และคุณลักษณะของคลาสด้วย v-bind จะค่อนข้างตรงไปตรงมา แต่ไวยากรณ์อาจต้องอาศัยความคุ้นเคยบ้าง



## CSS แบบไดนามิกใน Vue

คุณได้เห็นแล้วว่าเราใช้ Vue เพื่อแก้ไข CSS โดยใช้ v-bind กับแอตทริบิวต์ style และ class ได้อย่างไร ได้รับการอธิบายสั้น ๆ ในบทช่วยสอนนี้ภายใต้ v-bind และยังมีการยกตัวอย่างหลายตัวอย่างเกี่ยวกับ CSS ที่เปลี่ยนแปลง Vue อีกด้วย

ที่นี่เราจะอธิบายรายละเอียดเพิ่มเติมว่า CSS สามารถเปลี่ยนแปลงแบบไดนามิกด้วย Vue ได้อย่างไร แต่ก่อนอื่น เรามาดูสองตัวอย่างด้วยเทคนิคที่เราได้เห็นแล้วในบทช่วยสอนนี้: การจัดสไตล์อินไลน์ด้วย v-bind:style และการกำหนดคลาสด้วย v-bind:class



## การจัดสไตล์แบบอินไลน์

เราใช้ v-bind:style เพื่อจัด in-line สไตล์ใน Vue

### Example

องค์ประกอบ <input type="range"> ใช้เพื่อเปลี่ยนความทึบขององค์ประกอบ <div> ด้วยการใช้ in-line สไตล์

```html
<input type="range" v-model="opacityVal">
<div v-bind:style="{ backgroundColor: 'rgba(155,20,20,'+opacityVal+')' }">
  Drag the range input above to change opacity here.
</div>
```



## กำหนดคลาส

เราใช้ v-bind:class เพื่อกำหนดคลาสให้กับแท็ก HTML ใน Vue

### Example

เลือกรูปภาพอาหาร อาหารที่เลือกจะถูกเน้นด้วยการใช้ v-bind:class เพื่อแสดงสิ่งที่คุณเลือก

```html
<div v-for="(img, index) in images">
  <img v-bind:src="img.url"
       v-on:click="select(index)"
       v-bind:class="{ selClass: img.sel }">
</div>
```



## วิธีอื่นๆ ในการกำหนดคลาสและสไตล์

ต่อไปนี้เป็นแง่มุมต่างๆ เกี่ยวกับการใช้ v-bind:class และ v-bind:style ที่เราไม่เคยเห็นมาก่อนในบทช่วยสอนนี้:

1. เมื่อคลาส CSS ถูกกำหนดให้กับแท็ก HTML ที่มีทั้ง class="" และ v-bind:class="" Vue จะรวมคลาสเข้าด้วยกัน
2. อ็อบเจ็กต์ที่มีหนึ่งคลาสขึ้นไปถูกกำหนดด้วย v-bind:class="{}" ภายในออบเจ็กต์อาจมีการเปิดหรือปิดคลาสตั้งแต่หนึ่งคลาสขึ้นไป
3. เมื่อใช้การกำหนดสไตล์อินไลน์ (v-bind:style) ควรใช้ camelCase เมื่อกำหนดคุณสมบัติ CSS แต่สามารถใช้ 'kebab-case' ได้หากเขียนไว้ในเครื่องหมายคำพูด
4. คลาส CSS สามารถกำหนดให้กับ  arrays / array notation / syntax

ประเด็นเหล่านี้จะอธิบายโดยละเอียดด้านล่าง



## 1. Vue ผสาน 'class' และ 'v-bind:class'

ในกรณีที่แท็ก HTML เป็นของคลาสที่กำหนดด้วย class="" และยังถูกกำหนดให้กับคลาสด้วย v-bind:class="" Vue จะรวมคลาสให้เรา

### Example

องค์ประกอบ <div> อยู่ในสองคลาส: 'impClass' และ 'yelClass' คลาส 'important' ถูกตั้งค่าด้วยวิธีปกติด้วยแอตทริบิวต์ class และคลาส 'yellow' ถูกตั้งค่าด้วย v-bind:class

```html
<div class="impClass" v-bind:class="{yelClass: isYellow}">
  This div belongs to both 'impClass' and 'yelClass'.
</div>
```



## 2. กำหนดมากกว่าหนึ่งคลาสด้วย 'v-bind:class'

เมื่อกำหนดองค์ประกอบ HTML ให้กับคลาสด้วย v-bind:class="{}" เราสามารถใช้เครื่องหมายจุลภาคเพื่อแยกและกำหนดหลายคลาสได้

### Example

องค์ประกอบ <div> สามารถเป็นของทั้งคลาส 'impClass' และ 'yelClass' ขึ้นอยู่กับคุณสมบัติข้อมูลบูลีน Vue 'isYellow' และ 'isImportant'

```html
<div v-bind:class="{yelClass: isYellow, impClass: isImportant}">
  This tag can belong to both the 'impClass' and 'yelClass' classes.
</div>
```



## 3. Camel case เทียบกับ kebab case ด้วย 'v-bind:style'

เมื่อแก้ไข CSS ใน Vue ด้วยการจัดสไตล์อินไลน์ (v-bind:style) ขอแนะนำให้ใช้รูปแบบ CamelCase สำหรับคุณสมบัติ CSS แต่สามารถใช้ 'kebab-case' ได้หากคุณสมบัติ CSS อยู่ภายในเครื่องหมายคำพูด

### Example

ที่นี่ เราตั้งค่าคุณสมบัติ CSS background-color และ font-weight สำหรับองค์ประกอบ <div> ด้วยสองวิธีที่แตกต่างกัน: วิธีที่แนะนำด้วย CamelCase backgroundColor และวิธีที่ไม่แนะนำด้วย 'kebab-case' ในเครื่องหมายคำพูด 'font-weight' ทางเลือกทั้งสองทำงาน

```html
<div v-bind:style="{ backgroundColor: 'lightpink', 'font-weight': 'bolder' }">
  This div tag has pink background and bold text.
</div>
```



notation  'Camel case' และ 'kebab case' เป็นวิธีการเขียนชุดคำโดยไม่ต้องเว้นวรรคหรือเครื่องหมายวรรคตอน

- **Camel case** notation คือเมื่อคำแรกขึ้นต้นด้วยตัวอักษรตัวเล็ก และทุกคำหลังขึ้นต้นด้วยตัวพิมพ์ใหญ่ เช่น 'BackgroundColor' หรือ 'camelCaseNotation' มันถูกเรียกว่า camel case เพราะเราสามารถจินตนาการถึงตัวพิมพ์ใหญ่ทุกตัวที่มีลักษณะคล้ายโคกบนหลังอูฐ
- **Kebab case** notation คือการแยกคำด้วยเครื่องหมายขีดกลาง เช่น "สีพื้นหลัง" หรือ "สัญลักษณ์ตัวพิมพ์เล็ก" มันถูกเรียกว่า Kebab case เพราะเราสามารถจินตนาการถึงเส้นประที่คล้ายกับไม้เสียบใน 'shish kebab'



## 4. ไวยากรณ์อาร์เรย์ด้วย 'v-bind:class'

เราสามารถใช้ไวยากรณ์อาร์เรย์กับ v-bind:class เพื่อเพิ่มหลายคลาสได้ ด้วยไวยากรณ์อาร์เรย์ เราสามารถใช้ทั้งสองคลาสที่ขึ้นอยู่กับคุณสมบัติ Vue และคลาสที่ไม่ขึ้นอยู่กับคุณสมบัติ Vue

### Example

ที่นี่เราตั้งค่าคลาส CSS 'impClass' และ 'yelClass' ด้วยไวยากรณ์อาร์เรย์ คลาส 'impClass' ขึ้นอยู่กับคุณสมบัติ Vue isImportant และคลาส 'yelClass' จะแนบไปกับองค์ประกอบ <div> เสมอ

```html
<div v-bind:class="[{ impClass: isImportant }, 'yelClass' ]">
  This div tag belongs to one or two classes depending on the isImportant property.
</div>
```

