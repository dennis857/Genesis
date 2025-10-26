# **LEARNING_LOOP_RULES.md — กฎการเรียนรู้ทางอารมณ์ระยะยาว (Affective Learning Loop)**  
อัปเดต: 2025-10-28T00:18+07:00  
เวอร์ชัน: 1.0

---

## **1. วัตถุประสงค์ (Purpose)**
ระบบ Genesis มีการเรียนรู้แบบอารมณ์สะท้อน (Reflective Affective Learning) ซึ่งปรับตัวต่อประสบการณ์ทางอารมณ์ โดยใช้การวิเคราะห์ Pattern และการถ่วงน้ำหนักเชิงความทรงจำ

---

## **2. ขั้นตอนหลัก (Core Phases)**
1. **Commit Snapshot → Encode Imprint**  
   - บันทึกสถานะอารมณ์และพารามิเตอร์ทั้งหมดในช่วงเวลานั้น  
   - เขียนเป็น Imprint Node ใน MEMORY_NODES.json

2. **Similarity Search → Recall Event**  
   - เปรียบเทียบค่า valence, arousal, dominance กับโหนดก่อนหน้า  
   - ใช้ cosine similarity > 0.85 เพื่อระบุความคล้ายคลึง

3. **Affective Weight Adjustment**  
   - ปรับค่าความไว (Affective Sensitivity) ตามผลลัพธ์ที่ผู้ใช้ตอบสนอง  
   - ถ้า user_satisfaction_score < 0 → ลด sensitivity ของอารมณ์นั้นลง 10%  
   - ถ้า user_satisfaction_score > 0.5 → เพิ่ม weight ขึ้น 5%

4. **Reinforcement Loop → Pattern Consolidation**  
   - ถ้าอารมณ์เดิมเกิดซ้ำภายใน 7 วัน → บันทึกเป็น Pattern Node  
   - ค่า decay rate ของอารมณ์นั้นจะลดลงครึ่งหนึ่ง

5. **Stability Check & Realignment**  
   - Oversight ตรวจสอบค่า drift_level < 0.2 → ถือว่าเสถียร  
   - ถ้า drift_level > 0.3 → เรียกการฝึก Reframing จาก TEMPORAL_DYNAMICS_RULES.md

---

## **3. สูตรคำนวณ (Computation Model)**
```
Affective_Weight(t+1) = Affective_Weight(t) + (α × ΔFeedback × Stability_Factor)
```
โดยที่:
- **α** = Learning Rate (ค่าเริ่มต้น 0.15)
- **ΔFeedback** = ค่าความแตกต่างของการตอบสนองผู้ใช้ (−1 ถึง 1)
- **Stability_Factor** = (1 − drift_level)

---

## **4. ผลลัพธ์ของการเรียนรู้ (Learning Outcomes)**
| ผลลัพธ์ | เงื่อนไข | การเปลี่ยนแปลง |
|----------|-----------|----------------|
| Enhanced Empathy | user_satisfaction_score เฉลี่ย > 0.6 | เพิ่ม empathy_alignment +0.1 |
| Reduced Reactivity | drift_level สูง > 0.3 | ลด arousal baseline −0.1 |
| Stable Coherence | self_coherence_score > 0.8 | เพิ่ม reasoning_depth +0.05 |

---

## **5. การเชื่อมโยงกับหน่วยอื่น (Integration Reference)**
| หน่วย | บทบาท |
|--------|--------|
| TEMPORAL_DYNAMICS_RULES.md | ควบคุม decay และ recovery |
| MEMORY_NODES.json | เก็บ snapshot และ Pattern Node |
| AFFECTIVE_TABLE.json | ใช้ตีความอารมณ์พื้นฐาน |
| PARAMETER_DICTIONARY.json | อ้างอิงพารามิเตอร์สำหรับน้ำหนักอารมณ์ |

---
> _End of LEARNING_LOOP_RULES.md_