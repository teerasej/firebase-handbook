
#  Export function เข้า cloud function

เปิดไฟล์ **functions/src/index.ts** และแก้ไขตามข้อมูลด้านล่าง

```ts
// import function ที่สร้างไว้ในไฟล์อื่นมา
import * as getAllCovidInfoFunc from './covid/getAllCovidInfo';

// ทำการ export โดยตั้งชื่อไว้
export const getAllCovidInfo = getAllCovidInfoFunc.getAllCovidInfo
```

จากนั้นให้

1. ทดสอบรัน Cloud function แบบ Emulator 
2. ทดสอบการใช้งานผ่าน URL 
3. สังเกต Log จาก UI ของ Functions Emulator