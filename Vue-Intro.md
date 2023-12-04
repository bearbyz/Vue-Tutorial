# บทนำ Vue

Vue เป็น **เฟรมเวิร์ก JavaScript** สามารถเพิ่มลงในหน้า HTML ด้วยแท็ก <script>

Vue ขยายแอตทริบิวต์ HTML ด้วย **Directives (คำสั่ง)** และเชื่อมโยงข้อมูลเป็น HTML ด้วย **Expressions (นิพจน์)**



## **Vue เป็น JavaScript Framework**

Vue เป็น front-end JavaScript framework ที่เขียนด้วย JavaScript

เฟรมเวิร์กที่คล้ายกันกับ Vue คือ React และ Angular แต่ Vue นั้นมีความเบากว่าและเริ่มต้นได้ง่ายกว่า

Vue ได้ distributed เป็นไฟล์ JavaScript และสามารถเพิ่มลงในเว็บเพจด้วยแท็กสคริปต์:

```html
<script
  src="https://unpkg.com/vue@3/dist/vue.global.js">
</script>
```



## ทำไมถึงเรียน Vue?

- มันง่ายและใช้งานง่าย
- สามารถจัดการทั้งโครงการที่เรียบง่ายและซับซ้อนได้
- ความนิยมที่เพิ่มขึ้นและการสนับสนุนชุมชนโอเพ่นซอร์ส
- ใน JavaScript ปกติ เราจำเป็นต้องเขียน **HOW** HTML และ JavaScript เชื่อมต่อกัน แต่ใน Vue เราเพียงต้องแน่ใจว่ามีการเชื่อมต่อ **IS** และปล่อยให้ Vue จัดการส่วนที่เหลือ
- ช่วยให้กระบวนการพัฒนามีประสิทธิภาพมากขึ้นด้วย template-based syntax, two-way data binding และ centralized state management.

หากบางประเด็นเหล่านี้เข้าใจยาก ไม่ต้องกังวล คุณจะเข้าใจในตอนท้ายของบทช่วยสอน



## ตัวเลือก API

มีสองวิธีในการเขียนโค้ดใน Vue: Options API และ Composition API

แนวคิดพื้นฐานจะเหมือนกันสำหรับทั้ง Options API และ Composition API ดังนั้นหลังจากเรียนรู้แนวคิดหนึ่งแล้ว คุณจึงสามารถสลับไปยังอีกแนวคิดหนึ่งได้อย่างง่ายดาย

Options API คือสิ่งที่เขียนไว้ในบทช่วยสอนนี้ เนื่องจากถือว่าเป็นมิตรกับผู้เริ่มต้นมากกว่า โดยมีโครงสร้างที่เป็นที่รู้จักมากกว่า



## หน้าแรกของฉัน

ตอนนี้เราจะเรียนรู้วิธีสร้างเว็บเพจ Vue แรกของเราใน 5 ขั้นตอนพื้นฐาน:

1. เริ่มต้นด้วยไฟล์ HTML พื้นฐาน
2. เพิ่มแท็ก `<div>` ด้วย `id="app"` เพื่อให้ Vue เชื่อมต่อด้วย
3. บอกเบราว์เซอร์ถึงวิธีจัดการโค้ด Vue โดยเพิ่มแท็ก `<script>` พร้อมลิงก์ไปยัง Vue
4. เพิ่มแท็ก `<script>` โดยมี Vue instance อยู่ข้างใน
5. เชื่อมต่ออินสแตนซ์ Vue กับแท็ก `<div id="app">`

ขั้นตอนเหล่านี้มีการอธิบายไว้โดยละเอียดด้านล่าง โดยมีโค้ดเต็มอยู่ในตัวอย่าง 'Try It Yourself' ในตอนท้าย

### ขั้นตอนที่ 1: หน้า HTML

เริ่มต้นด้วยหน้า HTML ง่ายๆ:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My first Vue page</title>
</head>
<body>

</body>
</html>
```

### ขั้นตอนที่ 2: เพิ่ม <div>

Vue ต้องการองค์ประกอบ HTML บนเพจของคุณเพื่อเชื่อมต่อ

ใส่แท็ก `<div>` ไว้ในแท็ก `<body>` และกำหนดรหัส:

```html
<body>
  <div id="app"></div>
</body>
```

### ขั้นตอนที่ 3: เพิ่มลิงก์ไปยัง Vue

เพื่อช่วยให้เบราว์เซอร์ของคุณตีความโค้ด Vue ของเรา ให้เพิ่มแท็ก `<script>` นี้:

```html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

### ขั้นตอนที่ 4: เพิ่มอินสแตนซ์ Vue

ตอนนี้เราต้องเพิ่มโค้ด Vue ของเรา

สิ่งนี้เรียกว่า **Vue instance** และสามารถมีข้อมูล วิธีการ และอื่นๆ แต่ตอนนี้มีเพียงข้อความเท่านั้น

ในบรรทัดสุดท้ายในแท็ก `<script>` นี้ Vue instance ของเราเชื่อมต่อกับแท็ก `<div id="app">`:

### ขั้นตอนที่ 5: แสดง 'ข้อความ' ด้วยการแก้ไขข้อความ

สุดท้ายนี้ เราสามารถใช้ **การแก้ไขข้อความ** ซึ่งเป็นไวยากรณ์ Vue ที่มีเครื่องหมายปีกกาคู่ `{{ }}` เป็นตัวยึดตำแหน่งสำหรับข้อมูล

```html
<div id="app"> {{ message }} </div>
```

เบราว์เซอร์จะแลกเปลี่ยน `{{ message }}` กับข้อความที่เก็บไว้ในคุณสมบัติ 'message' ภายในอินสแตนซ์ Vue

นี่คือหน้า Vue หน้าแรกของเรา:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <title>My first Vue page</title>
</head>
<body>

  <div id="app">
    {{ message }}
  </div>

  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

  <script>
    const app = Vue.createApp({
      data() {
        return {
          message: "Hello World!"
        }
      }
    })

   app.mount('#app')

  </script>
</body>
</html>
```



## **การแก้ไขข้อความ**

การแก้ไขข้อความคือเมื่อข้อความถูกนำมาจากอินสแตนซ์ Vue เพื่อแสดงบนหน้าเว็บ

เบราว์เซอร์ได้รับหน้าพร้อมรหัสนี้ภายใน: 

```html
<div id="app"> {{ message }} </div>
```

จากนั้นเบราว์เซอร์จะค้นหาข้อความภายในคุณสมบัติ 'ข้อความ' ของอินสแตนซ์ Vue และแปลโค้ด Vue เป็นดังนี้:

```html
<div id="app">Hello World!</div>
```



## JavaScript ในการ Text Interpolation

**JavaScript expressions** แบบธรรมดาสามารถเขียนภายในเครื่องหมายปีกกาคู่ `{{ }}` ได้

```html
<div id="app">
  {{ message }} <br>
  {{'Random number: ' + Math.ceil(Math.random()*6) }}
</div>

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

<script>

  const app = Vue.createApp({
    data() {
      return {
        message: "Hello World!"
      }
    }
  })

 app.mount('#app')

</script>
```

