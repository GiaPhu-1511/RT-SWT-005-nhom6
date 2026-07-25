# GAP Analysis – LLM-based REST API Testing

**Evidence table:** N = 20 papers | SLR Dataset

---

## GAP Chính: [GAP-T]

Các nghiên cứu gần đây đã chứng minh rằng Large Language Models (LLMs) có thể hỗ trợ hiệu quả việc sinh REST API test cases từ OpenAPI Specification, yêu cầu tự nhiên (Natural Language Requirements) hoặc mã nguồn. Nhiều phương pháp cũng tích hợp multi-agent collaboration, reinforcement learning, retrieval-augmented generation (RAG), mutation guidance hoặc runtime feedback để cải thiện test generation.

Tuy nhiên, **vẫn chưa có một phương pháp thống nhất vừa sinh test cases, vừa tạo test oracle tự động, vừa khai thác runtime feedback để thích nghi trong quá trình kiểm thử, đồng thời được đánh giá trên bộ benchmark chuẩn với các metric thống nhất**. Phần lớn các nghiên cứu chỉ tối ưu một hoặc hai khía cạnh của quy trình kiểm thử REST API, khiến việc so sánh và áp dụng trong môi trường thực tế còn hạn chế.

---

## Chi tiết kiểm tra phản chứng

| Paper                                          | LLM | Runtime Feedback | Oracle | Benchmark/Evaluation | Có giải quyết hoàn toàn GAP-T không? | Lý do                                                                                        |
| ---------------------------------------------- | --- | ---------------- | ------ | -------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------- |
| Multi-Agent Collaborative Framework (2026)     | ✅   | ❌                | ❌      | ⚠️                   | ❌                                    | Cải thiện generation rate bằng multi-agent nhưng chưa hỗ trợ oracle và adaptive feedback.    |
| GPT + Katalon (2023)                           | ✅   | ❌                | ❌      | ⚠️                   | ❌                                    | Tập trung sinh test scripts từ OpenAPI, chưa khai thác feedback khi thực thi.                |
| Intelligent Agent from OpenAPI (2025)          | ✅   | ⚠️               | ❌      | ❌                    | ❌                                    | Sinh request tự động nhưng nhiều lỗi semantic, cần refinement trước CI/CD.                   |
| REST API Fuzzing using Llama-3 (2025)          | ✅   | ✅                | ❌      | ⚠️                   | ❌                                    | Tận dụng dependency và feedback để tăng coverage nhưng chưa xử lý oracle.                    |
| ASTRA (2026)                                   | ✅   | ✅                | ⚠️     | ⚠️                   | ❌                                    | Response evaluation giúp refine test nhưng chưa giải quyết đầy đủ oracle và benchmark chuẩn. |
| TestGPT-Server (2025)                          | ✅   | ✅                | ❌      | ❌                    | ❌                                    | Hiệu quả trên quy mô công nghiệp nhưng chưa nghiên cứu oracle và chuẩn đánh giá chung.       |
| MioHint (2026)                                 | ✅   | ❌                | ❌      | ⚠️                   | ❌                                    | Tăng line coverage thông qua mutation nhưng không tập trung runtime adaptation.              |
| Automated Test Data & Oracle Generation (2025) | ✅   | ❌                | ✅      | ⚠️                   | ❌                                    | Giải quyết oracle nhưng chỉ hỗ trợ oracle đơn giản và không tích hợp adaptive testing.       |
| APITestGenie (2026)                            | ✅   | ❌                | ❌      | ⚠️                   | ❌                                    | Sinh test từ requirement nhưng chưa sử dụng execution feedback.                              |
| MASTEST (2025)                                 | ✅   | ⚠️               | ❌      | ❌                    | ❌                                    | Multi-agent sinh test đúng cú pháp nhưng thiếu đánh giá oracle và adaptive execution.        |
| Requirements to Executable Tests (2026)        | ✅   | ❌                | ❌      | ❌                    | ❌                                    | Đạt endpoint coverage cao nhưng chưa tích hợp feedback và oracle.                            |
| RESTifAI (2025)                                | ✅   | ⚠️               | ✅      | ⚠️                   | ❌                                    | Cải thiện khả năng tái sử dụng và oracle nhưng chưa có framework đánh giá chuẩn.             |
| ARMeta (2026)                                  | ✅   | ❌                | ⚠️     | ❌                    | ❌                                    | Tác giả thừa nhận test oracle vẫn là bài toán mở.                                            |
| RESTGPT (2024)                                 | ✅   | ❌                | ❌      | ❌                    | ❌                                    | Tập trung rule extraction và value generation, không thực hiện adaptive testing.             |
| RL-based API Testing (2025)                    | ✅   | ✅                | ❌      | ❌                    | ❌                                    | Sử dụng reinforcement learning để tăng coverage nhưng chưa giải quyết oracle.                |
| RESTestBench (2026)                            | ✅   | ❌                | ❌      | ✅                    | ❌                                    | Đề xuất benchmark nhưng không phải framework kiểm thử hoàn chỉnh.                            |
| RestTSLLM (2025)                               | ✅   | ❌                | ❌      | ✅                    | ❌                                    | So sánh nhiều LLM trên benchmark nhưng không khai thác runtime feedback.                     |

---

## Feasibility Check – GAP Chính

| Tiêu chí     | Mức | Ghi chú                                                                                                                 |
| ------------ | --- | ----------------------------------------------------------------------------------------------------------------------- |
| Dataset      | ✅   | EMB, RESTestBench, PetStore, REST APIs công khai                                                                        |
| Tool/API     | ✅   | OpenAPI Specification, Python Requests, LLM APIs                                                                        |
| Compute      | ✅   | Có thể chạy trên máy cá nhân hoặc GPU phổ thông                                                                         |
| Ground truth | ✅   | HTTP Status Code, API Response, Fault Detection, Coverage                                                               |
| Skills       | ✅   | Có thể phát triển từ pipeline LLM sinh REST API test hiện có                                                            |
| Thời gian    | ✅   | Phù hợp phạm vi RBL2                                                                                                    |
| Contribution | ✅   | Đề xuất framework tích hợp **LLM + runtime feedback + automated oracle + standardized evaluation** cho REST API testing |

**Kết quả:** **[X] ✅ / [ ] ⚠️ / [ ] ❌**
