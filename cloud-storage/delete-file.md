

# การลบไฟล์ 

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > Storage > Files
3. ทดสอบการทำงานของโค้ดด้านล่าง


```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getStorage, ref, uploadBytes, listAll
, deleteObject } from "firebase/storage";


// ...

console.log('\n --- File ---')
console.log('   8: Upload File')
console.log('   9: List Files')

// เพิ่มตัวเลือกในการลบไฟล์
console.log('   10: Delete File')



//....

switch (command) {
    
    //...

       case 10:

            try {
                if (!signedInUser) {
                    console.log('   please sign in first.')
                    continue
                }

                // ระบุที่อยู่ไฟล์อ้างอิงบน Storage
                const targetFileName = readline.question('Target remote file (ex. assets/nextflow.png):')

                if (!targetFileName || targetFileName.length == 0) {
                    continue
                }

                const storage = getStorage(app)

                // สร้างตำแหน่งอ้างอิงของไฟล์เป้าหมาย
                const fileRef = ref(storage, targetFileName)

                console.log(`   deleting file: '${targetFileName}'.`)

                // สั่งลบไฟล์เป้าหมาย
                await deleteObject(fileRef)
                console.log(`   deleted.`)
            
            } catch (error) {
                console.log('Error:', error)
            }

            break
}
```

## ลองของ

- ทำให้ตัวเลือกด้านบน สามารถลบโฟลเดอร์ หรือ directory ได้ไหม?
