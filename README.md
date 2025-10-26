# Food Ordering System

**Food Ordering System** คือแอปพลิเคชันสำหรับช่วยจัดการระบบสั่งอาหารในร้านอาหาร ที่ลูกค้าสามารถสแกน QR Code ที่โต๊ะเพื่อสั่งอาหาร และพนักงานสามารถจัดการคำสั่งซื้อ เมนูอาหาร และโต๊ะได้แบบเรียลไทม์

ระบบนี้ประกอบด้วยแอปพลิเคชัน Frontend แยกกัน 2 ตัว คือ ระบบสำหรับลูกค้าและระบบจัดการสำหรับพนักงาน พร้อมด้วย Backend API ที่รองรับการทำงานแบบเรียลไทม์

- Customer repository: https://github.com/nathapatt/customer-fullstack-website.git
- Staff repository: https://github.com/apwjir/staff-fullstack-website.git
- Backend repository: https://github.com/4ank0rn/food_ordering_backend.git

---

## คุณสมบัติของระบบ (Key Features)

- **ระบบ QR Code**: ลูกค้าสแกน QR Code ที่โต๊ะเพื่อเข้าถึงระบบสั่งอาหาร
- **การสั่งอาหารแบบเรียลไทม์**: อัปเดตสถานะคำสั่งซื้อแบบทันทีผ่าน WebSocket
- **จัดการเมนู**: พนักงานสามารถเพิ่ม แก้ไข จัดการเมนูอาหารพร้อมอัปโหลดรูปภาพ
- **จัดการโต๊ะ**: ติดตามสถานะโต๊ะและสร้าง QR Code สำหรับแต่ละโต๊ะ
- **ระบบพนักงาน**: เข้าสู่ระบบด้วย Google OAuth และจัดการคำสั่งซื้อ
- **การอัปโหลดรูปภาพ**: ใช้ Cloudinary สำหรับจัดเก็บรูปภาพเมนู

---

## สมาชิกผู้พัฒนา

| ชื่อ                     | รหัสนักศึกษา |
| ---------------------  | ------------ |
| กัลป์กรณ์ จิรไชยหิรัญ        | 650610746    |    
| จิรพัทธ์ พลรัฐ             | 650610752    |
| ณฐภัทร เนรังษี            | 650610758    |

---

## Technology Stack

### Frontend

| Tech                  | Description                                 |
| --------------------- | ------------------------------------------- |
| React 19              | Framework สำหรับ Web Application ฝั่งผู้ใช้ |
| TypeScript            | ภาษาโปรแกรมที่เพิ่มระบบ Type ให้ JavaScript|
| Vite                  | Build Tool และ Development Server          |
| TailwindCSS           | ระบบตกแต่ง UI สำหรับลูกค้า                  |
| Ant Design            | UI Library สำหรับพนักงาน                   |
| React Query           | จัดการ State ของข้อมูล และ Data Fetching    |
| Socket.io Client      | การเชื่อมต่อแบบเรียลไทม์                    |

### Backend

| Tech        | Description                         |
| ----------- | ----------------------------------- |
| NestJS      | Framework สำหรับ Node.js Backend    |
| TypeScript  | ภาษาโปรแกรมที่เพิ่มระบบ Type       |
| Prisma ORM  | ORM ใช้เชื่อมต่อและ query ฐานข้อมูล |
| JWT         | ระบบยืนยันตัวตนด้วย JSON Web Token  |
| Socket.io   | WebSocket สำหรับการอัปเดตแบบเรียลไทม์|

### Other Services

| Tool           | Purpose                          |
| -------------- | -------------------------------- |
| PostgreSQL 17  | ฐานข้อมูลหลัก                    |
| Cloudinary     | จัดเก็บและจัดการรูปภาพ           |
| Google OAuth   | ระบบเข้าสู่ระบบผ่าน Google       |
| Docker         | Containerization และ Deployment  |

---

## การเตรียมข้อมูลเริ่มต้น (Seed Data)

มีสคริปต์สำหรับสร้างข้อมูลเริ่มต้นที่จำเป็นสำหรับการทดสอบระบบ โดยจะสร้าง:

- **โต๊ะ 10 โต๊ะ** (โต๊ะ 1-10) พร้อม QR Code tokens
- **บัญชี Admin** สำหรับเข้าใช้งานระบบพนักงาน
  - Email: admin@restaurant.com
  - Password: admin123

### ขั้นตอนการนำไปพัฒนาต่อ

หลังจากที่โคลนโปรเจคไปแล้วสามารถพัฒนาต่อได้โดย step ดังนี้:

1. **ตั้งค่า Environment Variables**
   ```bash
   cp .env.example .env
   # แก้ไขไฟล์ .env ตามความต้องการ
   # สำคัญ: ตั้งค่า Google OAuth และ Cloudinary credentials ก่อนเริ่มใช้งาน
   ```

   **Environment Variables ที่จำเป็น:**
   - `GOOGLE_CLIENT_ID` และ `GOOGLE_CLIENT_SECRET` - สำหรับการยืนยันตัวตน Google OAuth
   - `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` - สำหรับการอัปโหลดรูปภาพ

2. **เริ่มระบบด้วย Docker**
   ```bash
   docker-compose up -d
   ```

3. **Seed ข้อมูลเริ่มต้น**
   ```bash
   # เข้าไปใน backend container
   docker exec -it food_ordering_backend bash

   # รันคำสั่ง seed ข้อมูล
   npm run seed
   ```

4. **เข้าถึงระบบ**
   - **Customer Frontend**: http://localhost:[PORT_CUSTOMER]
     - **Development Route**: `/admin/qr` - เข้าถึงการเลือกโต๊ะโดยตรงสำหรับการทดสอบ
   - **Staff Frontend**: http://localhost:[PORT_STAFF]
   - **Backend API**: http://localhost:3000

### การใช้งานระบบ

#### สำหรับลูกค้า:
1. **วิธี QR Code**: สแกน QR code ที่โต๊ะเพื่อเริ่มสั่งอาหาร
2. **วิธีการพัฒนา**: เข้าไปที่ `/admin/qr` และคลิกปุ่มโต๊ะเพื่อจำลองการเข้าถึงโต๊ะ
3. เรียกดูเมนูและเพิ่มรายการลงในตะกร้า
4. สั่งอาหารและติดตามสถานะแบบเรียลไทม์

#### สำหรับพนักงาน:
1. เข้าสู่ระบบด้วยบัญชี admin
2. จัดการคำสั่งซื้อและอัปเดตสถานะ
3. เพิ่มรายการเมนูใหม่พร้อมรูปภาพ
4. สร้างและจัดการ QR codes สำหรับโต๊ะ