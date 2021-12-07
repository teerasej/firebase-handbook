

# การตรวจสอบว่า Email มีคนใช้งานหรือยัง


1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบกรอก Email เพื่อเช็คว่ามีอยู่บนระบบหรือไม่
3. สังเกตผลลัพธ์ที่ได้ 

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getAuth, createUserWithEmailAndPassword, sendEmailVerification,signInWithEmailAndPassword
, fetchSignInMethodsForEmail } from "firebase/auth";



//...


console.log('\n==== Firebase Client ====')
//..
// เพิ่มตัวเลือก
console.log('   3: Check email exists')


//...

switch (command) {
    
    //..


    // เพิ่มตัวเลือกที่ 3
    case 3:

        try {
            // ผู้ใช้กรอก Email 
            const email = readline.questionEMail()
            const auth = getAuth()

            // เรียกดูวิธีการ authentication ที่สามารถใช้ได้กับ email ที่ระบุ
            const methods = await fetchSignInMethodsForEmail(auth, email)

            // ถ้ามีวิธีการ authentication มากกว่า 1 วิธี แปลว่ามี email ดังกล่าวอยู่ในระบบ
            if(methods.length > 0) {
                console.log(`${email} already used.`)
            } else {
                console.log(`${email} is available`)
            }
            
        } catch (e) {
            console.error('error:',e)
        }
    break
}
```
