# คำสั่ง Vue

คำสั่ง Vue เป็นแอตทริบิวต์ HTML พิเศษที่มีคำนำหน้า `v-` ซึ่งทำให้แท็ก HTML มีฟังก์ชันการทำงานพิเศษ

คำสั่ง Vue เชื่อมต่อกับอินสแตนซ์ Vue เพื่อสร้างอินเทอร์เฟซผู้ใช้แบบไดนามิกและแบบโต้ตอบ

ด้วย Vue การสร้างเพจแบบตอบสนองนั้นง่ายกว่ามากและต้องใช้โค้ดน้อยกว่าเมื่อเทียบกับวิธี JavaScript แบบดั้งเดิม



## คำสั่ง Vue ที่แตกต่างกัน

คำสั่ง Vue ต่างๆ ที่เราใช้ในบทช่วยสอนนี้มีดังต่อไปนี้

| **Directive**                                            | **Details**                                                  |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| [v-bind](https://www.w3schools.com/vue/vue_v-bind.php)   | เชื่อมต่อแอตทริบิวต์ในแท็ก HTML กับตัวแปรข้อมูลภายในอินสแตนซ์ Vue         |
| [v-if](https://www.w3schools.com/vue/vue_v-if.php)       | สร้างแท็ก HTML ขึ้นอยู่กับเงื่อนไข คำสั่ง v-else-if และ v-else ใช้ร่วมกับคำสั่ง v-if |
| [v-show](https://www.w3schools.com/vue/vue_v-show.php)   | ระบุว่าควรมองเห็นองค์ประกอบ HTML หรือไม่ ขึ้นอยู่กับเงื่อนไข              |
| [v-for](https://www.w3schools.com/vue/vue_v-for.php)     | สร้างรายการแท็กตามอาร์เรย์ในอินสแตนซ์ Vue โดยใช้ for-loop           |
| [v-on](https://www.w3schools.com/vue/vue_v-on.php)       | เชื่อมต่อเหตุการณ์บนแท็ก HTML กับนิพจน์ JavaScript หรือวิธีการอินสแตนซ์ Vue นอกจากนี้เรายังสามารถกำหนดได้อย่างเจาะจงมากขึ้นว่าเพจของเราควรตอบสนองต่อเหตุการณ์ใดเหตุการณ์หนึ่งอย่างไรโดยใช้ตัวแก้ไขเหตุการณ์ |
| [v-model](https://www.w3schools.com/vue/vue_v-model.php) | ใช้ในรูปแบบ HTML พร้อมด้วยแท็กเช่น <form>, <input> และ <button> สร้างการเชื่อมโยงสองทางระหว่างองค์ประกอบอินพุตและคุณสมบัติข้อมูลอินสแตนซ์ Vue |

### ตัวอย่าง: คำสั่ง `v-bind`

เบราว์เซอร์จะค้นหาคลาสที่จะเชื่อมต่อองค์ประกอบ <div> จากอินสแตนซ์ Vue

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <style>
    .pinkBG {
      background-color: lightpink;
    }
  </style>
</head>
<body>

  <div id="app">
    <div v-bind:class="vueClass"></div>
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
  <script>
    const app = Vue.createApp({
      data() {
        return {
          vueClass: "pinkBG"
        }
      }
    })
    app.mount('#app')
  </script>
</body>
</html>
```

