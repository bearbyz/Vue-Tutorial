# Vue Lifecycle Hooks

Lifecycle hooks ใน Vue เป็นขั้นตอนหนึ่งในวงจรชีวิตของส่วนประกอบที่เราสามารถเพิ่มโค้ดเพื่อทำสิ่งต่างๆ ได้



## Lifecycle Hooks

ทุกครั้งที่ส่วนประกอบไปถึงขั้นตอนใหม่ในวงจรการใช้งาน ฟังก์ชันเฉพาะจะทำงาน และเราสามารถเพิ่มโค้ดให้กับฟังก์ชันนั้นได้ ฟังก์ชันดังกล่าวเรียกว่า lifecycle hooks เนื่องจากเราสามารถ "เชื่อมต่อ" โค้ดของเราเข้ากับขั้นตอนนั้นได้

สิ่งเหล่านี้คือ hooks วงจรการใช้งานทั้งหมดที่ส่วนประกอบมี:

1. `beforeCreate`
2. `created`
3. `beforeMount`
4. `mounted`
5. `beforeUpdate`
6. `updated`
7. `beforeUnmount`
8. `unmounted`
9. `errorCaptured`
10. `renderTracked`
11. `renderTriggered`
12. `activated`
13. `deactivated`
14. `serverPrefetch`

ด้านล่างนี้เป็นตัวอย่างของ hook วงจรการใช้งานเหล่านี้



## The 'beforeCreate' Hook

เบ็ดของวงจรการใช้งาน beforeCreate จะเกิดขึ้นก่อนที่จะเตรียมใช้งานส่วนประกอบ ดังนั้นนี่คือก่อนที่ Vue จะตั้งค่าข้อมูลของส่วนประกอบ คุณสมบัติที่คำนวณ วิธีการ และ Listener เหตุการณ์

hook beforeCreate สามารถใช้เป็นตัวอย่างในการตั้งค่า Listener เหตุการณ์ทั่วโลก แต่เราควรหลีกเลี่ยงการพยายามเข้าถึงองค์ประกอบที่เป็นของส่วนประกอบจาก hook วงจรการใช้งาน beforeCreate เช่น ข้อมูล ผู้ดู และเมธอด เนื่องจากยังไม่ได้สร้างที่ ขั้นตอนนี้

นอกจากนี้ มันไม่สมเหตุสมผลเลยที่จะพยายามเข้าถึงองค์ประกอบ DOM จาก beforeCreate lifecycle hook เนื่องจากองค์ประกอบเหล่านั้นจะไม่ถูกสร้างขึ้นจนกว่าจะติดตั้งส่วนประกอบแล้ว

### Example

##### `CompOne.vue`:

```html
<template>
    <h2>Component</h2>
    <p>This is the component</p>
    <p id="pResult">{{ text }}</p>
</template>

<script>
export default {
	data() {
		return {
			text: '...'
		}
	},
  beforeCreate() {
		this.text = 'initial text'; // This line has no effect
    console.log("beforeCreate: The component is not created yet.");
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'beforeCreate' Lifecycle Hook</h1>
  <p>We can see the console.log() message from 'beforeCreate' lifecycle hook, but there is no effect from the text change we try to do to the Vue data property, because the Vue data property is not created yet.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
#pResult {
  background-color: lightcoral;
  display: inline-block;
}
</style>
```

ในตัวอย่างข้างต้น บรรทัดที่ 15 ใน CompOne.vue ไม่มีผลใดๆ เนื่องจากในบรรทัดนั้น เราพยายามเปลี่ยนข้อความภายในคุณสมบัติข้อมูล Vue แต่คุณสมบัติข้อมูล Vue ยังไม่ได้สร้างจริงๆ นอกจากนี้ อย่าลืมเปิดคอนโซลของเบราว์เซอร์เพื่อดูผลลัพธ์ของการเรียกใช้ console.log() ที่บรรทัด 16



## The 'created' Hook

Lifecycle Hook ที่สร้างขึ้นจะเกิดขึ้นหลังจากที่ส่วนประกอบเริ่มต้น ดังนั้น Vue จึงได้ตั้งค่าข้อมูลของส่วนประกอบ คุณสมบัติในการคำนวณ วิธีการ และตัวฟังเหตุการณ์แล้ว

เราควรหลีกเลี่ยงการพยายามเข้าถึงองค์ประกอบ DOM จาก hook วงจรการใช้งานที่สร้างขึ้น เนื่องจากองค์ประกอบ DOM จะไม่สามารถเข้าถึงได้จนกว่าจะติดตั้งส่วนประกอบ

hook วงจรการใช้งานที่สร้างขึ้นสามารถใช้เพื่อดึงข้อมูลด้วยคำขอ HTTP หรือตั้งค่าข้อมูลเริ่มต้น เช่นเดียวกับในตัวอย่างด้านล่าง คุณสมบัติข้อมูล 'ข้อความ' จะได้รับค่าเริ่มต้น:

### Example

##### `CompOne.vue`:

```html
<template>
    <h2>Component</h2>
    <p>This is the component</p>
    <p id="pResult">{{ text }}</p>
</template>

<script>
export default {
	data() {
		return {
			text: '...'
		}
	},
  created() {
		this.text = 'initial text';
    console.log("created: The component just got created.");
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'created' Lifecycle Hook</h1>
  <p>We can see the console.log() message from 'created' lifecycle hook, and the text change we try to do to the Vue data property works, because the Vue data property is already created at this stage.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
#pResult {
  background-color: lightcoral;
  display: inline-block;
}
</style>
```



## The 'beforeMount' Hook

hook วงจรการใช้งาน beforeMount จะเกิดขึ้นก่อนที่จะประกอบส่วนประกอบ ดังนั้นก่อนที่ส่วนประกอบจะถูกเพิ่มลงใน DOM

เราควรหลีกเลี่ยงการพยายามเข้าถึงองค์ประกอบ DOM จาก hook วงจรการใช้งาน beforeMount เนื่องจากองค์ประกอบ DOM จะไม่สามารถเข้าถึงได้จนกว่าจะติดตั้งส่วนประกอบแล้ว

ตัวอย่างด้านล่างแสดงให้เห็นว่าเรายังเข้าถึงองค์ประกอบ DOM ในส่วนประกอบไม่ได้ บรรทัดที่ 11 ใน CompOne.vue ไม่ทำงาน และสร้างข้อผิดพลาดในคอนโซลของเบราว์เซอร์:

### Example

##### `CompOne.vue`:

```html
<template>
    <h2>Component</h2>
    <p>This is the component</p>
    <p ref="pEl" id="pEl">We try to access this text from the 'beforeMount' hook.</p>
</template>

<script>
export default {
  beforeMount() {
    console.log("beforeMount: This is just before the component is mounted.");
    this.$refs.pEl.innerHTML = "Hello World!"; // <-- We cannot reach the 'pEl' DOM element at this stage 
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'beforeMount' Lifecycle Hook</h1>
  <p>We can see the console.log() message from the 'beforeMount' lifecycle hook, but the text change we try to do to the 'pEl' paragraph DOM element does not work, because the 'pEl' paragraph DOM element does not exist yet at this stage.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
#pEl {
  background-color: lightcoral;
  display: inline-block;
}
</style>
```



## The 'mounted' Hook

หลังจากที่เพิ่มส่วนประกอบลงในแผนผัง DOM แล้ว ฟังก์ชัน mount() จะถูกเรียกใช้ และเราสามารถเพิ่มโค้ดของเราลงในสเตจนั้นได้

นี่เป็นโอกาสแรกที่เราต้องทำสิ่งต่างๆ ที่เกี่ยวข้องกับองค์ประกอบ DOM ที่เป็นของส่วนประกอบ เช่น การใช้แอตทริบิวต์ ref และวัตถุ $refs ดังที่เราทำในตัวอย่างที่สองด้านล่างนี้

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>Right after this component is added to the DOM, the mounted() function is called and we can add code to that mounted() function. In this example, an alert popup box appears after this component is mounted.</p>
  <p><strong>Note:</strong> The reason that the alert is visible before the component is visible is because the alert is called before the browser gets to render the component to the screen.</p>
</template>

<script>
export default {
  mounted() {
    alert("The component is mounted!");
  }
}
</script>
```

`App.vue`:

```html
<template>
  <h1>The 'mounted' Lifecycle Hook</h1>
  <button @click="this.activeComp = !this.activeComp">Create component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    width: 400px;
    background-color: lightgreen;
  }
</style>
```

หมายเหตุ: ระยะที่เมาท์เกิดขึ้นหลังจากที่เพิ่มส่วนประกอบลงใน DOM แล้ว แต่ในตัวอย่างด้านบน จะเห็นการแจ้งเตือน () ก่อนที่เราจะมองเห็นส่วนประกอบนั้น เหตุผลก็คือ องค์ประกอบแรกถูกเพิ่มลงใน DOM แต่ก่อนที่เบราว์เซอร์จะแสดงผลส่วนประกอบบนหน้าจอ สเตจที่เมาท์จะเกิดขึ้น และการแจ้งเตือน () จะมองเห็นได้ และหยุดเบราว์เซอร์ชั่วคราวในการแสดงผลส่วนประกอบ



ด้านล่างนี้เป็นตัวอย่างที่อาจมีประโยชน์มากกว่า: เมื่อต้องการวางเคอร์เซอร์ไว้ในช่องป้อนข้อมูลหลังจากประกอบส่วนประกอบของแบบฟอร์มแล้ว เพื่อให้ผู้ใช้สามารถเริ่มพิมพ์ได้

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Form Component</h2>
  <p>When this component is added to the DOM tree, the mounted() function is called, and we put the cursor inside the input element.</p>
  <form @submit.prevent>
    <label>
      <p>
        Name: <br>
        <input type="text" ref="inpName">
      </p>
    </label>
    <label>
      <p>
        Age: <br>
        <input type="number">
      </p>
    </label>
    <button>Submit</button>
  </form>
  <p>(This form does not work, it is only here to show the mounted lifecycle hook.)</p>
</template>

<script>
  export default {
    mounted() {
      this.$refs.inpName.focus();
    }
  }
</script>
```



## The 'beforeUpdate' Hook

hook วงจรการใช้งาน beforeUpdate จะถูกเรียกเมื่อใดก็ตามที่มีการเปลี่ยนแปลงในข้อมูลของส่วนประกอบของเรา แต่ก่อนที่การอัปเดตจะแสดงผลบนหน้าจอ hook วงจรการใช้งาน beforeUpdate จะเกิดขึ้นก่อน hook วงจรการใช้งานที่อัปเดต

สิ่งพิเศษเกี่ยวกับ hook beforeUpdate ก็คือเราสามารถทำการเปลี่ยนแปลงกับแอปพลิเคชันได้โดยไม่ต้องเรียกใช้การอัปเดตใหม่ ดังนั้นเราจึงหลีกเลี่ยงการวนซ้ำไม่สิ้นสุด นั่นคือเหตุผลที่ไม่ทำการเปลี่ยนแปลงแอปพลิเคชันใน hook วงจรการใช้งานที่ได้รับการอัปเดต เนื่องจากด้วย hook นั้น จะมีการวนซ้ำแบบไม่มีที่สิ้นสุด ลองดูตัวอย่างที่สามด้านล่างจากที่นี่ ซึ่งเป็นสีแดง

### Example

ฟังก์ชัน beforeUpdate() จะเพิ่มแท็ก <li> ให้กับเอกสารเพื่อระบุว่าฟังก์ชัน beforeUpdate() ได้ทำงานแล้ว

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>This is the component</p>
</template>
```

##### `App.vue`:

```html
<template>
  <h1>The 'beforeUpdate' Lifecycle Hook</h1>
  <p>Whenever there is a change in our page, the application is 'updated' and the 'beforeUpdate' hook happens just before that.</p>
  <p>It is safe to modify our page in the 'beforeUpdate' hook like we do here, but if we modify our page in the 'updated' hook, we will generate an infinite loop.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
  <ol ref="divLog"></ol>
</template>

<script>
export default {
  data() {
    return {
      activeComp: true
    }
  },
  beforeUpdate() {
    this.$refs.divLog.innerHTML += "<li>beforeUpdate: This happened just before the 'updated' hook.</li>";
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
</style>
```



## The 'updated' Hook

Hook วงจรการใช้งานที่อัปเดตจะถูกเรียกหลังจากที่ส่วนประกอบของเราได้อัปเดตแผนผัง DOM

### Example

ฟังก์ชั่น addedd() เขียนข้อความด้วย console.log() สิ่งนี้จะเกิดขึ้นทุกครั้งที่มีการอัปเดตเพจ ซึ่งในตัวอย่างนี้จะเกิดขึ้นทุกครั้งที่มีการเพิ่มหรือลบส่วนประกอบ

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>This is the component</p>
</template>
```

##### `App.vue`:

```html
<template>
  <h1>The 'updated' Lifecycle Hook</h1>
  <p>Whenever there is a change in our page, the application is updated and the updated() function is called. In this example we use console.log() in the updated() function that runs when our application is updated.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: true
    }
  },
  updated() {
    console.log("The component is updated!");
  }
}
</script>

<style>
#app {
  max-width: 450px;
}
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  width: 80%;
  background-color: lightgreen;
}
</style>
```

We can see the result in the browser console after clicking the "Add/Remove Component" button 10 times:

![console screenshot](https://www.w3schools.com/vue/img_LCHooks_updated.png)

หมายเหตุ: เราต้องระวังที่จะไม่แก้ไขเพจเองเมื่อมีการเรียก hook วงจรการใช้งานที่อัปเดต เนื่องจากเพจจะอัปเดตซ้ำแล้วซ้ำอีก ทำให้เกิดการวนซ้ำไม่สิ้นสุด



ลองมาดูว่าจะเกิดอะไรขึ้นถ้าเราทำตามข้อความข้างต้นที่เตือนเราไม่ให้ทำ เพจจะอัพเดทแบบไม่มีกำหนดมั้ย?:

### Example

ฟังก์ชัน updated() จะเพิ่มข้อความลงในย่อหน้า ซึ่งจะอัปเดตหน้าอีกครั้ง และฟังก์ชันจะทำงานซ้ำแล้วซ้ำอีกในวงวนไม่สิ้นสุด โชคดีที่เบราว์เซอร์ของคุณจะหยุดการวนซ้ำนี้ในที่สุด

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>This is the component</p>
</template>
```

##### `App.vue`:

```html
<template>
  <h1>The 'updated' Lifecycle Hook</h1>
  <p>Whenever there is a change in our page, the application is updated and the updated() function is called.</p>
  <p>The first change that causes the updated hook to be called is when we remove the component by clicking the button. When this happens, the update() function adds text to the last paragraph, which in turn updates the page again and again.</p>
  <button @click="this.activeComp = !this.activeComp">Add/Remove Component</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
  <div>{{ text }}</div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: true,
      text: "Hello, "
    }
  },
  updated() {
    this.text += "hi, ";
  }
}
</script>

<style>
#app {
  max-width: 450px;
}
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  width: 80%;
  background-color: lightgreen;
}
</style>
```

เมื่อเรียกใช้โค้ดด้านบนในเครื่องของคุณในโหมด dev คำเตือนคอนโซลเบราว์เซอร์ Chrome จะมีลักษณะดังนี้:

![screenshot browser console warning](https://www.w3schools.com/vue/img_LCHooks_updateLoop.png)



## The 'beforeUnmount' Hook

hook วงจรการใช้งาน beforeUnmount จะถูกเรียกก่อนที่ส่วนประกอบจะถูกลบออกจาก DOM

ดังที่เราเห็นในตัวอย่างด้านล่าง เรายังคงสามารถเข้าถึงองค์ประกอบส่วนประกอบใน DOM ใน hook beforeUnmount

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p ref="pEl">Strawberries!</p>
</template>
  
<script>
export default {
  beforeUnmount() {
    alert("beforeUnmount: The text inside the p-tag is: " + this.$refs.pEl.innerHTML);
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>Lifecycle Hooks</h1>
  <button @click="this.activeComp = !this.activeComp">{{ btnText }}</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: true
    }
  },
  computed: {
    btnText() {
      if(this.activeComp) {
        return 'Remove component'
      }
      else {
        return 'Add component'
      }
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    width: 400px;
    background-color: lightgreen;
  }
</style>
```



## The 'unmounted' Hook

hook วงจรการใช้งานที่ไม่ได้ประกอบเข้าจะถูกเรียกหลังจากส่วนประกอบถูกลบออกจาก DOM

ฮุคนี้สามารถใช้เพื่อลบผู้ฟังเหตุการณ์หรือยกเลิกตัวจับเวลาหรือช่วงเวลา

เมื่อถอดส่วนประกอบออกแล้ว ฟังก์ชัน unmounted() จะถูกเรียก และเราสามารถเพิ่มโค้ดของเราเข้าไปได้:

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>When this component is removed from the DOM tree, the unmounted() function is called and we can add code to that function. In this example we create an alert popup box when this component is removed.</p>
</template>

<script>
export default {
  unmounted() {
    alert("The component is removed (unmounted)!");
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>Lifecycle Hooks</h1>
  <button @click="this.activeComp = !this.activeComp">{{ btnText }}</button>
  <div>
    <comp-one v-if="activeComp"></comp-one>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: true
    }
  },
  computed: {
    btnText() {
      if(this.activeComp) {
        return 'Remove component'
      }
      else {
        return 'Add component'
      }
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin: 10px;
    width: 400px;
    background-color: lightgreen;
  }
</style>
```

หมายเหตุ: ขั้นตอนการยกเลิกการต่อเชื่อมเกิดขึ้นหลังจากที่ส่วนประกอบถูกลบออกจาก DOM แต่ในตัวอย่างด้านบน จะเห็นการแจ้งเตือน () ก่อนที่ส่วนประกอบจะหายไป เหตุผลก็คือ ขั้นแรกส่วนประกอบจะถูกลบออกจาก DOM แต่ก่อนที่เบราว์เซอร์จะแสดงผลการลบส่วนประกอบไปที่หน้าจอ ขั้นตอนการยกเลิกการต่อเชื่อมจะเกิดขึ้น และการแจ้งเตือน () จะมองเห็นได้ และหยุดเบราว์เซอร์ชั่วคราวไม่ให้ลบออกอย่างเห็นได้ชัด ส่วนประกอบ.



## The 'errorCaptured' Hook

hook วงจรการใช้งาน errorCaptured จะถูกเรียกเมื่อมีข้อผิดพลาดเกิดขึ้นในคอมโพเนนต์ย่อย/สืบทอด

เบ็ดนี้สามารถใช้สำหรับการจัดการข้อผิดพลาด การบันทึก หรือเพื่อแสดงข้อผิดพลาดให้กับผู้ใช้

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>This is the component</p>
  <button @click="generateError">Generate Error</button>
</template>

<script>
export default {
  methods: {
    generateError() {
      this.$refs.objEl.innerHTML = "hi";
    }
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'errorCaptured' Lifecycle Hook</h1>
  <p>Whenever there is an error in a child component, the errorCaptured() function is called on the parent.</p>
  <p>When the button inside the component is clicked, a method will run that tries to do changes to a $refs object that does not exist. This creates an error in the component that triggers the 'errorCaptured' lifecycle hook in the parent, and an alert box is displayed with information about the error.</p>
  <p>After clicking "Ok" in the alert box you can see the error in the browser console.</p>
  <div>
    <comp-one></comp-one>
  </div>
</template>

<script>
export default {
  errorCaptured() {
    alert("An error occurred");
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
</style>
```

ข้อมูลเกี่ยวกับข้อผิดพลาดยังสามารถบันทึกเป็นอาร์กิวเมนต์ของฟังก์ชัน errorCaptured() และอาร์กิวเมนต์เหล่านี้คือ:

1. ข้อผิดพลาด
2. ส่วนประกอบที่ทำให้เกิดข้อผิดพลาด
3. ประเภทแหล่งที่มาของข้อผิดพลาด

ในตัวอย่างด้านล่าง อาร์กิวเมนต์เหล่านี้ถูกจับในฟังก์ชัน errorCaptured() และเขียนลงในคอนโซล:

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>This is the component</p>
  <button @click="generateError">Generate Error</button>
</template>

<script>
export default {
  methods: {
    generateError() {
      this.$refs.objEl.innerHTML = "hi";
    }
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'errorCaptured' Lifecycle Hook</h1>
  <p>Whenever there is an error in a child component, the errorCaptured() function is called on the parent.</p>
  <p>Open the browser console to see the captured error details.</p>
  <div>
    <comp-one></comp-one>
  </div>
</template>

<script>
export default {
  errorCaptured(error,compInst,errorInfo) {
    console.log("error: ", error);
    console.log("compInst: ", compInst);
    console.log("errorInfo: ", errorInfo);
  }
}
</script>

<style>
#app > div {
  border: dashed black 1px;
  border-radius: 10px;
  padding: 10px;
  margin-top: 10px;
  background-color: lightgreen;
}
</style>
```



## The 'renderTracked' and 'renderTriggered' Lifecycle Hooks

hook renderTracked ทำงานเมื่อมีการตั้งค่าฟังก์ชันการเรนเดอร์ให้ติดตามหรือตรวจสอบส่วนประกอบที่เกิดปฏิกิริยา ฮุค renderTracked มักจะทำงานเมื่อมีการเตรียมใช้งานส่วนประกอบที่เป็นปฏิกิริยา

hook ของ renderTriggered ทำงานเมื่อองค์ประกอบปฏิกิริยาที่ติดตามการเปลี่ยนแปลง ดังนั้นจึงทริกเกอร์การเรนเดอร์ใหม่ เพื่อให้หน้าจอได้รับการอัปเดตด้วยการเปลี่ยนแปลงล่าสุด



**ส่วนประกอบที่เกิดปฏิกิริยา** เป็นส่วนประกอบที่สามารถเปลี่ยนแปลงได้

**ฟังก์ชันการเรนเดอร์** เป็นฟังก์ชันที่คอมไพล์โดย Vue ซึ่งคอยติดตามส่วนประกอบที่เกิดปฏิกิริยา เมื่อส่วนประกอบที่เกิดปฏิกิริยาเปลี่ยนแปลง ฟังก์ชันการเรนเดอร์จะถูกทริกเกอร์และเรนเดอร์แอปพลิเคชันไปที่หน้าจออีกครั้ง



hooks renderTracked และ renderTriggered มีไว้เพื่อใช้ในการดีบัก และใช้ได้เฉพาะในโหมดการพัฒนาเท่านั้น

หากต้องการดู alert() และ console.log() จาก hooks renderTracked และ renderTriggered คุณต้องคัดลอกโค้ดในตัวอย่างด้านล่างไปยังคอมพิวเตอร์ของคุณและเรียกใช้แอปพลิเคชันในโหมดการพัฒนา

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component One</h2>
  <p>This is a component.</p>
  <button @click="counter++">Add One</button>
  <p>{{ counter }}</p>
</template>
  
<script>
export default {
  data() {
    return {
      counter: 0
    }
  },
  renderTracked(evt) {
    console.log("renderTracked: ",evt);
    alert("renderTracked");
  },
  renderTriggered(evt) {
    console.log("renderTriggered: ",evt)
    alert("renderTriggered");
  }
}
</script>
```

##### `App.vue`:

```html
<template>
  <h1>The 'renderTracked' and 'renderTriggered' Lifecycle Hooks</h1>
  <p>The 'renderTracked' and 'renderTriggered' lifecycle hooks are used for debugging.</p>
  <p><mark>This example only works in development mode, so to see the hooks run, you must copy this code and run it on you own computer in development mode.</mark></p>
  <div>
    <comp-one></comp-one>
  </div>
</template>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin-top: 10px;
    background-color: lightgreen;
  }
</style>
```

หมายเหตุ: โค้ดในตัวอย่างข้างต้นมีจุดมุ่งหมายให้คัดลอกและรันในเครื่องคอมพิวเตอร์ของคุณในโหมดการพัฒนา เนื่องจาก hooks renderTracked และ renderTriggered ใช้งานได้ในโหมดการพัฒนาเท่านั้น



## The 'activated' and 'deactivated' Lifecycle Hooks

ดังที่เราเห็นข้างต้นในหน้านี้ เรามี hooks วงจรการใช้งานที่ต่อเชื่อมและไม่ได้ต่อเชื่อมไว้สำหรับเมื่อส่วนประกอบถูกถอดออกหรือเพิ่มลงใน DOM

hooks วงจรการใช้งานที่เปิดใช้งานและปิดใช้งานมีไว้สำหรับเมื่อมีการเพิ่มหรือลบส่วนประกอบไดนามิกที่แคชไว้ แต่ไม่ใช่จาก DOM แท็ก <KeepAlive> ใช้ในตัวอย่างด้านล่างเพื่อแคชส่วนประกอบไดนามิก

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>Below is a log with every time the 'mounted' or 'activated' hooks run.</p>
  <ol ref="olEl"></ol>
  <p>You can also see when these hooks run in the console.</p>
</template>
  
<script>
export default {
  mounted() {
    console.log("mounted");
    const liEl = document.createElement("li");
    liEl.innerHTML = "mounted";
    this.$refs.olEl.appendChild(liEl);
  },
  activated() {
    console.log("activated");
    const liEl = document.createElement("li");
    liEl.innerHTML = "activated";
    this.$refs.olEl.appendChild(liEl);
  }
}
</script>

<style>
  li {
    background-color: lightcoral;
    width: 5em;
  }
</style>
```

##### `App.vue`:

```html
<template>
  <h1>The 'activated' Lifecycle Hook</h1>
  <p>In this example for the 'activated' hook we check if the component is cached properly with <KeepAlive>.</p>
  <p>If the component is cached properly with <KeepAlive> we expect the 'mounted' hook to run once the first time the component is included (must be added to the DOM the first time), and we expect the 'activated' hook to run every time the component is included (also the first time).</p>
  <button @click="this.activeComp = !this.activeComp">Include component</button>
  <div>
    <KeepAlive>
      <comp-one v-if="activeComp"></comp-one>
    </KeepAlive>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin-top: 10px;
    background-color: lightgreen;
  }
</style>
```

ลองขยายตัวอย่างด้านบนเพื่อดูว่าทั้ง hooks ที่เปิดใช้งานและปิดใช้งานทำงานอย่างไร ลองใช้ hooks ที่ติดตั้งและไม่ได้ต่อเชื่อมด้วย เพื่อให้เราเห็นว่า hook ที่ติดตั้งทำงานเมื่อเพิ่มส่วนประกอบที่แคชไว้เป็นครั้งแรก และตะขอที่ไม่ได้ต่อเชื่อมจะไม่ทำงานสำหรับส่วนประกอบที่แคชไว้

### Example

##### `CompOne.vue`:

```html
<template>
  <h2>Component</h2>
  <p>Below is a log with every time the 'activated', 'deactivated', 'mounted' or 'unmounted' hooks run.</p>
  <ol ref="olEl"></ol>
  <p>You can also see when these hooks run in the console.</p>
</template>
  
<script>
export default {
  mounted() {
    this.logHook("mounted");
  },
  unmounted() {
    this.logHook("unmounted");
  },
  activated() {
    this.logHook("activated");
  },
  deactivated() {
    this.logHook("deactivated");
  },
  methods: {
    logHook(hookName) {
      console.log(hookName);
      const liEl = document.createElement("li");
      liEl.innerHTML = hookName;
      this.$refs.olEl.appendChild(liEl);
    }
  }
}
</script>

<style>
  li {
    background-color: lightcoral;
    width: 5em;
  }
</style>
```

##### `App.vue`:

```html
<template>
  <h1>The 'activated' and 'deactivated' Lifecycle Hooks</h1>
  <p>In this example for the 'activated' and 'deactivated' hooks we also see when and if the 'mounted' and 'unmounted' hooks are run.</p>
  <button @click="this.activeComp = !this.activeComp">Include component</button>
  <div>
    <KeepAlive>
      <comp-one v-if="activeComp"></comp-one>
    </KeepAlive>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeComp: false
    }
  }
}
</script>

<style scoped>
  div {
    border: dashed black 1px;
    border-radius: 10px;
    padding: 20px;
    margin-top: 10px;
    background-color: lightgreen;
  }
</style>
```



## The 'serverPrefetch' Lifecycle Hook

ฮุก 'serverPrefetch' จะถูกเรียกระหว่างการเรนเดอร์ฝั่งเซิร์ฟเวอร์ (SSR) เท่านั้น

การอธิบายและการสร้างตัวอย่างสำหรับฮุค 'serverPrefetch' จะต้องมีการแนะนำและการตั้งค่าที่ค่อนข้างยาว และนั่นอยู่นอกเหนือขอบเขตของบทช่วยสอนนี้