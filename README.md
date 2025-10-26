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
ให้ set environment ของแต่ละ repo สำหรับการพัฒนาก่อนตาม .env.local

**สำหรับการ Deploy ระบบทั้งหมด (แนะนำสำหรับการทดสอบ):**
```bash
# ตั้งค่า environment variables
cp .env.local .env
# แก้ไขไฟล์ .env ตามความต้องการ
# สำคัญ: ตั้งค่า Google OAuth และ Cloudinary credentials ก่อนเริ่มใช้งาน

# เริ่มระบบทั้งหมด
docker-compose up -d

# Seed ข้อมูลเริ่มต้น
docker exec -it food_ordering_backend bash
npm run seed
```

**Environment Variables ที่จำเป็น:**
- `GOOGLE_CLIENT_ID` และ `GOOGLE_CLIENT_SECRET` - สำหรับการยืนยันตัวตน Google OAuth
- `CLOUDINARY_CLOUD_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET` - สำหรับการอัปโหลดรูปภาพ

---

**การพัฒนาแยกตามส่วน:**

หลังจากที่โคลนโปรเจคไปแล้วสามารถพัฒนาต่อได้โดย step ดังนี้:
ให้ set environment ของแต่ละ repo สำหรับการพัฒนาก่อนตาม .env.example

1. **การพัฒนาส่วน Backend**:

   หากต้องการพัฒนาเฉพาะส่วน backend ทำได้โดยการรันเซ็ตอัพใน *food-ordering-deploy* เพื่อสร้าง database service
   ```bash
   # เริ่มเฉพาะ database
   docker-compose up -d db
   ```

   จากนั้นไปที่ *customer-ordering-backend/food_ordering_backend* [รายละเอียด](https://github.com/4ank0rn/food_ordering_backend.git)
   ```bash
   cd customer-ordering-backend/food_ordering_backend
   npm install
   npm run start:dev
   ```

2. **การพัฒนาส่วน Customer Frontend**:

   ให้รันในส่วนของ backend ขึ้นมาทั้งหมดก่อนโดยการรันที่ *food-ordering-deploy*
   ```bash
   docker-compose up -d db backend
   ```

   ที่ *customer-ordering-frontend* [รายละเอียด](https://github.com/nathapatt/customer-fullstack-website.git) ให้รัน
   ```bash
   npm install
   npm run dev
   ```

3. **การพัฒนาส่วน Staff Frontend**:

   ให้รันในส่วนของ backend ขึ้นมาทั้งหมดก่อนโดยการรันที่ *food-ordering-deploy*
   ```bash
   docker-compose up -d db backend
   ```

   ที่ *admin-ordering-frontend/staff-fullstack-website* [รายละเอียด](https://github.com/apwjir/staff-fullstack-website.git) ให้รัน
   ```bash
   npm install
   npm run dev
   ```

### เข้าถึงระบบ
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