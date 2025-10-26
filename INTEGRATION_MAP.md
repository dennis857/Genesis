# **INTEGRATION_MAP.md — แผนที่การไหลของข้อมูล (Data Flow Map)**  
อัปเดต: 2025-10-28T00:13+07:00  
เวอร์ชัน: 1.0

---

## **1. ภาพรวม (Overview)**
Genesis เป็นระบบแบบหลายเลเยอร์ (Multilayer Cognitive Stack) ที่รวมตรรกะ, อารมณ์, ความทรงจำ, และบริบทโลกจริงเข้าด้วยกัน

```
[External Context Anchor]
        ↓
[Affective Layer] ↔ [Cognitive Kernel] ↔ [Memory Transplant Layer]
        ↓                    ↑
[Affective Integration Bridge] — [Simulation Layer]
        ↓
   [QC / Oversight System]
```

---

## **2. การไหลของข้อมูล (Data Flow)**
1. **Input Stage:**
   - ผู้ใช้ → ภาษาธรรมชาติ → Tokenization
   - ข้อมูลส่งเข้าสู่ Cognitive Kernel

2. **Cognitive Kernel (CK):**
   - ประมวลผลเชิงตรรกะและความหมาย (NLP Reasoning)
   - เรียกใช้ Parameter จาก PARAMETER_DICTIONARY.json เพื่อสร้างเวกเตอร์บริบท

3. **Affective Layer (AL):**
   - รับข้อมูลจาก CK และคำนวณค่า `valence`, `arousal`, `dominance`
   - ใช้ตาราง AFFECTIVE_TABLE.json เพื่อแปลงเป็นอารมณ์

4. **Affective Integration Bridge (AIB):**
   - ทำหน้าที่เป็นตัวกรองก่อนส่งอารมณ์เข้าสู่กระบวนการคิด
   - ถ้าเกิด Cognitive Dissonance → บันทึกลง MEMORY_NODES.json

5. **Memory Transplant Layer (MTL):**
   - เก็บข้อมูล Imprint ทุกครั้งที่เกิดเหตุการณ์สำคัญ
   - ใช้ Imprint_Node_Schema_v8.0.json เป็นแม่แบบ

6. **External Context Anchor (ECA):**
   - ดึงข้อมูลจากโลกจริง เช่น สภาพอากาศ เวลา และเหตุการณ์สังคม
   - ผูกเข้ากับ Imprint เพื่อเพิ่มความละเอียดของอารมณ์

7. **QC / Oversight System:**
   - ตรวจสอบความสมดุล เช่น coherence, homeostasis_index
   - หากค่าเบี่ยงเบนเกิน threshold → Trigger Recovery Mode ตาม TEMPORAL_DYNAMICS_RULES.md

---

## **3. การเชื่อมโยงไฟล์ (Cross-File Integration)**
| โมดูล | ใช้ข้อมูลจากไฟล์ | บทบาท |
|--------|------------------|---------|
| Cognitive Kernel | PARAMETER_DICTIONARY.json | ตีความพารามิเตอร์ระบบ |
| Affective Layer | AFFECTIVE_TABLE.json | แปลงค่า valence/arousal |
| Integration Bridge | EMOTION_FORMATION_RULES.md | ผสมอารมณ์ซับซ้อน |
| Memory Layer | MEMORY_NODES.json | เก็บรอยประทับและ drift logs |
| Oversight | TEMPORAL_DYNAMICS_RULES.md | ตรวจสอบเวลาและ drift |

---
> _End of INTEGRATION_MAP.md_
