# PRISMA Flow

[Records từ database searching (N = 57)]
← Tổng từ search_log.csv 

↓
[Sau khi xóa duplicate (N = 39)]
← Số dòng bài báo độc nhất trong 01_all_records.csv

┌──────────────────────────────────────┐
│ Screened title + abstract (N = 39)   │
│                                      │
│ Excluded (N = 19):                   │
│ EC-D (Duplicate) = 0                 │
│ EC-A (Wrong Artifact) = 5            │
│ EC-S (Wrong Domain/Scope) = 6        │
│ EC-N (Not LLM/AI Driven) = 4         │
│ EC-O (Other Reasons) = 4             │
└──────────────────────────────────────┘

↓ 20 papers pass
← INCLUDE + UNSURE trong 02_after_screening_v1.csv

┌──────────────────────────────────────┐
│ Full-text assessed (N = 20)          │
│                                      │
│ Excluded (N = 6):                    │
│ QA1 (Not dynamic execution testing) = 2│
│ QA2 (No empirical metrics baseline) = 1│
│ QA3 (Not standard Web REST API) = 2  │
│ QA4 (Secondary study / SLR itself) = 1 │
└──────────────────────────────────────┘

↓
[Final included (N = 14)]
← INCLUDE trong 03_final_included.csv 