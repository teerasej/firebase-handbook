
# รัน Cloud Function และเชื่อมต่อกับ ngrok

หากยังไม่ได้รัน function emulator ให้รันคำสั่งด้านล่าง ภายในโปรเจค function

```
npm run-script serve 
```

จากนั้นให้รัน ngrok ด้วยคำสั่งด้านล่าง เช่น ปกติ cloud function emulator จะทำงานที่ port 5001  

```bash
ngrok http 5001 
```

เราจะได้ URL ชั่วคราวที่สามารถส่ง request เข้ามาที่ function emulator ได้ มีทั้ง **http** และ **https** 