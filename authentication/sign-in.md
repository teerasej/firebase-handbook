
# การลงชื่อเข้าใช้งาน 

แนวทางการป้องกันการ spam ในปัจจุบัน จะมีการใช้การส่ง Email ยืนยันให้ผู้ใช้คลิกผ่าน link 

## 1. ทดสอบการลงชื่อเข้าใช้

1. ทำการ implement เงื่อนไขการทำงานตามด้านล่าง
2. ทดสอบการลงชื่อเข้าใช้
3. สังเกตผลลัพธ์ที่ได้ 

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getAuth, createUserWithEmailAndPassword, sendEmailVerification
, signInWithEmailAndPassword } from "firebase/auth";


//...


console.log('\n==== Firebase Client ====')
console.log('   0: Exit')
console.log('   1: Create new user')

// เพิ่มตัวเลือกในการลงชื่อเข้าใช้
console.log('   2: Sign in user')

//...

switch (command) {
    
    //..


    // เพิ่มตัวเลือกที่ 2
    case 2:
    
        try {

            const email = readline.questionEMail()
            const password = readline.question('password:')
            console.log(email, password)

            const auth = getAuth()

            // ทำการลงชื่อเข้าใช้ด้วย email และ password
            const userCredential = await signInWithEmailAndPassword(auth, email, password)

            console.log(userCredential.user)

            
        } catch (e) {
            console.error('error:',e)
        }
        
        break
}
```

## 2. เช็คว่าผู้ใช้ยืนยันตัวตนผ่าน Verification Email หรือยัง 

จะสังเกตว่าผู้ใช้ที่ยังไม่ได้กดยืนยันตัวตนก็สามารถเข้าใช้งานระบบได้ 

ถ้าต้องการเราสามารถเช็คได้ว่าผู้ใช้ยืนยันตัวตนผ่าน Email หรือยัง เพื่อป้องกันไม่ให้ผู้ใช้ไม่ประสงค์ดี เข้าใช้งานระบบได้ทันที

```js
// index.js

// ...

// import function ที่ต้องการใช้งาน
import { getAuth, createUserWithEmailAndPassword, sendEmailVerification
, signInWithEmailAndPassword } from "firebase/auth";


//...


console.log('\n==== Firebase Client ====')
console.log('   0: Exit')
console.log('   1: Create new user')

// เพิ่มตัวเลือกในการลงชื่อเข้าใช้
console.log('   2: Sign in user')

//...

switch (command) {
    
    //..

    case 2:
    
        try {

            //.. 

            const userCredential = await signInWithEmailAndPassword(auth, email, password)

            console.log(userCredential.user)

            // เช็คว่า Email Verified หรือยัง
            if(userCredential.user.emailVerified) {
                console.log(`Hello, ${userCredential.user.email}`)
            } else {
                console.log('Sorry, But you need to check your email and click the verification link.')
            }
            
        } catch (e) {
            console.error('error:',e)
        }
        
        break
}
```