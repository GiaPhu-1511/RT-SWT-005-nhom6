
# GAP Analysis – LLM-based REST API Testing with Runtime Feedback

Evidence table: N = 8 papers | Ngày: 2026-06-17


## GAP Chính: [GAP-T]

Các nghiên cứu gần đây đã chứng minh rằng LLM có thể hỗ trợ sinh API test cases từ OpenAPI Specification và runtime feedback có thể cải thiện chất lượng đầu vào kiểm thử. Tuy nhiên, vẫn còn thiếu bằng chứng thực nghiệm đơn giản và trực tiếp về mức độ cải thiện của cơ chế runtime feedback đối với độ bao phủ kiểm thử và khả năng phát hiện lỗi khi áp dụng cho quy trình sinh test cases bằng LLM trên REST APIs.

## Chi tiết kiểm tra phản chứng

| Paper | LLM | OpenAPI | Runtime Feedback | Có giải quyết hoàn toàn GAP-T không? | Lý do |
|---------|-----|----------|------------------|------------------------------|--------|
| Wang (2026) | ✅ | ✅ | ⚠️ RL Reward | ❌ | Có cơ chế thích nghi dựa trên reward nhưng không đánh giá riêng tác động của runtime feedback đối với coverage và fault detection. |
| Liu (2026) | ✅ | ❌ | ✅ | ❌ | Chứng minh feedback giúp tăng coverage nhưng không thực hiện so sánh trực tiếp Manual vs LLM vs LLM+Feedback. |
| ASTRA (2026) | ✅ | ❌ | ✅ | ❌ | Sử dụng response feedback để refine test cases nhưng tập trung vào framework riêng và chi phí thực thi lớn. |
| LlamaRestTest (2025) | ✅ | ✅ | ✅ | ❌ | Chứng minh feedback cải thiện coverage nhưng không đánh giá theo quy trình đơn giản, dễ tái lập với cùng bộ metric. |
| DeepREST | ⚠️ | ✅ | ✅ | ❌ | Dùng RL và status code feedback nhưng tập trung vào tối ưu tìm kiếm trạng thái API. |
| RESTGPT | ✅ | ✅ | ❌ | ❌ | Tăng chất lượng OpenAPI nhưng không sử dụng runtime feedback. |
| PRIMG | ✅ | ❌ | ✅ | ❌ | Sử dụng compile/runtime errors để refine prompt nhưng không tập trung vào REST API testing. |
| ACH | ✅ | ❌ | ✅ | ❌ | Sử dụng execution feedback nhưng áp dụng cho test generation nói chung, không phải REST API testing. |
Feasibility Check – GAP Chính

Tiêu chí

Mức

Ghi chú

Dataset/SUT

✅

Mã đã xác định nhiều REST APIs như disease.sh, LanguageTool, Genome Nexus, RealWorld và GitLab.

OpenAPI Specification

⚠️

Mã hiện khai báo endpoint thủ công, chưa đọc và phân tích OpenAPI tự động.

LLM

✅

Đã tích hợp Gemini thông qua Vertex AI.

Runtime feedback

✅

Phần disease.sh đã đưa response/error vào prompt để sinh lại input.

Thực thi API thật

⚠️

Chỉ một phần gửi request thật; nhiều phần còn gán cứng status code.

Coverage metric

⚠️

Chưa được cài đặt trong mã hiện tại.

Fault-detection metric

⚠️

Chưa có ground truth, mutant hoặc tập lỗi đã biết.

Compute

✅

Có thể chạy bằng Google Colab hoặc máy cá nhân.

Skills

✅

Đã có mã tích hợp LLM, gửi HTTP request, ghi CSV và tổng hợp kết quả.

Thời gian

⚠️

Khả thi nếu thu hẹp số SUT và hoàn thiện metric cốt lõi trước khi chạy chính thức.

Contribution

✅

Đánh giá trực tiếp tác động của runtime feedback đối với LLM-generated REST API tests.

Kết quả: [ ] ✅ / [X] ⚠️ / [ ] ❌

Kết luận

GAP-T được giữ nguyên vì đây vẫn là khoảng trống nghiên cứu mà đề tài muốn giải quyết. Tuy nhiên, mã hiện tại mới chứng minh được khả năng xây dựng một feedback loop và so sánh các nhóm HTTP status code. Để kết luận về coverage và fault detection, nhóm cần thay các kết quả gán cứng bằng request thực tế, đọc endpoint từ OpenAPI Specification và bổ sung các metric tương ứng.