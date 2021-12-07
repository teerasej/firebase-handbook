


# Practice: Upload ไฟล์พร้อมกับโพสข้อความขึ้น FireStorePractice: Upload ไฟล์พร้อมกับโพสข้อความขึ้น FireStore


1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > Storage > Files
3. ทดสอบการทำงานของโค้ดด้านล่าง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getStorage, ref, uploadBytes } from "firebase/storage";
import * as fs from 'fs/promises'


//....

switch (command) {
    
    //...

        case 4:

            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            const message = readline.question('Messsage:')

            if (!message) {
                continue
            }

            // กำหนดตัวเลือกสำหรับให้เพิ่มไฟล์เข้าไปในโพส
            console.log('Attach photo?')
            console.log('1. No')
            console.log('2. Yes')

            const attachPhotoChoice = readline.questionInt('Type command:')
            
            let requestAttachPhoto = false
            

            if(attachPhotoChoice != 1) {
                requestAttachPhoto = true
            }

            // บันทึกข้อความขึ้น FireStore
            const fireStore = getFirestore(app)
            const noteCollection = collection(fireStore,'/notes')
            const doc = await addDoc(noteCollection, {
                userId: signedInUser.uid,
                message: message,
                createdDate: serverTimestamp()
            })

            // ถ้ามีการอัพโหลดรูปให้ระบุที่อยู่ของรูป
            if(requestAttachPhoto) {

                const fileName = readline.question('File name to upload:')

                if(!fileName || fileName.length == 0) {
                    continue
                }
                
                // อัพโหลดรูปขึ้น storage โดยกำหนดให้ไปอยู่ใน images directory
                const storage = getStorage(app)
                const remoteFileRef = ref(storage, `images/${fileName}`)
                const buffer = await fs.readFile(fileName)

                console.log('   uploading...')
                // อัพโหลด
                const result = await uploadBytes(remoteFileRef, buffer)
                console.log('   uploaded...')
                
                // อัพเดตที่อยู่ของไฟล์บน Storage ให้กับโพส
                await setDoc(doc, {
                    attachFile: result.ref.fullPath
                }, { merge: true })
            }
            
            break
}
```
