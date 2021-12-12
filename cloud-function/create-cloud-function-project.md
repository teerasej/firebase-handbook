
# สร้างโปรเจค Cloud Function ด้วย firebase CLI

## 1. สร้างโปรเจค

1. สร้างโฟลเดอร์โปรเจคใหม่ 
2. รันคำสั่ง

```bash
firebase init
```

3. เราจะสามารถเลือก emulator ที่ต้องการได้ (เลือกโดยการกด space bar เลื่อนตัวเลือกด้วยลูกศรขึ้นลง) ให้เลือกเป็น **Functions**

> จริงๆ เราสามารถข้ามขั้นตอนนี้ได้โดยการรันคำสั่ง `firebase init functions`

4. จะมีให้เลือกโปรเจค Firebase จริงที่ผูกกับ Emulator สามารถเลือก ระหว่าง 

- **Use an existing project** (ถ้ามีสร้างไว้อยู่แล้ว) 
- กับ **Create a new project** (อันนี้ระวัง เพราะ account ไม่ใส่ billing information จะสร้างโปรเจคได้จำกัด)


5. จะมีการให้เราเลือก template เป็นภาษาอะไร ในที่นี้จะเลือกเป็นโปรเจคเป็น typescript (เพราะเราต้องการใช้ import/export async/await ฮา)

6. **ESLint** ให้ตอบ no ไปก่อน สำหรับการ workshop จะได้ไม่เสียเวลา
7. **install dependencies with npm** ให้ตอบ yes
8. เสร็จเรียบร้อย ได้โปรเจคที่มีโฟลเดอร์ชื่อ functions อยู่ข้างใน


## 2. เปิดการทำงานของ Hot Reload

แก้ไขไฟล์ **functions/package.json** ตามลำดับ

1. ทำการเพิ่มคำสั่ง `"build:watch": "tsc --watch --preserveWatchOutput"` เข้าไปใน `script`
2. แก้ไขคำสั่ง `serve` ใน `script` ให้เป็นแบบด้านล่าง

```json
{
  ...
  "scripts": {
    ...
    "build:watch": "tsc --watch --preserveWatchOutput",
    "serve": "npm run build:watch | firebase emulators:start --only functions",
    ...
```

ทำให้พอเราแก้ไขโค้ดแล้วบันทึกไฟล์ จากนั้นรีเฟรชหรือส่ง request เข้ามาที่ cloud function ก็จะเป็นโค้ดชุดใหม่ 

ไม่ต้องปิดๆ เปิดๆ อีกต่อไป

