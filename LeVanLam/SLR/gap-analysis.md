# GAP Analysis – LLM-based REST API Testing with Runtime Feedback

**Member:** Le Van Lam
**Evidence table:** N = 8 papers | **Ngày:** 2026-06-26

---

## 0. Bối cảnh & Câu hỏi nghiên cứu

**RQ:** Đối với REST API có đặc tả OpenAPI, cơ chế **runtime feedback** (phản hồi thời gian chạy: HTTP status code, response body, lỗi thực thi) cải thiện được bao nhiêu về **độ bao phủ kiểm thử (coverage)** và **khả năng phát hiện lỗi (fault detection)** khi áp dụng vào quy trình sinh test case bằng LLM?

**PICO:**
- **P** = REST API có đặc tả OpenAPI/Swagger
- **I** = Test case sinh bởi LLM **có** vòng lặp runtime feedback
- **C** = Test case sinh thủ công / sinh bởi LLM **không có** runtime feedback
- **O** = Coverage (endpoint/line/branch), fault detection

---

## 1. GAP Chính — Tác động của Runtime Feedback chưa được đánh giá tách bạch

Các nghiên cứu gần đây đã chứng minh rằng LLM có thể hỗ trợ sinh API test case từ đặc tả OpenAPI, và rằng runtime feedback có thể cải thiện chất lượng đầu vào kiểm thử. Tuy nhiên, vẫn còn **thiếu bằng chứng thực nghiệm đơn giản, có kiểm soát và trực tiếp** về mức độ mà cơ chế runtime feedback đóng góp riêng vào coverage và fault detection trong quy trình sinh test case bằng LLM trên REST API.

Cụ thể, hầu hết các công trình hiện có:
1. **Gộp chung** runtime feedback vào trong một framework lớn (multi-agent, RL, fine-tuning) khiến không thể đo riêng đóng góp của riêng cơ chế feedback;
2. **Thiếu so sánh có kiểm soát** ba nhóm `Manual` vs `LLM (no feedback)` vs `LLM + feedback` trên cùng một bộ metric và cùng một REST API;
3. **Khó tái lập (low reproducibility)** do quy trình phức tạp, phụ thuộc model thương mại đắt tiền và chi phí thực thi cao.

> Đây chính là khoảng trống mà một thí nghiệm tối giản, dễ tái lập trên một REST API công khai (Swagger Petstore) có thể lấp đầy.

---

## 2. Chi tiết kiểm tra phản chứng

Kiểm tra từng công trình tiệm cận để xác nhận không công trình nào giải quyết **hoàn toàn** khoảng trống nêu trên.

| Paper | LLM | OpenAPI | Runtime Feedback | Giải quyết hoàn toàn GAP? | Lý do |
|-------|:---:|:-------:|:----------------:|:---------------------------:|-------|
| Wang (2026) | ✅ | ✅ | ⚠️ RL Reward | ❌ | Có cơ chế thích nghi dựa trên reward signal, nhưng gộp chung tác động — không đo riêng đóng góp của runtime feedback lên coverage và fault detection. |
| Liu (2026) | ✅ | ❌ | ✅ | ❌ | Cho thấy feedback giúp tăng coverage nhưng không thực hiện so sánh trực tiếp, có kiểm soát giữa Manual vs LLM vs LLM+Feedback. |
| ASTRA (2026) | ✅ | ❌ | ✅ | ❌ | Dùng response feedback để refine test case nhưng đóng gói trong framework riêng phức tạp, chi phí thực thi lớn, khó tái lập tối giản. |
| LlamaRestTest (2025) | ✅ | ✅ | ✅ | ❌ | Chứng minh feedback cải thiện coverage nhưng không thiết kế theo quy trình đơn giản, dễ tái lập với cùng một bộ metric (coverage + fault). |
| DeepREST | ⚠️ | ✅ | ✅ | ❌ | Dùng RL và status-code feedback nhưng mục tiêu chính là tối ưu khám phá trạng thái/chuỗi gọi API, không cô lập hiệu ứng feedback. |
| RESTGPT | ✅ | ✅ | ❌ | ❌ | Cải thiện chất lượng đặc tả OpenAPI nhưng không sử dụng runtime feedback trong vòng lặp sinh test. |
| PRIMG | ✅ | ❌ | ✅ | ❌ | Sử dụng compile/runtime error để refine prompt nhưng không tập trung vào ngữ cảnh REST API testing. |
| ACH | ✅ | ❌ | ✅ | ❌ | Sử dụng execution feedback nhưng áp dụng cho test generation nói chung, không phải REST API testing. |

**Chú thích:** ✅ = có / đáp ứng · ❌ = không · ⚠️ = có một phần (partial / gián tiếp)

---

## 3. Phân tích tổng hợp

Bảng phản chứng cho thấy một mẫu hình nhất quán: cộng đồng nghiên cứu **đã** sử dụng runtime feedback dưới nhiều dạng (RL reward, status-code, response body, compile/runtime error), và **đã** xác nhận nó có lợi. Tuy nhiên không có công trình nào đồng thời thỏa mãn cả ba điều kiện cần để trả lời RQ một cách dứt khoát:

- **(a) Cô lập biến** — đo riêng đóng góp của runtime feedback (ablation) thay vì gộp vào framework lớn;
- **(b) So sánh ba chiều có kiểm soát** — `Manual` vs `LLM no-feedback` vs `LLM + feedback` trên cùng REST API & cùng metric;
- **(c) Khả năng tái lập tối giản** — quy trình nhẹ, chạy được trên máy cá nhân, không phụ thuộc bắt buộc vào model thương mại đắt.

Khoảng trống này vừa **có ý nghĩa khoa học** (định lượng giá trị thực của feedback) vừa **khả thi về kỹ thuật** trong phạm vi RBL2.

---

## 4. Feasibility Check – GAP Chính

| Tiêu chí | Mức | Ghi chú |
|----------|:---:|---------|
| Dataset | ✅ | Swagger Petstore công khai (có sẵn OpenAPI spec) |
| Tool/API | ✅ | OpenAPI + Python + Requests |
| Compute | ✅ | Chạy trên máy cá nhân, không cần GPU lớn |
| Ground truth | ✅ | HTTP Status Code + Fault Detection |
| Skills | ✅ | Đã có code thực nghiệm |
| Thời gian | ✅ | Có thể hoàn thành trong RBL2 |
| Contribution | ✅ | Định lượng tác động của Runtime Feedback đối với LLM-generated API tests |

**Kết quả:** [X] ✅ FEASIBLE  /  [ ] ⚠️  /  [ ] ❌

---

## 5. Đề xuất hướng nghiên cứu (RBL2)

Thiết kế một thí nghiệm tối giản, có kiểm soát trên Swagger Petstore để định lượng đóng góp của runtime feedback:

- **Nhánh A — Manual baseline:** test case thiết kế thủ công.
- **Nhánh B — LLM no-feedback:** LLM sinh test case một lượt từ OpenAPI spec.
- **Nhánh C — LLM + runtime feedback:** LLM sinh test, thực thi, nhận HTTP status/response làm phản hồi và refine qua N vòng lặp.

So sánh ba nhánh trên cùng bộ metric: **endpoint coverage**, **fault detection rate** (và tùy chọn: số vòng lặp, chi phí token). Kết quả ablation A↔B↔C chính là bằng chứng trực tiếp lấp đầy khoảng trống đã nêu.
