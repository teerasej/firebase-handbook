
# การอัพโหลดไฟล์

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > Storage > Files
3. ทดสอบการทำงานของโค้ดด้านล่าง
4. กลับไปสังเกตข้อมูลใน Storage

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getStorage, ref, uploadBytes } from "firebase/storage";

// module สำหรับทำงานกับไฟล์
import * as fs from 'fs/promises'


// ...

console.log('\n==== Firebase Client ====')
console.log('   0: Exit')

// เพิ่มตัวเลือกในการอัพโหลดไฟล์
console.log('\n --- File ---')
console.log('   8: Upload File')


//....

switch (command) {
    
    //...

    case 8:
        try {
            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            // ระบุชื่อไฟล์ (กำหนดให้อยู่ในโฟลเดอร์โปรเจค)
            const fileName = readline.question('File name to upload:')

            if (!fileName || fileName.length == 0) {
                continue
            }

            // ระบุที่อยู่ของไฟล์แบบ path บน Storage
            const remoteLocation = readline.question('Remote location (ex. asset/images):')

            if (!remoteLocation || remoteLocation.length == 0) {
                continue
            }

            // เรียกใช้ storage instance
            const storage = getStorage(app)

            // ใน ref() ในการระบบที่อยู่ของไฟล์ (ในตอนนี้จะไม่มีไฟล์ดังกล่าวอยู่จริงๆ )
            const remoteFileRef = ref(storage, `${remoteLocation}/${fileName}`)

            // อ่านไฟล์เป็น buffer 
            const buffer = await fs.readFile(fileName)

            console.log(`   uploading '${fileName}' to '${remoteLocation}'...`)
            // อัพโหลดไปยังที่อยู่อ้างอิงของไฟล์บน storage
            const result = await uploadBytes(remoteFileRef, buffer)
            console.log('   uploaded...')

        } catch (error) {
            console.log('Error', error)
        }


        break
}
```
