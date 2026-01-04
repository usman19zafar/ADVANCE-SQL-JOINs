```mermaid
flowchart TD
    A[Table A] -->|Exists in B| B[Analytical B]
    B -->|Filtered existence| R[Result Set]
```

# SEMI JOIN (Advanced Template)

## 1. Purpose
Perform an analytical **EXISTS‑based join** where:
- A row from A is returned **only if** a qualifying row exists in B  
- B is window‑ranked to enforce business rules  
- Useful for filtering A based on analytical conditions in B  

## 2. Four-Part Flow
- First Part: Analytical subquery Bx  
- Second Part: Main table A  
- Third Part: EXISTS correlation  
- Fourth Part: Final SELECT (A‑only output)  

## 3. Template
```sql
WITH Bx AS (                                      -- First Part
    SELECT
        B.<join_key>,
        ROW_NUMBER() OVER (
            PARTITION BY B.<join_key>
            ORDER BY B.<score> DESC
        ) AS rn,
        SUM(B.<metric>) OVER (
            PARTITION BY B.<join_key>
        ) AS total_metric
    FROM <table_2> B
    WHERE B.<status> = 'Active'
)
SELECT                                              -- Fourth Part
    A.<column_list_from_A>
FROM <table_1> A                                    -- Second Part
WHERE EXISTS (                                      -- Third Part
    SELECT 1
    FROM Bx
    WHERE Bx.<join_key> = A.<join_key>
      AND Bx.rn = 1
);
```
