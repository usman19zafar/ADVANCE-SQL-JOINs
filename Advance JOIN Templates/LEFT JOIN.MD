```mermaid
flowchart TD
    A[Table A] -->|All A rows| J[Join Attempt]
    J -->|Top‑N, Windowed Match| B[Filtered B]
    A -.->|NULLs when no match| N[Null-extended Output]
```

# LEFT JOIN — Advanced Template

## 1. Purpose
Return all rows from A while enriching them with:
- Top‑N or latest analytical values from B  
- Window‑filtered metrics  
- Conditional business logic  
NULLs appear when no qualifying B row exists.

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Analytical subquery B  
- Third Part: LEFT JOIN with ranking filter  
- Fourth Part: Final SELECT with NULL‑safe enrichment  

## 3. Template
```sql
WITH Bx AS (
    SELECT
        B.<column_list_from_B>,
        ROW_NUMBER() OVER (
            PARTITION BY B.<partition_key>
            ORDER BY B.<priority> DESC, B.<created_at> DESC
        ) AS rn,
        AVG(B.<value>) OVER (
            PARTITION BY B.<partition_key>
        ) AS avg_value
    FROM <table_2> B
    WHERE B.<status> = 'Active'
)
SELECT
    A.<column_list_from_A>,
    Bx.<column_list_from_B>,
    Bx.avg_value
FROM <table_1> A
LEFT JOIN Bx
    ON A.<join_key> = Bx.<join_key>
   AND Bx.rn = 1;
```
