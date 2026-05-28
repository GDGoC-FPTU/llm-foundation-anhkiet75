# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> temperature càng cao, văn phong càng đa dạng và cách diễn đạt càng sáng tạo.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Chatbot hỗ trợ khách hàng cần nhất quán và chính xác, khách hàng hỏi cùng một câu phải nhận được câu trả lời đáng tin cậy, không ngẫu nhiên. Temperature thấp giảm rủi ro model hallucination

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Tính toán chi phí

  Giả định hợp lý: 350 tokens/call ≈ 200 input + 150 output (prompt + response)

  Tổng số calls/ngày: 10,000 × 3 = 30,000 calls/ngày

  Tokens/ngày:
  - Input: 30,000 × 200 = 6,000,000 tokens
  - Output: 30,000 × 150 = 4,500,000 tokens

  GPT-4o đắt hơn GPT-4o-mini ~33 lần
  
  (Vì tỉ lệ giá input 5/0.15 = 33.3x và output 20/0.6 = 33.3x — tỉ lệ nhất quán nên không phụ thuộc vào cách chia input/output)


**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> Nên dùng GPT-4o: Hệ thống phân tích hợp đồng pháp lý hoặc tư vấn y tế — nơi mà một câu trả lời sai có thể gây thiệt hại tài chính/pháp lý lớn
   hơn nhiều so với $3,500/tháng tiết kiệm được. Độ chính xác cao hơn của GPT-4o trực tiếp giảm rủi ro nghiệp vụ.

  Nên dùng GPT-4o-mini: Chatbot FAQ, tóm tắt nội dung đơn giản, phân loại ticket hỗ trợ khách hàng — các tác vụ có câu trả lời chuẩn, dễ kiểm
  tra, và sai sót nhỏ không gây hậu quả nghiêm trọng. Tiết kiệm ~$3,500/tháng để tái đầu tư vào tính năng khác.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
>  Streaming quan trọng nhất khi response dài và người dùng đang chờ trực tiếp — ví dụ chatbot hội thoại, viết code, hay giải thích kỹ thuật.
  Thay vì chờ 5–10 giây rồi nhận toàn bộ text cùng lúc, người dùng thấy chữ xuất hiện ngay lập tức, tạo cảm giác hệ thống đang "suy nghĩ" thay
  vì bị treo — điều này giảm perceived latency đáng kể dù actual latency không đổi. Non-streaming phù hợp hơn khi output cần xử lý trước khi
  hiển thị — ví dụ: pipeline tự động hóa (phân loại email, gọi API theo chuỗi), structured output cần parse JSON, hay batch processing chạy nền
   không có user nào đang chờ — lúc đó việc nhận toàn bộ response một lần đơn giản hóa code và tránh lỗi partial-parse.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
