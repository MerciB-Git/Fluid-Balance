# บันทึกน้ำเข้า-น้ำออก (Fluid Balance PWA)

แอปจดการดื่มน้ำ (ml) และปัสสาวะ (cc) รายวัน สรุปยอดสะสมทุกครั้งที่กรอก
ติดตั้งลงหน้าจอโฮมมือถือได้ เปิดเต็มจอ ใช้ออฟไลน์ได้ ข้อมูลเก็บไว้ในเครื่อง

## ไฟล์ในโปรเจกต์
- `index.html` — ตัวแอปทั้งหมด (HTML + CSS + JS ในไฟล์เดียว)
- `manifest.webmanifest` — ชื่อแอป ไอคอน สีธีม โหมดเต็มจอ
- `sw.js` — service worker สำหรับใช้งานออฟไลน์
- `icons/` — ไอคอนแอป 192/512/maskable/apple-touch

## ลองรันในเครื่อง
ต้องเปิดผ่าน http ไม่ใช่ดับเบิลคลิกไฟล์ ไม่งั้น service worker จะไม่ทำงาน

    python3 -m http.server 8080
    # เปิด http://localhost:8080

## เอาขึ้นเว็บ (เลือกทางใดทางหนึ่ง)

**Netlify** — ง่ายที่สุด ลากโฟลเดอร์นี้ไปวางที่ https://app.netlify.com/drop

**GitHub Pages**

    git init && git add . && git commit -m "fluid balance app"
    gh repo create fluid-balance --public --source=. --push
    # เปิด Settings > Pages > Source: Deploy from branch > main / root

**Cloudflare Pages / Vercel** — เชื่อม repo แล้วกด deploy ได้เลย ไม่ต้อง build

## ปักไอคอนลงหน้าจอโฮม
- **iPhone (Safari)** เปิดลิงก์ > ปุ่มแชร์ > เพิ่มไปยังหน้าจอโฮม
- **Android (Chrome)** เปิดลิงก์ > เมนู ⋮ > ติดตั้งแอป / เพิ่มลงในหน้าจอหลัก

## เก็บข้อมูลยังไง
ใช้ `localStorage` ของเบราว์เซอร์ (คีย์ `fluidlog:v1`) — ข้อมูลอยู่ในเครื่องเท่านั้น ไม่ส่งออกไปไหน
ถ้าล้างข้อมูลเบราว์เซอร์หรือถอนแอป ข้อมูลจะหาย ควรกด "คัดลอกสรุปวันนี้" เก็บไว้เป็นระยะ

## โครงสร้างข้อมูล 1 รายการ

    { "id": "...", "date": "2026-07-12", "time": "07:30", "drink": 250, "pee": 0 }
