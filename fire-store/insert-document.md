
# การเพิ่มข้อมูลลง Collection

สำหรับการเพิ่มข้อมูลลงใน FireStore จะใช้แนวคิดของ Collection และ Document ในระบบฐานข้อมูลแบบ NoSQL 

ซึ่ง function ของ firebase/firestore ก็จะถอดแบบออกมาเลยครับ

## 1. เพิ่มข้อมูลลง FireStore

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > FireStore Database > Data
3. ทดสอบการทำงานของโค้ดด้านล่าง
4. กลับไปสังเกตข้อมูลใน FireStore

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getFirestore, collection, addDoc } from 'firebase/firestore';



// ...

console.log('\n==== Firebase Client ====')
console.log('   0: Exit')

// เพิ่มตัวเลือกในการสร้างข้อมูลที่อิงกับผู้ใช้
console.log('\n --- Note ---')
console.log('   4: Create tweet')


//....

switch (command) {
    
    //...

    case 4:

        //..

        // เข้าถึง firestore 
        const fireStore = getFirestore(app)

        // อ้างอิงถึง collection ตาม path ชื่อ notes
        const noteCollection = collection(fireStore,'/notes')
        

        console.log('   posting new tweet...')
        // ทำการเพิ่มข้อมูลลง document สำหรับ note collection
        // id ของ doc จะถูกสุ่มขึ้นเองใน firestore 
        await addDoc(noteCollection, {

            // ใช้ uid ของ user 
            userId: signedInUser.uid,

            // กำหนดข้อความ
            message: message
        })
        console.log('   posted.')

        break
}
```

## 2. การใช้ time stamp

ปกติเราต้องการบันทึกว่าข้อมูลถูกสร้าง หรือแก้ไขล่าสุดเมื่อไหร่ ในที่นี้เรามี function ชื่อ `serverTimestamp()` ช่วย

```js
// import serverTimestamp()
import { getFirestore, collection, addDoc
, serverTimestamp } from 'firebase/firestore';

//..

await addDoc(noteCollection, {
    userId: signedInUser.uid,
    message: message,

    // เรียกใช้ serverTimeStamp เพื่อใช้เป็น createdDate
    createdDate: serverTimestamp()
})

```