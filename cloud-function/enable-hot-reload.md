

# เปิดการทำงานของ Hot Reload

แก้ไขไฟล์ **functions/package.json** ตามลำดับ

1. ทำการเพิ่มคำสั่ง `"build:watch": "tsc --watch --preserveWatchOutput"` เข้าไปใน `script`
2. แก้ไขคำสั่ง `serve` ใน `script` ให้เป็นแบบด้านล่าง

```json
{
  ...
  "scripts": {
    ...
    "build:watch": "tsc --watch --preserveWatchOutput",
    "serve": "npm run build:watch | firebase emulators:start --only functions",
    ...
```

ทำให้พอเราแก้ไขโค้ดแล้วบันทึกไฟล์ จากนั้นรีเฟรชหรือส่ง request เข้ามาที่ cloud function ก็จะเป็นโค้ดชุดใหม่ 

ไม่ต้องปิดๆ เปิดๆ อีกต่อไป
