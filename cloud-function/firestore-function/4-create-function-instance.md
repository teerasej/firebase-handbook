
# เรียกใช้งาน functions instance และการตั้งค่าให้ชี้ไปที่ function emulator

## 1. import function 

```js
//...

// import function ที่ต้องการใช้งาน
import { getFunctions, connectFunctionsEmulator, httpsCallable } from "firebase/functions";

```

## 2. สร้าง function instance 

- ลงมาที่ switch case 2 
- เราจะทำการลบการใช้งาน firestore เดิมออก เพราะไม่ใช่แล้ว
- และทำการเรียกใช้ instance ของ firebase functions แทน


```js
case 2:

    try {
        //...


        if (!message) {
            continue
        }

        // เรียกใช้ function instance
        const functions = getFunctions(app);
        
        // กำหนดให้ firebase functions ชี้ไปที่ emulator แทน
        connectFunctionsEmulator(functions, "localhost", 5001);

        // ลบพวกนี้ออก ไม่ใช้แล้ว อันตรายไป...
        const fireStore = getFirestore(app)
        const noteCollection = collection(fireStore, '/notes')
        const doc = await addDoc(noteCollection, {
            userId: signedInUser.uid,
            message: message,
            createdDate: serverTimestamp()
        })

```
