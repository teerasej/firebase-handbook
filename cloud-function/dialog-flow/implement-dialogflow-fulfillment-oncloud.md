

# สร้างกลไกการอ่านข้อมูล Request จาก DialogFlow

## 1. ติดตั้ง package 

```
npm install dialogflow-fulfillment
npm install --save-dev @types/dialogflow-fulfillment
```

## 2. เขียนส่วนการอ่านข้อมูล Request จาก DialogFlow และตอบกลับ 

เปิดไฟล์ **functions/src/index.ts** และแก้ไขโค้ดตามด้านล่าง

```ts
// import WebhookClient 
import { WebhookClient } from "dialogflow-fulfillment";
import * as functions from "firebase-functions";

export const webhook = functions.https.onRequest((request, response) => {
    
    // สร้าง Trycatch
    try {
    
        functions.logger.info('start function...')

        // สร้าง webhook client โดยนำ request และ response ที่ได้จาก function มาใช้งาน
        // ในที่นี้ request แบบที่ไม่ได้มาจาก DialogFlow จะทำให้เกิด error
        const agent = new WebhookClient({
          request: request,
          response: response
        });
        
        // log ดูชื่อ intent
        functions.logger.info(agent.intent)
        // log ดู parameter ที่ส่งมากับ intent
        functions.logger.info(agent.parameters)

        // สร้าง intent map เพื่อตอบกลับ intent ใน DialogFlow
        let intentMap = new Map()

        // เทียบชื่อ intent 
        if(agent.intent == 'registerNewPerson') {
            
            // ส่งข้อความกลับไปที่ intent ตามชื่อ
            intentMap.set('registerNewPerson', (agent:WebhookClient) => {
              agent.add('this is working...')
            })
        }

        // กำหนด intent map ให้กับ agent 
        agent.handleRequest(intentMap)
        
      } catch (error) {
        // log error ถ้ามีข้อผิดพลาด
        functions.logger.error(error)
      }

})

```