# PRISMA Flow Diagram — LLM-based REST API Test Generation and Testing

**Thành viên:** Nguyễn Thị Hoa

[Records từ database searching (N = 63)]
← Tổng từ search-log.md

↓
[Sau khi xóa duplicate (N = 52 )]
← Số dòng trong 01_all_records.csv

┌──────────────────────────────────────┐
│ Screened title + abstract (N = 52) │
│                                      │
│ Excluded (N = 41):                 │
│ EC-D = 3                           │
│ EC-A = 7                          │
│ EC-S = 18                          │
│ EC-N = 0                          │
│ EC-O = 13                          │
└──────────────────────────────────────┘

↓ 11 papers pass
← INCLUDE + UNSURE trong 02_after_screening_v1.csv

┌──────────────────────────────────────┐
│ Full-text assessed (N = 11)        │
│                                      │
│ Excluded (N = 4):                 │
│ EC-A = 1                           │
│ EC-G = 0                           │
│ EC-R = 2                           │
│ IC-E = 1                          │
└──────────────────────────────────────┘

↓
[Final included (N = 7)]
← INCLUDE trong 03_final_included.csv