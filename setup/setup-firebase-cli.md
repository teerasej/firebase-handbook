
# Setup Firebase CLI

## 1. ดาวน์โหลดและติดตั้ง CLI

เราสามารถติดตั้ง Firebase CLI ได้ตามคำสั่งด้านล่าง 

```bash
npm install -g firebase-tools
```

หรือถ้าติดปัญหาในการใช้ npm ลง ก็ให้ใช้ curl ได้เลย

```bash
curl -sL https://firebase.tools | bash
```

หรือถ้าไม่ได้จริงๆ ลอง[คลิกไปดูบนหน้าเว็บของ Firebase](https://firebase.google.com/docs/cli) จะมีพวก workaround อยู่ครับ

## 2. Sign in ด้วย Firebase Account 

ให้เปิด Terminal หรือ Command Prompt หรือ Powershell และรันคำสั่งด้านล่าง 

```bash
firebase login
```

จะเป็นการเริ่มขั้นตอนการลงชื่อเข้าใช้ ให้ทำให้เรียบร้อย ไม่งั้นใช้ไม่ได้นะเออ