# Scoped Styling

การจัดสไตล์ที่กำหนดไว้ภายในแท็ก <style> ในคอมโพเนนต์หรือใน App.vue นั้นมีให้ใช้ทั่วโลกในทุกองค์ประกอบ

เพื่อให้สไตล์ถูกจำกัดไว้เฉพาะคอมโพเนนต์ เราสามารถใช้แอตทริบิวต์ scope บนส่วนประกอบนั้นได้: **<style scoped>**



## Global Styling

CSS ที่เขียนอยู่ภายในแท็ก <style> ในไฟล์ *.vue ใด ๆ ทำงานได้ทั่วโลก

ซึ่งหมายความว่า ถ้าเราตั้งค่าแท็ก <p> ให้มีสีพื้นหลังสีชมพูภายในแท็ก <style> ในไฟล์ *.vue ไฟล์เดียว สิ่งนี้จะส่งผลต่อแท็ก <p> ในไฟล์ *.vue ทั้งหมดในโปรเจ็กต์นั้น

### Example

ในแอปพลิเคชันนี้ เรามีไฟล์ *.vue สามไฟล์: App.vue และสองคอมโพเนนต์ CompOne.vue และ CompTwo.vue

การจัดสไตล์ CSS ภายใน CompOne.vue ส่งผลต่อแท็ก <p> ในไฟล์ *.vue ทั้งสามไฟล์:

```html
<template>
  <p>This p-tag belongs to 'CompOne.vue'</p>
</template>

<script></script>

<style>
  p {
    background-color: pink;
    width: 150px;
  }
</style>
```



## Scoped Styling

เพื่อหลีกเลี่ยงไม่ให้การจัดสไตล์ในองค์ประกอบหนึ่งส่งผลต่อการจัดสไตล์ขององค์ประกอบในคอมโพเนนต์อื่นๆ เราใช้แอตทริบิวต์ 'scoped' บนแท็ก <style>:

### Example

แท็ก <style> ใน CompOne.vue ได้รับแอตทริบิวต์ที่กำหนดขอบเขต:

```html
<template>
  <p>This p-tag belongs to 'CompOne.vue'</p>
</template>

<script></script>

<style scoped>
  p {
    background-color: pink;
    width: 150px;
  }
</style>
```