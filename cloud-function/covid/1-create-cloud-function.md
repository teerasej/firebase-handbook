
# สร้าง Cloud functions ในการเรียกข้อมูลผู้ติดเชื้อโดยรวม

## 1. ติดตั้ง Axios 

เราจะใช้ Axios เป็นตัวส่งและรับ request ให้ทำการติดตั้งโดยใช้คำสั่งด้านล่าง 

```bash
npm i axios
```

หรือ

```bash
yarn add axios 
```

## 2. สร้างไฟล์ และเขียน function 

```ts
// functions/src/covid/getAllCovidInfo.ts

import * as functions from "firebase-functions";
import * as axios from "axios";

export const getAllCovidInfo = functions.https.onRequest(async (request, response) => {

    // สร้าง instance ของ axios ในการใช้งาน
    const http = axios.default;

    // ส่ง request และรับ json 
    const covidResult = await http.get('https://covid19.ddc.moph.go.th/api/Cases/today-cases-all')

    // ทำการ log ใน cloud functions
    functions.logger.info(covidResult.data)

    // ตอบกลับ client ด้วยข้อมูลที่ได้มา
    response.status(200).json(covidResult.data)
})
```

