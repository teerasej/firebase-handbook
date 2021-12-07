
# การอัพเดตแก้ไขข้อมูลบน FireStore

สำหรับการอัพเดตแก้ไขข้อมูลของ document ใน FireStore จะใช้แนวคิดของ Collection และ Document ในระบบฐานข้อมูลแบบ NoSQL เช่นกัน

ซึ่ง function ของ firebase/firestore ก็จะถอดแบบออกมาเลยครับ

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบแสดงข้อมูลที่มี document id จาก collection 
3. ทดสอบการทำงานของโค้ดด้านล่าง
4. ระบุ document id และข้อความที่ต้องการแก้ไข

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getFirestore, collection, addDoc, getDocs, doc, serverTimestamp, query, where, deleteDoc
, getDoc, updateDoc } from 'firebase/firestore';



// ...

console.log('\n --- Note ---')
console.log('   4: Create tweet')
console.log('   5: List tweets')
console.log('   6: Remove tweet')

// เพิ่มตัวเลือกในการอัพเดต document
console.log('   7: Edit tweet')


//....

switch (command) {
    
    //...

    case 7:

        try {
            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            // รับ document Id
            const messageId = readline.question('Message ID to Edit:')
            
            
            const fireStore = getFirestore(app)

            // ระบุตำแหน่งของ document 
            const targetDoc = doc(fireStore, '/notes', messageId)

            // query ข้อมูล 
            const editingDoc = await getDoc(targetDoc)
            console.log(`Current message: ${editingDoc.data().message}`)
            const newMessage = readline.question('New Message:')

            await updateDoc(targetDoc, {
                message: newMessage,
                updatedDate: serverTimestamp()
            })

            // หรีือบางตัวอย่างจะใช้ setDoc (อย่าลืม import setDoc มาล่ะ )
            // วิธีนี้จะทำให้ไม่ต้อง query ข้อมูลมาที่ client
            // 
            // await setDoc(targetDoc, {
            //     message: newMessage,
            //     updatedDate: serverTimestamp()
            // }, { merge: true });

            console.log(`   doc ${messageId} updated with '${newMessage}'.`)

        } catch (error) {
            console.log('Error', error)
        }

        break
}
```
