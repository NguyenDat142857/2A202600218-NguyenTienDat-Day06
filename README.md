---

# 🚀 AI Tutor — Intelligent Learning Assistant (Internal Q&A System)

---

## 🧠 Project Overview

**AI Tutor** là một trợ lý học tập thông minh giúp sinh viên tra cứu, hiểu và tương tác với kiến thức từ tài liệu nội bộ (slides, notes, syllabus) thông qua giao diện hỏi đáp tự nhiên. 

Khác với các chatbot thông thường, AI Tutor được thiết kế như một **Learning Companion** (người bạn đồng hành học tập), tập trung vào việc hiểu ngữ cảnh, giải thích tư duy và xây dựng lớp tin cậy (trust layer) giữa người máy và người học.

---

## ❗ The Problem

Trong môi trường học thuật, người học thường đối mặt với các rào cản:
* **Information Overload:** Mất quá nhiều thời gian để lục lại thông tin từ hàng trăm trang slide và tài liệu rời rạc.
* **Lack of Clarity:** Dễ hiểu sai kiến thức nhưng không có công cụ giải thích tức thời.
* **AI Hallucination:** Khi dùng AI phổ thông, người dùng không biết khi nào AI đang "nói dối", dẫn đến rủi ro sai lệch kiến thức nghiêm trọng.
* **Dependency:** Quá phụ thuộc vào thời gian phản hồi của giảng viên/trợ giảng.

---

## 💡 The Solution

Hệ thống **Retrieval-Augmented Generation (RAG)** thông minh giúp cá nhân hóa việc học:

* **Augmentation, not Replacement:** Hỗ trợ mở rộng khả năng học tập, không thay thế vai trò của giảng viên.
* **Step-by-step Logic:** Không chỉ đưa ra đáp án, AI Tutor giải thích quy trình tư duy.
* **Transparent Sourcing:** Luôn đi kèm trích dẫn (citations) chính xác từ tài liệu gốc.
* **Uncertainty Handling:** Hệ thống biết nói "Tôi không chắc" và cung cấp các hướng xử lý thay thế.

---

## ⚙️ Key Features

| Tính năng | Mô tả |
| :--- | :--- |
| **📚 RAG Engine** | Truy xuất thông tin trực tiếp từ Vector Database của tài liệu nội bộ để giảm thiểu ảo tưởng (hallucination). |
| **🔗 Citation-based** | Gắn thẻ nguồn (source tagging) cho từng phân đoạn câu trả lời để người dùng tự kiểm chứng. |
| **💬 Smart Follow-up** | Gợi ý các câu hỏi đào sâu kiến thức dựa trên ngữ cảnh vừa hỏi. |
| **⚠️ Uncertainty UX** | Hiển thị mức độ tự tin và cảnh báo khi dữ liệu trong kho tài liệu không đủ để trả lời. |

---

## 🧩 System Architecture

Dòng chảy dữ liệu của AI Tutor dựa trên kiến trúc RAG hiện đại:
1.  **User Query:** Người dùng đặt câu hỏi.
2.  **Embedding:** Chuyển đổi câu hỏi thành vector không gian.
3.  **Vector Search:** Tìm kiếm các đoạn tài liệu liên quan nhất trong **FAISS / ChromaDB**.
4.  **Context Injection:** Đưa các đoạn tài liệu tìm được vào Prompt gửi cho LLM.
5.  **Generation:** **OpenAI API** tạo câu trả lời dựa trên ngữ cảnh đã cung cấp.
6.  **Response + Citation:** Trả về kết quả kèm link/trang tài liệu gốc.

---

## 🧪 Design Principles (UX for AI)

Dựa trên bài học từ **Day 5**, dự án tập trung vào việc thiết kế trải nghiệm cho hệ thống xác suất (**Probabilistic System**):

### 4 User Paths Handling:
1.  **✔️ Success Path (AI đúng):** Cung cấp câu trả lời nhanh, gọn, kèm nguồn.
2.  **❌ Failure Path (AI sai):** Cung cấp công cụ feedback (Thumbs up/down) để hệ thống tự học.
3.  **⚠️ Uncertainty Path (AI không chắc):** AI chủ động báo cáo mức độ tự tin thấp và gợi ý người dùng kiểm tra lại tài liệu cụ thể.
4.  **💔 Trust Loss Path (User mất niềm tin):** Luôn hiển thị nút "Xem tài liệu gốc" để người dùng đối chiếu trực tiếp.

---

## 📊 Evaluation Metrics

Để đảm bảo chất lượng đầu ra, hệ thống được đánh giá qua các chỉ số:
* **Answer Accuracy:** $\ge 80\%$ (Độ chính xác nội dung).
* **Citation Accuracy:** $\ge 90\%$ (Trích dẫn đúng nguồn).
* **Hallucination Rate:** $< 5\%$ (Tỷ lệ thông tin sai lệch).
* **User Trust Score:** Đo lường định tính về mức độ an tâm của sinh viên khi sử dụng.

---

## 🎯 Impact & Future Directions

### Impact:
* 🚀 **Học nhanh hơn:** Giảm 70% thời gian tìm kiếm tài liệu.
* 🧠 **Hiểu sâu hơn:** Giải thích đa chiều giúp ghi nhớ lâu.
* 🌍 **Bình đẳng hóa:** Mọi sinh viên đều có trợ lý riêng 24/7.

### Future:
* **Adaptive Learning:** Tự động điều chỉnh độ khó dựa trên lịch sử hỏi đáp.
* **Multimodal:** Hỗ trợ đọc hiểu cả Video bài giảng và sơ đồ hình ảnh.
* **LMS Integration:** Tích hợp trực tiếp vào Canvas/Moodle.

---

## 🧠 Core Insight

> **"AI không cần phải luôn luôn đúng, nhưng nó phải tuyệt đối minh bạch khi nó có thể sai."**

---

## 🔥 Closing Statement

> **“We are not replacing teachers — we are augmenting how students learn.”**

---
*Created by Nguyễn Tiến Đạt - 2026*
