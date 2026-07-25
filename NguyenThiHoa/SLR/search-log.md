# Search Log — LLM-based REST API Test Generation and Testing

**Thành viên:** Nguyễn Thị Hoa
**Ngày thực hiện:** 2026-06-01

---

## Chuỗi tìm kiếm (Query Strings)

### String A

**Query nguyên văn:**
("REST API" OR "OpenAPI" OR "Swagger") AND ("LLM" OR "GPT" OR "Large Language Model") AND ("test generation" OR "automated testing" OR "test cases")

**Database:** Google Scholar
**Công cụ hỗ trợ export dữ liệu:** Publish or Perish (PoP)

**Bộ lọc:**
- Year: 2023–2026
- Title words: "REST API" OR "OpenAPI" OR "Swagger" - lý do: Google Scholar mặc định sẽ tìm kiếm từ khóa trên toàn bộ văn bản (Full-text) của bài báo. Nếu bạn không dùng bộ lọc Tiêu đề (Title words), nó sẽ trả về hàng nghìn kết quả "rác"

**Ngày search:** 2026-06-01 14:30

**Số kết quả:** 34 papers

---

### String B

**Query nguyên văn:**
("REST API" OR "OpenAPI" OR "Swagger") AND ("LLM" OR "GPT" OR "Large Language Model") AND ("test generation" OR "automated testing" OR "test cases")

**Database:** Semantic Scholar
**Công cụ hỗ trợ export dữ liệu:** Publish or Perish (PoP)

**Bộ lọc:**
- Year: 2023–2026

**Ngày search:** 2026-06-01 14:35

**Số kết quả:** 21 papers

---

### String C

**Query nguyên văn:**
("REST API" OR "OpenAPI" OR "Swagger") AND ("LLM" OR "GPT" OR "Large Language Model") AND ("test generation" OR "automated testing" OR "test cases")

**Database:** Scopus
**Công cụ hỗ trợ export dữ liệu:** Publish or Perish (PoP)

**Bộ lọc:**
- Year: 2023-2026

**Ngày search:** 2026-06-01 14:40

**Số kết quả:** 8 papers

---

## Tổng hợp trước dedup

| Database | String | Kết quả |
|-----------|-----------|-----------|
| Google Scholar | String A | 34 |
| Semantic Scholar | String B | 21 |
| Scopus | String C | 8 |
| **Tổng trước dedup** | | **63** |

---

## Dedup

| Mục | Số lượng |
|------|------|
| Tổng trước dedup | 63 |
| Sau dedup |52 |
| Bị loại do trùng | 11 |

---

## Phần S — Cross-reference Search (Snowballing)

> Snowballing chỉ thực hiện sau khi hoàn thành screening V2.

**Phương pháp:** Backward snowballing

**Thực hiện:**
- Đọc reference list của các paper trong `03_final_included.csv`
- Tìm các paper liên quan bằng CrossRef và Google Scholar

**Ngày thực hiện:** YYYY-MM-DD

**Paper included đã scan:** [N]

**Paper mới phát hiện:** [X]

**Paper pass IC/EC:** [Y]

---

## Ghi chú

- Dedup thực hiện bằng Zotero.
- Metadata được xuất từ Zotero dưới định dạng CSV.
- Screening được thực hiện theo tiêu chí trong `ie_criteria.md`.
- Final included papers được lưu trong `03_final_included.csv`.