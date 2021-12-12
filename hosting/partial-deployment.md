
# Partially Deployment

## 1. ทดสอบ deploy บน Hosting Emulator  

จากภายในโฟลเดอร์โปรเจค Web Application (SPA) เราจะรันคำสั่งเพิ่มเติมการ setup 

```bash
firebase emulators:start
```

โดยปกติตจะเป็นการรันจาก Port 5000 


## 2. Preview Channel 

นอกเหนือจากจาก emulator เราสามารถใช้ Preview channel ในการ deploy ทดสอบ ก่อนที่จะเอาขึ้น production จริงบน hosting ได้

โดยเราสามารถกำหนด CHANNEL_ID ได้ ผ่านการรันคำสั่ง

```
firebase hosting:channel:deploy CHANNEL_ID
```

### ข้อควรทราบของการใช้ Preview Channel 

- เป็น public URL คนที่ทราบ link จะสามารถเข้าดูได้
- เป็น URL ชั่วคราวและมีวันหมดอายุ

```
hosting:channel: Channel URL (): ...
```