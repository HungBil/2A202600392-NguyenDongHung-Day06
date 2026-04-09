# Individual Reflection — Nguyễn Đông Hưng (2A202600392)

## 1. Role

**Business Analyst (BA) + Team Lead.** Phụ trách phân tích bài toán, phân công công việc cho các thành viên, review và fix system prompt, kiểm tra giao diện sản phẩm cuối.

---

## 2. Đóng góp cụ thể

- **Phân tích bài toán & phân công nhóm:** Xác định problem statement cho track VinFast ("khách không biết chọn xe nào phù hợp"), chia rõ từng phần SPEC cho từng thành viên (Canvas → Hưng, User Stories → Nhân, Eval + ROI + Failure modes → Vương, Frontend + Agent → Nghĩa). Đảm bảo mỗi người có output cụ thể để track tiến độ.

- **Viết AI Product Canvas & Problem Statement:** Xây dựng phần 1 của SPEC — xác định user segment (khách cá nhân lần đầu tìm xe VinFast), pain point rõ ràng (15–30 phút chờ tư vấn), justify Augmentation thay vì Automation, và thiết kế learning signal (correction log, data flywheel qua Summarizer Agent lưu vào `data_vf/data/context/`).

- **Test & review system prompt + giao diện:** Chạy thử nhiều lượt hội thoại với chatbot "Vivi", kiểm tra prompt có giữ đúng guardrails không (từ chối trả lời về lãi suất, không đoán khi thiếu tiêu chí), review UI luồng chat widget tích hợp trong trang About và trang 3D viewer, đề xuất fix các trường hợp edge case (prompt injection, câu hỏi ngoài scope).

---

## 3. SPEC — Mạnh nhất & Yếu nhất

**Mạnh nhất: Phần 4 — Top 3 Failure Modes.**
Nhóm xác định được 3 failure mode nguy hiểm nhất và quan trọng là phân biệt rõ "*user có biết AI sai không*" — case nguy hiểm nhất là khi user KHÔNG biết bị sai (AI im lặng hoặc gợi ý xe vượt budget mà không báo). Mitigation cụ thể: nói thẳng giới hạn catalog, không để user bị "treo" — luôn có escape hatch (hotline / tư vấn viên / showroom).

**Yếu nhất: Phần 5 — ROI 3 kịch bản.**
3 kịch bản Conservative / Realistic / Optimistic chủ yếu chỉ khác nhau ở tỷ lệ adoption (20%/40%/60%), assumptions nền vẫn giống nhau. Để thực sự có ý nghĩa, mỗi kịch bản nên gắn với một assumption thị trường khác nhau — ví dụ: Conservative = triển khai 1 showroom thí điểm, Realistic = 5 showroom, Optimistic = tích hợp toàn website VinFast. Sẽ thuyết phục hơn nhiều.

---

## 4. Đóng góp khác

- Trong quá trình test system prompt, phát hiện chatbot "Vivi" trả lời cả câu hỏi về lãi suất trả góp (vi phạm guardrail) — đề xuất fix thêm constraint cứng trong `prompts.py` và kiểm tra lại sau khi fix.
- Review flow UI: phát hiện trường hợp nút "Xem mô hình 3D" không hiển thị đúng khi tên xe có dấu cách — báo cáo cho teammate phụ trách frontend để fix.
- Hỗ trợ chuẩn bị slide demo: đề xuất cấu trúc trình bày theo flow Problem → Auto/Aug decision → Demo live → Failure mode chính.

---

## 5. Điều học được

Trước hackathon, nghĩ BA chỉ là "người viết requirement". Qua hackathon này mới hiểu **BA trong AI product là người phải quyết định ranh giới của AI** — cụ thể là Auto hay Aug, AI được phép trả lời gì và phải im lặng gì. Những quyết định này không phải kỹ thuật, mà là **product decision có hậu quả trực tiếp**: nếu AI tự động hóa quyết định mua xe (auto), sai một lần là mất tin khách hàng hoàn toàn. Nếu để khách quyết định cuối (aug), chi phí sai thấp hơn nhiều. Đây là bài học từ việc viết Canvas và test thực tế, không phải lý thuyết.

---

## 6. Nếu làm lại

Sẽ **phân công và chốt scope sớm hơn 1 tiếng** — buổi sáng nhóm mất khoảng 30–45 phút thảo luận vòng vòng về việc chọn track nào (VinFast hay Vinmec). Nếu BA ra quyết định nhanh dứt khoát hơn từ M1 (9:00), nhóm sẽ có thêm gần 1 tiếng để build và test. Cụ thể: sẽ chuẩn bị sẵn 1 bảng so sánh 3 track (user pain, feasibility, AI fit) để chọn trong 10 phút, không để thảo luận open-ended kéo dài.

---

## 7. AI giúp gì / AI sai gì

**AI giúp:**
- Dùng Antigravity (Claude/Gemini) để brainstorm failure modes — AI gợi ý thêm case "prompt injection khi user yêu cầu AI đóng vai nhân viên sale ưu tiên xe có hoa hồng cao" mà nhóm chưa nghĩ đến. Case này thực tế và có mitigation rõ ràng.
- Dùng AI để iterate nhanh system prompt qua nhiều vòng — thay vì viết tay, AI giúp draft → test → fix trong 15–20 phút thay vì 1–2 tiếng.

**AI sai/mislead:**
- Khi review SPEC, AI (Claude) liên tục đề xuất thêm tính năng: đặt lịch lái thử, so sánh nhiều variant màu xe, gợi ý phụ kiện... Nghe hợp lý nhưng tất cả đều vượt scope hackathon. Phải chủ động cut để không bị scope creep. **Bài học: AI brainstorm không có giới hạn scope — người BA phải là người giữ scope, không phải AI.**
