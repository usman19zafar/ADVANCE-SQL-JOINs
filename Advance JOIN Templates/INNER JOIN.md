```mermaid
flowchart TD
    A[Table A] -->|Analytical match| B[Windowed, Ranked Subquery]
    B -->|Top‑N per key| R[Result Set]
```

# INNER JOIN — Advanced Template

## 1. Purpose
Perform an analytical, multi‑predicate, window‑aware join where:
- Table B is pre‑filtered using ranking or partition logic  
- Only the **top‑ranked** or **business‑qualified** rows from B are joined  
- The join enforces **strict matching** on keys and analytical conditions  

## 2. Four-Part Flow
- First Part: Main table A  
- Second Part: Analytical subquery B (ranked, filtered, partitioned)  
- Third Part: Multi‑predicate join condition  
- Fourth Part: Final SELECT with enriched metrics  

## 3. Template
```sql
WITH Bx AS (
    SELECT
        B.<column_list_from_B>,
        ROW_NUMBER() OVER (
            PARTITION BY B.<partition_key>
            ORDER BY B.<sort_key> DESC
        ) AS rn,
        SUM(B.<metric>) OVER (
            PARTITION BY B.<partition_key>
        ) AS total_metric
    FROM <table_2> B
    WHERE B.<status> IN ('Active','Pending')
      AND B.<date> >= DATEADD(DAY, -90, GETDATE())
)
SELECT
    A.<column_list_from_A>,
    Bx.<column_list_from_B>,
    Bx.total_metric
FROM <table_1> A
INNER JOIN Bx
    ON A.<join_key> = Bx.<join_key>
   AND Bx.rn = 1;
```
