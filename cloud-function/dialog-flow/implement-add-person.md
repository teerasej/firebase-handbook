
# สร้างกลไกการบันทึกข้อมูลบน Cloud Function

## 1. ติดตั้ง package 

```
npm install firebase-admin
```

## 2. เขียนส่วนการบันทึกข้อมูลลง Firebase 

สร้างไฟล์ **functions/src/addPerson.ts** ตามด้านล่าง

```ts
import * as admin from 'firebase-admin'

export const addPerson = async (firstName:string) => {
    await admin.firestore().collection('persons').add({ firstName: firstName })
}
```


## 3. นำมาใช้งานใน webhook function 

เราจะทำการเรียกใช้ addPerson() ในไฟล์ webhook.ts

```ts

// import addPerson
import { addPerson } from './addPerson';
import { WebhookClient } from "dialogflow-fulfillment";
import * as functions from "firebase-functions";

export const webhook = functions.https.onRequest((request, response) => {
    
    try {
    
        functions.logger.info('start function...')
    
        const agent = new WebhookClient({
          request: request,
          response: response
        });
        
        functions.logger.info(agent.intent)
        functions.logger.info(agent.parameters)
    
        let intentMap = new Map()
    
        if(agent.intent == 'registerNewPerson') {
            
            // เรียกใช้งาน addPerson
            addPerson(agent.parameters.fisrtName)

            intentMap.set('registerNewPerson', (agent:WebhookClient) => {
              // ส่งข้อความกลับ
              agent.add('person created...')
            })
        }
    
        agent.handleRequest(intentMap)
        
      } catch (error) {
        functions.logger.error(error)
      }

})

```