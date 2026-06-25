# Search Log — LLM-based REST API Test Generation and Testing

**Thành viên:** Võ Gia Phú
**Ngày thực hiện:** 2026-06-01

---

## Chuỗi tìm kiếm (Query Strings)

### String A

**Query nguyên văn:**

("REST API" OR "Web API")
AND
("OpenAPI" OR "Swagger")
AND
("LLM" OR "GPT" OR "Large Language Model")
AND
("API test generation" OR "test case generation")

**Database:** Semantic scholar

**Bộ lọc:**
- Year: 2020–2026
- English only
- Conference + Journal

**Ngày search:** 2026-06-01

**Số kết quả:** 112 papers

---

### String B

**Query nguyên văn:**

("REST API" OR API OR OpenAPI)
AND
("LLM" OR GPT OR "Large Language Model")
AND
(testing OR "test generation" OR "test case generation")
AND
(coverage OR effectiveness OR performance OR evaluation)

**Database:** Google Scholar

**Bộ lọc:**
- Year: 2020–2026
- English only
- Conference + Journal

**Ngày search:** 2026-06-01

**Số kết quả:** 74

---

### String C

**Query nguyên văn:**

("API test generation")
AND
("LLM" OR "Large Language Model")
AND
("manual testing" OR "hand-written test cases" OR "expert-designed tests")
AND
("coverage" OR "bug detection")

**Database:** Google Scholar

**Bộ lọc:**
- Year: 2020–2026
- English only
- Conference + Journal

**Ngày search:** 2026-06-01

**Số kết quả:** 93

---

## Tổng hợp trước dedup

| Database | String | Kết quả |
|-----------|-----------|-----------|
| Semantic scholar | String A | 112 |
| Google Scholar | String B | 74 |
| Google Scholar | String C | 93 |
| **Tổng trước dedup** | | 279 |

---

## Dedup

| Mục | Số lượng |
|------|------|
| Tổng trước dedup | 279 |
| Sau dedup | 120 |
| Bị loại do trùng | 159 |

---

## Phần S — Cross-reference Search (Snowballing)

> Snowballing chỉ thực hiện sau khi hoàn thành screening V2.

**Phương pháp:** Backward snowballing

**Thực hiện:**
- Đọc reference list của các paper trong `03_final_included.csv`
- Tìm các paper liên quan bằng CrossRef và Google Scholar

**Ngày thực hiện:** 2026-06-04

**Paper included đã scan:** 25

**Paper mới phát hiện:** 0

**Paper pass IC/EC:** 0


---

## Ghi chú

- Dedup thực hiện bằng Zotero.
- Metadata được xuất từ Zotero dưới định dạng CSV.
- Screening được thực hiện theo tiêu chí trong `ie_criteria.md`.
- Final included papers được lưu trong `03_final_included.csv`.