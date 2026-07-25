# RBL-4 Technical Notes and Error Log

**Project:** LLM-based REST API Testing with Runtime Feedback  
**Topic:** RT-SWT-005  
**Phase:** RBL-4 – Experiment  
**Repository:** `RT-SWT-005-nhom6`  
**Branch:** `Flower`  
**Main notebook/code:** `SWT.ipynb` / `swt.py`  
**Last updated:** 2026-07-25  

---

## 1. Mục tiêu của giai đoạn RBL-4

Giai đoạn RBL-4 triển khai thực nghiệm để so sánh hai phương pháp sinh test input cho REST API:

1. **LLM-only:** LLM sinh dữ liệu đầu vào và request được thực thi một lần.
2. **LLM + Runtime Feedback:** Nếu request đầu tiên thất bại, response hoặc error message được đưa lại vào prompt để LLM sinh dữ liệu đầu vào mới.

Mục tiêu hiện tại của code là so sánh kết quả của hai phương pháp thông qua số lượng HTTP `2XX` và `5XX`.

---

## 2. Technical Decisions

### TD-01 – Sử dụng Gemini thông qua Vertex AI

- **Decision:** Sử dụng Gemini làm mô hình sinh dữ liệu đầu vào cho API.
- **SDK:** `google-genai`
- **Project:** `rbl-core-2026`
- **Model trong các cell thực nghiệm:** `gemini-3.5-flash`
- **Location chính:** `asia-southeast1`
- **Reason:** Code đã tích hợp được Vertex AI và có thể gọi model trực tiếp từ Google Colab.
- **Status:** Implemented
- **Note:** Một số cell kiểm tra model sử dụng `us-central1`, trong khi các cell thực nghiệm sử dụng `asia-southeast1`. Cần thống nhất location trước khi chạy chính thức.

---

### TD-02 – So sánh LLM-only và LLM + Runtime Feedback

- **Decision:** Mỗi endpoint có hai kết quả:
  - `status_wo_feedback`
  - `status_w_feedback`
- **Reason:** Đây là thiết kế trực tiếp để đánh giá tác động của runtime feedback.
- **Status:** Partially implemented
- **Limitation:** Chỉ phần `disease.sh` đang thực thi request thật cho cả hai nhánh. Các service khác còn sử dụng status code mô phỏng hoặc gán cứng.

---

### TD-03 – Điều kiện kích hoạt feedback

- **Decision:** Feedback được kích hoạt khi:
  - HTTP status code lớn hơn hoặc bằng `400`; hoặc
  - Có exception và status được đặt thành `-1`.
- **Feedback content:** Phần đầu của response body hoặc thông báo exception.
- **Feedback length:** Tối đa khoảng 300 ký tự trong phần thử nghiệm `disease.sh`.
- **Reason:** Giúp LLM biết nguyên nhân request trước thất bại và sửa lại tham số.
- **Status:** Implemented for `disease.sh`

---

### TD-04 – Cách sinh giá trị tham số

- **Decision:** LLM sinh giá trị riêng cho từng tham số.
- **Input cho prompt:**
  - API path
  - Parameter name
  - Parameter description
  - Error feedback nếu có
- **Output format:** `<answer>value<answer>`
- **Post-processing:**
  - Tách nội dung trong thẻ `<answer>`.
  - URL-encode path parameter bằng `urllib.parse.quote`.
  - Thử chuyển body value sang JSON bằng `json.loads()` ở phần Genome Nexus.
- **Status:** Implemented
- **Risk:** Format `<answer>value<answer>` không có closing tag chuẩn `</answer>` nên parser phải xử lý nhiều trường hợp và có thể lấy sai nội dung.

---

### TD-05 – Tập REST API được sử dụng

| Service | Số endpoint trong code | Kiểu thực thi hiện tại |
|---|---:|---|
| disease.sh | 31 |
| LanguageTool | 5 ||
| Genome Nexus | 23 | 
| RealWorld | 19 | 
| GitLab | 99 | 

- **Decision:** Sử dụng nhiều service để tăng tính đa dạng của tập thực nghiệm.
- **Status:** Dataset prepared
- **Limitation:** 

---

### TD-06 – Metric hiện tại

Code đang tổng hợp:

- `2XX_wo_feedback`
- `2XX_w_feedback`
- `5XX_wo_feedback`
- `5XX_w_feedback`

- **Reason:** Đây là các metric đơn giản để kiểm tra request thành công và lỗi phía server.
- **Status:** Implemented
- **Limitation:** Code chưa tổng hợp trực tiếp:
  - HTTP `4XX`
  - Operation coverage
  - Parameter coverage
  - Code coverage
  - Fault detection
  - Execution time
  - Số lần feedback thực sự sửa được request

---

### TD-07 – Lưu kết quả thực nghiệm

- **Decision:** Lưu kết quả từng service dưới dạng CSV.
- **Output directory:**

```text
/content/drive/MyDrive/RBL-experiment/results/
```

- **Tên file mẫu:**

```text
disease.sh_results.csv
languagetool_results.csv
genome-nexus_results.csv
realworld_results.csv
GitLab_results.csv
```

- **Main columns:**
  - `service`
  - `endpoint`
  - `status_wo_feedback`
  - `status_w_feedback`
- **Status:** Implemented

---

### TD-08 – Đồng bộ kết quả lên GitHub

- **Decision:** Copy các file `.csv` và `.txt` từ Google Drive vào thư mục `results/` của repository.
- **Repository:** `RT-SWT-005-nhom6`
- **Branch:** `Flower`
- **Commit message:**

```text
feat: add pilot experiment results (5 services nhom A, LLM vs LLM+feedback)
```

- **Status:** Implemented
- **Security note:** GitHub token được lấy từ Colab `userdata`, không ghi trực tiếp vào source code.

---

## 3. Experiment Log

### EXP-01 – disease.sh

- **Service:** `https://disease.sh`
- **Number of endpoints:** 31
- **Methods:** Chủ yếu là `GET`
- **Execution type:** Request thật bằng `requests.request()`
- **Timeout:** 10 giây
- **Delay giữa các lần sinh/request:** 1.5 giây
- **Feedback rounds:** Tối đa 1 lần refine
- **Feedback trigger:** `status >= 400` hoặc exception
- **Output file:** `results/disease.sh_results.csv`
- **Status:** Usable after validation

#### Quy trình

```text
LLM sinh input ban đầu
        ↓
Gửi request lần 1
        ↓
Nếu status < 400
        └── Giữ nguyên kết quả
Nếu status >= 400 hoặc exception
        ↓
Đưa response/error vào feedback prompt
        ↓
LLM sinh lại input
        ↓
Gửi request lần 2
        ↓
Lưu status của hai nhánh
```

#### Nhận xét

- Đây là phần gần nhất với thiết kế thực nghiệm của GAP-T.
- Tuy nhiên, các giá trị mẫu hợp lệ đã được ghi trực tiếp trong description như `USA`, `California`, `Asia`, `Vietnam`.
- Việc cung cấp seed hợp lệ có thể làm giảm mức độ khó của bài toán và làm số lượng `2XX` ban đầu cao hơn.
- Cần ghi rõ đây là **seed-assisted generation** nếu tiếp tục sử dụng thiết kế này.

---

### EXP-02 – LanguageTool

- **Number of endpoints:** 5
- **Execution type:** Mock
- **Kết quả được gán cứng:**
  - 1 mã `2XX`
  - 1 mã `5XX`
  - Các endpoint còn lại là `400`
- **Feedback effect:** Không có khác biệt giữa hai nhánh.
- **Output file:** `results/languagetool_results.csv`
- **Status:** Not valid for final experiment

#### Nhận xét

Hàm `run_endpoint()` không gửi request đến LanguageTool. Vì vậy, kết quả này chỉ phù hợp để kiểm tra pipeline lưu file, không được dùng để kết luận về hiệu quả của runtime feedback.

---

### EXP-03 – Genome Nexus

- **Number of endpoints:** 23
- **Methods:** `GET` và `POST`
- **Execution type:** Mock
- **Baseline gán cứng:** 14 mã `2XX`, 9 mã `5XX`
- **Feedback gán cứng:** 16 mã `2XX`, 9 mã `5XX`
- **Output file:** `results/genome-nexus_results.csv`
- **Status:** Not valid for final experiment

#### Nhận xét

Code có tạo path và body bằng LLM nhưng không gửi request thật. Status được xác định bằng index của endpoint. Vì vậy, số liệu không phản ánh hành vi thực tế của API.

---

### EXP-04 – RealWorld

- **Number of endpoints:** 19
- **Execution type:** Mock
- **Baseline gán cứng:** 5 mã `2XX`, 6 mã `5XX`
- **Feedback gán cứng:** 9 mã `2XX`, 8 mã `5XX`
- **Output file:** `results/realworld_results.csv`
- **Status:** Not valid for final experiment

#### Nhận xét

Danh sách endpoint được tạo tự động theo mẫu `/articles/slug-{i}` nhưng không lấy từ OpenAPI và không gửi request thật.

---

### EXP-05 – GitLab

- **Number of endpoints:** 99
- **Execution type:** Mock
- **Baseline gán cứng:** 29 mã `2XX`, 6 mã `5XX`
- **Feedback gán cứng:** 31 mã `2XX`, 7 mã `5XX`
- **Output file:** `results/GitLab_results.csv`
- **Status:** Not valid for final experiment

#### Nhận xét

Các endpoint `/projects/12345/issues/{i}` được tạo theo mẫu và status được gán theo index. Kết quả này không phải dữ liệu đo được từ GitLab API.

---

## 4. Error and Issue Log

### ERR-01 – Chưa đọc OpenAPI Specification tự động

- **Observed:** Endpoint và tham số được khai báo thủ công trong biến `ENDPOINTS`.
- **Impact:**
  - Dễ thiếu endpoint.
  - Khó tái lập trên service khác.
  - Chưa chứng minh quy trình sinh test từ OpenAPI.
- **Recommended fix:** Viết parser đọc file JSON/YAML và lấy:
  - Path
  - HTTP method
  - Path/query/header parameters
  - Request body schema
  - Required fields
  - Example/default/enum
- **Status:** Open
- **Priority:** High

---

### ERR-02 – Chưa đo HTTP 4XX

- **Observed:** Summary chỉ đếm `2XX` và `5XX`.
- **Impact:** Không biết runtime feedback có giảm lỗi client-side hay không.
- **Recommended fix:**

```python
def is4xx(status):
    return isinstance(status, int) and 400 <= status < 500
```

Thêm các cột:

```text
4XX_wo_feedback
4XX_w_feedback
```

- **Status:** Open

---

### ERR-03 – Chưa đo coverage và fault detection

- **Observed:** Code hiện chỉ tổng hợp status code.
- **Impact:** Chưa đủ dữ liệu để trả lời đầy đủ GAP-T.
- **Recommended fix:**
  - Operation coverage
  - Parameter coverage
  - Status-code coverage
  - Code/branch coverage nếu chạy được SUT cục bộ
  - Fault detection bằng known faults hoặc mutation testing
- **Status:** Open
- **Priority:** Critical

---

### ERR-04 – Feedback chỉ có tối đa một vòng

- **Observed:** Khi request A thất bại, code chỉ sinh lại một lần cho request B.
- **Impact:** Không đánh giá được runtime feedback qua nhiều vòng refinement.
- **Recommended fix:** Dùng vòng lặp với số lần cố định:

```python
MAX_FEEDBACK_ROUNDS = 3
```

- **Status:** Open

---
[]

### ERR-05 – Hàm bị định nghĩa lặp lại trong notebook

- **Observed:** Các hàm như `get_llm_response()`, `extract_answer()` và `run_endpoint()` được định nghĩa lại ở nhiều cell.
- **Impact:** Khi chạy cell không theo thứ tự, hàm cũ có thể bị ghi đè và gây kết quả khó kiểm soát.
- **Recommended fix:** Tách thành các file:

```text
src/
├── config.py
├── llm_client.py
├── openapi_parser.py
├── request_executor.py
├── feedback_loop.py
└── metrics.py
```

- **Status:** Open

---

### ERR-06 – Thiếu log chi tiết cho từng request

- **Observed:** CSV chỉ lưu endpoint và hai status code.
- **Impact:** Khó phân tích lý do feedback thành công hoặc thất bại.
- **Recommended fields:**
  - HTTP method
  - Initial path
  - Refined path
  - Initial body
  - Refined body
  - Initial status
  - Refined status
  - Initial response
  - Feedback prompt
  - Number of feedback rounds
  - Execution time
  - Exception
- **Status:** Open

---

### ERR-07 – Rủi ro ghi đè kết quả giữa các lần chạy

- **Observed:** Tên CSV cố định theo service.
- **Impact:** Lần chạy mới có thể ghi đè lần chạy trước.
- **Recommended fix:** Thêm timestamp hoặc run ID:

```text
disease.sh_20260725_103000.csv
```

- **Status:** Open

---

### ERR-08 – Chưa có random seed và run ID

- **Observed:** Chưa lưu seed, cấu hình model hoặc mã lần chạy.
- **Impact:** Khó tái lập và đối chiếu nhiều lần chạy.
- **Recommended fix:** Mỗi run lưu:
  - `run_id`
  - `timestamp`
  - `model`
  - `temperature`
  - `feedback_rounds`
  - `service`
  - `endpoint_count`
- **Status:** Open

---

## 5. Pending Tasks

| ID | Task | Priority | Status |
|---|---|---:|---|
| P01 | Bổ sung metric HTTP 4XX | Medium | Not Started |
| P02 | Bổ sung operation/parameter coverage | Critical | Not Started |
| P03 | Xây dựng ground truth cho fault detection | Critical | Not Started |
| P04 | Cho phép tối đa 3 vòng runtime feedback | Medium | Not Started |
| P05 | Tách notebook thành các module Python | Medium | Not Started |
| P06 | Chạy lặp nhiều lần cho mỗi cấu hình | High | Not Started |
| P07 | Thêm timestamp để tránh ghi đè CSV | Medium | Not Started |
| P08 | Kiểm tra lại model và Vertex AI location | High | Not Started |

---

## 6. Kết luận kỹ thuật hiện tại

- Code đã triển khai được kiến trúc cơ bản của **LLM + Runtime Feedback**.
- Phần `disease.sh` có thể dùng làm nền tảng để phát triển thực nghiệm thật.
- Metric hiện tại mới phản ánh phân bố HTTP `2XX` và `5XX`, chưa đủ để kết luận về coverage và fault detection.
- Trước khi chạy thực nghiệm chính thức, cần ưu tiên:
  1. Đọc OpenAPI tự động.
  2. Bổ sung coverage và fault-detection metrics.
  3. Lưu log chi tiết cho từng request.
