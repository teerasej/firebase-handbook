
# สร้าง Cloud Function ที่ใช้ในการสร้าง user ใหม่

## 1. สร้าง Cloud function

สร้างไฟล์ **functions/src/users/createUser.ts**

```ts
// functions/src/users/createUser.ts

import * as functions from "firebase-functions";

// เรียกใช้ firebase-admin
import * as admin from 'firebase-admin'

// ตั้งชื่อ function ว่า createUser
export const createUser = functions.https.onRequest(async (request, response) => {

    // ใช้ try catch ในการส่ง response
    try {

        // ถึงข้อมูล json ออกมาจาก body ได้เลย parse มาให้เรียบร้อย
        const { email, password } = request.body

        // เรียกใช้ authentication service ของ firebase
        const auth = admin.auth()

        // สั่งสร้าง user ใหม่
        const newUser = await auth.createUser({
            email: email,
            password: password
        })

        // ตอบกลับไปที่ client 
        response.status(200).send('ok')
    } catch (error) {
        response.status(500).json(error)
    }

})
```

## 2. Export Cloud function 

เราจะทำการปรับปรุงไฟล์ **functions/src/index.ts**


```ts
// functions/src/index.ts

//.. 
import * as functions from "firebase-functions";
import * as admin from 'firebase-admin'

// import ตัว function 
import * as createUserFunc from './users/createUser'


admin.initializeApp()

//..

// export ให้ Cloud function ทำงาน
export const createUser = createUserFunc.createUser
```