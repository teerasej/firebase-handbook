
# Hard code authentication

การใช้งาน API ในส่วนที่เหลือจะเป็นส่วนที่ต้องมีการ authenticate ผู้ใช้ดังกล่าวเข้าระบบก่อน 

ดังนั้น

1. เราจะทำการสร้าง function สำหรับ authenticate ผู้ใช้ออกมาต่างหาก 
2. และทำการ authenticate ผู้ใช้ 1 บัญชีแบบ hard code ตอนเริ่มโปรแกรม

## 1. สร้าง function สำหรับ authenticate ผู้ใช้

```js
// index.js

// import statements...

// สร้าง signIn function ไว้ตอนเริ่มโปรแกรม
const signIn = async (email, password) => {
    try {

        console.log(email, password)

        const auth = getAuth()
        const userCredential = await signInWithEmailAndPassword(auth, email, password)

        if (userCredential.user.emailVerified) {
            console.log(`Hello, ${userCredential.user.email}`)

            // return user object ถ้า sign in ได้สำเร็จ
            return userCredential.user

        } else {
            console.log('Sorry, But you need to check your email and click the verification link.')
        }

    } catch (e) {
        console.error('error:', e)

        // return null ถ้ามีข้อผิดพลาด
        return null;
    }
}

```

## 2. ทำการ authenticate ผู้ใช้ 1 บัญชีแบบ hard code ตอนเริ่มโปรแกรม

```js
// index.js 

// ...

let command = -1;

// สร้างตัวแปรเพื่อเช็ค
let signedInUser;

// ทำการ authenticate ผู้ใช้ 1 บัญชีแบบ hard code ก่อนแสดง menu
signedInUser = await signIn( 'Email ที่ลงทะเบียนในระบบแล้ว','รหัสผ่าน')

do {
    console.log('\nFirebase Client')

     do {
            console.log('Firebase Client')

            console.log('   0: Exit')
            console.log('   1: Create new user')
            console.log('   2: Sign in user')
            console.log('   3: Check email exists')

            console.log('Type command:')
            const command = readline.questionInt()

            if (command == 0) {
                break;
            }

            switch (command) {

                case 1:
                    try {
                        
                        //...
                        const userCredential = await createUserWithEmailAndPassword(auth, email, password)
                        
                        // หลังจากลงทะเบียนแล้ว ก็กำหนด user object เก็บไว้ใช้งานในตัวแปร signedInUser
                        signedInUser = userCredential.user
                        console.log(signedInUser)

                        //..
                    } catch (e) {
                        //..
                    }
                    break

                case 2:
                    const email = readline.questionEMail()
                    const password = readline.question('password:')

                    // ปรับให้ใช้งาน function signIn แทน
                    signedInUser = await signIn(email, password)

                    break
```