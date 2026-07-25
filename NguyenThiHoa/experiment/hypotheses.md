# Hypotheses — LLM-based REST API Test Generation and Testing

**Thành viên:** Nguyễn Thị Hoa

## RQ1 : Đánh giá khả năng bao phủ

Câu hỏi: Các test case do LLM sinh ra cho REST APIs có đạt được độ bao phủ điểm cuối (endpoint coverage) trung bình từ 90% trở lên không?

### H0
Các test case do LLM (Large Language Models) sinh ra KHÔNG đạt độ bao phủ điểm cuối trung bình ≥ 90% trên các tập dữ liệu thực nghiệm.

### H1
Các test case do LLM sinh ra ĐẠT độ bao phủ điểm cuối trung bình ≥ 90% trên các tập dữ liệu thực nghiệm.

### Statistical test dự kiến
One-sample Wilcoxon Signed-Rank Test (Lý do: Dữ liệu về độ bao phủ % trích xuất từ các bài báo thường có cỡ mẫu nhỏ (N=7) và không tuân theo phân phối chuẩn, do đó sử dụng kiểm định phi tham số One-sample Wilcoxon để so sánh trung vị với một hằng số 90% là chính xác nhất).

---

## RQ2 : Đánh giá khả năng phát hiện lỗi

Câu hỏi: Các test case do LLM sinh ra có khả năng phát hiện trung bình từ 2 lỗi thực tế (real bugs) trở lên trên mỗi hệ thống REST API không?

### H0
Các test case do LLM sinh ra KHÔNG đạt khả năng phát hiện trung bình ≥ 2 lỗi thực tế trên mỗi REST API được kiểm thử.

### H1
Các test case do LLM sinh ra ĐẠT khả năng phát hiện trung bình ≥ 2 lỗi thực tế trên mỗi REST API được kiểm thử.

### Statistical test dự kiến
One-sample Wilcoxon Signed-Rank Test (hoặc Binomial Test nếu chuyển dữ liệu thành dạng nhị phân: Đạt/Không đạt mục tiêu 2 bugs).

---

## RQ3 : So sánh hiệu năng (Comparative Evaluation) - Rất quan trọng cho SLR

Câu hỏi: Test case do LLM sinh ra có mang lại độ bao phủ và khả năng phát hiện lỗi cao hơn so với các phương pháp tự động/thủ công truyền thống (như Search-based, Fuzzing) không?

### H0
KHÔNG CÓ sự khác biệt có ý nghĩa thống kê về độ bao phủ và số lỗi phát hiện được giữa LLM-generated tests và phương pháp kiểm thử truyền thống (LLM ≤ Truyền thống).

### H1
LLM-generated tests mang lại độ bao phủ và số lỗi phát hiện được CAO HƠN có ý nghĩa thống kê so với phương pháp kiểm thử truyền thống.

### Statistical test dự kiến
Mann-Whitney U Test (nếu dữ liệu trích xuất từ các bài báo là các nhóm độc lập) hoặc Wilcoxon Signed-Rank Test ghép cặp (nếu các bài báo chạy thử nghiệm LLM và công cụ truyền thống trên cùng một tập REST APIs).