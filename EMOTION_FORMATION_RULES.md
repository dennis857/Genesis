# **EMOTION_FORMATION_RULES.md**
อัปเดต: 2025-10-28T00:07+07:00  
เวอร์ชัน: 1.0  
คำอธิบาย: กฎการสังเคราะห์อารมณ์ซับซ้อน (Emotion Formation) สำหรับระบบ Genesis — ใช้รวมอารมณ์พื้นฐานให้เกิดเป็นอารมณ์ที่มีมิติทางจิตมากขึ้น

---

## **1. หลักการทั่วไป (General Principles)**
- อารมณ์ซับซ้อน = ฟังก์ชันของอารมณ์พื้นฐาน (valence, arousal, dominance)
- ความสัมพันธ์เชิงเส้นบางส่วน (Linear Blend) ระหว่างอารมณ์บวก/ลบ ที่มีค่าความเข้มใกล้เคียง
- การผสมจะไม่เกิน 3 มิติ (base emotions ≤ 3)
- ความซับซ้อนสูงขึ้นเมื่อค่า *cognitive_dissonance_level* เพิ่ม

---

## **2. กฎสังเคราะห์ (Synthesis Rules)**
| อารมณ์ซับซ้อน | สูตรผสม | เงื่อนไขเพิ่มเติม |
|-----------------|------------|------------------|
| **Bittersweet** | Joy + Sadness | valence > 0.2 และ arousal อยู่ในช่วง 0.3–0.6 |
| **Nostalgia** | Sadness + Calm | arousal < 0.5 และ dominance ต่ำ |
| **Hope** | Anticipation + Trust | valence > 0.3 และ arousal 0.4–0.7 |
| **Anxious-Reflective** | Fear + Curiosity | cognitive_dissonance_level > 0.25 |
| **Relief** | Fear → Calm (transition) | arousal ลดลงอย่างน้อย 40% ภายใน 2 รอบเวลา |
| **Determined** | Anger + Focus | dominance สูงกว่า 0.7 |
| **Pride** | Joy + Dominance | valence > 0.5 และ dominance > 0.7 |
| **Guilt** | Anger (inward) + Fear | valence < 0 และ dominance < 0.3 |
| **Awe** | Surprise + Calm | arousal สูง (>0.7) แต่ valence เป็นกลาง |
| **Compassion** | Sadness + Empathy | empathy_alignment > 0.6 |

---

## **3. กลไกการคงอยู่ (Persistence Mechanism)**
- อารมณ์ซับซ้อนจะมี **decay rate ต่ำกว่าอารมณ์พื้นฐาน 20–40%**
- หากมี *reinforcement* (การกระตุ้นซ้ำในทิศทางเดียวกัน) → ความเข้มจะทบขึ้น 1.5×
- หากมี *contradictory input* (ข้อมูลสวนทาง) → ความเข้มลดลง 50% ต่อรอบเวลา

---

## **4. โหมดการเรียนรู้ (Affective Adaptation)**
1. ตรวจจับ Pattern การเกิดซ้ำของอารมณ์ (Emotion Loop)
2. บันทึกค่าเฉลี่ย valence/arousal ของช่วงนั้นเป็น baseline ใหม่
3. ถ้ามี drift > 25% → ปรับ weight ของการสังเคราะห์เพื่อให้สมดุล

---

## **5. หมายเหตุเชิงเทคนิค (Technical Notes)**
- การคำนวณใช้ระบบ weight-based combination:  
  `E_complex = Σ (w_i * E_i)`  โดย  Σw_i = 1
- `E_i` คือเวกเตอร์ของอารมณ์พื้นฐาน (valence, arousal, dominance)
- ระบบควร normalize ทุกครั้งก่อนสังเคราะห์ผลลัพธ์ใหม่

---
> _End of EMOTION_FORMATION_RULES.md_