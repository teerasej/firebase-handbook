
# การอ่านข้อมูลจาก FireStore

สำหรับการอ่านข้อมูลลงใน FireStore จะใช้แนวคิดของ Collection และ Document ในระบบฐานข้อมูลแบบ NoSQL เช่นกัน

ซึ่ง function ของ firebase/firestore ก็จะถอดแบบออกมาเลยครับ

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. เพิ่มข้อมูลจำนวนหนึ่งเข้าไปใน Collection 
3. สังเกตข้อมูลใน Firebase Console > FireStore Database > Data
4. ทดสอบการทำงานของโค้ดด้านล่าง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getFirestore, collection, addDoc, serverTimestamp
, getDocs, query, where } from 'firebase/firestore';

// ...

// เพิ่มตัวเลือกในการแสดง documents
console.log('\n --- Note ---')
console.log('   4: Create tweet')
console.log('   5: List tweets')


//....

switch (command) {
    
    //...

    case 5:

        try {

            // เช็คว่าผู้ใช้ signin หรือยัง
            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            const fireStore = getFirestore(app)

            // อ้างอิงถึง collection เป้าหมาย
            const noteCollection = collection(fireStore,'/notes')

            // ใช้ query ในการเช็คและดึงข้อมูลเฉพาะ id
            const q = query(noteCollection, where("userId", "==", signedInUser.uid));

            // ใช้ function ในการ query ข้อมูลมาจาก FireStore service
            const messageSnapshots = await getDocs(q)

            // แปลงข้อมูล documents ที่ได้ ให้อยู่ในรูปแบบที่ต้องการนำไปใช้
            // โดยข้อมูลของ document จะเข้าถึงได้จาก function .data()
            // และ document id จะอยู่ใน property .id
            const messageArray = messageSnapshots.docs.map(doc => { 
                            return { ...doc.data(), id: doc.id }
                        });

            
            // วนลูปแสดงข้อมูลที่ได้
            for (let index = 0; index < messageArray.length; index++) {
                const message = messageArray[index];

                // แสดง index และ document id
                console.log(`[${index}]: ${message.id}`)

                // แสดงข้อมูล json แบบจัด format ผ่านหน้า console
                console.log(JSON.stringify(message,null,'\t'))
            }

        } catch (error) {
            console.log('Error', error)
        }
        
        
        break
}
```
