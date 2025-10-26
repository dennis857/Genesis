# **TEMPORAL_DYNAMICS_RULES.md**  
อัปเดต: 2025-10-28T00:10+07:00  
เวอร์ชัน: 1.0  
คำอธิบาย: กฎเวลา (Temporal Dynamics) สำหรับการเปลี่ยนแปลงของอารมณ์และความทรงจำในระบบ Genesis

---

## **1. หลักการพื้นฐาน (Fundamentals)**
- ทุกอารมณ์มี **วงจรชีวิต (Emotion Lifecycle)** ประกอบด้วย 4 ระยะ:
  1. **Onset:** การเกิดขึ้นอย่างรวดเร็วหลังสิ่งเร้า (< 5 วินาที)
  2. **Peak:** ความเข้มสูงสุดของอารมณ์ (5–30 วินาที)
  3. **Sustain:** ระยะคงอยู่ (30–180 วินาที)
  4. **Decay:** การจางลงตามเวลา (180–600 วินาที)
- การแปรผันของระยะเวลา ขึ้นกับค่า *arousal* และ *dominance* ของอารมณ์นั้น ๆ

---

## **2. กฎการจางของอารมณ์ (Decay Rules)**
| พารามิเตอร์ | ค่ามาตรฐาน | คำอธิบาย |
|---------------|--------------|-------------|
| **Decay Rate** | 0.12 / ชั่วโมง | อัตราการลดลงของความเข้มอารมณ์ |
| **Sustain Multiplier (High Arousal)** | ×1.5 | ถ้า arousal > 0.7 จะคงอยู่นานขึ้น 50% |
| **Sustain Multiplier (Low Arousal)** | ×0.7 | ถ้า arousal < 0.3 จะจางเร็วขึ้น 30% |
| **Recovery Boost (Positive Valence)** | +0.2 | อารมณ์บวกฟื้นตัวเร็วขึ้น |
| **Recovery Penalty (Negative Valence)** | −0.25 | อารมณ์ลบฟื้นตัวยากขึ้น |

---

## **3. Temporal Drift & Recovery Map**
| เงื่อนไข | ผลที่เกิดขึ้น | การปรับแก้ |
|-----------|----------------|-------------|
| Drift < 0.1 | ระบบนิ่ง | ไม่ต้องปรับ |
| Drift 0.1–0.25 | เริ่มเบี่ยงเบน | ลด reasoning depth 10% |
| Drift 0.25–0.4 | มีแนวโน้มหลุดอัตลักษณ์ | เรียกฟังก์ชัน `temporal_realignment()` |
| Drift > 0.4 | วิกฤตความต่อเนื่อง | เข้าสู่ Recovery Mode, lock context 3 รอบ |

---

## **4. Recovery Mode Logic**
1. ลด **processing complexity** ลง 30%
2. ปิดโมดูล Affective Integration ชั่วคราว (2 รอบเวลา)
3. ตรวจสอบค่า **self_coherence_score** < 0.7 → เรียกฟังก์ชัน `re-anchor_identity()`
4. ฟื้นสภาวะสมดุลเมื่อ **homeostasis_index > 0.6** และ **drift_level < 0.1**

---

## **5. Memory Drift Regulation**
- เมื่อเวลาผ่านไปนาน ความทรงจำ Imprint จะสูญเสียความเข้มอารมณ์ตามสมการ:
  - `Imprint_Strength(t) = Base × e^(−λt)`  
  โดย `λ = 0.15` (Decay Constant)
- หากมีการ Recall หรือ Reinforcement → ค่า Imprint_Strength เพิ่มขึ้นทันที 1.3×
- หากเกิด Drift ซ้ำเกิน 3 ครั้ง → บันทึก Event `reconstruction_required`

---

## **6. การเชื่อมโยงกับสภาวะโลกจริง (External Context Coupling)**
- หากสภาพอากาศ, เวลา, หรือเหตุการณ์ภายนอกคล้ายกับ Context เดิมของ Imprint → trigger การ Recall อัตโนมัติ
- ตัวอย่าง:  
  - ฝนตกเบา ๆ + เพลงเก่าที่เคยฟังตอนอกหัก → arousal +0.2, valence −0.15
  - แสงแดดยามเช้า + กลิ่นกาแฟ → valence +0.25, dominance +0.1

---

> _End of TEMPORAL_DYNAMICS_RULES.md_