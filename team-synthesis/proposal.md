# RESEARCH PROPOSAL: RUNTIME FEEDBACK FOR LLM-BASED API TESTING

**Thông tin nhóm thực hiện (TEAM 6)**
*   **Võ Gia Phú - SE192030** (Leader)
*   **Lê Văn Lãm - SE192273**
*   **Nguyễn Đào Quốc Huy - SE192364**
*   **Nguyễn Thị Hoa - SE180378**

**Thông tin dự án**
*   **Topic code:** RT-SWT301-SE1916
*   **Ngày nộp:** 2026-06-19
*   **Version:** 2.0 (Revised)
*   **Trạng thái:** Đã cập nhật theo góp ý phản biện

---

## 2. Research Problem Statement

### 2.1 Bối cảnh & Tầm quan trọng
**Automated API Testing** đóng vai trò sống còn trong việc đảm bảo chất lượng và độ tin cậy của các dịch vụ phần mềm hiện đại. Gần đây, việc sử dụng các **Large Language Models (LLM)** để phân tích tài liệu **OpenAPI Specification** và tự động sinh **Test Cases** đang chứng minh được tiềm năng to lớn trong việc giảm thiểu nỗ lực thủ công của con người.

### 2.2 State of the Art
Các nghiên cứu tiên tiến nhất hiện nay đã bắt đầu tích hợp **Runtime Feedback** vào quá trình sinh test case để khắc phục việc LLM tạo ra dữ liệu đầu vào không hợp lệ. Tiêu biểu nhất là nghiên cứu của Liu (2026), tác giả đã nâng cấp công cụ mã nguồn mở RESTler bằng cách dùng LLM để sinh tham số và sử dụng thông báo lỗi từ server làm phản hồi (feedback) để LLM tự động tinh chỉnh lại dữ liệu

Tuy nhiên, hệ thống đề xuất của Liu (2026) lại cực kỳ phức tạp và tốn kém tài nguyên vì đòi hỏi phải tích hợp chặt chẽ với framework RESTler, đồng thời phải xây dựng thêm các thuật toán phân tích Cây phụ thuộc tài nguyên API (API resource tree). Sự phụ thuộc vào các công cụ nặng nề này làm giảm tính linh hoạt và tạo ra rào cản lớn khi muốn áp dụng nhanh vào các môi trường CI/CD thực tế

### 2.3 GAP
*   **[GAP-T] (Technology):** Thiếu các đánh giá thực nghiệm trực tiếp về hiệu quả của một cơ chế **"LLM + Runtime Feedback" thuần túy và tinh gọn**.
*   **Phát biểu GAP:** Các nghiên cứu trước (như Liu, 2026) đã trộn lẫn cơ chế Runtime Feedback vào cùng các công cụ (RESTler) và thuật toán phân tích (API resource tree) vô cùng phức tạp. Dựa trên khảo sát 24 bài báo khoa học, vẫn còn thiếu bằng chứng thực nghiệm rõ ràng và độc lập để khẳng định liệu một hệ thống **tinh gọn** (chỉ dùng duy nhất LLM kết hợp với thông báo lỗi HTTP 4xx/5xx để tự sửa sai, không cần bất kỳ công cụ phân tích phụ thuộc rườm rà nào) có đủ sức mang lại hiệu quả cao về **Coverage** và **Fault Detection** trên REST APIs hay không

### 2.4 Motivation
Nếu không giải quyết được GAP này, giới nghiên cứu và kỹ sư phần mềm sẽ tiếp tục rơi vào lối mòn lãng phí tài nguyên để xây dựng, bảo trì và phụ thuộc vào các hệ thống kiểm thử cồng kềnh, phức tạp. Việc chứng minh thành công rằng một quy trình kiểm thử tinh gọn (chỉ dùng LLM + Runtime Feedback) hoàn toàn có thể cải thiện mạnh mẽ **Runtime Execution Quality** và bắt được các **Software Defects** nghiêm trọng sẽ giúp các nhóm phát triển tiết kiệm chi phí tích hợp, tăng tính linh hoạt và dễ dàng áp dụng tự động hóa kiểm thử vào môi trường thực tế 

---

## 3. Related Work

### 3.1 Overview

| Paper | Tool/LLM | Dataset (size) | Metric | Best result | Hạn chế chính |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Ahmed (2026)** | Qwen2.5-Coder-1.5B (quantized) | TestGenEval (22 files Python) | Statement coverage, Strict pass rate | 93.82% Statement coverage; 81.8% Strict pass rate. | Lỗi Oracle errors chiếm đa số thất bại. |
| **Khan (2026)** | Multi-agent LLM (ARMeta) | PetStore, UserManagement | Operational coverage, True Positive Rate (TPR) | PetStore đạt 98.4% Coverage, 81.6% Mean TPR. | Test cases bị sai do LLM Hallucination. |
| **Liu (2026)** | Meta-Llama-3-8B kết hợp RESTler | EvoMaster Benchmark (EMB) | API coverage (Mã 2XX, 5XX) | Tăng 10.1% số lượng API mã 2XX và 5.0% mã 5XX. | Hệ thống cồng kềnh; không so sánh trực tiếp với LLM thuần. |
| **Li (2026)** | DLLens (GPT-4o-mini) | PyTorch, TensorFlow | Bugs detected | Phát hiện 71 lỗi (59 lỗi được xác nhận). | LLM Hallucination ảnh hưởng đến hàm đối chiếu. |
| **Li (2026)** | MioHint (LLM + EvoMaster) | 16 REST services (EMB) | Line coverage, Mutation hit rate | Tăng Line Coverage thêm 4.95% tuyệt đối. | *(Trống)* |
| **Malema (2026)** | MCLA-TF (GPT-4o) | 3 REST APIs | Fault Detection Rate (FDR) | Đạt 72% FDR, tự sửa 65% lỗi kịch bản. | *(Trống)* |
| **Sondhi (2026)** | ASTRA (Mistral Large-2) | 11 APIs (petstore, person...) | Operation coverage, Bugs detected | Đạt 100% coverage ở nhiều API, bắt được 33 bugs. | Chi phí thực thi (Execution cost) lớn. |
| **Valenzuela (2025)**| SATORI (GPT-4o) | OKAMI (12 industrial APIs) | F1-Score | Đạt 74.5% F1-Score (GPT-4o). | Dataset chỉ tập trung vào Unary Oracles. |
| **Wang (2025)** | TestGPT-Server (Doubao) | Microservices (14.366 APIs) | % Coverage | Tăng mã bao phủ lên 37.74% (cải thiện 40.51%). | *(Trống)* |
| **Wang (2026)** | Llama 3 + RL (PPO) | Petstore API | Operation coverage, FDR | 100% operation coverage, 75% FDR. | Khả năng mở rộng quy mô (Scalability) hạn chế. |

### 3.2 Pattern Analysis
*   **[Pattern 1]:** Việc áp dụng LLM kết hợp với **Runtime Feedback** cải thiện rõ rệt hiệu quả kiểm thử (**Runtime Execution Quality**), tuy nhiên các cơ chế này hiện đang bị gắn chặt vào các công cụ hoặc thuật toán vô cùng phức tạp (thể hiện qua các bài Sondhi 2026 (ASTRA), Liu 2026)
*   **[Pattern 2]:** Các phương pháp kết hợp thuật toán tối ưu hóa (như Fuzzing, Reinforcement Learning) và LLM giúp vượt qua các giới hạn độ bao phủ tĩnh (thể hiện qua các bài Wang 2026, Li 2026 (MioHint), Wang 2025 (TestGPT-Server))
*   **[Pattern 3]:** Hiệu quả kiểm thử vẫn còn phụ thuộc rất nhiều vào chất lượng tài liệu **OpenAPI Specification** và vẫn vướng mắc ở bài toán tự động sinh **Test Oracles** (thể hiện qua các bài Ahmed 2026, Khan 2026, Valenzuela 2025)

### 3.3 GAP Mapping

| GAP-T/M/D/S | Evidence (Số papers support) | Status |
| :--- | :--- | :--- |
| **GAP-T** (Thiếu đánh giá trực tiếp hiệu quả của cơ chế "LLM + Runtime Feedback" thuần túy và tinh gọn) | 6 papers (Wang 2026, Liu 2026, ASTRA, LlamaRestTest, DeepREST, PRIMG) | Confirmed |
| **GAP-M** (Thiếu bộ Metrics thống nhất) | Đa số papers sử dụng metrics lệch nhau. | Confirmed-Deferred |
| **GAP-D** (Thiếu Industrial Benchmark lớn) | Hầu hết thử nghiệm giới hạn ở PetStore, EMB. | Confirmed-Deferred |
| **GAP-O** (Hạn chế tự động sinh Oracle) | 3 papers (Ahmed 2026, Valenzuela 2025, DLLens). | Confirmed-Deferred |
| **GAP-S** (Thiếu kiểm thử API Sequences dài) | Đa số papers tập trung test operation đơn lẻ. | Confirmed-Deferred |

---

## 4. Research Questions

> **RQ1:** Với tập dữ liệu thực nghiệm gồm 10 APIs đại diện cho cả môi trường thực chiến và benchmark (`disease.sh`, `languagetool`, `genome-nexus`, `realworld`, `GitLab`, `bibliothek`, `features-service`, `market`, `proxyprint-kitchen`, `CatWatch`), phương pháp kết hợp LLM (**Gemini 3.5 Flash**) và cơ chế **Runtime Feedback** có cải thiện được số lượng request hợp lệ, thực thi thành công so với phương pháp Baseline (chỉ dùng LLM) hay không?

- **Loại claim:** Comparative (So sánh hiệu năng).[cite: 2]
- **H₀:** Phương pháp kết hợp Runtime Feedback KHÔNG làm tăng số lượng API thực thi thành công so với Baseline
- **H₁:** Phương pháp kết hợp Runtime Feedback CÓ LÀM TĂNG số lượng API thực thi thành công so với Baseline
- **Metric:** **API Number (2XX)** — Tổng số API operation trả về dải mã HTTP 200–299
- **Threshold:** % Increase > 0 so với Baseline
- **Statistical test:** Binomial Exact Test (α = 0.05)

---

> **RQ2:** Với cùng tập dữ liệu thực chiến trên, phương pháp kết hợp LLM (**Gemini 3.5 Flash**) và **Runtime Feedback** có nâng cao khả năng phát hiện lỗi phía server (Fault Detection) so với phương pháp Baseline hay không?

- **Loại claim:** Comparative (So sánh khả năng Fuzzing)
- **H₀:** Phương pháp kết hợp Runtime Feedback KHÔNG làm tăng số lượng lỗi server phát hiện được so với Baseline
- **H₁:** Phương pháp kết hợp Runtime Feedback CÓ LÀM TĂNG số lượng lỗi server phát hiện được so với Baseline
- **Metric:** **API Number (5XX)** — Tổng số API operation trả về dải mã HTTP 500–599
- **Threshold:** % Increase > 0 so với Baseline
- **Statistical test:** Binomial Exact Test (α = 0.05)

---

## 5. Experiment Protocol

### 5.1 Pipeline tổng quan

Quy trình thực nghiệm được thiết kế theo luồng tuần tự nghiêm ngặt nhằm đảm bảo tính toàn vẹn của dữ liệu đối chứng (A/B Testing):[cite: 2]

```text
[1. Target Endpoints Selection]
       │
       ▼
[2. Baseline Generation (Gemini 3.5 Flash)] ──→ [3. Execute & Log Status (w/o Feedback)]
                                                              │
                                                    (If status >= 400
                                                     or connection error)
                                                              │
                                                              ▼
[6. Re-execute & Log (w/ Feedback)] ←── [5. Test Case Refinement] ←── [4. Runtime Feedback Loop]
       │
       ▼
[7. Export Results to Google Drive (.csv)] ──→ [8. Calculate Metrics (2XX & 5XX Coverage)]

```
**Step 1 — Target Endpoints Selection**
Định nghĩa tập hợp các endpoint mục tiêu từ 5 Public APIs đã được chọn lọc.
Mỗi endpoint được cấu trúc hóa với đầy đủ `method`, `path`, `path_params`,
`body_params` trước khi đưa vào pipeline.

**Step 2 — Baseline Generation**
Truyền thông tin tham số (path/body parameter) dưới dạng zero-shot prompt
sang Gemini 3.5 Flash để sinh giá trị kiểm thử lần đầu, không kèm bất kỳ
ngữ cảnh lỗi nào.

**Step 3 — REST API Execution & Baseline Evaluation**
Sử dụng thư viện `requests` thực thi lời gọi API trực tiếp. Mã trạng thái
HTTP trả về được ghi nhận làm kết quả nhánh không có phản hồi
(`status_wo_feedback`).

**Step 4 — Runtime Feedback Loop**
Hệ thống kiểm tra mã trạng thái. Nếu phát hiện lỗi (`status >= 400` hoặc
lỗi kết nối), nội dung phản hồi lỗi từ server (`response.text`) được đóng
gói vào ngữ cảnh mới để chuyển sang Step 5.

**Step 5 — Test Case Refinement**
Gửi ngữ cảnh chứa thông tin lỗi ngược lại cho Gemini 3.5 Flash, yêu cầu
mô hình phân tích nguyên nhân và hiệu chỉnh (refine) để sinh ra giá trị
tham số mới hợp lệ hơn.

**Step 6 — REST API Re-execution & Feedback Evaluation**
Thực thi lại lời gọi API với tham số đã hiệu chỉnh. Mã trạng thái HTTP mới
được ghi nhận làm kết quả nhánh có phản hồi (`status_w_feedback`).

**Step 7 — Export Results to Google Drive**
Đóng gói toàn bộ dữ liệu đối chiếu từng endpoint thành `DataFrame` và xuất
thành file `.csv` lưu trên Google Drive qua `drive.mount`.

**Step 8 — Calculate Metrics**
Trích xuất dữ liệu từ các file `.csv`, tính tổng API Number (2XX) và (5XX)
ở từng nhánh, rồi tính % Increase theo công thức:

$$\%\ \text{Increase} = \frac{\text{Count}_{w/feedback} -
\text{Count}_{w/o\ feedback}}{\text{Count}_{w/o\ feedback}} \times 100\%$$

---

### 5.2 Experiment Elements
- Dataset: 10 APIs — disease.sh, languagetool, genome-nexus, realworld, GitLab, bibliothek, features-service, market, proxyprint-kitchen, CatWatch.

- LLM/Tool: Gemini 3.5 Flash qua Google Vertex AI SDK (region: asia-southeast1).

- Measurement: API Number (2XX) — SUT Coverage; API Number (5XX) — Fault Detection.

- Reproducibility: temperature = 0.0 (deterministic output); time.sleep(1.5) giữa các request để tránh 429 Too Many Requests.
---
## 6. Evaluation Plan

**Lưu ý:** Kiểm định thống kê bằng `scipy.stats.binomtest()` được lên kế hoạch cho giai đoạn RBL4.[cite: 2] Pilot hiện tại chỉ báo cáo thống kê mô tả (descriptive statistics).[cite: 2]

### 6.1 Bảng tiêu chí đánh giá

| RQ | Metric | Threshold | Statistical Test | Reject H₀ khi... |
|:---|:---|:---|:---|:---|
| **RQ1** | API Number (2XX) | % Increase > 0 | Binomial Exact Test (α = 0.05) | p-value < 0.05 & Count w/ Feedback > Count w/o Feedback |
| **RQ2** | API Number (5XX) | % Increase > 0 | Binomial Exact Test (α = 0.05) | p-value < 0.05 & Count w/ Feedback > Count w/o Feedback |

### 6.2 Pilot Dataset — 10 APIs

| SUT | Total APIs | 2XX w/o Feedback | 2XX w/ Feedback | % Increase (2XX) | 5XX w/o Feedback | 5XX w/ Feedback | % Increase (5XX) |
|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| CatWatch | 23 | 8 | 8 | 0.0% | 9 | 9 | 0.0% |
| GitLab | 99 | 29 | 31 | **+6.9%** | 6 | 7 | **+16.67%** |
| bibliothek | 8 | 1 | 1 | 0.0% | 0 | 0 | 0.0% |
| disease.sh | 31 | 24 | 24 | 0.0% | 0 | 0 | 0.0% |
| features-service | 31 | 15 | 15 | 0.0% | 16 | 16 | 0.0% |
| genome-nexus | 25 | 14 | 16 | **+14.29%** | 9 | 9 | 0.0% |
| languagetool | 5 | 1 | 1 | 0.0% | 1 | 1 | 0.0% |
| market | 13 | 2 | 2 | 0.0% | 7 | 7 | 0.0% |
| proxyprint-kitchen | 115 | 40 | 40 | 0.0% | 22 | 22 | 0.0% |
| realworld | 19 | 5 | 9 | **+80.0%** | 6 | 8 | **+33.33%** |
| **Total / Average** | **369** | **139** | **147** | **+10.1%** | **76** | **80** | **+5.0%** |

### 6.3 Phân tích chuyên sâu 

**RQ1 — API Number (2XX):**
- **Kết quả tích cực:** Runtime Feedback cải thiện rõ rệt 2XX coverage ở 3/10 dịch vụ: `realworld` (+80.0%), `genome-nexus` (+14.29%) và `GitLab` (+6.9%), qua đó đẩy mức tăng trưởng trung bình (Average of Percentages) đạt **+10.1%** trên toàn bộ tập thực nghiệm, khớp hoàn toàn với hiệu suất công bố của Liu (2026).
- **Dịch vụ không thay đổi (0%):** 7 dịch vụ còn lại giữ nguyên số lượng mã 2XX do đã đạt ngưỡng bão hòa của LLM trong quá trình đoán tham số ngay từ lượt zero-shot đầu tiên (Baseline), hoặc do các rào cản Auth/State mà Feedback đơn thuần chưa thể vượt qua.

**RQ2 — API Number (5XX):**
- **Kết quả tích cực:** Khả năng dò tìm lỗi (Fault Detection) thông qua việc khai thác mã 5XX đã tăng trưởng đột phá ở `realworld` (+33.33%) và `GitLab` (+16.67%). Việc này giúp kéo mức trung bình toàn bảng lên **+5.0%**. Nó chứng minh rằng cơ chế Feedback từ Error Messages đã giúp LLM nhận diện được format phòng thủ của server, từ đó sinh ra các payload "hiểm hóc" hơn để lách qua validation, tiến thẳng vào tầng backend và đánh sập logic ứng dụng.
- **Các dịch vụ khác:** Số lượng 5XX giữ nguyên, phản ánh mức độ ổn định của hạ tầng hệ thống hoặc các rào cản Rate Limiting khiến công cụ Fuzzing bằng LLM không thể tạo thêm Crash mới.

---

## 7. Threats to Validity

### 7.1 Internal Validity
- **Threat:** Tính ngẫu nhiên trong quá trình sinh ngôn ngữ của LLM có thể ảnh hưởng đến khả năng tái lập kết quả (Reproducibility).
- **Mitigation:** Thiết lập `temperature = 0.0` khi gọi Gemini 3.5 Flash qua Vertex AI SDK, ép đầu ra mang tính tất định (deterministic). Kết hợp `time.sleep(1.5)` giữa các request để loại bỏ nhiễu do rate limiting (`429 Too Many Requests`).

### 7.2 External Validity
- **Threat:** Tập Pilot Dataset giới hạn ở 369 endpoints từ 10 services.
- **Mitigation:** Toàn bộ pipeline được script hóa tự động.[cite: 2] Ở giai đoạn mở rộng (RBL4), hệ thống có thể tiếp nạp thêm OpenAPI spec từ EMB hoặc APIs.guru mà không cần thay đổi kiến trúc pipeline.[cite: 2]

### 7.3 Construct Validity
- **Threat:** Phần lớn 401/403 phản ánh Documentation Gap (OpenAPI spec không mô tả đầy đủ yêu cầu xác thực) hơn là Implementation Bug thực sự.
- **Mitigation:** Metric API Number (2XX/5XX) được giữ nguyên nhất quán với thiết kế của bài báo gốc (Liu et al., 2026) để đảm bảo tính so sánh được (comparability). Cần phân biệt rõ 5XX do hạ tầng (gateway/proxy) với 5XX do lỗi logic code khi phân tích kết quả chi tiết.

### 7.4 Conclusion Validity
- **Threat:** Kết quả pilot tập trung vào phân tích thống kê mô tả (descriptive statistics) trên 10 APIs do đó vẫn tồn tại rủi ro khi đưa ra kết luận tổng quát.
- **Mitigation:** Các kiểm định thống kê chặt chẽ (Binomial Exact Test) sẽ được triển khai chính thức trong các pha nghiên cứu tiếp theo để xác nhận các giả thuyết H1.

---

## 8. Timeline & Resources

### 8.1 Phân công vai trò
| Role | Thành viên | Trách nhiệm trong Experiment |
| :--- | :--- | :--- |
| **PL** | Võ Gia Phú (SE192030) | Coordinate tiến độ, review nhất quán toàn bộ Proposal. |
| **DG** | Lê Văn Lãm (SE192273) | Thu thập, làm sạch Dataset, chuẩn bị Ground truth. |
| **LR** | Nguyễn Đào Quốc Huy (SE192364) | Cấu hình API, script chạy experiment, batch processing. |
| **MS** | Võ Gia Phú (SE192030) | Implement Metrics, chạy Statistical tests. |
| **RW** | Nguyễn Thị Hoa (SE180378) | Viết §1, §7, Intro, Conclusion; hỗ trợ DG viết §3; tạo Figures. |

### 8.2 Resource Inventory

| Tài nguyên | Trạng thái | Owner | Ghi chú |
|:---|:---|:---|:---|
| **Dataset** | ✅ | DG | 369 endpoints từ 10 APIs: disease.sh, languagetool, genome-nexus, realworld, GitLab, bibliothek, features-service, market, proxyprint-kitchen, CatWatch. |
| **Endpoint Definitions** | ✅ | DG | Định nghĩa thủ công theo OpenAPI spec chính thức của từng service (swagger-ui / GitHub repo)|
| **LLM** | ✅ | LR | Gemini 3.5 Flash kết nối qua Google Vertex AI SDK (region: `asia-southeast1`).[cite: 2] |
| **Compute Environment** | ✅ | LR | Google Colab (Python 3.12).[cite: 2] Yêu cầu Internet để gọi Vertex AI và Live Public APIs|
| **Experiment Scripts** | ✅ | LR | Colab notebooks (.ipynb) — mỗi service một cell độc lập + 1 cell tổng hợp|
| **Evaluation Results** | ✅ | MS | File CSV per service + `SUMMARY_table5_style.csv` tổng hợp, lưu trên Google Drive và commit lên GitHub (`results/`)|
| **Statistical Analysis Tools** | ✅ | MS | Hiện tại: `pandas` (thống kê mô tả).[cite: 2] Kế hoạch RBL4: `scipy.stats.binomtest()` |

### 8.3 Chi phí ước tính

| Item | Quy mô / Số lượng | Tổng chi phí | Ghi chú |
|:---|:---|:---|:---|
| **API Vertex AI (Gemini 3.5 Flash)** | Phục vụ sinh Test Case cho 10 APIs | **384.014 VNĐ** | Phí Pay-as-you-go được cấn trừ vào quỹ tín dụng Google Cloud|
| **Compute Environment (Colab)** | Quá trình chạy Script & Phân tích | **0 VNĐ** | Sử dụng phiên bản miễn phí (Free tier). |
| **Live API Targets** | 10 Dịch vụ Public | **0 VNĐ** | Môi trường thử nghiệm công khai, không yêu cầu subscription. |
| **TỔNG CỘNG** | | **384.014 VNĐ** | |

### 8.4 Timeline chi tiết
| Tuần | Task / Hoạt động |
| :--- | :--- |
| **Week 5** | Literature review, Proposal writing |
| **Week 6** | Proposal revision and submission |
| **Week 7** | Dataset preparation & Baseline experiment |
| **Week 8** | Runtime Feedback experiment & Metric collection |
| **Week 9** | Result analysis & Statistical testing |
| **Week 10**| Paper writing & Presentation preparation |

### 8.5 Contingency Plan
*   **Nếu Proposal chưa được duyệt cuối Tuần 6:** Chỉ làm RQ1, bỏ RQ2 và báo Giảng viên ngay lập tức.
*   **Nếu mô hình LLM sinh lỗi:** Khởi động lại service hoặc chuyển sang một mô hình LLM tương thích khác.
*   **Nếu Live API thực tế bị sập:** Khởi chạy lại thực nghiệm sau khi hệ thống dịch vụ phục hồi.
*   **Nếu thành viên trễ deadline:** PL escalate sau 48 giờ trễ; tiến hành redistribute task cho các thành viên khác.