
# ทดสอบการทำงาน

1. ในที่นี้ให้ลองกำหนด intent ใน dialog flow สามารถรับ parameter ที่ชื่อ **firstName** ดู 
   1. เข้าไปที่ส่วน intent
   2. เลือก intent ที่ต้องการ
   3. กำหนด training phase ให้รับ pamameter
   4. กำหนดชื่อ parameter เป็น **firstName** และกำหนดให้ **required**
   5. อย่าลืมใส่ prompt เพื่อทำให้สมบูรณ์มากขึ้น 

<img width="1082" alt="2021-12-13_23-03-57" src="https://user-images.githubusercontent.com/85179/145846830-4f393757-c6a4-495a-b50e-ea6995168bb3.png">


1. จากนั้นให้ลองใช้ dialog flow หรือ channel chat อื่นๆ ส่งข้อมูลเข้ามา
2. จากนั้นสังเกตผลลัพธ์ใน firebase emulator

## Note 

ทาง LINE Thailand ได้[นำเสนอตัวอย่างของการ custom message ไว้](https://medium.com/linedevth/%E0%B9%80%E0%B8%9E%E0%B8%B4%E0%B9%88%E0%B8%A1%E0%B8%84%E0%B8%A7%E0%B8%B2%E0%B8%A1%E0%B8%99%E0%B9%88%E0%B8%B2%E0%B8%AA%E0%B8%99%E0%B9%83%E0%B8%88%E0%B9%83%E0%B8%AB%E0%B9%89-line-bot-%E0%B8%82%E0%B8%AD%E0%B8%87%E0%B8%84%E0%B8%B8%E0%B8%93%E0%B8%94%E0%B9%89%E0%B8%A7%E0%B8%A2%E0%B8%81%E0%B8%B2%E0%B8%A3%E0%B8%AA%E0%B9%88%E0%B8%87%E0%B8%82%E0%B9%89%E0%B8%AD%E0%B8%84%E0%B8%A7%E0%B8%B2%E0%B8%A1%E0%B8%A3%E0%B8%B9%E0%B8%9B%E0%B9%81%E0%B8%9A%E0%B8%9A%E0%B8%95%E0%B9%88%E0%B8%B2%E0%B8%87%E0%B9%86%E0%B8%9C%E0%B9%88%E0%B8%B2%E0%B8%99-dialogflow-6ec1a9c2c05e) สามารถลองประยุกต์ต่อยอดได้ครับ