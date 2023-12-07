# Vue Form Inputs

เราได้เห็นตัวอย่างบางส่วนของ**อินพุตแบบฟอร์ม**ก่อนหน้านี้ในบทช่วยสอนนี้ บนหน้า Vue Forms และ v-model

หน้านี้คือชุดของตัวอย่างการ**ป้อนแบบฟอร์ม**เพิ่มเติมใน Vue เช่น ปุ่มตัวเลือก ช่องทำเครื่องหมาย รายการแบบเลื่อนลง และช่องป้อนข้อความปกติ



## Radio Buttons

ปุ่มตัวเลือกที่เป็นของตัวเลือกเดียวกันจะต้องมีชื่อเดียวกันจึงจะสามารถเลือกได้เพียงปุ่มเดียวเท่านั้น

เช่นเดียวกับอินพุตทั้งหมดใน Vue เราจะบันทึกค่าอินพุตของปุ่มตัวเลือกด้วย v-model แต่แอตทริบิวต์ value จะต้องได้รับการตั้งค่าอย่างชัดเจนบนแท็ก <input type="radio">

นี่คือวิธีที่เราสามารถใช้ปุ่มตัวเลือกในรูปแบบ Vue:

### Example

##### `App.vue`:

```html
<template>
  <h1>Radio Buttons in Vue</h1>
  <form @submit.prevent="registerAnswer">
    <p>What is your favorite animal?</p>
    <label>
      <input type="radio" name="favAnimal" v-model="inpVal" value="Cat"> Cat
    </label>
    <label>
      <input type="radio" name="favAnimal" v-model="inpVal" value="Dog"> Dog
    </label>
    <label>
      <input type="radio" name="favAnimal" v-model="inpVal" value="Turtle"> Turtle
    </label>
    <label>
      <input type="radio" name="favAnimal" v-model="inpVal" value="Moose"> Moose
    </label>
    <button type="submit">Submit</button>
  </form>
  <div>
    <h3>Submitted choice:</h3>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inpVal: '',
      inpValSubmitted: 'Not submitted yet'
    }
  },
  methods: {
    registerAnswer() {
      if(this.inpVal) {
        this.inpValSubmitted = this.inpVal;
      }
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 0 20px 20px 20px;
    margin-top: 20px;
    display: inline-block;
  }
  button {
    margin: 10px;
  }
  label {
    display: block;
    width: 80px;
    padding: 5px;
  }
  label:hover {
    cursor: pointer;
    background-color: rgb(211, 244, 211);
    border-radius: 5px;
  }
  #pAnswer {
    background-color: lightgreen;
    padding: 5px;
  }
</style>
```



## Checkboxes

เมื่ออินพุตช่องทำเครื่องหมาย (<input type="checkbox">) เชื่อมต่อกับอาร์เรย์เดียวกันกับ v-model ค่าสำหรับช่องทำเครื่องหมายที่เลือกจะถูกรวบรวมในอาร์เรย์นั้น:

### Example

##### `App.vue`:

```html
<template>
  <h1>Checkbox Inputs in Vue</h1>
  <form @submit.prevent="registerAnswer">
    <p>What kinds of food do you like?</p>
    <label>
      <input type="checkbox" v-model="likeFoods" value="Pizza"> Pizza
    </label>
    <label>
      <input type="checkbox" v-model="likeFoods" value="Rice"> Rice
    </label>
    <label>
      <input type="checkbox" v-model="likeFoods" value="Fish"> Fish
    </label>
    <label>
      <input type="checkbox" v-model="likeFoods" value="Salad"> Salad
    </label>
    <button type="submit">Submit</button>
  </form>
  <div>
    <h3>Submitted answer:</h3>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      likeFoods: [],
      inpValSubmitted: 'Not submitted yet'
    }
  },
  methods: {
    registerAnswer() {
      this.inpValSubmitted = this.likeFoods;
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 0 20px 20px 20px;
    margin-top: 20px;
    display: inline-block;
  }
  button {
    margin: 10px;
  }
  label {
    display: block;
    width: 80px;
    padding: 5px;
  }
  label:hover {
    cursor: pointer;
    background-color: rgb(211, 244, 211);
    border-radius: 5px;
  }
  #pAnswer {
    background-color: lightgreen;
    padding: 5px;
  }
</style>
```



## Drop-down List

รายการแบบเลื่อนลงประกอบด้วยแท็ก <select> พร้อมด้วยแท็ก <option> อยู่ข้างใน

เมื่อใช้รายการแบบเลื่อนลงใน Vue เราจำเป็นต้องเชื่อมต่อแท็ก <select> กับ v-model และให้ค่าแก่แท็ก <option>:

### Example

##### `App.vue`:

```html
<template>
  <h1>Drop-down List in Vue</h1>
  <form @submit.prevent="registerAnswer">
    <label for="cars">Choose a car:</label>
    <select  v-model="carSelected" id="cars">
      <option disabled value="">Please select one</option>
      <option>Volvo</option>
      <option>Saab</option>
      <option>Opel</option>
      <option>Audi</option>
    </select>
    <br><br>
    <input type="submit" value="Submit">
  </form>
  <div>
    <h3>Submitted answer:</h3>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      carSelected: '',
      inpValSubmitted: 'Not submitted yet'
    }
  },
  methods: {
    registerAnswer() {
      if(this.carSelected) {
        this.inpValSubmitted = this.carSelected;
      }
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 0 20px 20px 20px;
    margin-top: 20px;
    display: inline-block;
  }
  button {
    margin: 10px;
  }
  label {
    width: 80px;
    padding: 5px;
  }
  label:hover {
    cursor: pointer;
    background-color: rgb(211, 244, 211);
    border-radius: 5px;
  }
  #pAnswer {
    background-color: lightgreen;
    padding: 5px;
  }
</style>
```



## **<select multiple>**

ด้วยแอตทริบิวต์หลายรายการในแท็ก <select> รายการแบบเลื่อนลงจะขยายและเราสามารถเลือกได้มากกว่าหนึ่งตัวเลือก

หากต้องการเลือกมากกว่าหนึ่งตัวเลือก ผู้ใช้ Windows ต้องกดปุ่ม 'ctrl' และผู้ใช้ macOS ต้องกดปุ่ม 'command'

เมื่อใช้ <select multiple> ใน Vue เราจำเป็นต้องเชื่อมต่อแท็ก <select> กับ v-model และให้ค่าแก่แท็ก <option>:

### Example

##### `App.vue`:

```html
<template>
  <h1>Select Multiple in Vue</h1>
  <p>Depending on your operating system, use the 'ctrl' or the 'command' key to select multiple options.</p>
  <form @submit.prevent="registerAnswer">
    <label for="cars">Choose one or more cars:</label><br>
    <select  v-model="carsSelected" id="cars" multiple>
      <option>Volvo</option>
      <option>Saab</option>
      <option>Opel</option>
      <option>Audi</option>
      <option>Kia</option>
    </select>
    <button type="submit">Submit</button>
  </form>
  <div>
    <h3>Submitted answer:</h3>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      carsSelected: [],
      inpValSubmitted: 'Not submitted yet'
    }
  },
  methods: {
    registerAnswer() {
      if(this.carsSelected) {
        this.inpValSubmitted = this.carsSelected;
      }
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 0 20px 20px 20px;
    margin-top: 20px;
    display: inline-block;
  }
  button, select {
    margin: 10px;
    display: block;
  }
  label {
    width: 80px;
    padding: 5px;
  }
  label:hover {
    cursor: pointer;
    background-color: rgb(211, 244, 211);
    border-radius: 5px;
  }
  #pAnswer {
    background-color: lightgreen;
    padding: 5px;
  }
</style>
```



## Read Only Form Inputs

การใช้ v-model บนอินพุตแบบฟอร์มจะสร้างการเชื่อมโยงแบบสองทาง ซึ่งหมายความว่าหากอินสแตนซ์ข้อมูล Vue เปลี่ยนแปลง แอ็ตทริบิวต์ค่าอินพุตก็จะเปลี่ยนไปด้วย

สำหรับอินพุตแบบฟอร์มแบบอ่านอย่างเดียว เช่น <input type="file"> แอตทริบิวต์ value ไม่สามารถเปลี่ยนจากอินสแตนซ์ข้อมูล Vue ได้ ดังนั้นเราจึงไม่สามารถใช้ v-model ได้

สำหรับอินพุตแบบฟอร์มแบบอ่านอย่างเดียว เช่น <input type="file"> เราจำเป็นต้องใช้ @change เพื่อเรียกเมธอดที่อัปเดตอินสแตนซ์ข้อมูล Vue:

### Example

##### `App.vue`:

```html
<template>
  <h1>Input Type File</h1>
  <form @submit.prevent="registerAnswer">
    <label>Choose a file:
      <input @change="updateVal" type="file">
    </label>
    <button type="submit">Submit</button>
  </form>
  <div>
    <h3>Submitted answer:</h3>
    <p id="pAnswer">{{ inpValSubmitted }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      fileInp: null,
      inpValSubmitted: 'Not submitted yet'
    }
  },
  methods: {
    registerAnswer() {
      if(this.fileInp) {
        this.inpValSubmitted = this.fileInp;
      }
    },
    updateVal(e) {
      this.fileInp = e.target.value;
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 0 20px 20px 20px;
    margin-top: 20px;
    display: inline-block;
  }
  button {
    margin: 10px;
    display: block;
  }
  #pAnswer {
    background-color: lightgreen;
    padding: 5px;
  }
</style>
```

ข้อมูล: ในตัวอย่างข้างต้น ชื่อไฟล์ที่ส่งจะมีพาธของไฟล์ C:\fakepath\ อยู่ข้างหน้า นี่เป็นการป้องกันไม่ให้ซอฟต์แวร์ที่เป็นอันตรายคาดเดาโครงสร้างไฟล์ของผู้ใช้



## Other Form Inputs

ด้วยการป้อนแบบฟอร์มที่กล่าวถึงข้างต้น เราต้องระบุค่าสำหรับแอตทริบิวต์ value แต่ด้วยการป้อนแบบฟอร์มด้านล่าง ผู้ใช้จะระบุค่า:

- `<input type="color">`
- `<input type="date">`
- `<input type="datetime-local">`
- `<input type="number">`
- `<input type="password">`
- `<input type="range">`
- `<input type="search">`
- `<input type="tel">`
- `<input type="text">`
- `<input type="time">`
- `<textarea>`

เนื่องจากผู้ใช้ให้ค่าสำหรับอินพุตแบบฟอร์มเหล่านี้แล้ว สิ่งที่เราต้องทำใน Vue คือการเชื่อมต่ออินพุตกับคุณสมบัติข้อมูลด้วย v-model

นี่คือวิธีใช้ <input type="range"> ใน Vue:

### Example

##### `App.vue`:

```html
<form @submit.prevent="registerAnswer">
  <label>How tall are you?<br>
    <input v-model="heightInp" type="range" min="50" max="235"> {{ heightInp }} cm
  </label>
  <button type="submit">Submit</button>
</form>
```

และนี่คือวิธีใช้ <input type="color"> ใน Vue:

### Example

##### `App.vue`:

```html
<form @submit.prevent="registerAnswer">
  <label>Choose a color: 
    <input v-model="colorInp" type="color">
  </label>
  <button type="submit">Submit</button>
</form>
```

และนี่คือวิธีใช้ <textarea> ใน Vue:

### Example

##### `App.vue`:

```html
<form @submit.prevent="registerAnswer">
  <label>
    <p>What do you think about our product?</p> 
    <textarea v-model="txtInp" placeholder="Write something.." rows="4" cols="35"></textarea>
  </label>
  <button type="submit">Submit</button>
</form>
```

เรียนรู้เพิ่มเติมเกี่ยวกับวิธีการทำงานของอินพุตแบบฟอร์ม HTML ประเภทต่างๆ ในบทช่วยสอน HTML ของเรา