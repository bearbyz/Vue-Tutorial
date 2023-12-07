# Vue HTTP Requests

คำขอ HTTP เป็นส่วนหนึ่งของการสื่อสารระหว่างไคลเอนต์และเซิร์ฟเวอร์

ไคลเอนต์ส่งคำขอ HTTP ไปยังเซิร์ฟเวอร์ ซึ่งจัดการคำขอและส่งกลับการตอบสนอง HTTP



## HTTP

HTTP ย่อมาจาก Hypertext Transfer Protocol

เบราว์เซอร์ของเราส่งคำขอ HTTP ตลอดเวลาในเบื้องหลังเมื่อเราท่องอินเทอร์เน็ต เมื่อเราเข้าถึงหน้าอินเทอร์เน็ต เบราว์เซอร์ของเรา (ไคลเอนต์) จะส่งคำขอ HTTP หลายรายการเพื่อให้เซิร์ฟเวอร์ส่งหน้าที่เราต้องการพร้อมไฟล์และข้อมูลที่เกี่ยวข้องทั้งหมดเป็นการตอบกลับ HTTP

คำขอ HTTP ประเภทที่พบบ่อยที่สุดคือ POST, GET, PUT, PATCH และ DELETE เรียนรู้เพิ่มเติมเกี่ยวกับคำขอ HTTP ประเภทต่างๆ ในหน้าวิธีการร้องขอ HTTP ของเรา

เรียนรู้เพิ่มเติมเกี่ยวกับ HTTP ในหน้า HTTP คืออะไรของเรา



## The 'fetch' Method

ในการรับข้อมูลจากเซิร์ฟเวอร์ใน Vue เราสามารถใช้ JavaScript fetch() วิธีการ

เมื่อเราใช้เมธอด fetch() ในบทช่วยสอนนี้ เราจะไม่ระบุวิธีการร้องขอ HTTP และนั่นหมายความว่าวิธีการร้องขอเริ่มต้น GET คือสิ่งที่ใช้ในเบื้องหลัง

วิธีการ fetch() คาดว่าที่อยู่ URL จะเป็นอาร์กิวเมนต์เพื่อที่จะรู้ว่าจะรับข้อมูลจากที่ไหน

นี่คือตัวอย่างง่ายๆ ที่ใช้วิธีการ fetch() เพื่อส่งคำขอ HTTP GET และรับข้อมูลเป็นการตอบกลับ HTTP ข้อมูลที่ร้องขอในกรณีนี้คือข้อความภายในไฟล์ในเครื่อง file.txt:

### Example

##### `App.vue`:

```html
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <p v-if="data">{{ data }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null,
    };
  },
  methods: {
    fetchData() {
      const response = fetch("file.txt");
      this.data = response;
    }
  }
};
</script>
```

ในตัวอย่างข้างต้น เราได้รับผลลัพธ์เพียง "[object Promise]" เท่านั้น แต่นั่นไม่ใช่สิ่งที่เราต้องการ

เราได้รับผลลัพธ์นี้เนื่องจากการ fetch() เป็นวิธีการตามสัญญาที่ส่งคืนอ็อบเจ็กต์สัญญา ดังนั้นการส่งคืนเมธอด fetch() ครั้งแรกจึงเป็นเพียงออบเจ็กต์ซึ่งหมายความว่ามีการส่งคำขอ HTTP แล้ว นี่คือสถานะ "รอดำเนินการ"

เมื่อเมธอด fetch() ได้รับข้อมูลที่เราต้องการจริง ๆ คำสัญญาก็เป็นจริง

เพื่อรอการตอบสนองให้บรรลุผลด้วยข้อมูลที่เราต้องการ เราจำเป็นต้องใช้ตัวดำเนินการ await ที่อยู่ด้านหน้าเมธอด fetch():

```js
const response = await fetch("file.txt");
```

When the `await` operator is used inside a method, the method is required to be declared with the `async` operator:

```js
async fetchData() {
  const response = await fetch("file.txt");
  this.data = response;
}
```

ตัวดำเนินการ async จะบอกเบราว์เซอร์ว่าวิธีการดังกล่าวเป็นแบบอะซิงโครนัส ซึ่งหมายความว่าเบราว์เซอร์จะรอบางสิ่งบางอย่าง และเบราว์เซอร์สามารถทำงานอื่นต่อไปได้ในขณะที่รอให้วิธีการดำเนินการเสร็จสิ้น

ตอนนี้สิ่งที่เราได้รับคือ "การตอบกลับ" และไม่ใช่แค่ "คำสัญญา" อีกต่อไป ซึ่งหมายความว่าเราเข้าใกล้การรับข้อความจริงในไฟล์ file.txt ไปอีกก้าวแล้ว:

### Example

##### `App.vue`:

```html
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <p v-if="data">{{ data }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null,
    };
  },
  methods: {
    async fetchData() {
      const response = await fetch("file.txt");
      this.data = response;
    }
  }
};
</script>
```

ในการรับข้อความภายในไฟล์ file.txt เราจำเป็นต้องใช้เมธอด text() ในการตอบกลับ เนื่องจากเมธอด text() เป็นเมธอดตามสัญญา เราจึงจำเป็นต้องใช้ตัวดำเนินการ await ข้างหน้าเมธอด

ในที่สุด! ตอนนี้เรามีสิ่งที่ต้องการเพื่อรับข้อความจากภายในไฟล์ file.txt ด้วยเมธอด fetch():

### Example

##### `App.vue`:

```html
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <p v-if="data">{{ data }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null,
    };
  },
  methods: {
    async fetchData() {
      const response = await fetch("file.txt");
      this.data = await response.text();
    }
  }
};
</script>
```



## Fetch Data from a JSON File

ในตัวอย่างก่อนหน้านี้ เราดึงข้อความจากไฟล์ .txt แต่มีหลายวิธีในการจัดเก็บข้อมูล และตอนนี้เราจะมาดูกันว่าเราสามารถดึงข้อมูลจากไฟล์ .json ได้อย่างไร

JSON เป็นรูปแบบไฟล์ทั่วไปที่ใช้งานง่าย เนื่องจากข้อมูลถูกจัดเก็บเป็นข้อความเพื่อให้มนุษย์อ่านได้ง่าย และรูปแบบ JSON ยังได้รับการสนับสนุนอย่างกว้างขวางในภาษาการเขียนโปรแกรม เพื่อให้เราสามารถ เช่น ระบุสิ่งที่ ข้อมูลที่จะแยกจากไฟล์ .json

หากต้องการอ่านข้อมูลจากไฟล์ .json การเปลี่ยนแปลงเพียงอย่างเดียวที่เราต้องทำกับตัวอย่างด้านบนคือการดึงไฟล์ .json และใช้วิธี json() แทนวิธี text() ในการตอบกลับ

วิธีการ json() อ่านการตอบสนองจากคำขอ HTTP และส่งกลับวัตถุ JavaScript

เราใช้แท็ก <pre> ที่นี่เพื่อแสดงข้อความที่จัดรูปแบบ JSON เนื่องจากจะรักษาช่องว่างและการขึ้นบรรทัดใหม่เพื่อให้อ่านได้ง่ายขึ้น

### Example

##### `App.vue`:

```html
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <pre v-if="data">{{ data }}</pre>
  </div>
</template>

<script>
export default {
  data() {
    return {
      data: null,
    };
  },
  methods: {
    async fetchData() {
      const response = await fetch("bigLandMammals.json");
      this.data = await response.json();
    }
  }
};
</script>
```

เนื่องจากผลลัพธ์ของเมธอด json() คืออ็อบเจ็กต์ JavaScript เราจึงสามารถแก้ไขตัวอย่างด้านบนเพื่อแสดงสัตว์แบบสุ่มจากไฟล์ bigLandMammals.json:

### Example

##### `App.vue`:

```html
<template>
  <p>Try clicking the button more than once to see new animals picked randomly.</p>
  <button @click="fetchData">Fetch Data</button>
  <div v-if="randomMammal">
    <h2>{{ randomMammal.name }}</h2>
    <p>Max weight: {{ randomMammal.maxWeight }} kg</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      randomMammal: null
    };
  },
  methods: {
    async fetchData() {
      const response = await fetch("bigLandMammals.json");
      const data = await response.json();
      const randIndex = Math.floor(Math.random()*data.results.length);
      this.randomMammal = data.results[randIndex];
    }
  }
};
</script>
```



## Data from an API

API ย่อมาจาก Application Programming Interface คุณสามารถเรียนรู้เพิ่มเติมเกี่ยวกับ API ได้ที่นี่

มี API ฟรีที่น่าสนใจมากมายที่เราสามารถเชื่อมต่อและใช้งานได้ เพื่อรับข้อมูลสภาพอากาศ ข้อมูลตลาดหลักทรัพย์ ฯลฯ

การตอบสนองที่เราได้รับเมื่อเราเรียกใช้ API ด้วยคำขอ HTTP สามารถมีข้อมูลได้ทุกประเภท แต่มักจะมีข้อมูลในรูปแบบ JSON

### Example

สามารถคลิกปุ่มเพื่อรับผู้ใช้แบบสุ่มจาก Random-data-api.com API

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Click the button to fetch data with an HTTP request.</p>
  <p>Each click generates an object with a random user from <a href="https://random-data-api.com/" target="_blank">https://random-data-api.com/</a>.</p>
  <p>The robot avatars are lovingly delivered by <a href="http://Robohash.org" target="_blank">RoboHash</a>.</p>
  <button @click="fetchData">Fetch data</button>
  <pre v-if="data">{{ data }}</pre>
</template>

<script>
  export default {
    data() {
      return {
        data: null,
      };
    },
    methods: {
      async fetchData() {      
        const response = await fetch("https://random-data-api.com/api/v2/users"); 
        this.data = await response.json();
      }   
    }
  };
</script>
```

เราสามารถแก้ไขตัวอย่างก่อนหน้านี้ได้เล็กน้อยเพื่อรวมผู้ใช้แบบสุ่มในลักษณะที่เป็นมิตรต่อผู้ใช้มากขึ้น:

### Example

เราจะแสดงชื่อผู้ใช้แบบสุ่มในแท็ก <pre> พร้อมด้วยตำแหน่งงานและรูปภาพเมื่อมีการคลิกปุ่ม

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Click the button to fetch data with an HTTP request.</p>
  <p>Each click generates an object with a random user from <a href="https://random-data-api.com/" target="_blank">https://random-data-api.com/</a>.</p>
  <p>The robot avatars are lovingly delivered by <a href="http://Robohash.org" target="_blank">RoboHash</a>.</p>
  <button @click="fetchData">Fetch data</button>
  <div v-if="data" id="dataDiv">
    <img :src="data.avatar" alt="avatar">
    <pre>{{ data.first_name + " " + data.last_name }}</pre>
    <p>"{{ data.employment.title }}"</p>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        data: null,
      };
    },
    methods: {
      async fetchData() {      
        const response = await fetch("https://random-data-api.com/api/v2/users"); 
        this.data = await response.json();
      },    
    }
  };
</script>

<style>
#dataDiv {
  width: 240px;
  background-color: aquamarine;
  border: solid black 1px;
  margin-top: 10px;
  padding: 10px;
}
#dataDiv > img {
  width: 100%;
}
pre {
  font-size: larger;
  font-weight: bold;
}
</style>
```



## HTTP Request in Vue with The 'axios' Library

ไลบรารี JavaScript 'axios' ยังช่วยให้เราส่งคำขอ HTTP ได้

หากต้องการสร้างและรันตัวอย่างบนเครื่องของคุณเอง คุณต้องติดตั้งไลบรารี 'axios' ก่อนโดยใช้เทอร์มินัลในโฟลเดอร์โปรเจ็กต์ของคุณ เช่นนี้:

```
npm install axios
```

นี่คือวิธีที่เราสามารถใช้ไลบรารี 'axios' ใน Vue เพื่อดึงข้อมูลผู้ใช้แบบสุ่ม:

### Example

มีการเปลี่ยนแปลงเพียงเล็กน้อยกับตัวอย่างก่อนหน้านี้เพื่อทำคำขอ HTTP ด้วยไลบรารี 'axios' แทน

##### `App.vue`:

```html
<template>
  <h1>Example</h1>
  <p>Click the button to fetch data with an HTTP request.</p>
  <p>Each click generates an object with a random user from <a href="https://random-data-api.com/" target="_blank">https://random-data-api.com/</a>.</p>
  <p>The robot avatars are lovingly delivered by <a href="http://Robohash.org" target="_blank">RoboHash</a>.</p>
  <button @click="fetchData">Fetch data</button>
  <div v-if="data" id="dataDiv">
    <img :src="data.data.avatar" alt="avatar">
    <pre>{{ data.data.first_name + " " + data.data.last_name }}</pre>
    <p>"{{ data.data.employment.title }}"</p>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        data: null,
      };
    },
    methods: {
      async fetchData() {      
        this.data = await axios.get("https://random-data-api.com/api/v2/users");
      }
    }
  };
</script>

<style>
#dataDiv {
  width: 240px;
  background-color: aquamarine;
  border: solid black 1px;
  margin-top: 10px;
  padding: 10px;
}
#dataDiv > img {
  width: 100%;
}
pre {
  font-size: larger;
  font-weight: bold;
}
</style>
```