

# สร้าง Cloud function ในการเรียกข้อมูลผู้ติดเชื้อใหม่

## 1. สร้าง Cloud function ใหม่ 

```ts
// functions/src/covid/getCOVIDNewCase.ts

import * as functions from "firebase-functions";
import { getCovidDataJSON } from './getCovidDataJSON';

export const getCOVIDNewCase = functions.https.onRequest(async (request, response) => {

    // เรียกใช้ข้อมูล
    const data = await getCovidDataJSON()

    // สังเกตว่าเป็นการสร้าง json ใหม่ และเจาะจงเฉพาะข้อมูล
    response.status(200).json({ newCase: data[0].new_case})

})
```

## 2. Export function เข้า cloud function

เปิดไฟล์ **functions/src/index.ts** และแก้ไขตามข้อมูลด้านล่าง

```ts

import * as getAllCovidInfoFunc from './covid/getAllCovidInfo';

// import function ที่สร้างไว้
import * as getCOVIDNewCaseFunc from './covid/getCOVIDNewCase';

export const getAllCovidInfo = getAllCovidInfoFunc.getAllCovidInfo

// ทำการ export โดยตั้งชื่อไว้
export const getCOVIDNewCase = getCOVIDNewCaseFunc.getCOVIDNewCase
```

จากนั้นให้

1. ทดสอบรัน Cloud function แบบ Emulator 
2. ทดสอบการใช้งานผ่าน URL 
3. สังเกต Log จาก UI ของ Functions Emulator