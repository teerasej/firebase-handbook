

# การแสดงรายการไฟล์และ folder

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. สังเกตข้อมูลใน Firebase Console > Storage > Files
3. ทดสอบการทำงานของโค้ดด้านล่าง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getStorage, ref, uploadBytes
, listAll } from "firebase/storage";



// ...

console.log('\n --- File ---')
console.log('   8: Upload File')

// เพิ่มตัวเลือกในการแสดงรายการไฟล์
console.log('   9: List Files')


//....

switch (command) {
    
    //...

     case 9:

        try {
            if (!signedInUser) {
                console.log('   please sign in first.')
                continue
            }

            const storage = getStorage(app)

            // อ้างอิงถึง root ของ Storage ใน project
            const rootRef = ref(storage)

            // เราสามารถระบุ path ที่ต้องการอ้างอิงตำแหน่งเพื่อแสดงไฟล์ และโฟลเดอร์ได้ด้วย
            // const pathRef = ref(storage, 'path')

            // query ข้อมูลไฟล์ และโฟลเดอร์จากตำแหน่งอ้างอิง
            const fileList = await listAll(rootRef)

            // โฟลเดอร์จะอยู่ใน property ชื่อ .prefixes
            if (fileList.prefixes.length > 0) {
                console.log('Folders:')
                fileList.prefixes.forEach(folder => {
                    console.log(`   ${folder.name}`)
                });
            }

            // ไฟล์จะอยู่ใน property ชื่อ .items
            if (fileList.items.length > 0) {
                console.log('\nFiles:')
                fileList.items.forEach(file => {
                    console.log(`   ${file.name}`)
                });
            }



        } catch (error) {
            console.log('Error:', error)
        }

        break
}
```

## ลองของ

- ทำให้ตัวเลือกด้านบน สามารถแสดงไฟล์ที่อยู่ในโฟลเดอร์ย่อย (sub-folder) ของ Storage ด้วยได้ไหม?
