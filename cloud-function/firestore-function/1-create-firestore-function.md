
# สร้าง Cloud Function ที่ทำการเพิ่มข้อมูลลง FireStore

สร้างไฟล์ **functions/src/messages/createMessage.ts**

```ts
// functions/src/messages/createMessage.ts


import * as functions from "firebase-functions";
import * as admin from 'firebase-admin'

// ตั้งชื่อ function ว่า createMessage สังเกตว่าเราใช้ .onCall แทน .onRequest
export const createMessage = functions.https.onCall(async (data, context) => {

    // check auth จาก context ว่ามีข้อมูลที่ authen แล้วหรือเปล่า (ปกติจะส่งมาโดย SDK)
    if(context.auth?.token == null) {
        // โยน error 
        return new functions.https.HttpsError('unauthenticated', 'oops....')
    }

    functions.logger.info(`token: ${context.auth?.token.email}`)

    try {
        // ดึงข้อมูลจาก data
        const { message, userId } = data

        // เข้าถึง firestore
        const firestore = admin.firestore()

        // เพิ่ม document ลง collection notes
        await firestore.collection('notes').add({ message: message, userId: userId})
        
        // ข้อมูลที่ส่งกลับจะถูกแปลงเป็น object 
        return {
            status: 200
        }
    } catch (error:any) {
        return new functions.https.HttpsError('internal', error.message)
    }

})
```