
# การลงทะเบียนด้วย Email 

สำหรับการลงทะเบียนสร้างบัญชีผู้ใช้บน Firebase พื้นฐาน เราสามารถเลือกใช้วิธีกำหนด Email เป็น username และรหัสผ่านแบบทั่วไปได้ 

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบการลงทะเบียน และสังเกตผลลัพธ์ใน Firebase Console

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";


// ...

console.log('\n==== Firebase Client ====')
console.log('   0: Exit')

// เพิ่มตัวเลือกในการสร้างผู้ใช้ใหม่
console.log('   1: Create new user')

//....

// สร้างกลไกในการรับค่า email และ password จนไปถึงการสร้างบัญชีผู้ใช้ใหม่
switch (command) {
    case 1: 
        try {

            // รับค่า email และ password
            const email = readline.questionEMail()
            const password = readline.question('password:')
            console.log(email, password)    

            // สร้าง authentication object 
            // ใน firebase sdk เวอร์ชั่นล่าสุด จะใช้ auth object ในการเข้าถึง api ต่างๆ 
            const auth = getAuth();

            // เรียกใช้ function ในการลงทะเบียนผู้ใช้ใหม่ ด้วย Email และ Password
            // ผลลัพธ์จะได้ user credential object
            const userCredential = await createUserWithEmailAndPassword(auth, email, password)

            // แสดงข้อมูลของ User
            console.log(userCredential.user)
            

        } catch (error) {
            console.log('Error', error)
        }
    break
}
```