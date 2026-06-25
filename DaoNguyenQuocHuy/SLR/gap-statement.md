# Gap Statement – LLM-based API Test Generation for REST APIs

Evidence table: N = 24 papers

## Các khoảng trống phát hiện

### GAP-T (Technology): Thiếu các phương pháp kết hợp LLM với phản hồi thực thi động và tối ưu hóa chiến lược kiểm thử dài hạn

**Mô tả:**
Phần lớn nghiên cứu sử dụng LLM để sinh test cases hoặc tham số đầu vào từ OpenAPI Specification, nhưng ít nghiên cứu kết hợp đồng thời khả năng suy luận của LLM với cơ chế học từ phản hồi thực thi (runtime feedback) và tối ưu hóa chiến lược kiểm thử theo thời gian.

**Bằng chứng:**

* GPT-4, GPT-4o, GPT-3.5, DeepSeek, Llama-3 và Mistral xuất hiện trong phần lớn nghiên cứu (Ahmed 2026; Han 2025; Kim 2024; Pereira 2026; Saha 2025; Wang 2025).
* Chỉ một số ít nghiên cứu sử dụng phản hồi thực thi để cải thiện chiến lược sinh test:

  * Liu (2026): sử dụng response feedback.
  * Sondhi (2026 – ASTRA): sử dụng information-rich response messages.
  * Wang (2026): kết hợp Llama-3 với Reinforcement Learning.
* Không có nghiên cứu nào báo cáo việc kết hợp đồng thời:

  * OpenAPI reasoning,
  * Runtime feedback,
  * RL optimization,
  * Multi-step adaptive planning.

---

### GAP-M (Metric): Thiếu bộ tiêu chí đánh giá thống nhất giữa các nghiên cứu

**Mô tả:**
Các nghiên cứu sử dụng nhiều loại metric khác nhau khiến việc so sánh trực tiếp trở nên khó khăn.

**Bằng chứng:**
Từ cột Metric trong Evidence Table:

* Coverage metrics:

  * Statement Coverage (Ahmed 2026)
  * Operation Coverage (Han 2025; Khan 2026; Wang 2026)
  * API Coverage (Liu 2026)
  * Line Coverage (Li 2026 – MioHint)
  * Method/Branch Coverage (Kim 2025)

* Fault metrics:

  * Fault Detection Rate (Malema 2026; Wang 2026)
  * Bugs Detected (DLLens 2026)

* Quality metrics:

  * Precision / Recall / F1 (Kim 2024)
  * Classification Accuracy (Sondhi 2025)

Không có metric chuẩn được sử dụng xuyên suốt tất cả nghiên cứu.

---

### GAP-D (Dataset): Thiếu benchmark lớn và đa dạng phản ánh môi trường công nghiệp thực tế

**Mô tả:**
Đa số nghiên cứu đánh giá trên các benchmark nhỏ hoặc API công khai quen thuộc.

**Bằng chứng:**
Từ cột Dataset/API:

* PetStore xuất hiện nhiều lần:

  * Han (2025)
  * Khan (2026)
  * Malema (2026)
  * Wang (2026)

* EMB Benchmark được sử dụng nhiều:

  * Li (2026 – MioHint)
  * Liu (2026)

* Dataset quy mô lớn hiếm:

  * DLLens (2026): PyTorch + TensorFlow.
  * Wang (2025 – TestGPT): hệ thống ByteDance quy mô công nghiệp.

Phần lớn nghiên cứu chưa đánh giá trên:

* API quy mô lớn nhiều dịch vụ.
* Stateful workflows phức tạp.
* Hệ thống microservice thực tế.

---

### GAP-O (Oracle Generation): Chưa giải quyết triệt để bài toán sinh oracle tự động

**Mô tả:**
Nhiều nghiên cứu đạt coverage cao nhưng vẫn gặp khó khăn trong việc xác định kết quả mong đợi chính xác của test case.

**Bằng chứng:**
Từ cột Limitation:

* Ahmed (2026):

  * Oracle errors dominate failures.

* Valenzuela (2025):

  * OKAMI dataset contains only unary oracles.

* Pereira (2026):

  * Manual inspection introduces subjectivity.

* DLLens (2026):

  * Hallucination affects generated counterparts.

Các nghiên cứu hiện vẫn phụ thuộc vào:

* Manual validation.
* Human inspection.
* Simplified oracle assumptions.

---

### GAP-S (Sequence Testing): Thiếu nghiên cứu về kiểm thử chuỗi API dài và phụ thuộc trạng thái

**Mô tả:**
Phần lớn nghiên cứu tập trung vào endpoint đơn lẻ hoặc chuỗi thao tác ngắn.

**Bằng chứng:**

* Các dataset phổ biến:

  * PetStore
  * Restcountries
  * Genome Nexus
  * EMB services

* Không có nghiên cứu nào trong Evidence Table báo cáo:

  * Multi-user workflows.
  * Long transaction chains.
  * Cross-service state transitions.
  * Enterprise business process testing.

Các nghiên cứu hiện chủ yếu tối ưu coverage của endpoint hoặc operation đơn lẻ.

---

## Phát biểu GAP tổng hợp

Mặc dù các nghiên cứu hiện tại cho thấy LLM có khả năng cải thiện đáng kể việc sinh API test cases và tăng coverage, vẫn tồn tại khoảng trống đáng kể trong việc kết hợp suy luận LLM với runtime feedback và tối ưu hóa chiến lược kiểm thử dài hạn. Đồng thời, sự thiếu thống nhất về metric đánh giá, hạn chế của benchmark hiện tại, khó khăn trong sinh oracle tự động và việc chưa hỗ trợ đầy đủ các workflow API phức tạp khiến khả năng áp dụng thực tế của các phương pháp hiện nay vẫn còn hạn chế.
