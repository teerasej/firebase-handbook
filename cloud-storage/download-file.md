


# การดาวน์โหลดไฟล์ 

## 1. ติดตั้ง package เพ่ิมเติม

```bash
npm i axios
```

```bash
yarn add axios
```

## 2. สร้างกลไกการดาวน์โหลดไฟล์


1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > Storage > Files
3. ทดสอบการทำงานของโค้ดด้านล่าง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getStorage, ref, uploadBytes, listAll, deleteObject
, getDownloadURL } from "firebase/storage";
import Axios from "axios";

// ...

console.log('\n --- File ---')
console.log('   8: Upload File')
console.log('   9: List Files')
console.log('   10: Delete File')
// เพิ่มตัวเลือกในการดาวน์โหลดไฟล์
console.log('   11: Download File')



//....

switch (command) {
    
    //...

        case 11:

            try {
                if (!signedInUser) {
                    console.log('   please sign in first.')
                    continue
                }

                // รับค่าที่อยู่อ้างอิงของไฟล์บน Storage
                const targetFileName = readline.question('Target remote file:')

                if (!targetFileName || targetFileName.length == 0) {
                    continue
                }

                const storage = getStorage(app)

                // สร้างตำแหน่งอ้างอิงของไฟล์เป้าหมาย
                const fileRef = ref(storage, targetFileName)

                console.log(`   Downloading file: '${targetFileName}'.`)

                // ขอ URL ไฟล์จริงสำหรับดาวน์โหลด
                const downloadURL = await getDownloadURL(fileRef)

                // ใช้ Axios ในการดาวน์โหลดไฟล์
                const res = await Axios.get(downloadURL, { responseType: "arraybuffer" });

                // เขียนไฟล์ลงในตำแหน่งที่ต้องการบนเครื่อง
                await fs.writeFile(fileRef.name, res.data);

                console.log(`   downloaded.`)

            } catch (error) {
                console.log('Error:', error)
            }

            break
}
```

## ลองของ

- ทำให้ตัวเลือกด้านบน สามารถดาวน์โหลดไฟล์ในโฟลเดอร์่ทั้งหมดลงมาในโฟลเดอร์ของโปรเจคได้ไหม
- ทำให้ตัวเลือกด้านบน กำหนดโฟลเดอร์ หรือ directory สำหรับเก็บไฟล์ที่จะถูกดาวน์โหลดลงมาในเครื่องได้ไหม
