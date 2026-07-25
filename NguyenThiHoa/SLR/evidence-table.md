# Evidence Table — LLM-based REST API Test Generation and Testing

**Thành viên:** Nguyễn Thị Hoa  
**Total included papers (N = 7):**

### Paper 1: ID#2

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** Leveraging large language models to improve rest api testing
- **Năm:** 2024
- **Venue:** ACM/IEEE 44th International Conference on Software Engineering (ICSE)
- **Authors:** Kim, M; Stennett, T; Shah, D; Sinha, S; Orso, A
- **DOI/URL:** 10.1145/3639476.3639769
https://dl.acm.org/doi/abs/10.1145/3639476.3639769


| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** | RESTGPT (sử dụng GPT-3.5 / GPT-4) |
| **Dataset** | Các OpenAPI Specifications của REST API thực tế (Real-world APIs) |
| **Metric** | Độ chính xác trích xuất luật (Rule extraction precision) và sinh giá trị (Value generation) |
| **Kết quả** | RESTGPT vượt trội hơn công cụ NLP2REST. Độ chính xác (Precision) tăng mạnh từ 79% lên 97% khi kết hợp với module xác thực. |
| **Hạn chế tự nêu** |"These techniques are limited in the types of rules they can extract and can produce inaccurate results." |

---

### Paper 2: ID#24

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** Design, Implementation, and Evaluation of an LLM-Powered System for Automated REST API Testing
- **Năm:** 2025
- **Venue:** IEEE/ACM International Conference on Intelligent Software Methodologies (SMARTCODE)
- **Authors:** Kesraoui, A; Houssaini, OI; [others]
- **DOI/URL:** https://ieeexplore.ieee.org/abstract/document/11273754/

| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** |LLM-Powered Agent Framework |
| **Dataset** |3 OpenAPI Specifications thực tế (bao gồm Spotify API) |
| **Metric** |Độ bao phủ mã (Code Coverage), Tỷ lệ sinh test thành công |
| **Kết quả** | Khung framework có khả năng làm giàu (enrich) file đặc tả API ban đầu và tự động hóa quy trình sinh test, mang lại triển vọng lớn trong việc thay thế công sức thủ công.|
| **Hạn chế tự nêu** | "Limitations, particularly in handling the extended length of API specifications." |

---

### Paper 3: ID#34

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** LlamaRestTest: Effective REST API Testing with Small Language Models
- **Năm:** 2025
- **Venue:** Proceedings of the ACM on Software Engineering (PACMSE)
- **Authors:** Kim, Myeongsoo; Sinha, Saurabh; Orso, Alessandro
- **DOI/URL:** 10.1145/3715737
https://www.semanticscholar.org/paper/8d70bc01b7ecdb150da653fa46717ad0a1c2d604


| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** | Llama 3 (Llama3-8B) được fine-tuning và quantization (Small Language Model) |
| **Dataset** | 12 real-world REST services (bao gồm Spotify) |
| **Metric** | Method/Branch/Line Coverage, Tỷ lệ input hợp lệ (Validity rate), Số lỗi Server Errors |
| **Kết quả** | Bản LlamaREST-EX đạt 72.44% tỷ lệ sinh input hợp lệ (vượt xa bản gốc 22.94% và RESTGPT 68.82%). LlamaRestTest đánh bại RESTler, MoRest, EvoMaster về độ bao phủ code và khả năng tìm lỗi 500 |
| **Hạn chế tự nêu** | Việc áp dụng kỹ thuật lượng tử hóa (quantization xuống 2-bit, 4-bit) giúp tăng hiệu suất phần cứng nhưng phải đánh đổi bằng việc giảm nhẹ độ bao phủ (coverage) so với mô hình gốc. |

---

### Paper 4: ID#35

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** Technology adoption performance evaluation applied to testing of REST APIs using ChatGPT
- **Năm:** 2024
- **Venue:** Journal of Systems and Software / Automated Software Engineering
- **Authors:** Poth, Alexander; Rrjolli, Olsi; Arcuri, Andrea
- **DOI/URL:** 10.1007/s10515-024-00477-2
https://www.semanticscholar.org/paper/a7d0f86bb60354325df1e322f1aa081dd480ea8b

| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** | ChatGPT (GPT-3.5 / GPT-4) |
| **Dataset** | Các REST APIs công nghiệp tại tập đoàn Volkswagen AG |
| **Metric** | Hiệu suất sinh test (Efficiency), Đánh giá hiệu năng áp dụng công nghệ (TAPE framework) |
| **Kết quả** |LLM hỗ trợ rất tốt trong việc sinh test-case nhanh chóng. Tuy nhiên, việc áp dụng chúng vào mô hình doanh nghiệp quy mô lớn (scalable enterprise setup) đòi hỏi nhiều nỗ lực cấu hình.|
| **Hạn chế tự nêu** |"Integrate them into an automated test suite requires a significant amount of work." |

---

### Paper 5: ID#38

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** KAT: Dependency-Aware Automated API Testing with Large Language Models
- **Năm:** 2024
- **Venue:** 2024 IEEE International Conference on Software Testing, Verification and Validation (ICST)
- **Authors:** Le, Tri; Trần, T.; Cao, Duy; Le, Vy; Nguyen, Tien; Nguyen, Vu
- **DOI/URL:** 10.1109/ICST60714.2024.00017
https://www.semanticscholar.org/paper/5013f14c8e5cc2d8ddb0f51eab62b52f3f5e83c5


| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** | KAT framework sử dụng GPT kết hợp Advanced Prompting |
| **Dataset** | 12 real-world RESTful services |
| **Metric** | Độ bao phủ mã trạng thái (Status code coverage), Số lỗi phát hiện, Tỷ lệ False positive |
| **Kết quả** |Cải thiện 15.7% độ bao phủ status code so với công cụ SOTA RestTestGen. Phát hiện được nhiều mã trạng thái không có trong tài liệu (undocumented) và giảm thiểu báo cáo sai (false positives). |
| **Hạn chế tự nêu** | Đòi hỏi phải xây dựng một đồ thị phụ thuộc hoạt động (Operation Dependency Graph) trước. Nếu mô tả API bằng ngôn ngữ tự nhiên quá sơ sài, LLM sẽ khó hiểu được các phụ thuộc ẩn (hidden dependencies).|

---

### Paper 6: ID#41

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** SATORI: Static Test Oracle Generation for REST APIs using Generative AI
- **Năm:** 2025
- **Venue:** 2025 40th IEEE/ACM International Conference on Automated Software Engineering (ASE)
- **Authors:** Alonso, Juan C.; Martin-Lopez, Alberto; Segura, Sergio; Bavota, Gabriele; Ruiz-Cortés, Antonio
- **DOI/URL:** 10.1109/ASE63991.2025.00116
https://www.semanticscholar.org/paper/9fe9ba94df54d21999b9d3b1d7908b7910d8312b


| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** | SATORI (dùng Large Language Models để sinh Static Test Oracle) |
| **Dataset** | OKAMI dataset (gồm 17 operations từ 12 industrial APIs)|
| **Metric** | Điểm F1-score (của Test oracles), Tỷ lệ oracles hợp lệ |
| **Kết quả** | SATORI đạt F1-score 74.3%, vượt qua công cụ AGORA+ (69.3%). Có khả năng tự động sinh hàng trăm valid test oracles mỗi operation. Khi kết hợp cùng AGORA+ có thể phát hiện 90% oracles. |
| **Hạn chế tự nêu** | Vì là phương pháp tĩnh (static black-box), "Nếu test suite thiếu tính đa dạng, các bất biến (invariants) dự đoán có thể bị sai hoặc thiếu sót." Phụ thuộc hoàn toàn vào phần text mô tả trong file OAS. |

---

### Paper 7: ID#48

**Paper (Tên + Năm + Venue):**
- **Tiêu đề:** From Requirements to Executable Tests: LLM-Based System Test Generation for REST APIs
- **Năm:** 2026
- **Venue:** Vilnius University Open Series
- **Authors:** Kochanovskis, Jaroslav; Slotkiene, Asta
- **DOI/URL:** 10.15388/lmitt.2026.13
https://www.semanticscholar.org/paper/32d940db08eb12e25afea7d03e677bc49ea086a3


| Cột | Giá trị |
|-----|--------|
| **Tool/LLM** |LLM-Based Agent kết hợp Pydantic sinh mã Pytest |
| **Dataset** | 2 real-world REST APIs |
| **Metric** | Tỷ lệ sinh test (Test generation rate), Độ bao phủ điểm cuối (Endpoint reachability), Pass rate |
| **Kết quả** | Hệ thống tự động chuyển yêu cầu ngôn ngữ tự nhiên thành test case. Đạt 100% full endpoint reachability coverage và cung cấp kịch bản thực thi tự động ổn định. |
| **Hạn chế tự nêu** |"The generated output is not accepted directly; instead, it is processed through a validation pipeline..." |

---

