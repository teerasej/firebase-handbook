
# การส่งอีเมลล์ยืนยันตัวตน (Verification Email)

แนวทางการป้องกันการ spam ในปัจจุบัน จะมีการใช้การส่ง Email ยืนยันให้ผู้ใช้คลิกผ่าน link 

## 1. การส่ง Email ยืนยันตัวตน

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบการลงทะเบียน และสังเกตผลลัพธ์ใน Firebase Console
3. เช็คกล่อง Email และคลิกลิ้งค์
4. ทดสอบแก้ไข Email Template: Firebase console > Authentication > Template
5. บันทึก template และทดสอบลงทะเบียนอีกครั้ง

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getAuth, createUserWithEmailAndPassword
, sendEmailVerification } from "firebase/auth";


//....

switch (command) {
    case 1: 
        try {

            //...

            console.log(userCredential.user)
            
            // ส่ง Email สำหรับการยืนยันตัวตน
            await sendEmailVerification(user)

        } catch (error) {
            console.log('Error', error)
        }
    break
}
```

## 2. การกำหนด Redirect URI 

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบการลงทะเบียน และสังเกตผลลัพธ์ใน Firebase Console
3. เช็คกล่อง Email และคลิกลิ้งค์
4. สังเกตผลลัพธ์ที่เปลี่ยนไป

```js
// index.js

//....

switch (command) {
    case 1: 
        try {

            //...

            console.log(userCredential.user)

            // กำหนด redirect URL หลังจากผู้ใช้กด link ใน Verification Email แล้ว
            let actionCodeSettings = {
                url: 'http://localhost:3000/?email=' + user.email,
            }

            // ส่ง action code setting
            await sendEmailVerification(user,actionCodeSettings)

        } catch (error) {
            console.log('Error', error)
        }
    break
}
```