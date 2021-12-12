

# ติดตั้ง และใช้งาน ngrok

## 1. ติดตั้ง Ngrok 

ถ้าเราติดตั้ง Node.js Runtime ไว้แล้ว เราสามารถ ใช้คำสั่งด้านล่างในการติดตั้ง ngrok ได้เลย

### Windows 

```bash
npm install -g ngrok
```

### MacOS, Linux 

```bash
sudo npm install --unsafe-perm -g ngrok
```

## 2. setup key บนเครื่องที่ต้องการใช้งาน

ขั้นตอนนี้จะแบ่งเป็น 2 ส่วน และจะมีการสร้างบัญชีบนเว็บของ ngrok ถ้ายังไม่มี

### 2.1 เข้าไปเอา token ในหน้า dashboard 

เข้าไปที่ [Ngrok - your auth token](https://dashboard.ngrok.com/get-started/your-authtoken) ซึ่งจะมีการลงชื่อเข้าใช้งานบัญชีของเว็บ ngrok

ตรงนี้ ให้ทำการ copy auth token ที่แสดงบนหน้าเว็บมา

**ถ้าไม่มีให้สร้าง หรือทำการ login ด้วย Google Account ก็ได้**

### 2.2 ติดตั้ง auth token 

จากนั้นกลับมาที่ Terminal บนเครื่องของเรา ให้รันคำสั่ง 

```bash
ngrok authtoken [token ที่ copy มาจากขั้นตอนที่แล่้ว]
```

ถ้าไม่มีข้อความ error จะถือว่าเสร็จสมบูรณ์

## การใช้งาน 

รันคำสั่ง 

```bash
ngrok http [หมายเลข port ของ server ที่ต้องการ map กับ ngrok] 
```

เช่น ปกติ cloud function emulator จะทำงานที่ port 5001 ก็ให้รันคำสั่งด้านล่าง 

```bash
ngrok http 5001 
```

การใช้บริการแบบฟรี ตัว domain ที่สร้างขึ้นมาจะเป็นแบบชั่วคราว และจะมีข้อจำกัด หากต้องการใช้งานจริงจังก็จะต้องเสียเงินนะ