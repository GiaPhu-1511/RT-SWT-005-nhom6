# Gap Statement — LLM-based REST API Test Generation and Testing
**Thành viên:** Nguyễn Thị Hoa  

Evidence table: 7 papers

---

### GAP-T (Technology)
--Khoảng trống: Đa số các giải pháp hiện tại phụ thuộc quá nhiều vào LLM tĩnh (như GPT-3.5/GPT-4 hoặc Llama) để sinh kịch bản kiểm thử (test cases) một chiều dựa trên tài liệu đặc tả (OpenAPI spec). Điều này dẫn đến hai hạn chế kỹ thuật lớn: (1) Giới hạn về cửa sổ ngữ cảnh (Context Window) khiến LLM không thể xử lý các tài liệu đặc tả API công nghiệp khổng lồ, và (2) Hiện tượng "ảo giác" (hallucination) khiến LLM thường xuyên sinh ra mã lỗi cú pháp hoặc các điểm cuối (endpoints) không tồn tại, bắt buộc phải có hệ thống xác thực phụ trợ (validation pipeline) cồng kềnh. Ngoài ra, việc đưa LLM vào luồng chạy CI/CD tự động của doanh nghiệp quy mô lớn vẫn còn rất nhiều thách thức cấu hình.

**Bằng chứng:**
Paper ID#24 nhấn mạnh giới hạn của LLM khi xử lý các API specifications có độ dài lớn.
- Paper ID#48 và ID#2 đều báo cáo rằng LLM tự sinh lỗi cú pháp và "ảo giác" ra tham số sai, buộc phải có quá trình kiểm duyệt lại thủ công hoặc tự động.
- Paper ID#35 (Poth et al.) khẳng định việc áp dụng tự động LLM vào cấu hình CI/CD doanh nghiệp (như tại Volkswagen) đòi hỏi khối lượng công việc khổng lồ để duy trì.

---

### GAP-M (Metric)
--Khoảng trống: Các nghiên cứu hiện tại quá tập trung vào các tiêu chí đo lường bề mặt (shallow metrics) như độ bao phủ dòng/nhánh mã (Line/Branch Coverage), độ bao phủ mã trạng thái (Status Code Coverage) hoặc tỷ lệ điểm cuối được gọi (Endpoint reachability). Rất ít nghiên cứu có khả năng đo lường độ sâu về kiểm thử chuỗi nghiệp vụ có tính phụ thuộc dữ liệu (Stateful/Business logic API testing), hoặc đánh giá tỷ lệ dương tính giả (False Positives) một cách hệ thống trong các hệ thống API phức tạp.


**Bằng chứng:**
- Paper ID#38 (KAT framework) và ID#34 (LlamaRestTest) đều chủ yếu báo cáo Status Code và Code Coverage. Dù KAT có đề cập đến đồ thị phụ thuộc (Dependency Graph), nó vẫn gặp khó khăn nếu mô tả ngôn ngữ tự nhiên sơ sài.
- Dù SATORI (Paper ID#41) có sinh Test Oracles tĩnh đạt F1-score khá tốt (74.3%), nhưng mô hình này vẫn thất bại khi đối mặt với các ràng buộc bất biến phức tạp (complex invariants) nếu test suite thiếu tính đa dạng.
---

### GAP-D (Dataset)
--Khoảng trống: Các thực nghiệm hiện tại bị giới hạn trên các tập dữ liệu quá nhỏ hoặc các bộ khung tiêu chuẩn cũ (benchmarks) không phản ánh đúng sự phức tạp của hệ thống phần mềm thực tế hiện đại. Phần lớn các bài báo chỉ kiểm thử trên dưới 15 dịch vụ REST API, chủ yếu là các dự án mã nguồn mở hoặc các API đơn giản, làm giảm tính khái quát hóa (generalizability) của mô hình khi áp dụng vào lĩnh vực công nghiệp thực thụ.


**Bằng chứng:**
- Hầu hết các nghiên cứu (ID#2, ID#34, ID#38) đều sử dụng tập EvoMaster Benchmark hoặc chọn ngẫu nhiên khoảng 10-12 public REST APIs (như Spotify).
- Paper ID#48 chỉ thực nghiệm trên vỏn vẹn 2 REST APIs thực tế.
- Paper ID#24 chỉ thử nghiệm giới hạn trên 3 OpenAPI specifications.

---

## Phát biểu GAP tổng hợp

****Mặc dù Mô hình Ngôn ngữ Lớn (LLM) đã chứng minh tiềm năng to lớn trong việc tự động hóa sinh test cases và test oracles cho REST API (giúp nâng cao đáng kể độ bao phủ mã), nhưng lĩnh vực này vẫn tồn tại những khoảng trống cốt lõi về khả năng mở rộng (scalability) và độ tin cậy (reliability).

Cụ thể, các nghiên cứu chưa giải quyết triệt để bài toán (GAP-T) LLM bị "ảo giác" và tràn cửa sổ ngữ cảnh khi xử lý các tài liệu đặc tả API công nghiệp khổng lồ, khiến chúng khó tích hợp trực tiếp vào CI/CD mà không qua hệ thống xác thực. Hơn nữa, việc đánh giá chủ yếu dựa trên (GAP-M) các tiêu chí bao phủ bề mặt (như Status Code) thay vì tập trung vào kiểm thử luồng nghiệp vụ phức tạp có trạng thái. Cuối cùng, (GAP-D) thực nghiệm hiện tại thường bị bó hẹp trong các tập dữ liệu mã nguồn mở quy mô nhỏ (chỉ dưới 15 APIs), làm giảm đáng kể khả năng khái quát hóa kết quả vào môi trường thực tế của doanh nghiệp.

Những khoảng trống này mở ra cơ hội nghiên cứu cấp thiết cho việc phát triển các mô hình lai (Hybrid LLM-Fuzzing) hoặc ứng dụng RAG (Retrieval-Augmented Generation) để vượt qua giới hạn đọc hiểu tệp OpenAPI Specifications cỡ lớn.