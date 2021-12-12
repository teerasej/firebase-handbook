# Full Deployment ขึ้น Hosting 

จะทำขั้นตอนนี้ได้ ต้อง[ทำการ setup project ให้เรียบร้อย](setup-local-project.md)ก่อน

รันคำสั่งด้านล่าง ใน Terminal ของโปรเจค

```bash
firebase deploy --only hosting
```

จะเห็นว่าถ้าการ deploy เสร็จสมบูรณ์ เราจะสามารถใช้ link ที่ปรากฎขึ้นมาใน console เข้าใช้งานได้

- จริงๆ จะมีส่วนการตั้งค่าให้สามารถ Deploy แบบอัตโนมัติได้ 