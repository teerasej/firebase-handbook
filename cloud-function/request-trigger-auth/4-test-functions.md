
# ทดสอบ Cloud function

1. ทดสอบรัน Cloud function แบบ Emulator 
2. ทดสอบการใช้งานผ่าน URL โดยใช้คำสั่ง curl ใน terminal

โดยแทนค่า 

- [URL]: URL ของ Cloud function create user
- [email address]: email address ที่ต้องการกำหนดเป็น username
- [pass_word]: รหัสผ่าน

```bash
curl -X POST [URL] -H 'Content-Type: application/json' -d '{"email":"[email address]","password":"[pass_word]"}'
```

ทดสอบใส่ค่าที่ไม่ถูกต้องสำหรับ email และ password ดู

3. กลับไปที่ Firebase console และดูข้อมูลในส่วน authentication

