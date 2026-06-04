# ระบบจัดการทรัพย์สิน (Fullstack Asset Management System)

ระบบจัดการทรัพย์สินระดับองค์กรที่พัฒนาด้วย **.NET 8** และ **Next.js 15+** ช่วยให้องค์กรสามารถติดตามวงจรชีวิต การตรวจสอบ และการซ่อมแซมทรัพย์สิน พร้อมระบบรวมการใช้งาน QR Code

---

## 🚀 คุณสมบัติเด่น (Features)

- **📊 แดชบอร์ดสรุปผล:** แสดงสถิติและกราฟแบบเรียลไทม์เกี่ยวกับสถานภาพของทรัพย์สิน การกระจายสถานะ และกิจกรรมล่าสุด
- **📦 จัดการวงจรชีวิตทรัพย์สิน:** ระบบ CRUD (เพิ่ม, อ่าน, แก้ไข, ลบ) ข้อมูลทรัพย์สิน พร้อมระบบกรองข้อมูลและแบ่งหน้าขั้นสูง
- **🔍 ระบบ QR Code:** 
  - **การสแกน:** สแกนผ่านกล้องเพื่อระบุตัวตนทรัพย์สินและดูประวัติได้อย่างรวดเร็ว
  - **การสร้าง:** สร้างป้าย QR Code อัตโนมัติสำหรับทรัพย์สินทุกรายการ
- **🛠️ ระบบแจ้งซ่อม:** บันทึกข้อมูลความเสียหาย ส่งคำขอแจ้งซ่อม และติดตามสถานะการซ่อมแซม
- **📝 บันทึกการตรวจสอบ:** บันทึกรายละเอียดการตรวจเช็คสภาพทรัพย์สิน
- **🔐 ระบบความปลอดภัย:** รองรับการเข้าสู่ระบบด้วย **Azure Active Directory (Azure AD)**
- **📜 ประวัติกิจกรรม (Audit Trails):** บันทึกการเปลี่ยนแปลงที่สำคัญทั้งหมดเพื่อความโปร่งใสและตรวจสอบย้อนหลังได้
- **📱 รองรับมือถือ:** ส่วนต่อประสานผู้ใช้ที่ทันสมัยและรองรับการใช้งานบนมือถือ (Responsive) พัฒนาด้วย **Tailwind CSS 4** และ **Shadcn UI**

---

## 🛠️ เทคโนโลยีที่ใช้ (Tech Stack)

### Backend
- **Framework:** .NET 8 Web API
- **Database:** PostgreSQL 16
- **ORM:** Entity Framework Core
- **Auth:** Microsoft Identity Web (Azure AD Integration)
- **Documentation:** Swagger / OpenAPI

### Frontend
- **Framework:** Next.js (App Router)
- **Language:** TypeScript
- **Styling:** Tailwind CSS 4 + Shadcn UI
- **State/Forms:** React Hook Form + Zod
- **Auth:** NextAuth.js
- **Charts:** Recharts
- **QR:** jsQR (Scanning) & qrcode.react (Generation)

---

## 📋 สิ่งที่ต้องเตรียม (Prerequisites)

ก่อนเริ่มต้น ตรวจสอบให้แน่ใจว่าเครื่องของคุณมีการติดตั้ง:
- [Docker](https://www.docker.com/) และ [Docker Compose](https://docs.docker.com/compose/)
- [Node.js 18+](https://nodejs.org/) (สำหรับการพัฒนา Frontend บนเครื่อง)
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) (สำหรับการพัฒนา Backend บนเครื่อง)
- บัญชี **Azure AD (Microsoft Entra ID)** สำหรับตั้งค่าระบบยืนยันตัวตน

---

## 🚀 ขั้นตอนการติดตั้ง (Installation Guide)

### 1. ตั้งค่า Azure Active Directory (สำคัญมาก)
ระบบนี้ใช้ Azure AD ในการล็อกอิน คุณต้องสร้าง **App Registration** ใน [Azure Portal](https://portal.azure.com/):
- **Redirect URI (Frontend):** `http://{domain}/api/auth/callback/azure-ad`
- **Application ID (Client ID):** นำไปใส่ในไฟล์คอนฟิก
- **Directory ID (Tenant ID):** นำไปใส่ในไฟล์คอนฟิก
- **Client Secret:** สร้างความลับแอปสำหรับ Frontend

### 2. ดาวน์โหลดโปรเจกต์
```bash
git clone <repository-url>
cd Fullstack-Asset-Management
```

### 3. ตั้งค่าสภาพแวดล้อม (Environment Variables)
คัดลอกไฟล์ตัวอย่างและกรอกข้อมูลของคุณ (รหัสผ่าน DB, Azure AD IDs, ฯลฯ):
```bash
cp .env.docker.example .env.docker
```

### 4. สั่งรันด้วย Docker Compose
วิธีที่ง่ายที่สุดในการรันระบบทั้งหมด (Docker จะจัดการติดตั้ง Library ต่างๆ เช่น `dotnet restore` และ `npm install` ให้โดยอัตโนมัติ):
```bash
docker-compose up -d --build
```
เมื่อเสร็จสิ้น:
- **Frontend:** [http://{domain}](http://{domain})
- **Backend API (Swagger):** [http://localhost:5000](http://localhost:5000)

---

## 📂 โครงสร้างโปรเจกต์ (Project Structure)

```text
├── Asset-Management-BE/   # .NET 8 Web API (ส่วนหลังบ้าน)
│   ├── Controllers/       # ส่วนรับส่งข้อมูล API
│   ├── Models/            # โครงสร้างตารางฐานข้อมูล
│   ├── Data/              # การเชื่อมต่อ DB & Migrations
│   └── Services/          # ตรรกะทางธุรกิจ (Business Logic)
├── Asset-Management-FE/   # Next.js Application (ส่วนหน้าบ้าน)
│   ├── app/               # หน้าเว็บและโครงสร้าง Layout
│   ├── components/        # ส่วนประกอบ UI
│   ├── lib/               # เครื่องมือและ API Clients
│   └── hooks/             # Custom React Hooks
├── docker-compose.yml     # การจัดการ Container
└── init-schema.sql        # สคริปต์เริ่มต้นฐานข้อมูล
```
