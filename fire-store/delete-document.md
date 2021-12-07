
# การลบข้อมูลบน FireStore

สำหรับการลบข้อมูลลงใน FireStore จะใช้แนวคิดของ Collection และ Document ในระบบฐานข้อมูลแบบ NoSQL เช่นกัน

ซึ่ง function ของ firebase/firestore ก็จะถอดแบบออกมาเลยครับ

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบแสดงข้อมูลที่มี document id จาก collection 
3. ทดสอบการทำงานของโค้ดด้านล่าง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getFirestore, collection, addDoc, getDocs, doc, serverTimestamp, query, where
, deleteDoc } from 'firebase/firestore';


// ...

console.log('\n --- Note ---')
console.log('   4: Create tweet')
console.log('   5: List tweets')

// เพิ่มตัวเลือกในการลบ document
console.log('   6: Remove tweet')


//....

switch (command) {
    
    //...

    case 6:

        try {

            // เช็คว่าผู้ใช้ ลงชื่อเข้าใช้งานหรือยัง
            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            // อ่านค่า message Id
            const messageId = readline.question('Message ID to delete:')                         

            const fireStore = getFirestore(app)

            // ระบุตำแหน่งของ document เป้าหมาย โดยอาศัยชื่อ  collection และ id ของ document (ในที่นี้เราเรียกว่า message Id)
            const deletingDoc = doc(fireStore,'/notes', messageId)

            // สั่งลบ document ตามที่อ้างอิง
            await deleteDoc(deletingDoc)
        
            console.log(`   doc ${messageId} deleted.`)
            
        } catch (error) {
            console.log('Error', error)
        }
        
        
        break
}
```
