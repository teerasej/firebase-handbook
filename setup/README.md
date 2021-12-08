
# Setup Localhost Project

## 1. สร้างโฟลเดอร์โปรเจค

สร้างโฟลเดอร์โปรเจค my-firebase

และรันคำสั่ง npm init เพื่อกำหนดข้อมูลพื้นฐานของโปรเจค Node

```bash
npm init
```

## 2. ติดตั้ง package ที่จำเป็น

ทำการรันคำสั่งด้านล่างเพื่อติดตั้ง firebase package 

```bash
npm i firebase readline-sync
```

```bash
yarn add firebase readline-sync
```

## 3. ทำการ init firebase app 

สร้างไฟล์ index.js 

```js
// เรียกใช้ function 'initializeApp' จาก module 'firebase/app'
import { initializeApp } from "firebase/app";

const firebaseConfig = {
    //... configuration ที่ได้จากการ Setup SDK บน Firebase console 
    // ให้เลือกเพิ่ม WWW app และคัดลอกมาได้เลย
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);

```

## 4. สร้าง top level async function 

ในปัจจุบัน ตัว Node.js ยังไม่สามารถทำงานแบบ Asynchronous แบบเป็นค่าเริ่มต้นได้ เราเลยต้องสร้าง Async function ด้านนอกสุด 

เพื่อให้เราสามารถเขียนใช้งานโค้ด javascript แบบใช้ keyword async/await ได้

```js
// ...

const app = initializeApp(firebaseConfig);

// สร้าง top level async function 
(async () => {

})();

```


## 5. สร้างเมนูคำสั่งเพื่อให้สั่งงานผ่าน Console ได้ 

เราจะสร้างเมนูบน console อย่างง่ายๆ และรันทดสอบด้วยคำสั่ง

```bash
node index
```

โค้ดที่เพิ่ม 

```js
// ...
import * as readline from "readline-sync";

// ...

const app = initializeApp(firebaseConfig);

(async () => {


    let command = -1;

    // วนลูปรับคำสั่งไปเรื่อยๆ จนกว่า command จะเป็น 0
    do {
        // แสดง menu 
        console.log('\n==== Firebase Client ====')
        console.log('   0: Exit')

        // รับคำสั่งเป็นตัวเลข
        console.log('Type command:')
        command = readline.questionInt()

    } while(command != 0)
})();
```

## ไฟล์สมบูรณ์ 

```js

import { initializeApp } from "firebase/app";
import * as readline from "readline-sync";

const firebaseConfig = {
    //... configuration ที่ได้จากการ Setup SDK บน Firebase console 
    // ให้เลือกเพิ่ม WWW app และคัดลอกมาได้เลย
};

const app = initializeApp(firebaseConfig);

(async () => {

    let command = -1;

    do {
        console.log('\n==== Firebase Client ====')
        console.log('   0: Exit')

        console.log('Type command:')
        command = readline.questionInt()

    } while(command != 0)
})();
```