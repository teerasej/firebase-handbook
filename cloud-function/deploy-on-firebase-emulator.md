
# Deploy และทดสอบ Cloud Function บน Firebase Emulator

ให้เปิด terminal เข้าไปที่โฟลเดอร์ **functions** และรันคำสั่งด้านล่าง เพื่อทำการ deploy function ไปที่ Firebase project 

**แบบนี้คือการ deploy บน firebase service จริง**

```bash
firebase deploy --only functions
```

ตรงนี้จะพบว่า ถ้าไม่ได้ปรับเป็น Pay as you go (ฺBlaze Plan) จะไม่สามารถ deploy ได้ (แอบเหนียวหน่อย)

**เราจึงจะสลับไป deploy ทดสอบบน emulator แทน** โดยใช้คำสั่งด้านล่างเพื่อเริ่มการทำงานของ Emulator 

```bash
firebase emulators:start --only functions
```

เสร็จแล้วใช้ปุ่มลัด Ctrl + C เพื่อหยุดการทำงาน

## ทำการ build และ redeploy ใหม่ในโปรเจค TypeScript 

ด้วยคำสั่งที่มีมาให้ใน package.json ทำให้เราสามารถใช้คำสั่งลัดที่โปรเจคเตรียมไว้ได้

```bash
npm run-script serve
```

ซึ่งคำสั่งนี้จะทำ 2 อย่าง ก็คือ 

```bash
// build โปรเจค typescript จะมีการ compile โค้ด typescript เป็น javascript 
npm run build 

// เริ่มการทำงานของ emulator 
firebase emulators:start --only functions
```

> ถ้ามีการเปิด hot reload ตามขั้นตอนการ[สร้างโปรเจคก่อนหน้านี้](create-cloud-function-project.md) ก็ไม่ต้องปิดเปิดใหม่เมื่อมีการแก้ไขโค้ด