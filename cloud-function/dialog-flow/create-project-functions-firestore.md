

# สร้างโปรเจค functions และ Firestore emulator

## 1. สร้างโฟลเดอร์โปรเจคใหม่ 

จากนั้นรันคำสั่ง 

```
firebase init
```

และเลือกตัวเลือก functions และ firestore

## 2. เลือกโปรเจค Firebase 

จะมีตัวเลือกให้สร้างโปรเจค Firebase ใหม่ (Create a new proejct) หรือใช้โปรเจค Firebase ที่มีอยู่แล้ว (Use Existing Project)

ถ้าเรียนกันมาตั้งแต่ตอนแรกๆ ก็ให้เลือกโปรเจค Firebase ที่สร้างไว้ก่อนหน้านี้นะ

## 3. กำหนดการทำงานของ FireStore Emulator 

- **What file should be used for Firestore Rules?** ให้ใช้ค่าเริ่มต้น firestore.rules 
- **What file should be used for Firestore indexes?** ให้ใช้ค่าเริ่มต้น firestore.indexes.json

## 4. กำหนดการทำงานของ Cloud functions project 

- **What language would you like to use to write Cloud Functions?** ให้เลือกเป็น typescript
- **Do you want to use ESLint to catch probable bugs and enforce style? (Y/n)** ตอบ n เพื่อความคล่องตัว (แต่ตอนทำจริงจะเปิดก็ได้นะ)
- **Do you want to install dependencies with npm now? (Y/n)** ตอบ y

## 5. เปิดการทำงานของ Hot Reload

เพื่อให้อำนวยความสะดวกในการพัฒนา [ให้ทำตามขั้นตอนนี้](../enable-hot-reload.md)

## 6. แก้ไขให้ตัวโปรเจครันการทำงานของ Firestore emulator ด้วย

แก้ไขไฟล์ **functions/package.json** โดยให้แก้ไขคำสั่ง `serve` ใน `script` ให้เป็นแบบด้านล่าง

```json
{
  ...
  "scripts": {
    ...
    "serve": "npm run build:watch | firebase emulators:start --only functions,firestore",
    ...
```

## 7. เขียน function webhook

เปิดไฟล์ **functions/src/index.ts **และแก้ไขโค้ดให้เป็นแบบด้านล่าง 

```ts
import * as functions from "firebase-functions";

export const webhook = functions.https.onRequest((request, response) => {
    response.send("Hello from Firebase!")
})

```


## 8. ทดสอบการทำงาน

ใช้คำสั่งด้านล่าง ภายในโปรเจค function

```
npm run-script serve 
```

และทดสอบใช้งาน URL ของ Cloud Functions
