
# สร้าง function ใช้งานภายใน

เราจะแยกส่วนของการเรียกข้อมูลจาก Web API มา เพื่อแยกใช้กับ Cloud function อื่นๆ 

## 1. สร้าง TypeScript function ธรรมดา

สร้างไฟล์ใหม่ สังเกตว่าเหมือนกับการเขียนใช้งาน typescript ทั่วไป

```ts
// functions/src/covid/getCovidDataJSON.ts

import * as axios from "axios";

export const getCovidDataJSON = async () => {

    const http = axios.default;
    const covidResult = await http.get('https://covid19.ddc.moph.go.th/api/Cases/today-cases-all')
    return covidResult.data
}
```

## 2. ปรับปรุงให้ getAllCovidInfo เรียกใช้ข้้อมูลจาก function ที่แยกไว้ต่างหาก

เสร็จตรงนี้แล้วให้ 

1. ทดสอบรัน Cloud function แบบ Emulator 
2. ทดสอบการใช้งานผ่าน URL 
3. สังเกต Log จาก UI ของ Functions Emulator

```ts
// functions/src/covid/getAllCovidInfo.ts

import * as functions from "firebase-functions";
import { getCovidDataJSON } from './getCovidDataJSON';

export const getAllCovidInfo = functions.https.onRequest(async (request, response) => {

    const data = await getCovidDataJSON()
    response.status(200).json(data)
})
```