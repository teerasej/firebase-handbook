
#  Export function เข้า cloud function

เปิดไฟล์ **functions/src/index.ts** และแก้ไขตามข้อมูลด้านล่าง

```ts
//... 
import * as admin from 'firebase-admin'
import * as createMessageFunc from './messages/createMessage';

admin.initializeApp()

//..
export const createMessage = createMessageFunc.createMessage

```

จากนั้นให้ ทดสอบรัน Cloud function แบบ Emulator ดูว่ามีชื่อ function แสดงขึ้นมาไหม