# SPEC Final — Nhom16

## Track: Vinmec

## Product: AI Symptom Triage — Gợi ý chuyên khoa thông minh

---

## 0. TL;DR

Chúng tôi xây dựng một AI hỗ trợ bệnh nhân chọn đúng chuyên khoa ngay từ bước đầu tiên khi đặt lịch khám tại Vinmec.

Thay vì phải đoán hoặc tìm kiếm bên ngoài, người dùng chỉ cần mô tả triệu chứng → hệ thống sẽ:

* Hỏi thêm (nếu cần)
* Gợi ý tối đa 2 chuyên khoa phù hợp
* Cảnh báo nếu có dấu hiệu nguy hiểm (red flag)

👉 Đây là **augmentation**, không phải automation:
AI không chẩn đoán bệnh — chỉ giúp người dùng chọn đúng “entry point”.

---

## 1. Problem Statement

Trong quy trình đặt lịch khám hiện tại:

* Người dùng phải chọn chuyên khoa ngay từ đầu
* Nhưng ~30–40% không biết chọn khoa nào

Hậu quả:

* Chọn sai → mất thời gian → chuyển khoa
* Gọi tổng đài → chờ lâu
* Tự Google → thiếu tin cậy

👉 Vấn đề cốt lõi:
**Người dùng không biết bắt đầu từ đâu trong hệ thống y tế**

---

## 2. Solution Overview

### 🎯 Giải pháp

AI Symptom Triage tích hợp trực tiếp vào flow đặt lịch:

1. User nhập triệu chứng
2. AI hỏi thêm nếu cần
3. Trả về:

   * ≤ 2 chuyên khoa phù hợp
   * Lý do đơn giản, dễ hiểu
   * Hoặc cảnh báo nguy hiểm

---

### 🎯 Nguyên tắc thiết kế

* Không chẩn đoán bệnh
* Luôn có fallback (lễ tân / bác sĩ)
* Không tạo false certainty
* UX đơn giản, nhanh (< 5s)

---

## 3. AI Product Canvas

### Value

* Giảm sai chuyên khoa
* Giảm friction khi đặt lịch
* Tăng conversion booking

### Trust

* Domain y tế → high risk
* Cần:

  * Red flag detection
  * Explainable output
  * Escalation option

### Feasibility

* LLM + RAG (triệu chứng → chuyên khoa)
* Latency < 5s
* Cost thấp (~0.003–0.008$/query)

---

## 4. User Flows (4 Paths)

### ✅ Happy Path

* User: “Đau đầu, buồn nôn”
* AI → hỏi thêm → gợi ý: Thần kinh
* User đặt lịch

---

### ⚠️ Low-confidence Path

* Input mơ hồ: “Mệt, đau người”

AI:

* Hiển thị 2 lựa chọn
* Gợi ý gặp lễ tân

👉 AI thừa nhận “không chắc chắn”

---

### ❌ Failure Path

* AI gợi ý sai

Recovery:

* Bác sĩ điều chỉnh
* User có thể hỏi lại

---

### 🔁 Correction Path

* User feedback: “Chưa đúng”

System:

* Hỏi thêm context
* Update gợi ý
* Log làm training signal

---

## 5. Learning Signals

### Primary Signals

* Suggested vs actual department
* User correction rate
* Escalation rate

### Secondary Signals

* Time to booking
* Drop-off rate

👉 Insight:
Dữ liệu này tạo **data moat** (domain-specific + human feedback)

---

## 6. Evaluation Metrics

### 🎯 Objective

**Maximize Recall > Precision**

---

### Metrics Table

| Metric               | Target | Threshold      |
| -------------------- | ------ | -------------- |
| Correct Routing Rate | ≥ 75%  | < 60% = fail   |
| Red Flag Recall      | 100%   | Miss = STOP    |
| Suggestion Count     | ≤ 2    | > 2 = fail     |
| Escalation Rate      | < 30%  | > 50% = bad UX |

---

### Key Insight

Metric không chỉ là kỹ thuật
👉 mà là **product decision (trade-off risk vs UX)**

---

## 7. Failure Modes & Mitigation

### ❗ Red Flag Miss (Critical)

* Ví dụ: đột quỵ, đau tim

Mitigation:

* Rule-based detector riêng
* Override AI output
* Highlight cảnh báo

---

### ❗ Too Many Suggestions

Mitigation:

* Hard limit ≤ 2
* Default: Nội tổng quát

---

### ❗ Outdated Data

Mitigation:

* Sync database hàng ngày

---

## 8. System Design

### Architecture

* LLM (reasoning)
* RAG (triệu chứng → khoa)
* Red flag detector
* Verifier layer

---

### Flow

User input → Preprocess →
→ Red flag check →
→ LLM + RAG →
→ Verifier →
→ Output

---

## 9. UX Principles

1. Không tạo cảm giác “AI luôn đúng”
2. Luôn có exit option
3. Giải thích ngắn gọn
4. Không overload thông tin
5. Response < 5s

---

## 10. ROI Estimation

| Scenario     | Users/day | Accuracy | Benefit             |
| ------------ | --------- | -------- | ------------------- |
| Conservative | 50        | 60%      | Giảm tải nhẹ        |
| Realistic    | 150       | 75%      | Giảm 20% sai khoa   |
| Optimistic   | 400       | 85%      | Scale toàn hệ thống |

---

## 11. Kill Criteria

* Miss 1 red flag → STOP
* Accuracy < 60% → Rebuild
* Escalation > 50% → Redesign

---

## 12. Why This Matters

Chúng tôi không cố thay thế bác sĩ.

👉 Chúng tôi giải quyết một vấn đề nhỏ nhưng quan trọng:
**Giúp bệnh nhân bắt đầu đúng chỗ trong hệ thống y tế.**

---

## 13. Demo Statement (for presentation)

“We are not diagnosing the disease — we are helping patients choose the right entry point into the healthcare system.”

---
