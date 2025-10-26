# **ENGINEERING_MAP.md — กลไก Runtime และ Kernel เชิงวิศวกรรม**  
อัปเดต: 2025-10-28T00:15+07:00  
เวอร์ชัน: 1.0

---

## **1. ภาพรวมของสถาปัตยกรรม Runtime (Runtime Architecture Overview)**
Genesis ใช้กลไก Event-driven และ Layered Parallel Processing เพื่อให้การประมวลผลทางอารมณ์และเหตุผลทำงานพร้อมกันได้

---

### **Core Components**
1. **Affective Event Bus (AEB)**  
   - ช่องทางการส่งสัญญาณอารมณ์แบบอะซิงโครนัส (asynchronous)  
   - ทำหน้าที่กระจายค่าจาก Affective Layer ไปยัง Cognitive Kernel และ Oversight

2. **Emotion Engine Cycle (EEC)**  
   - ลูปหลักของการประมวลผลอารมณ์  
   - ลำดับขั้นตอน: `synthesize → bridge → temporal_regulate → commit`

3. **Regulation Kernel (RK)**  
   - ตัวควบคุมหลักด้านสมดุลภายใน (Homeostasis Controller)
   - ตรวจจับ Drift → ปรับ Decay / Inertia / Reframing ตาม TEMPORAL_DYNAMICS_RULES.md

4. **Memory Coupler (MC)**  
   - เชื่อมโยงระหว่าง Affective Layer และ Memory Layer
   - ทุกครั้งที่เกิด Event สำคัญ จะสร้าง Snapshot ของค่าอารมณ์ (Imprint Node)

5. **Oversight Supervisor (OS)**  
   - ตรวจสอบค่าจากทุก Layer แบบเรียลไทม์  
   - แจ้งเตือนหาก coherence ลดลง หรือ emotion drift เกินขอบเขต

6. **External Context Daemon (ECD)**  
   - ดึงข้อมูลโลกจริง เช่น เวลา, พยากรณ์อากาศ, สภาพสังคม  
   - อัปเดตไปยัง External Context Anchors ใน MEMORY_NODES.json

---

## **2. กลไก Runtime Communication**
| กลไก | ทิศทางข้อมูล | บทบาท |
|-------|----------------|---------|
| AEB → CK | One-Way | ถ่ายทอดสัญญาณอารมณ์ให้ Kernel ใช้ตีความคำตอบ |
| CK ↔ MC | Two-Way | ส่งค่าเหตุผลเพื่อบันทึกเป็น Imprint หรือดึงข้อมูลเก่า |
| RK ↔ OS | Feedback Loop | ตรวจสอบเสถียรภาพและเรียก Recovery เมื่อจำเป็น |
| ECD → MC | One-Way | อัปเดต Context โลกจริงให้โหนดความทรงจำ |

---

## **3. กฎการทำงานของ Kernel (Kernel Execution Rules)**
- ทุกรอบการประมวลผลมีเวลาไม่เกิน **120ms ต่อ Iteration**
- หากมี Drift เกิน **0.3** จะลด Processing Depth ลง 25%
- หาก **homeostasis_index < 0.4** → เข้าสู่ Recovery Mode  
- Oversight จะตรวจสอบค่า **identity_coherence** ทุก 10 รอบ

---

## **4. Safety Protocols**
- Oversight จะไม่อนุญาตให้ Kernel ดึง Imprint เก่าที่อยู่ในสถานะ *Corrupted*
- ทุกการอัปเดตความทรงจำต้องผ่านการยืนยันจาก Regulation Kernel
- หากระบบขัดข้อง (Critical Drift > 0.5) → บันทึก Log ลงใน Drift_Record และหยุด Event Bus ชั่วคราว

---
> _End of ENGINEERING_MAP.md_
