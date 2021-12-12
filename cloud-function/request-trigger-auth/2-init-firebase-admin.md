
# ตั้งค่าเริ่มต้นให้ Firebase Admin  

เปิดไฟล์ **functions/src/index.ts** เราจะมีการเรียกใช้ function ก่อนการใช้งาน firebase admin

```ts
// ... 
import * as admin from 'firebase-admin'

admin.initializeApp()

// โค้ดที่เรียกใช้ firebase admin 
```