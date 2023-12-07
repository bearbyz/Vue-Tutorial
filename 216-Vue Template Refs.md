# Vue Template Refs

**การอ้างอิงเทมเพลต** Vue ใช้เพื่ออ้างถึงองค์ประกอบ DOM ที่เฉพาะเจาะจง

เมื่อแอตทริบิวต์การอ้างอิงถูกตั้งค่าบนแท็ก HTML องค์ประกอบ DOM ผลลัพธ์จะถูกเพิ่มให้กับวัตถุ $refs

เราสามารถใช้แอตทริบิวต์ ref และวัตถุ $refs ใน Vue เป็นทางเลือกแทนวิธีการใน JavaScript ธรรมดา เช่น getElementById() หรือ querySelector()



## The 'ref' Attribute and The '$refs' Object

แท็ก HTML ที่มีแอตทริบิวต์การอ้างอิงจะถูกเพิ่มลงในวัตถุ $refs และสามารถเข้าถึงได้ในภายหลังจากภายในแท็ก <script>

### Example

ข้อความภายใน <p> องค์ประกอบมีการเปลี่ยนแปลง

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Click the button to put "Hello!" as the text in the green p element.</p>
  <button @click="changeVal">Change Text</button>
  <p ref="pEl">This is the initial text</p>
</template>

<script>
  export default {
    methods: {
      changeVal() {
        this.$refs.pEl.innerHTML = "Hello!";
      }
    }
  }
</script>
```

ด้านล่างนี้เป็นอีกตัวอย่างหนึ่งที่ $refs object ถูกใช้เพื่อคัดลอกค่าของแท็กหนึ่งไปยังอีกแท็กหนึ่ง

### Example

The text from the first `<p>` tag is copied into the second `<p>` tag.

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p ref="p1">Click the button to copy this text into the paragraph below.</p>
  <button @click="transferText">Transfer text</button>
  <p ref="p2">...</p>
</template>

<script>
  export default {
    methods: {
      transferText() { 
        this.$refs.p2.innerHTML = this.$refs.p1.innerHTML;
      }
    }
  };
</script>
```



## Get The Input Value from '$refs'

เราสามารถไปเพิ่มเติมในองค์ประกอบ HTML ที่เพิ่มเข้าไปในวัตถุ $refs เพื่อเข้าถึงคุณสมบัติใดๆ ที่เราต้องการ

### Example

องค์ประกอบ <p> ได้รับเนื้อหาเดียวกันกับสิ่งที่ถูกเขียนในช่องป้อนข้อมูล

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Start writing inside the input element, and the text will be copied into the last paragraph by the use of the '$refs' object.</p>
  <input ref="inputEl" @input="getRefs" placeholder="Write something..">
  <p ref="pEl"></p>
</template>

<script>
  export default {
    methods: {
      getRefs() { 
        this.$refs.pEl.innerHTML = this.$refs.inputEl.value;
      }
    }
  };
</script>
```



## 'ref' with v-for

องค์ประกอบ HTML ที่สร้างด้วย v-for พร้อมด้วยแอตทริบิวต์ ref จะถูกเพิ่มลงในวัตถุ $refs ในรูปแบบอาร์เรย์

### Example

ปุ่มจะแสดงองค์ประกอบรายการที่สามที่จัดเก็บเป็นองค์ประกอบอาร์เรย์ภายใน $refs วัตถุ

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Click the button to reveal the 3rd list element stored as an array element in the $refs object.</p>
  <button @click="getValue">Get the 3rd list element</button><br>
  <ul>
    <li v-for="x in liTexts" ref="liEl">{{ x }}</li>
  </ul>
  <pre>{{ thirdEl }}</pre>
</template>

<script>
  export default {
    data() {
      return {
        thirdEl: ' ',
        liTexts: ['Apple','Banana','Kiwi','Tomato','Lichi']
      }
    },
    methods: {
      getValue() { 
        this.thirdEl = this.$refs.liEl[2].innerHTML;
        console.log("this.$refs.liEl = ",this.$refs.liEl);
      }
    }
  };
</script>

<style>
pre {
  background-color: lightgreen;
  display: inline-block;
}
</style>
```