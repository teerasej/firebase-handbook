
# เรียกใช้งาน callable function

จากนั้นให้เราเขียนเรียกใช้งาน callable function ได้ตาม

```js
const functions = getFunctions(app);
connectFunctionsEmulator(functions, "localhost", 5001);

// เรียก function ชื่อ createMessage (ต้องเป็นชื่อเดียวกับที่สร้างไว้ใน Cloud function ไม่งั้นหาไม่เจอนา)
const createMessage = httpsCallable(functions, 'createMessage');

// เรียกใช้ function โดยใส่ข้อมูลลงไปใน JSON
const result = await createMessage({ userId: signedInUser.uid, message: message })

// ลองเอาข้อมูลที่ส่งกลับมาแสดงใน console
console.log('   message created:', result.data)
```

เสร็จแล้วให้ทดสอบรัน client ด้วยคำสั่ง 

```bash
node index
```

และลองเลือกตัวเลือกที่ 2 เพื่อใส่ข้อมูล จากนั้นลองไปดูใน firestore ว่ามีอะไรเปลี่ยนแปลงไหม