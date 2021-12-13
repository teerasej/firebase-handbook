
# กำหนด URL ของ Cloud Function เป็น Webhook ของ DialogFlow Agent

1. ในส่วนของ DialogFlow ให้เลือก Agent ที่ต้องการ 
2. จากนั้นลงมาคลิกที่ **fulfillment**
3. กด enable การตั้งค่าของ webhook
4. นำ url ที่ได้จาก ngrok หรือ cloud function มาใส่ไว้
5. กด Save 


<img width="1084" alt="2021-12-13_22-19-53" src="https://user-images.githubusercontent.com/85179/145840891-28fccfcf-b6b1-4742-99a4-1c8b18c7a8ca.png">


## Note 

- จะเห็นว่ามีส่วน inline editor ซึ่งเป็นการเขียน Cloud fucntion ได้เหมือนกัน แต่จะเป็นการเขียนผ่านหน้าเว็บ dialog flow เลย การเปิดใช้งานในส่วนนี้ จะมีการใส่ billing information (บัตรเครดิตหน่ะแหละ) ใน workshop นี้เราไม่ได้ต้องการใช้ส่วนนี้เลยจะข้ามไปนะครับ
- 1 Agent สามารถมีได้แค่ 1 Webhook นะ แต่ไม่ต้องห่วง request ที่ส่งไปจะมีชื่อของ intent ให้เราไปแยกแยะอีกที
