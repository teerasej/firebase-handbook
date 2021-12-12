
# 

1. ทำการ download หรือ clone project จากที่นี่ https://github.com/teerasej/node-firebase-authentication-public
2. ทำการ restore module ด้วยคำสั่ง

```bash
npm i
```

3. นำข้อมูล config จาก Firebase console > Project setting มาใส่ในส่วนบรรทัดที่ 37

```js
const firebaseConfig = {
    // configuration values...        
};
```

4. กรอก email และ password ที่ทำการสร้างไว้ใน Firebase console > Authentication มาใส่ในส่วนบรรทัดที่ 55

```js
 signedInUser = await signIn('email', 'password')
```


