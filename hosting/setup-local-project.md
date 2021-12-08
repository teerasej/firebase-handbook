
# Setup Local Project and deploy

## 1. เริ่มการ setup 

จากภายในโฟลเดอร์โปรเจค Web Application (SPA) เราจะรันคำสั่งเพิ่มเติมการ setup 

```bash
firebase init hosting
```

## 2. ตั้งค่า firebase hosting 

ขั้นตอนและคำถามจะแตกต่างไปตามเงื่อนไขที่เลือก เช่น ในที่นี้เราจะใช้วิธีการแบบไม่ auto deploy ผ่าน github แต่จะใช้การสั่งจากเครื่องเราโดยตรง 

### เลือกโปรเจคสำหรับผู้กับบริการ hosting

1. **Please select an option:** เริ่มแรกจะเป็นการกำหนด project ที่จะใช้ deploy firebase hosting โดยเราสามารถเลือกจากที่มีอยู่ หรือจะสร้างใหม่ก็ได้
   
2. **Select a default Firebase project for this directory:** ตรงนี้สามารถเลือกโปรเจคที่มีอยู่ใน Account ของเราได้

### กำหนดข้อมูลของโปรเจค

- What do you want to use as your public directory? กำหนด directory สำหรับใช้ในการ upload ไฟล์ที่พร้อมใช้ไป deploy (ใน workshop นี้เราจะใช้ build)
- Configure as a single-page app (rewrite all urls to /index.html)? (ใน workshop นี้เราจะตอบว่า yes)
- Set up automatic builds and deploys with GitHub? เลือกว่าจะให้มีการ build อัตโนมัติตอนสั่ง deploy และผ่าน github ไหม (ใน workshop นี้เราจะตอบว่า no)
- File build/index.html already exists. Overwrite? ต้องการ overwrite ไฟล์ html หรือไม่ (ใน workshop นี้เราจะตอบว่า no)

## 3. สั่ง build โปรเจคด้วยตัวเองเพื่อให้ได้ไฟล์ที่พร้อมอัพโหลด

ในตัวอย่างนี้เราใช้ create-react-app ในการสร้างโปรเจค เราจึงสามารถใช้คำสั่งด้านล่างในการ build ไฟล์ให้พร้อมใช้ในโฟลเดอร์ build 

```bash
npm run build
```

## 4. Deploy ขึ้น Hosting 

รันคำสั่งด้านล่าง 

```bash
firebase deploy
```

จะเห็นว่าถ้าการ deploy เสร็จสมบูรณ์ เราจะสามารถใช้ link ที่ปรากฎขึ้นมาใน console เข้าใช้งานได้